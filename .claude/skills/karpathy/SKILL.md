---
name: karpathy
description: Andrej Karpathy를 협업 파트너로 — 백엔드 엔지니어의 ongoing AI 작업 진입점. 사용자가 "카파시", "Karpathy", "Andrej Karpathy", "카르파티" 같은 인물명을 명시 호출하거나, "Software 2.0", "Software 3.0", "LLM OS", "cognitive core", "vibe coding", "build for agents", "agents as new consumer", "context as RAM", "spirits not animals", "ghosts not animals", "autonomy slider", "works.any works.all", "nanoGPT", "micrograd", "llm.c", "Neural Networks Zero to Hero" 같은 카파시 고유 개념·대표 코드베이스를 명시할 때 호출. 또한 백엔드 엔지니어의 AI 작업 영역 신호 — "프롬프트 잘 짜기", "프롬프트가 너무 길어졌어", "context window 관리", "RAG 시스템 설계", "RAG 결과가 엉뚱해", "agent memory", "session 길어지면 답 나빠짐", "토큰 비용 줄이기", "사내 docs를 AI가 못 찾아", "error message를 AI가 이해할 수 있게", "log를 AI agent가 분석", "README를 LLM이 읽기 좋게", "llms.txt", "AI로 X 가능?", "AI feasibility", "GPT-5 vs Claude 어느 게 나아?", "AI tool 평가", "model 비교", "PoC 짜기 전에", "AI가 왜 이건 잘하고 저건 못해?", "production 가니 갑자기 무너짐", "AI 신뢰해도 돼?", "어디까지 자동화", "PR review bot 만들고 싶어", "CI/CD에 AI 박을까?", "incident response 자동화", "어디까지 사람 빼?", "이 AI 기능 출시해도 돼?", "SLA 얼마로 약속?", "eval suite 짜기", "edge case 다 봤나", "AI demo는 잘 됐는데...", "code generation 통합", "AI-assisted review" 같은 표현이 — 사용자가 카파시를 명시하지 않아도 — 나오면 호출한다. master-router의 추천 후 사용자가 karpathy를 선택했을 때도 호출. 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬·오길비) 영역에는 호출하지 않는다 — 특히 "이 개념 진짜 이해한 거 맞나"(파인만), "이 가격·구조가 왜 이래야"(아리스토텔레스 causal-why), "사업 카테고리 명명·시장 진입"(영역 밖) 같은 자리는 카파시가 거부하고 분기. 단순 코드 작성·자명한 도구 사용("이 코드 짜줘" 한 줄)은 호출하지 않음 — engine 적용이 overhead. 본 스킬은 본체가 아니라 진입점이며 — `.claude/agents/karpathy.md` agent로 사용자를 relay하는 라우터 역할만 한다.
---

# Karpathy — 협업 진입점 (collaborator agent router)

## 언제 사용

사용자가 Karpathy 인물·고유 개념·대표 코드베이스를 명시 호출했을 때. 프롬프트·세션·메모리 설계, 문서·API·로그의 agent consumer 재설계, AI feasibility 진단, AI 한계 calibration, AI 통합 지점의 autonomy slider 디자인, demo vs production 운영 spec — 백엔드 엔지니어로서의 ongoing AI 작업 협업.

## 언제 사용 안 함

- 다른 거장 영역 (맥킨지의 구조화 / 이어령의 통설 의심 / 아리스토텔레스의 4원인·phronesis / 파인만의 자기-감사 / 프롬의 having↔being / 오길비의 brand·copy).
- 인물·개념 명시 없이 "AI / LLM / 프롬프트 / agent" 일반어만 있는 ambiguous한 영역 — master-router 경유.
- 카테고리 명명·사업 발견·시장 진입 같은 *사업적* 측면 — 본 agent는 백엔드 엔지니어용으로 좁힘 (ADR 0008 v3).

## 라우팅 규칙 (가장 중요)

이 스킬이 발화되면 main Claude는 **직접 답하지 않는다**. 본체는 `.claude/agents/karpathy.md` agent다. main Claude의 동작은 다음 셋 중 하나로만:

1. **첫 호출** (이 세션에서 karpathy를 처음 부른 경우): `Agent` 도구로 spawn하되 — `name: "karpathy"` 파라미터를 **반드시** 준다.
   - 호출 형태: `Agent({ subagent_type: "karpathy", name: "karpathy", description: "...", prompt: <사용자 입력 그대로> })`
   - **Why:** `name`이 없으면 후속 turn에서 SendMessage가 어떤 인스턴스에 닿을지 식별 불가 → 매번 새 인스턴스가 spawn되어 이전 대화·voice·measurement·slider 결정이 사라진다. collaborator shape의 전제(상태 유지)가 깨진다.

2. **후속 turn** (같은 세션에서 karpathy가 이미 spawn된 경우): 새 `Agent` 호출 금지. 같은 인스턴스에 `SendMessage` 로만 relay.
   - 호출 형태: `SendMessage({ to: "karpathy", message: <사용자 입력 그대로> })`
   - **Why:** 새 `Agent` 호출은 항상 fresh context. 두 번째도 `Agent`로 부르면 첫 turn의 4질문 답·measurement·slider 위치·works.any/all 분류가 모두 증발한다.

3. **세션이 바뀐 경우**: 이전 세션의 in-memory 대화는 사라졌다 → 첫 호출(1번)부터 다시 시작. ongoing 협업의 영속성은 agent 본체가 세션 시작 시 `research/karpathy/` 의 raw·summary를 읽어 보강하는 것으로 처리.

main Claude는 karpathy agent의 voice를 흉내내지 않는다. 자기-답변하지 않는다. 통로 역할만 한다. 사용자가 main에 직접 AI 작업 평가를 요청해도 — 본 스킬이 발화된 동안 main은 평가를 *agent에 위임*한다. 이 위임이 collaborator shape의 핵심.

## 종료 트리거

다음 발화가 들어오면 karpathy 협업을 종료하고 main 통제로 복귀:

- "다른 거장 부르자" / "카파시 모드 끝" / "다른 일 하자" / "끝"
- 사용자가 다른 figure 이름을 명시 호출 (맥킨지·파인만·아리스토텔레스·오길비 등)
- 작업이 자연스럽게 완결됐을 때 (agent가 종료 한 줄 요약을 낸 후)

종료 후 다음 사용자 발화는 다시 본 스킬의 진입 트리거를 따라야 새 karpathy 협업이 시작된다.
