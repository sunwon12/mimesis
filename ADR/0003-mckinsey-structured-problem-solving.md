# ADR 0003: 맥킨지 — 구조화된 문제 해결 스킬

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/mckinsey-structured-problem-solving/`
- **Source figure(s)**: McKinsey (대표 lineage: Barbara Minto · Ethan Rasiel · Charles Conn & Robert McLean)
- **Primary sources**:
  - [research raw](../research/mckinsey/structured-problem-solving-raw.md)
  - [research summary](../research/mckinsey/structured-problem-solving-summary.md)
  - Barbara Minto, *The Pyramid Principle* (Pyramid / SCQA / MECE 정의)
  - Ethan Rasiel, *The McKinsey Way* (MECE 운영 테스트 · "don't boil the ocean" · hypothesis-driven)
  - Charles Conn & Robert McLean, *Bulletproof Problem Solving* (7-step process · one-hour answer · impact×movability · false precision 경계)

## Context

mimesis의 첫 두 스킬은 단일 인물(이어령·프롬)의 단일 mental move였다. 두 번째 도전 영역은 사용자가 가장 자주 부딪히는 "복잡·모호한 의사결정"이다: 비즈니스 전략, 제품 결정, 정책 설계, 그리고 개인의 진로/이직 같은 비가역 결정.

이 영역에서 사람들이 막히는 양상은 일관적이다 — (1) 문제 자체가 한 문장으로 안 써지고, (2) 데이터부터 모으다가 길을 잃고, (3) 분석은 쌓이는데 "그래서 뭐 해야 하지"로 안 모이고, (4) 마지막에 의사결정자에게 던지는 보고가 bottom-up이라 답을 못 찾는다.

이 4가지 막힘을 통째로 풀어주는 사고법이 맥킨지에서 60년에 걸쳐 정착된 "structured problem solving"이다. 단일 인물에 귀속되지는 않지만(Minto는 communication, Rasiel은 day-to-day discipline, Conn/McLean은 7-step process로 각자 다른 결을 다듬었다), 한 firm의 일관된 사고 전통이 명확히 있으므로 mimesis의 "거장 귀속" 원칙을 firm-anchored 변형으로 적용한다.

## Decomposition

summary의 구조를 그대로 옮기되, 스킬화에 필요한 5개 축으로 재정리한다:

### Core principles (summary §Core principles)
1. **Structure is upstream of thinking, not its residue.** (Q9, Q15, Q21) — Rasiel의 "structure·MECE·hypothesis"는 한 stool의 세 다리. Conn은 구조가 창의성을 가능케 한다고 본다.
2. **MECE는 vibe가 아니라 binary 테스트다.** (Q1, Q10) — Minto의 정의를 Rasiel이 두 yes/no 질문으로 운영화.
3. **Answer first — 단, answer는 verdict가 아니라 hypothesis.** (Q4, Q12, Q20, Q26) — Minto의 writing rule + Rasiel의 problem-solving rule + Conn의 one-hour answer = 같은 원칙의 세 surface.
4. **Pyramid는 reader cognitive load의 geometry.** (Q5) — 스타일이 아니라 이해의 물리학.
5. **Prune by impact × movability.** (Q13, Q19) — boil-the-ocean의 반대 원칙.
6. **Output은 finding deck이 아니라 decision-maker용 story.** (Q7, Q14, Q22, Q27) — synthesize와 communicate는 한 단계.
7. **Calibrate certainty out loud.** (Q23) — false precision은 그 자체로 anti-pattern.

### Mental moves (summary §The mental moves) — 9 steps
스킬에는 9개를 모두 살렸다. 7±2 제약 내에서 절차의 충실도가 더 중요하다고 판단 — step 5(one-hour answer)와 step 7(iterate)은 빠지면 process 전체가 waterfall로 무너지기 때문에 절대 빼지 않는다.

(Q16/Q17/Q25 → step 1, Q3/Q10/Q11/Q18/Q24 → step 2, Q9/Q12/Q26 → step 3, Q13/Q19 → step 4, Q20/Q26/Q28 → step 5, Q20/Q21/Q26 → step 6, Q28 → step 7, Q3/Q22 → step 8, Q4/Q7/Q23 → step 9)

### Heuristics (summary §Heuristics & decision rules)
운영 가능한 휴리스틱 7개를 살림: MECE binary 테스트, 자식 2~5(3이 best), 한 시간 답 진단, impact×movability 두 축 동시 통과, "어색함은 정의 결함 신호", 추천에 조건 첨부, 50페이지 금지. (각 Q번호는 SKILL.md Why 줄에 직결.)

### Anti-patterns (summary §Anti-patterns)
8개 모두 살림: boil the ocean(Q13), 데이터부터 모으기(Q17/Q25), MECE 위반(Q1/Q10), bottom-up 보고(Q8), 가설 없는 분석(Q9/Q12/Q26), 확답으로 가장(Q23), 못 움직이는 가지에 시간 쓰기(Q19), 작년 모델 import(Q24).

### Open tensions (summary §Open tensions)
SKILL.md 본문에는 5개 tension을 모두 박지 않았다 — lean 원칙. 단 step 5/6 ("답을 죽일 증거")의 Why에 "sunflower bias / answer-first vs confirmation bias" 긴장의 raw 해결책 (work plan은 hypothesis를 죽이도록 짠다)을 녹였다.

## Decision

### 트리거 (description 설계)
사용자가 실제로 쓸 표현을 12개 박았다: "이 문제 어디서부터 풀어야 하지", "이게 너무 모호한데", "MECE", "구조화 좀 해줘", "이슈 트리", "가설 세워볼까", "어떻게 정리해서 보고하지", "전략 자료 만들어야 하는데", "what why how가 다 섞여있어", "scope가 너무 넓어", "boil the ocean 하지 말라는데 어떻게 줄이지", "임원한테 뭐라고 답해야 하지". "맥킨지/pyramid를 명시 안 해도 트리거" 한 줄을 박았고, should-NOT-trigger 경계 3종(단순 실행 / 빠른 피드백 루프 / 창의적 발산)을 명시. Triggering guide 5개 항목 통과.

### 스킬 단위 — 왜 5요소를 한 스킬로 묶었는가
MECE만, Pyramid만, SCQA만, Hypothesis-driven만, Issue tree만 — 각각을 5개 스킬로 분해하는 안도 검토했다. 그러나:

1. **substantive task에서 트리거되어야 한다** (Principle #5). 사용자가 "이슈 트리 짜줘"라고 정확히 말하는 경우는 드물고, 실제 호출 시그널은 "이 문제 어디서부터..." 같은 복합 막힘이다. 그 막힘을 풀려면 5요소가 함께 가야 한다 — MECE 트리를 짜도 hypothesis 라벨이 없으면 분석이 안 끝나고, hypothesis가 있어도 pyramid가 없으면 보고가 무너진다.
2. **맥킨지의 원전이 이미 묶음으로 작동한다.** Rasiel의 "structure·MECE·hypothesis"는 세 다리의 stool로 제시되고, Conn/McLean의 7-step은 정의→분해→가설→가지치기→work plan→synthesize→communicate를 한 loop로 짠다. 인위적으로 자르는 게 오히려 원본 사고를 왜곡한다.
3. **소형 스킬 5개보다 substantive 묶음 스킬 1개가 호출 확률이 높다** — under-trigger 경향(Principle #1)을 고려할 때, 묶음이 트리거 표면이 더 넓다.

### 스킬명 — 왜 method-slug가 gerund가 아닌 명사구인가
mimesis Hard rules는 "가능하면 gerund(-ing)"를 권장하지만 예외를 허용한다 ("인물 고유 개념명은 예외"). "structured-problem-solving"은:
- gerund 후보들(`structuring`, `decomposing`, `pyramid-ing`)이 각각 5요소 중 하나만 가리켜 묶음을 표현하지 못한다.
- 맥킨지 firm 내부와 외부에서 이 묶음을 부르는 표준 명사구가 이미 "structured problem solving" (Conn/McLean 책의 챕터 제목 포함).
- 즉, 인물 고유 개념명에 해당하는 firm 고유 개념명이므로 예외 적용. ADR에 그 근거를 명시.

또한 figure-anchored 룰을 firm-anchored로 적용했다 — McKinsey는 단일 인물이 아니지만 README에 figure로 등재됐고, 5요소가 한 firm의 일관된 사고 전통이라 lineage(Minto/Rasiel/Conn&McLean)는 본문 인용과 ADR Decomposition에서 surface 한다.

### 포함한 mental moves
9개 step 전부 + 7개 heuristic + 8개 anti-pattern + 2개 example (B2C SaaS 이탈률 결정 + 개인 이직 결정). example을 비즈니스 한 케이스, 개인 한 케이스로 결을 넓힌 것은 사용자가 후자에서 호출을 놓치기 쉽기 때문 — 개인 의사결정에서도 변수가 많고 비가역이면 이 스킬이 작동한다는 신호를 example로 박았다.

### 의도적으로 잘라낸 것
- **Open tensions 5개를 SKILL.md 본문에 노출하지 않음** — lean 원칙. "calibrate certainty out loud"와 "hypothesis to be falsified" 두 점만 step 5/6/9의 Why에 녹여 confirmation-bias 긴장의 실용적 해결을 살렸다. 나머지(MECE 인위성, 체크리스트화 위험)는 적용 로그가 쌓이면 후속 ADR로 분리.
- **Marvin Bower 계열 "obligation to dissent"** — summary §Gaps에서 raw에 없다고 명시. 스킬에는 안 박았다.
- **TOSCA / 7 characteristics of a good problem statement 디테일** — raw에 verbatim이 없어 step 1을 추상적으로 남김. 후속 researcher pass가 이걸 보강하면 step 1을 더 구체화 가능.
- **Red team / pre-mortem 같은 confirmation-bias 카운터수단** — raw가 안 다뤘고, 묶음 스킬 안에서 다루면 스코프가 흐려진다. 별도 스킬 후보.

### Resource 분리 여부
references/scripts/assets 디렉토리를 만들지 않았다.
- 본문이 ~250줄 (500줄 임계 이하).
- 결정론적 helper(가지치기 계산, MECE 검증 자동화 등)는 현재 단계에서 박제할 만큼 호출 패턴이 안 쌓였다 — application log 후 재평가.
- pyramid/SCQA 보고 템플릿을 `assets/` 로 빼는 것도 검토했으나, 사용자 도메인이 너무 다양해서(B2B vs 개인) 한 템플릿보다 example 2개가 강하다고 판단.

## Consequences

### Positive
- 사용자가 "어디서부터 풀지" 막혔을 때 단일 호출로 정의→분해→가설→가지치기→work plan→synthesize→보고까지 일관된 산출물(Output expected의 7개 artifact)을 얻는다.
- under-trigger 경향을 묶음 스킬 + 12개 트리거 표현으로 보강 — 사용자가 "맥킨지"를 명시 안 해도 호출 가능.
- example 2개(비즈니스 + 개인)로 적용 범위를 넓혔다. 진로 결정 같은 비가역 개인 의사결정에서도 활용 가능.
- 5요소의 lineage(Minto/Rasiel/Conn&McLean)를 ADR Decomposition에 명시 — 후속 스킬(예: feynman과 비교한 학습법 lineage, lee-eo-ryeong-questioning과 결합한 문제 발견)이 이 ADR을 참조해 다른 결을 분리해갈 수 있다.

### Negative / Trade-offs
- **묶음 스킬이라 학습 곡선이 가파르다** — 9 step + 7 heuristic + 8 anti-pattern을 한 번에 마주하면 압도될 수 있다. 사용자가 일부만 적용해도 가치가 나오도록 step 1과 step 5(one-hour answer)를 핵심 진단점으로 박았다.
- **MECE의 인위성 문제 미해결** — summary open tension에 적힌 대로 raw가 이 비판에 직접 답하지 않는다. 본문에는 "두 번째 cut을 해라" (step 2)로 부분 완화만 했다.
- **묶음의 특성상 작은 의사결정에 오용될 위험** — should-NOT-trigger 경계 3종을 description에 박았지만, 사용자가 "정리 좀 해줘" 라고만 말하면 단순 정리 task에서도 호출될 수 있다. application log로 모니터링 필요.
- **firm-anchored 적용의 일관성 부담** — figure-anchored 룰의 firm 변형을 한 번 허용했으므로, 후속에 "베인" "BCG" 등 다른 firm 스킬이 들어오면 같은 원칙을 적용해야 한다. 이건 README의 figure 등재 단계에서 거를 수 있다.

### Open questions
- step 5(one-hour answer)와 step 7(iterate)이 실제 적용에서 가장 자주 빠진다는 가설 — application log로 검증해야 함.
- example을 더 도메인-specific하게 (예: 정책 결정, 조직 재설계) 늘려야 할까, 아니면 현재 2개로 충분한가.
- Pyramid/SCQA 보고 템플릿을 `assets/template.md` 로 빼는 것이 가치가 있을지 — 3번째 application 후 재평가.
- Confirmation-bias 카운터수단(red team, pre-mortem)을 별도 스킬로 분리할 가치가 있는가, 아니면 이 스킬의 step 6에 흡수할 가치가 있는가.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - step 1의 problem statement 한 문장이 실제로 한 문장으로 수렴하는 빈도
  - step 5의 one-hour answer가 step 1로 돌려보내는 빈도 (진단 신호로서의 유용성)
  - 12개 트리거 표현 중 실제로 호출에 기여한 표현
  - 개인 의사결정 example이 호출에 기여하는지 (비즈니스 도메인 외 확장 가설 검증)
