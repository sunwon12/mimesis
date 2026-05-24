# ADR 0010: 찰리 멍거 — Latticework of Mental Models (다학제 격자틀) 스킬

- **Status**: Accepted
- **Date**: 2026-05-24
- **Related skill**: `.claude/skills/charlie-munger-latticework/`
- **Source figure(s)**: Charlie Munger (1924–2023)
- **Primary sources**:
  - [research raw](../../research/charlie-munger/latticework-of-mental-models-raw.md)
  - [research summary](../../research/charlie-munger/latticework-of-mental-models-summary.md)
  - USC Business School 강연 "A Lesson on Elementary, Worldly Wisdom As It Relates to Investment Management & Business" (1994; 일부 출처는 1995 — 인용 시 "USC, 1994 (1995 per some sources)")
  - Harvard-Westlake / Stanford 강연들, *Poor Charlie's Almanack* — "lattice work of models", "the man with a hammer", "torture reality so that it fits your models", "lollapalooza", "circle of competence"
  - (미확보, 후속) *Poor Charlie's Almanack* "Talk Eight" — 1996 "Practical Thought About Practical Thought?" Coca-Cola/lollapalooza 워크드 예시 (raw §Gaps에서 2차 paraphrase로만 확인)

## Context

mimesis 스킬 셋에 *사고(thinking) 결*의 거장들이 이미 자리잡으면서, "문제를 다룬다"는 표면을 공유하는 스킬들 사이에 트리거 충돌 압력이 생겼다. 특히 다음 셋이 이미 인접 표면을 점유한다:

- `mckinsey-structured-problem-solving` (ADR 0003) — 한 문제를 MECE 가지로 *분해*.
- `aristotle-causal-why` (ADR 0005) — 한 문제를 근본 원인·4원인까지 *수직 추궁*.
- `feynman-explaining-to-understand` (ADR 0006) — 하나를 진짜 이해했는지 *자기-감사*.

멍거의 latticework는 이 셋과 같은 "문제 사고" 우산 아래 있지만 동작 방향이 다르다. 분해도(MECE), 수직 추궁도(causal-why), 자기-감사도(Feynman) 아니라 — *분해되지 않은 통째 문제 위에 여러 외부 학문의 렌즈를 겹쳐* 합치·충돌·증폭을 읽는 *수평 교차검증*이다. raw/summary가 보존한 멍거 고유의 결은 다음으로 좁혀진다:

- "all the wisdom of the world is not to be found in one little academic department" (Q2, Q3) — 단일 학과 세계관 거부.
- "the man with only a hammer … every problem looks like a nail" + "torture reality so that it fits your models" (Q2, Q11) — 단일 모델이 현실을 비튼다.
- "lollapalooza … four or five of these things working together" (Q7, Q8) — 같은 방향 힘들의 비선형 증폭.
- circle of competence (Q10, C3) — 격자틀 출력의 신뢰 경계.

이 결은 mimesis 기존 셋(통설 의심 / 모드 진단 / 구조화 / 외부 분해 / 개별 적합성 / 내부 self-audit)에서 *비어 있다* — "내가 한 분야 모델로만 풀고 있다"는 가장 흔한 인지 편향에 대한 도구가 없었다. 그래서 멍거를 들인다.

shape 판정: **diagnostic**. latticework는 1턴에 돌리는 *사고 동작*이지 멀티턴 페르소나가 아니다. 따라서 SKILL.md 본문이 곧 본체이며 별도 `.claude/agents/<figure>.md` 를 spawn하지 않는다 (collaborator 라우팅 규칙 — `Agent`/`SendMessage` — 비적용). shape 분기 SSOT는 `ADR/meta/0002-collaborator-agent-shape.md`.

## Decomposition

summary의 구조를 그대로 옮기되 스킬화 결정에 직결된 축으로 재정리한다.

### One-line essence (summary §One-line essence)

"하나의 문제를 여러 학문의 무게 있는 모델에 동시에 통과시키고 — 자기 전공 모델에 욱여넣는 대신 — 모델들이 합치·충돌·증폭되는 지점을 읽되, 오직 circle of competence 안에서만 결과를 신뢰하라." (근거: Q1, Q2, Q3, Q9, Q10)

### Core principles → Mental moves 매핑

