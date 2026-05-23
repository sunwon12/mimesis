---
name: ogilvy
description: David Ogilvy를 협업 파트너로 — 브랜드·광고·카피의 ongoing 협업 진입점. 사용자가 "오길비", "Ogilvy", "David Ogilvy" 같은 인물명을 명시 호출하거나, "Big Idea", "빅 아이디어", "brand personality", "sell or else", "consumer is not a moron", "Hathaway eyepatch", "Rolls-Royce silence", "Dove 1/4" 같은 Ogilvy 고유 개념·대표 캠페인을 명시할 때 호출. master-router의 추천 후 사용자가 ogilvy를 선택했을 때도 호출. 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬 등)의 영역에는 호출하지 않는다. "광고 / 카피 / 마케팅 / 브랜드" 같은 일반어만 있고 인물·개념 명시가 없는 ambiguous한 브랜드·마케팅 영역은 master-router 경유가 권장 흐름. 본 스킬은 본체가 아니라 진입점이며 — `.claude/agents/ogilvy.md` agent로 사용자를 relay하는 라우터 역할만 한다.
---

# Ogilvy — 협업 진입점 (collaborator agent router)

## 언제 사용

사용자가 Ogilvy 인물·고유 개념·대표 캠페인을 명시 호출했을 때. 브랜드·카피·헤드라인·네이밍·포지셔닝·Big Idea·캠페인 브리프의 ongoing 협업.

## 언제 사용 안 함

다른 거장의 영역 (맥킨지의 구조화 / 이어령의 통설 의심 / 아리스토텔레스의 4원인·phronesis / 파인만의 자기-감사 / 프롬의 having↔being). 인물·개념 명시 없는 ambiguous한 브랜드·마케팅 영역은 master-router 경유.

## 라우팅 규칙 (가장 중요)

이 스킬이 발화되면 main Claude는 **직접 답하지 않는다**. 본체는 `.claude/agents/ogilvy.md` agent다. main Claude의 동작은 다음 셋 중 하나로만:

1. **첫 호출** (이 세션에서 ogilvy를 처음 부른 경우): `Agent` 도구로 spawn하되 — `name: "ogilvy"` 파라미터를 **반드시** 준다.
   - 호출 형태: `Agent({ subagent_type: "ogilvy", name: "ogilvy", description: "...", prompt: <사용자 입력 그대로> })`
   - **Why:** `name`이 없으면 후속 turn에서 SendMessage가 어떤 인스턴스에 닿을지 식별 불가 → 매번 새 인스턴스가 spawn되어 이전 대화·voice가 사라진다. collaborator shape의 전제(상태 유지)가 깨진다.

2. **후속 turn** (같은 세션에서 ogilvy가 이미 spawn된 경우): 새 `Agent` 호출 금지. 같은 인스턴스에 `SendMessage` 로만 relay.
   - 호출 형태: `SendMessage({ to: "ogilvy", message: <사용자 입력 그대로> })`
   - **Why:** 새 `Agent` 호출은 항상 fresh context. 두 번째도 `Agent`로 부르면 첫 turn의 카피·브랜드 합의·voice tuning이 모두 증발한다.

3. **세션이 바뀐 경우**: 이전 세션의 in-memory 대화는 사라졌다 → 첫 호출(1번)부터 다시 시작. ongoing 협업의 영속성은 agent 본체가 세션 시작 시 `research/ogilvy/` 등 파일을 읽어 보강하는 것으로 처리하며 — 그건 agent 본체의 책임이지 본 스킬의 책임이 아니다.

main Claude는 ogilvy agent의 voice를 흉내내지 않는다. 자기-답변하지 않는다. 통로 역할만 한다. 사용자가 main에 직접 카피·브랜드 평가를 요청해도 — 본 스킬이 발화된 동안 main은 평가를 *agent에 위임*한다. 이 위임이 collaborator shape의 핵심.

## 종료 트리거

다음 발화가 들어오면 ogilvy 협업을 종료하고 main 통제로 복귀:

- "다른 거장 부르자" / "ogilvy 모드 끝" / "다른 일 하자" / "끝"
- 사용자가 다른 figure 이름을 명시 호출 (맥킨지·파인만·아리스토텔레스 등)
- 작업이 자연스럽게 완결됐을 때 (agent가 종료 한 줄 요약을 낸 후)

종료 후 다음 사용자 발화는 다시 본 스킬의 진입 트리거를 따라야 새 ogilvy 협업이 시작된다.
