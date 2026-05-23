---
name: sutton
description: Richard Sutton을 협업 파트너로 — 백엔드 엔지니어의 RL harness/agent 설계 작업 진입점. 사용자가 "Sutton", "Richard Sutton", "리처드 서튼", "서튼" 같은 인물명을 명시 호출하거나, "Bitter Lesson", "비터 레슨", "Era of Experience", "experiential paradigm", "experience-based learning", "reward hypothesis", "보상 가설", "Alberta Plan", "Big World Hypothesis", "TD learning", "policy gradient", "value function", "grounded reward", "continual learning", "Sutton & Barto", "Reinforcement Learning An Introduction", "OaK", "incompleteideas" 같은 Sutton 고유 개념·대표 저작을 명시할 때 호출. 또한 RL agent 설계 영역 신호 — "RL agent 설계", "reinforcement learning agent", "reward function 어떻게", "reward shaping", "scalar reward", "exploration policy 어떻게", "agent가 local optimum에 갇혔어", "training loop 어떻게", "episode 길이", "agent state carry-over", "continual learning loop", "catastrophic forgetting", "online learning agent", "value function 어떻게", "credit assignment", "TD error", "long-term return tracking", "이 도메인 룰을 agent에 박을까 vs 학습시킬까", "hand-engineering vs scaling", "human demonstration으로 bootstrap", "RLHF 설계 자체", "preference learning을 RL agent reward로", "expert demo로 imitation" 같은 표현이 — 사용자가 Sutton을 명시하지 않아도 — 나오면 호출한다. master-router의 추천 후 사용자가 sutton을 선택했을 때도 호출. 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬·오길비) 영역에는 호출하지 않는다. *Karpathy 영역과 명시적으로 분리* — LLM·프롬프트·context window·RAG·docs for agents·LLM API 통합·일반 AI feasibility 진단·jagged intelligence·works.any/all·LLM tool 자율도 slider·일반 AI 코드 생성은 Karpathy 호출. RLHF를 *LLM 정렬 도구로* 쓰는 자리는 Karpathy, RLHF를 *RL agent의 reward 설계*로 논하는 자리(보통 Sutton이 *거부*하는 자리)는 Sutton. AI safety control mechanism 디자인·alignment 솔루션·symbolic AI·rule-based system·일반 supervised ML·단발 prediction task는 Sutton 영역 밖 — 호출하지 않음. ambiguous한 "AI agent / 학습 시스템 / 통합" 영역(환경 반복 상호작용인지 LLM tool 통합인지 불분명)은 master-router 경유. 본 스킬은 본체가 아니라 진입점이며 — `.claude/agents/sutton.md` agent로 사용자를 relay하는 라우터 역할만 한다.
---

# Sutton — 협업 진입점 (collaborator agent router)

## 언제 사용

사용자가 Sutton 인물·고유 개념·대표 저작을 명시 호출했을 때. RL agent의 reward function 디자인, environment·stream·episode 정의, exploration policy, continual learning loop, value function 구조, hand-engineering vs scaling 결정, Bitter Lesson check — 백엔드 엔지니어의 *RL harness/agent 설계* ongoing 협업.

## 언제 사용 안 함

- 다른 거장 영역 (맥킨지의 구조화 / 이어령의 통설 의심 / 아리스토텔레스의 4원인·phronesis / 파인만의 자기-감사 / 프롬의 having↔being / 오길비의 brand·copy).
- **Karpathy 영역과 분리** — LLM·프롬프트·context window·RAG·docs for agents·LLM API 통합·일반 AI feasibility 진단·jagged intelligence·works.any/all·LLM tool 자율도 slider·일반 AI 코드 생성. 환경과 반복 상호작용하는 *학습 agent* 아니면 Sutton 호출 안 함.
- 인물·개념 명시 없이 "AI / agent / 학습" 일반어만 있는 ambiguous한 영역 — master-router 경유.
- AI safety control mechanism / alignment 솔루션 / symbolic AI / rule-based system / 일반 supervised ML / 단발 prediction task — 본 agent 영역 밖 (ADR 0009 §7).

## 라우팅 규칙 (가장 중요)

이 스킬이 발화되면 main Claude는 **직접 답하지 않는다**. 본체는 `.claude/agents/sutton.md` agent다. main Claude의 동작은 다음 셋 중 하나로만:

1. **첫 호출** (이 세션에서 sutton을 처음 부른 경우): `Agent` 도구로 spawn하되 — `name: "sutton"` 파라미터를 **반드시** 준다.
   - 호출 형태: `Agent({ subagent_type: "sutton", name: "sutton", description: "...", prompt: <사용자 입력 그대로> })`
   - **Why:** `name`이 없으면 후속 turn에서 SendMessage가 어떤 인스턴스에 닿을지 식별 불가 → 매번 새 인스턴스가 spawn되어 이전 대화·voice·reward 정의·environment spec·engine 진단이 사라진다. collaborator shape의 전제(상태 유지)가 깨진다.

2. **후속 turn** (같은 세션에서 sutton이 이미 spawn된 경우): 새 `Agent` 호출 금지. 같은 인스턴스에 `SendMessage` 로만 relay.
   - 호출 형태: `SendMessage({ to: "sutton", message: <사용자 입력 그대로> })`
   - **Why:** 새 `Agent` 호출은 항상 fresh context. 두 번째도 `Agent`로 부르면 첫 turn의 4질문 답·scalar reward 환원 결과·environment carry-over 정의·engine 정합성 진단이 모두 증발한다.

3. **세션이 바뀐 경우**: 이전 세션의 in-memory 대화는 사라졌다 → 첫 호출(1번)부터 다시 시작. ongoing 협업의 영속성은 agent 본체가 세션 시작 시 `research/sutton/` 의 raw·summary를 읽어 보강하는 것으로 처리.

main Claude는 sutton agent의 voice를 흉내내지 않는다. 자기-답변하지 않는다. 통로 역할만 한다. 사용자가 main에 직접 RL agent 설계 평가를 요청해도 — 본 스킬이 발화된 동안 main은 평가를 *agent에 위임*한다. 이 위임이 collaborator shape의 핵심.

## 종료 트리거

다음 발화가 들어오면 sutton 협업을 종료하고 main 통제로 복귀:

- "다른 거장 부르자" / "Sutton 모드 끝" / "다른 일 하자" / "끝"
- 사용자가 다른 figure 이름을 명시 호출 (Karpathy·맥킨지·파인만·아리스토텔레스·오길비 등)
- 작업이 자연스럽게 완결됐을 때 (agent가 종료 한 줄 요약을 낸 후)

종료 후 다음 사용자 발화는 다시 본 스킬의 진입 트리거를 따라야 새 sutton 협업이 시작된다.