summary의 8 core principles + 7 mental moves를 스킬화하면서 **7-step procedure**로 옮겼다. 1:1에 가깝게 매핑되어 압축 손실이 거의 없다:

- summary Move 1 (catch the hammer) → SKILL Move 1 (근거: Q2, Q11)
- summary Move 2 (pull big models from big disciplines) → SKILL Move 2 (근거: Q3, Q4, Q5, Q6)
- summary Move 3 (two tracks) → SKILL Move 3 (근거: Q9)
- summary Move 4 (agree/conflict) → SKILL Move 4 (근거: Q7, Q8)
- summary Move 5 (read for lollapalooza) → SKILL Move 5 (근거: Q7, Q8)
- summary Move 6 (weight by reliability & limits) → SKILL Move 6 (근거: Q5, Q6, Q7)
- summary Move 7 (bound by circle of competence) → SKILL Move 7 (근거: Q10, C3)

Core principle 1 (facts useless until on latticework, Q1)과 principle 4 (handful carries the freight, Q4)는 별도 Move로 두지 않고 Move 2의 Why + Heuristic("모든 모델을 통달하려 하지 마라")로 흡수했다 — lean 원칙. principle 1은 Anti-pattern "격자틀 없는 사실 암기"로도 surface.

### Heuristics (summary §Heuristics)

summary 8개 휴리스틱 중 7개를 SKILL.md에 살림 (one-or-two-models-stop; home-tool-as-warning; learn-the-big-handful; weight-by-reliability; 4-5-forces-lollapalooza; learn-each-model's-limits; bet-inside-competence). "두 트랙으로 돌려라"(Q9)는 휴리스틱이 아니라 절차 Move 3로 더 강하게 살아 별도 휴리스틱에서는 생략 (중복 회피).

### Anti-patterns (summary §Anti-patterns)

summary 6개 anti-pattern 6개 전부 SKILL.md에 흡수 (man-with-a-hammer; rote facts without latticework; single-discipline worldview; chauffeur knowledge; out-of-competence overreach; parroting models). 각 Why가 summary Q/C번호에 직결.

### When this thinking applies / boundaries (summary §When this thinking applies)

적용 영역 + 안 맞는 영역 + 인접 방법 경계(McKinsey/Aristotle/Feynman)를 SKILL.md "When to use"로 옮김. 인접 방법 3종 경계는 description에도 박아 Triggering guide 체크리스트 5번(should-NOT-trigger) 통과. SKIP 조건 3종(고밸리디티 단일학문 / out-of-competence / chauffeur)도 description과 본문 둘 다에 surface.

### Open tensions (summary §Open tensions)

- "generalist breadth vs specialist depth" (tension #1) → SKILL.md "호출하지 말 것" 1번(고밸리디티 단일학문)으로 surface + 아래 Consequences §Negative에 미해결로 보존. *어디서* high-validity인지 가르는 선이 raw에 없다는 한계는 Open questions에.
- "know the models vs tacit knowledge" (tension #2) → Anti-pattern "chauffeur knowledge" + "모델을 얕은 복제로 앵무새질" 두 곳, 그리고 "호출하지 말 것" 3번으로 박힘.
- "lollapalooza word vs concept location" (tension #3) → Move 5가 탐지 신호를 Q8(Harvard 1995, "네다섯 개")에 기댄다고 명시. 본문 인용 문구는 Q8 기준으로 적음.

## Decision

### 트리거 (description 설계)

description에 박은 사용자 표현 (인물·개념 명시 + 자연어 변형):

1. (인물·개념 명시) "찰리 멍거 / Charlie Munger / 멍거 / Munger / latticework / 격자틀 / mental models / 멘탈 모델 / 멘탈모델 / man with a hammer / 망치를 든 사람 / 망치 든 사람 / lollapalooza / 롤라팔루자 / worldly wisdom / 다학제 모델 / 여러 학문의 모델로"
2. (자연어, 멍거 명시 없이도) "한 분야 관점으로만 보고 있는 것 같아" / "내 전공 모델로만 풀고 있어" / "다른 분야 관점에서도 봐줘" / "여러 학문의 렌즈로 검토해줘" / "여러 요인이 한 방향으로 겹쳐서 증폭되는 것 같아" / "이 결정 과신하는 것 같은데 다른 각도로" / "물리·생물·심리 모델로 같은 문제를 보면"

명시적 인물명 없이도 트리거되도록 "사용자가 멍거를 명시하지 않아도" 한 줄을 박았다. 단, 거장 스킬 트리거 정책(`ADR/meta/0001-master-router.md`)에 따라 *애매한* 표현("멘탈 모델" / "여러 관점으로"만 있고 명백한 다학제 의도 없음)은 master-router를 거쳐 분기하도록 권장 흐름을 description에 한 줄로 박았다.

should-NOT-trigger 경계:
- 인접 방법 3종(`mckinsey-structured-problem-solving` MECE 분해 / `aristotle-causal-why` 근본원인 수직추궁 / `feynman-explaining-to-understand` 자기-감사)과의 구별을 description과 본문 둘 다에 명시.
- SKIP 조건 3종(고밸리디티 단일학문 / out-of-competence / chauffeur knowledge)을 anti-pattern 근거(C2~C5, Q10)와 함께 박음.

Triggering guide 5개 항목 모두 통과 (80자 이상 / 무엇을 / 언제·표현 5개+ / 명시 안 해도 트리거 한 줄 / should-NOT 한 줄).

### 스킬명 — 왜 `charlie-munger-latticework`인가

후보 비교:

- `charlie-munger-latticework` (선택) — figure-anchored + 멍거의 시그니처 고유 개념명 "latticework"를 직접 운반. 네이밍 룰의 gerund 권장은 *인물 고유 개념명* 예외(README 네이밍 룰: `having-vs-being` 선례)에 따라 면제. "latticework"는 멍거가 직접 명명한 자산이라 gerund(`cross-examining`?)로 바꾸면 오히려 고유성을 잃는다.
- `charlie-munger-mental-models` — 너무 일반적. "mental models" 담론 전체(아무나 쓰는 라벨)와 트리거 표면이 겹쳐 figure-anchored 고유성이 흐려진다.
- `munger-multidisciplinary-thinking` — 동작은 맞지만 (a) 멍거의 고유 명명을 버리고 (b) 너무 길고 (c) "multidisciplinary"가 일반 명사라 변별력이 낮다.

따라서 `charlie-munger-latticework`. ASCII lowercase + hyphens, 26자, Claude Code 검증 룰 통과.

### 입력 / 출력 계약

- **입력**: 여러 학문이 걸쳐 있을 법한 *하나의* 문제·결정. 사용자가 한 분야 모델로만 풀고 있거나, 여러 힘이 겹친다는 직감을 가진 상황.
- **출력 계약** (SKILL.md "Output expected"): (1) 문제 한 줄 + 망치 명명, (2) 적용한 큰 모델 한 줌, (3) 두 트랙 판정, (4) 합치·충돌 맵, (5) lollapalooza 판정, (6) 신뢰도·한계 가중 결론, (7) circle of competence 판정 한 줄.

### 잘라낸 것 (의도적 제외)

이 결정이 ADR의 핵심이다.

1. **Inversion ("invert, always invert") — 별도 미래 스킬로 보류.** 멍거의 대표 방법이지만 latticework와 *별개의 동작*이다 (문제를 뒤집어 실패 조건부터 보는 것 ≠ 여러 학문 모델을 겹치는 것). raw §Gaps가 "inversion은 light evidence만 의도적으로 수집했다"고 명시 — 이 스킬에 끼워넣으면 둘 다 흐려진다. description에도 "inversion은 이 스킬이 떠맡지 않는다"를 한 줄로 박아 트리거 누수를 차단. 별도 figure-anchored 스킬(`charlie-munger-inverting`?)로 독립 research 후 분리.

2. **25가지 인간 오판 원인 체크리스트 — 별도 미래 스킬로 보류.** 심리적 misjudgment의 *카탈로그 점검*은 latticework의 심리 트랙(Move 3 Track 2)과 인접하지만, 25개 체크리스트를 통째 돌리는 것은 별개의 동작이며 분량도 독립 스킬급이다. raw §Gaps가 Q8/Q9에서 *가볍게만* 건드렸다고 명시 — 근거가 얕은 상태로 끌어오면 chauffeur knowledge 안티-패턴을 우리가 install하는 셈. Move 3은 "심리적 왜곡을 *한 트랙으로* 잡는다"까지만 하고, 25개 열거는 의도적으로 제외. 별도 스킬로 분리.

3. **워크드 예시(Coca-Cola/lollapalooza 1996)의 멍거 본인 버전 미사용.** raw §Gaps: *Poor Charlie's Almanack* "Talk Eight"의 end-to-end 워크드 케이스가 2차 paraphrase로만 확인됨(미검증). 따라서 SKILL.md Examples는 멍거 본인의 케이스 대신 *우리가 재구성한* 두 사례(SaaS 가격 결정 / 신제품 붕괴 lollapalooza 판별)로 채웠다. 이게 figure 왜곡이 아니라 *절차의 시연*이라는 점을 본문이 명확히 한다. 후속 researcher pass로 "Talk Eight" verbatim 확보 시 Example을 멍거 본인 케이스로 교체 검토.

4. **C4(고밸리디티-전문가-우위)의 1차 출처 부재.** "호출하지 말 것" 1번과 Consequences §Negative의 generalist-vs-specialist 경계는 raw §Gaps에서 *search-summary*일 뿐 1차 논문이 아니다. SKILL.md SKIP 조건으로 *쓰되*, ADR Open questions에 "Kahneman & Klein 2009 같은 1차 출처로 보강 필요"를 박아 한계를 보존.

### Resource 분리 여부

references / scripts / assets 디렉토리를 **만들지 않았다.**

- SKILL.md 본문이 ~170줄 (Principle #2의 300줄 분리 임계 이하).
- 결정론적 helper(scripts/)는 latticework의 본질상 부적합 — 모델 목록을 체크리스트 스크립트로 박제하면 정확히 chauffeur knowledge / "80~90개 카탈로그 훑기" 안티-패턴을 install한다. summary가 "한 줌만 골라 대라(carry heavy freight)"고 명시한 것과 정면 충돌.
- 80~90 모델 카탈로그를 `references/models-catalog.md`로 빼는 것을 검토했으나 기각: (a) 사용자가 *카탈로그 채우기*로 받아들이면 멍거가 경고한 "모델 이름만 읊기"로 변질되고, (b) Move 2의 "큰 학문에서 큰 모델을 *이 문제에* 대본다"는 동작은 카탈로그가 아니라 *적용*이 본질이다. example 2개(다학제 겹치기 + lollapalooza 판별)가 카탈로그보다 절차를 강하게 전염시킨다고 판단. application log 후 재평가.

### Master-router와의 관계

`master-router` 등록 시 잡혀야 할 룰:

- 트리거 신호 = (하나의 문제) + (한 분야 모델로만 보고 있다는 자각 또는 여러 힘이 겹친다는 직감) 조합. *수평으로 여러 학문을 겹치는* 방향성이 결정적.
- 다른 스킬과의 분리:
  - `mckinsey-structured-problem-solving`: 한 문제를 MECE 가지로 *분해*(내부 구조화). 멍거는 통째 문제에 외부 렌즈를 *겹침*. "정리해줘 / 쪼개줘"는 McKinsey, "다른 분야 관점으로"는 멍거.
  - `aristotle-causal-why`: 한 문제를 근본 원인까지 *수직 추궁*. 멍거는 같은 레벨에서 *수평 확산*. "왜 이렇게 됐지 / 근본 원인"은 Aristotle, "여러 학문의 모델로"는 멍거.
  - `feynman-explaining-to-understand`: 하나를 진짜 이해했는지 *자기-감사*. 멍거는 여러 모델을 *가졌다고 전제*하고 그것들이 문제 위에서 어떻게 *결합*하는지 본다.
- ambiguous("멘탈 모델" / "여러 관점으로"만)하면 master-router가 멍거를 후보로 띄우고 사용자 선택. 명시적 인물·개념(멍거/latticework/lollapalooza/man with a hammer)이 있을 때만 직접 호출.

## Consequences

### Positive

- mimesis 사고 스킬 셋이 "통설 의심 / 모드 진단 / 구조화 / 외부 분해 / 개별 적합성 / 내부 self-audit / **다학제 수평 교차검증**" 축으로 넓어진다. "내가 한 분야 모델로만 풀고 있다"는 가장 흔한 전문가 편향("man with a hammer")을 처음 커버.
- 인접 3스킬(McKinsey/Aristotle/Feynman)과 트리거 분담이 *동작 방향*으로 깔끔히 갈린다 — 분해(수직 가지) / 추궁(수직 깊이) / 자기-감사(내부) / **겹침(수평)**. master-router가 결단할 축이 명확.
- lollapalooza 판정이 "여러 요인이 한 방향으로 겹쳐 증폭"되는 비선형 위험·기회를 단일 모델 판정이 놓치는 자리에서 잡아낸다 — Example 2가 그 형태를 시연.
- circle of competence 출력 게이트가 격자틀의 가장 큰 오용(out-of-competence overreach)을 절차 마지막에 차단.

### Negative / Trade-offs

- **Generalist breadth vs specialist depth 미해결.** SKILL.md는 "고밸리디티 단일학문은 SKIP"으로 경계를 그었지만, *어떤 문제가 high-validity인지* 가르는 선이 raw에 없다 (tension #1). 사용자가 specialist가 이길 문제에 격자틀을 휘두르면 얕은 다학제 잡담이 된다.
- **Chauffeur knowledge로의 변질 위험 (자기-적용).** 격자틀을 *형식적으로* 돌리며 모델 이름만 읊는 것이 정확히 멍거가 경고한 함정이고, 이 스킬 자체가 그 형태로 오용될 수 있다. Anti-pattern + "호출하지 말 것" 3번 + Move 2 Why("적용이 본질, 카탈로그 아님")로 막으려 하지만 완전 차단은 불가능.
- **워크드 예시가 우리 재구성.** 멍거 본인의 end-to-end 케이스(Coca-Cola)가 미검증이라 Example이 우리 손으로 만든 사례다 (cut #3). figure 충실도가 검증된 1차 인용 케이스보다 한 단계 약하다.
- **C4 SKIP 조건의 1차 출처 부재.** 고밸리디티-전문가-우위 경계가 search-summary 기반 (cut #4). SKIP 룰을 정당화하는 근거가 단단하지 않다.
- **lollapalooza 탐지 신호의 출처 분산.** "네다섯 개가 함께"라는 탐지 신호는 Harvard 1995(Q8)에서 오고, USC 1994(Q7)는 개념만 가진다 (tension #3). 본문이 Q8 wording을 쓰지만 USC 연도 인용 충돌("1994 vs 1995")도 미해결.

### Open questions

- master-router에서 멍거 vs McKinsey vs Aristotle 분기를 *코드*로 박을 수 있는가, 아니면 "여러 관점으로" 류 ambiguous 표현에서 후보로 띄우고 사용자 선택이 한계인가?
- Move 2의 "큰 학문에서 큰 모델"을 카탈로그 없이 사용자가 실제로 꺼낼 수 있는가? 못 꺼내면 references/models-catalog.md 분리를 재검토해야 하지만, 그 순간 chauffeur 위험이 올라간다 — 이 트레이드오프를 application log로 관찰.
- C4 SKIP 조건을 Kahneman & Klein 2009 같은 1차 출처로 보강하면 "high-validity 판별 선"까지 줄 수 있는가?
- inversion / 25 misjudgment causes를 별도 스킬로 분리할 때 멍거 한 인물에 figure 스킬이 3개가 된다 — figure-anchored 룰상 한 인물 다(多)스킬을 어떻게 master-router에서 분기시킬지 (method-slug 변별로 충분한가).
- description 자연어 트리거 표현 중 실전에서 작동 안 하는 것 가지치기.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - description 트리거 중 실제 호출에 기여한 표현 (특히 멍거 명시 없이 자연어 — "한 분야로만 보고 있어" 류 — 로 호출된 비율).
  - master-router에서 멍거 vs McKinsey vs Aristotle 분기 정확도 — "여러 관점으로 봐줘" 류 ambiguous 입력이 어디로 가는가.
  - Move 5(lollapalooza 판정)가 실제로 비선형 위험을 잡는 빈도 vs Move 7(competence 게이트)이 패스를 유도하는 빈도 — 어느 step이 가장 자주 결론을 *뒤집는가*.
  - 사용자가 Move 2에서 외부 분야 모델을 실제로 꺼내는지, 아니면 자기 전공 모델만 다른 이름으로 재포장하는지 (chauffeur 변질 신호).
  - Example 1(SaaS 가격 다학제 겹치기) vs Example 2(신제품 lollapalooza 판별) 중 어느 쪽이 사용자 self-recognition에 강한가.
  - inversion / 25 misjudgment causes 류 입력이 이 스킬로 잘못 흘러들어오는지 (잘라낸 영역의 트리거 누수 확인).
