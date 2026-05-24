# ADR 0012: 도넬라 메도즈 — Systems Thinking (stocks·flows, feedback, leverage points) 스킬

- **Status**: Accepted
- **Date**: 2026-05-24
- **Related skill**: `.claude/skills/donella-meadows-systems-thinking/`
- **Source figure(s)**: Donella H. Meadows (1941–2001)
- **Primary sources**:
  - [research raw](../../research/donella-meadows/systems-thinking-raw.md)
  - [research summary](../../research/donella-meadows/systems-thinking-summary.md)
  - *Thinking in Systems: A Primer* (Chelsea Green, 2008; posthumous, ed. Diana Wright)
  - "Leverage Points: Places to Intervene in a System" (The Sustainability Institute, 1999; 1997 *Whole Earth* 단축본의 확장)
  - "Dancing with Systems" (메도즈 사후 출간 에세이 — "you can't control a system, you can dance with it")
  - (미확보/2차, 후속) Solow 1972 *World Dynamics* 서평("맞는 데이터, 틀린 구조" 반증 비판), Abson et al. 2017 / Fischer & Riechers 2019(deep-point 과잉강조 비판) — summary §Gaps에서 2차 요약으로만 확인.

## Context

mimesis의 "문제 사고(thinking)" 우산 아래에 이미 네 거장이 인접 표면을 점유하고 있다:

- `mckinsey-structured-problem-solving` (ADR 0003) — 한 문제를 MECE 가지로 *정적 분해*.
- `aristotle-causal-why` (ADR 0005) — 한 결과를 근본 원인까지 *수직 단일 인과* 추궁.
- `charlie-munger-latticework` (ADR 0010) — 분해되지 않은 통째 문제 위에 여러 학문 모델을 *수평으로 겹침*.
- `feynman-explaining-to-understand` (ADR 0006) — 하나를 진짜 이해했는지 *자기-감사*.

이 넷이 공유하는 공백이 하나 있다 — **시간과 피드백**. 넷 다 *한 시점의 정지된 문제*를 다룬다(분해·인과·겹침·감사 모두 스냅샷 동작). 그런데 실무에서 가장 흔히 막히는 문제 중 하나는 "고치려 할수록 재발한다 / 자꾸 진동한다 / 성장이 폭주하거나 정체한다"는 *시간에 걸친 행동 패턴*이다. 이건 분해해도, 단일 인과로 추궁해도, 여러 모델을 겹쳐도 잡히지 않는다 — 원인이 결과를 다시 낳는 *피드백 루프*와 그 사이의 *delay*가 핵심이기 때문이다.

메도즈의 시스템 사고가 정확히 이 공백을 메운다. summary가 보존한 메도즈 고유의 결:

- "structure drives behavior" — 행동은 개인이 아니라 구조에서 나온다(Q22, Q24). 사람을 갈아도 같은 구조면 같은 행동.
- stock은 flow의 누적이고 누적엔 시간이 걸린다 → 진동·오버슈트·붕괴는 항상 delay에서(Q6, Q10, Q11).
- 12 leverage points: 개입 지점을 약함(parameter)→강함(paradigm)으로 랭킹하되 효과↑일수록 저항↑(Q4, Q20).
- "leverage points are counterintuitive" — 사람들은 위치는 맞혀도 *미는 방향*을 거꾸로 잡는다(Q2, Q3).
- "you can't control a system, you dance with it" — 산출은 통제가 아니라 가설(C2, Q21).

이 결은 기존 넷에서 비어 있다. 그래서 메도즈를 들인다.

shape 판정: **diagnostic**. "이 문제 시스템으로 봐줘"는 1턴에 돌리는 *사고 동작*이지 멀티턴 페르소나 대화가 아니다. 따라서 SKILL.md 본문이 곧 본체이며, 별도 `.claude/agents/donella-meadows.md`를 spawn하지 않는다(collaborator 라우팅 규칙 — `Agent`/`SendMessage` — 비적용). 페르소나 대화로 변질되면 점유 축("시스템 동역학 — 피드백·레버리지 1턴 진단")이 무너진다. shape 분기 SSOT는 `ADR/meta/0002-collaborator-agent-shape.md`.

## Decomposition

summary의 구조를 스킬화 결정에 직결된 축으로 재정리한다.

### One-line essence (summary §One-line essence)

"문제를 '누가 잘못했나'가 아니라 '어떤 구조(stock·flow·feedback loop·delay)가 이 시간에 걸친 행동 패턴을 *낳고 있나*'로 다시 본 뒤, 그 구조 위에서 개입 지점을 약함→강함 순으로 랭킹하되 — 강할수록 시스템이 더 저항하고 직관은 방향을 거꾸로 민다는 것을 경고한다." (근거: Q3, Q22, Q20)

### Core principles → procedure 매핑

summary의 7 core principles + 7 mental moves를 스킬화하면서 **7-step procedure + 12-point 랭킹 체크리스트**로 옮겼다. 매핑:

- summary Move 1 (behavior-over-time) → SKILL Move 1 (근거: Q11, Q10, Q6) — principle 5 흡수.
- summary Move 2 (stock/flow 식별) → SKILL Move 2 (근거: Q5, Q6).
- summary Move 3 (feedback loop R/B + delay) → SKILL Move 3 (근거: Q7, Q8, Q9, Q10).
- summary Move 4 (structure → behavior) → SKILL Move 4 (근거: Q22, Q23, Q24) — principle 1 + bounded rationality 흡수.
- summary Move 5 (limiting factor) → SKILL Move 5 (근거: Q27).
- summary Move 6 (12 leverage 랭킹) → SKILL Move 6 + 별도 표 (근거: Q4).
- summary Move 7 (counterintuitive 경고) → SKILL Move 7 (근거: Q12, Q20, Q3, C2) — principle 2·3·4·7 흡수.

principle 6(boundaries are invented, Q25/Q26)은 별도 Move로 두지 않고 "호출하지 말 것"의 경계 조항 + Anti-pattern("내 모델이 네 모델보다 크다" 게임)으로 surface — 경계 설정이 자의적이 되는 영역은 SKIP 조건이라 When-to-use에 박는 게 가장 강하다고 판단(lean 원칙).

### 12 leverage points (summary §The 12 leverage points)

12개를 SKILL.md에 **랭킹 체크리스트 표**로 그대로 박았다 (task 지시 요건). 각 항목을 "이런 개입 후보가 있나?"를 묻는 *식별 질문*으로 변환 — 카탈로그 암기가 아니라 *후보 매핑 도구*로 쓰게 하기 위함. summary의 "왜 이 위치인가" 근거열은 표의 식별 질문 안에 압축해 흡수(중복 회피). "위로 갈수록 효과↑ 저항↑"(Q20)와 "deep만 강조하면 시작점 상실"(C4, C5) 경고를 표 머리·꼬리에 박아 *우월성 선언이 아니라 정렬+저항경고 도구*로 프레이밍.

### Heuristics (summary §Heuristics)

summary 8개 휴리스틱 중 7개를 SKILL.md에 살림(delay; the-more-X; goal+monitor+response; 사람-교체-무용; limiting-factor; 관심≠레버리지; 누락-피드백-복원). "개입 전 beat를 들어라"(C3)는 휴리스틱이자 Move 7·Anti-pattern에 걸쳐 있어 휴리스틱에도 한 줄 살리되 결론 가설화와 묶음.

### Anti-patterns (summary §Anti-patterns)

summary 8개 anti-pattern 전부 SKILL.md에 흡수(개인 탓 / 약한 레버리지 만지작 / 직관대로 밀기 / 정지 사진 / 경계 과대 / 통제 환상 / 12점 고정 공식화 / 관찰 없이 처방 직행). 추가로 open tension #3(deep만 강조하면 실행 막막)을 9번째 anti-pattern("deep만 강조해 시작점 상실")으로 명시 — summary가 "후속 스킬은 랭킹을 우월성 선언이 아니라 후보 정렬+저항 경고로 써야 한다"(C4, C5)고 직접 지시했기 때문.

### Open tensions (summary §Open tensions)

- "랭킹은 효과 순인데 효과가 클수록 못 바꾼다"(tension #1) → 12점 표 머리("효과↑ 저항↑")와 Move 7로 surface, Consequences §Negative에 미해결로 보존.
- "counterintuitive하니 분석하라 ↔ 통제·최적화는 불가능"(tension #2) → Move 7·Anti-pattern("통제 환상")에서 *분석의 산출을 통제가 아니라 가설로* 재정의해 부분 봉합. Output expected가 결론을 가설+면책으로 강제.
- "deep 우월 ↔ deep만 강조하면 막막"(tension #3) → 9번째 anti-pattern + 12점 표 꼬리("deep으로 올라가는 경로까지 줘라").

## Decision

### 트리거 (description 설계)

description에 박은 사용자 표현:

1. (인물·개념 명시) "도넬라 메도즈 / Donella Meadows / 메도즈 / Meadows / Thinking in Systems / 시스템 사고 / systems thinking / leverage points / 레버리지 포인트 / 피드백 루프 / feedback loop / stock and flow / 스톡 플로우 / 시스템 다이내믹스 / system dynamics"
2. (자연어, 메도즈 명시 없이도) "미봉책인데 자꾸 재발해 / 땜질하는데 문제가 안 사라져 / 악순환이야 / 고치려 할수록 더 나빠져 / 이걸 시스템적으로 보고 싶어 / 어디를 건드려야 효과가 클까 / 근본 개입 지점이 어디지 / 자꾸 진동하고 출렁여 / 성장이 폭주·정체하는데 왜인지"

명시 인물명 없이도 트리거되도록 "메도즈를 명시하지 않아도" 한 줄을 박았다. 단, 거장 스킬 트리거 정책(`ADR/meta/0001-master-router.md`)에 따라 *애매한* 표현("이 문제 분석해줘"만 있고 정적분해 vs 다학제겹침 vs 단일인과 vs 동적피드백 의도 불분명)은 master-router를 거쳐 분기하도록 권장 흐름을 description에 박았다.

should-NOT-trigger 경계 — 인접 3스킬과의 구별을 *동작 방향*으로 명시:
- vs `mckinsey-structured-problem-solving`: 정적 MECE *분해*(스냅샷 가지) ↔ 메도즈는 시간·누적 구조.
- vs `charlie-munger-latticework`: 여러 학문 모델을 *수평으로 겹침* ↔ 메도즈는 한 시스템을 *수직 동역학 구조*로 파고듦.
- vs `aristotle-causal-why`: 단일 *수직 인과*("원인 하나→결과 하나") ↔ 메도즈는 다대다·피드백 인과(원인이 결과를 다시 낳음).
- 가르는 결정선: **동적 피드백 루프와 시간 지연을 보는가**. 피드백이 없으면 이 스킬이 아니다.

SKIP 조건 4종을 When-to-use와 description 둘 다에 박음:
1. 단일 선형 인과로 충분 → aristotle-causal-why가 더 빠름.
2. 분 단위 reversible 실험이 더 쌈 → 전체 구조 진단은 무겁다.
3. 정량 모델 과신·analysis paralysis 우려 → 통제 환상.
4. 경계 설정이 자의적이 되는 영역 → 경계는 질문 의존.

Triggering guide 5개 항목 모두 통과(80자 이상 / 무엇을 / 언제·표현 5개+ / 명시 안 해도 트리거 한 줄 / should-NOT 경계 + master-router 한 줄).

### 스킬명 — 왜 `donella-meadows-systems-thinking`인가

- **풀네임 사용**: "meadows"는 흔한 성이자 일반명사(목초지)라, charlie-munger 선례(흔한 성 → 풀네임)대로 `donella-meadows`로 figure를 박았다. `meadows-systems-thinking`은 변별력이 낮고, `donella`만으로는 인물 식별이 약하다.
- **method-slug = `systems-thinking`**: gerund 권장(`-ing`)을 이미 "thinking"이 충족. "systems thinking"은 메도즈의 대표 저작(*Thinking in Systems*)과 직결되는 시그니처 라벨이라 고유성을 운반한다. 후보 `leverage-points`는 12점 도구 하나로 스킬을 축소시켜(behavior-over-time·stock·feedback을 잘라냄) 기각. 후보 `dancing-with-systems`는 시적이지만 트리거 표면이 약하다.
- ASCII lowercase + hyphens, 33자, Claude Code 검증 룰 통과.

### 입력 / 출력 계약

- **입력**: 시간에 걸친 행동 패턴(재발·진동·폭주·정체)이 의심되거나, 개입 후보가 여럿이라 "어디부터?"를 정해야 하는 *하나의* 문제. 사용자가 "누구 탓 / 미봉책 / 악순환"으로 프레이밍한 상황.
- **출력 계약** (SKILL.md "Output expected"): (1) 행동 패턴 한 줄(+의심 delay), (2) stock/flow 맵, (3) feedback loop 목록(R/B + B 부품 + delay), (4) structure→behavior 한 단락(+limiting factor), (5) 12 leverage 랭킹(관심 쏠린 지점 표시), (6) counterintuitive 경고 + *가설 형태* 결론 + "먼저 beat를 듣고 반박받아라" 면책.

### 잘라낸 것 (의도적 제외)

이 결정이 ADR의 핵심이다.

1. **시스템 archetype 카탈로그(fixes that fail, shifting the burden, tragedy of the commons 등)를 별도 도구로 끌어오지 않음.** *Thinking in Systems*는 8개 안팎의 system trap/archetype을 제시하지만, summary에 정식 Q로 채번되지 않았다(raw에서 archetype별 개별 근거 미수집). 근거가 얕은 상태로 8개 archetype 체크리스트를 박으면 멍거 ADR이 경고한 "카탈로그 훑기"와 같은 변질을 install한다. Move 3(R/B 분류) + Move 4(structure→behavior)가 archetype 인식의 *원리*를 담으므로, 명명된 archetype 열거는 의도적 제외. 후속 researcher pass로 archetype별 1차 근거(원문 챕터·예시) 확보 시 `references/system-archetypes.md`로 분리 검토.

2. **정량 SD 모델링(Forrester식 컴퓨터 시뮬레이션, stock-flow 방정식)을 절차에서 제외.** 메도즈의 뿌리는 Forrester의 정량 모델링이지만(Q3), 이 스킬은 *1턴 진단*이고 방정식 시뮬레이션은 별개 동작이며 도구·분량이 독립 스킬급이다. 더 결정적으로 — 메도즈 본인이 정량 모델은 "맞는 데이터, 틀린 구조"일 수 있다고 경고했고(C6, Solow 1972), summary가 통제 환상·analysis paralysis를 anti-pattern으로 박았다. 절차는 *정성적 구조 진단 + 가설*까지만 하고, 정량 시뮬레이션은 SKIP 조건(#3 정량 모델 과신)으로 오히려 차단.

3. **"Dancing with Systems"의 14개 실천 지침 전체를 옮기지 않음.** "먼저 beat를 들어라 / 모델을 공개해 반박받아라 / 모르면 배워라"(C3)만 Move 7·휴리스틱·Output 면책으로 살리고, 나머지(예: "기대치를 책임지라", "고귀함의 영역을 넓혀라" 등)는 제외. **Why:** 이 스킬은 *진단 procedure*이지 메도즈의 윤리·태도 매니페스토 전체가 아니다. 핵심은 "산출을 통제가 아니라 가설로, 관찰·반증에 열어둔다"는 *진단 자세* 하나 — 그것만 박으면 tension #2(분석 ↔ 통제불가)가 봉합된다. 나머지를 다 끌어오면 lean이 깨지고 페르소나 설교로 변질된다.

4. **MECE/멍거/단일인과와의 대비가 메도즈 본인 인용이 아님(summary §Gaps).** When-to-use·description의 인접 스킬 경계는 summary가 명시했듯 *간접 근거(Q5·Q6·Q25·Q26·다대다 인과 언급)에서 추론한 우리의 분기*이지 메도즈가 세 방법을 직접 호명한 인용이 아니다. 따라서 SKILL.md는 "메도즈 vs 맥킨지"를 메도즈의 *주장*으로 적지 않고, *우리 레포의 트리거 분담 규칙*으로 적었다(동작 방향 차이로 가름). 이 구별은 ADR Consequences와 Open questions에 보존.

5. **deep-point 과잉강조 비판(C5)·Solow 정량 비판(C6)의 1차 출처 부재.** 9번째 anti-pattern과 SKIP #3은 summary §Gaps에서 2차 요약(Abson et al. 인용문헌, Solow 서평 미확보)으로만 근거된다. SKILL.md에 *쓰되*, ADR Open questions에 "1차 출처(Fischer & Riechers 2019, Solow *World Dynamics* 서평)로 보강 필요"를 박아 한계를 보존.

### Resource 분리 여부

references / scripts / assets 디렉토리를 **만들지 않았다.**

- SKILL.md 본문이 ~110줄(12점 표 포함, Principle #2의 300줄 분리 임계 이하).
- 결정론적 helper(scripts/)는 부적합 — stock/loop 식별·레버리지 랭킹을 스크립트로 박제하면 정확히 "12점을 고정 공식으로 사용"하는 anti-pattern(C1: "순서가 미끄럽다, 모든 항목에 예외")을 install한다. 메도즈가 사다리를 "work in progress"로 못 박은 것과 정면 충돌.
- 12 leverage points를 `references/leverage-points.md`로 빼는 것을 검토했으나 기각: (a) 12점은 이 스킬의 *핵심 동작*(Move 6)이라 본문에서 빠지면 절차가 절름발이가 되고, (b) 표 자체가 ~14줄로 분리 임계에 한참 못 미친다. system archetype 카탈로그(cut #1)는 *분리 후보지만 근거 미확보*라 지금은 references/도 만들지 않고 후속 research를 기다린다. application log 후 재평가.

### Master-router와의 관계

`master-router` 등록 시 잡혀야 할 룰:

- 트리거 신호 = (하나의 문제) + (시간에 걸친 행동 패턴: 재발·진동·폭주·정체 / 또는 "어디를 건드려야 효과가 클까") 조합. *동적 피드백·시간 지연* 방향성이 결정적.
- 다른 스킬과의 분리(동작 방향):
  - `mckinsey-structured-problem-solving`: 정적 MECE 분해. "정리·쪼개줘"는 McKinsey, "자꾸 재발·진동해 / 시스템으로 봐줘"는 메도즈.
  - `charlie-munger-latticework`: 여러 학문 모델 수평 겹침. "다른 분야 관점으로"는 멍거, "이 구조가 이 행동을 낳아"는 메도즈.
  - `aristotle-causal-why`: 단일 수직 인과. "왜 이렇게 됐지(원인 하나)"는 Aristotle, "원인이 결과를 다시 낳는 악순환"은 메도즈.
- ambiguous("이 문제 분석해줘"만)하면 master-router가 메도즈를 후보로 띄우고 사용자 선택. 명시적 인물·개념(메도즈/leverage points/feedback loop/stock-flow)이 있을 때만 직접 호출.

## Consequences

### Positive

- mimesis 사고 스킬 셋이 "통설 의심 / 모드 진단 / 정적 분해 / 단일 수직 인과 / 다학제 수평 겹침 / 자기-감사 / **동적 피드백·레버리지 진단**" 축으로 넓어진다. *시간과 피드백*이라는 기존 공백을 처음 커버 — "고치려 할수록 재발한다"는 가장 흔한 구조적 좌절에 도구가 생긴다.
- 인접 3스킬(McKinsey/Munger/Aristotle)과 트리거 분담이 *동작 방향*으로 깔끔히 갈린다 — 정적 분해(수직 가지) / 수평 겹침 / 단일 수직 인과 / **동적 피드백(시간·루프)**. master-router가 결단할 축이 명확.
- "structure drives behavior" 재귀속이 "누구 탓"의 함정에서 빠져나오게 한다 — 사람 교체로 해결하려는 가장 흔한 약한-레버리지 반사를 Move 4가 잡는다.
- counterintuitive 경고 + 가설-형태 결론 강제가 시스템 사고의 가장 큰 오용(정답 레버리지를 밀면 통제된다는 환상)을 절차 마지막에 차단. Output 면책이 "진단=처방"으로의 미끄러짐을 막는다.

### Negative / Trade-offs

(거장 프레임의 한계 — summary §Critiques & limits·Open tensions 반영)

- **강력함 ↔ 실행가능성 미해결(tension #1).** 12점 랭킹은 효과 순인데 효과가 클수록 시스템이 가장 격렬히 저항한다(목표·패러다임). 메도즈는 "바꾸기 어려움"과 "레버리지 크기"를 별개 축으로 분리하라 하지만, 그래서 실무자가 "그럼 어디부터?"에 답하기 어렵다는 비판(C4, C5)이 남는다. 9번째 anti-pattern으로 완화했으나 완전 해소는 아니다.
- **deep/shallow 상호작용 미해명(tension #3).** 사다리 상위가 우월하다는 게 자산이지만, deep만 강조하면 시작점을 못 찾고, deep과 shallow 레버리지가 *어떻게 상호작용하는지*는 raw에 없다. SKILL.md는 "shallow에서 시작해 deep으로 올라가는 경로"를 권하지만 그 경로의 구체적 규칙은 비어 있다.
- **분석 ↔ 통제불가의 봉합이 불완전(tension #2).** 산출을 "가설"로 재정의해 봉합했으나, 정량 모델이 "맞는 데이터, 틀린 구조"일 수 있다는 반증가능성 문제(C6)는 남는다 — 정성 진단조차 틀린 구조 위에 설 수 있다. 면책 한 줄로는 이 위험을 *경고*할 뿐 *해소*하지 못한다.
- **경계 설정의 자의성.** principle 6(경계는 질문 의존)을 SKIP 조건으로 박았지만, 사용자가 경계를 너무 좁거나 넓게 잡으면 진단 전체가 오도된다 — 그리고 "올바른" 경계를 가르는 객관 기준은 메도즈에게도 없다.
- **인접 스킬 경계가 메도즈 본인 인용이 아님(cut #4).** description·When-to-use의 McKinsey/Munger/Aristotle 대비는 *우리 레포의 분기 규칙*이지 메도즈의 직접 주장이 아니다 — figure 충실도 면에서 "메도즈가 직접 그은 선"보다 한 단계 약하다.
- **deep-point 비판·Solow 정량 비판의 1차 출처 부재(cut #5).** 9번째 anti-pattern과 SKIP #3의 근거가 2차 요약 기반이다.

### Open questions

- master-router에서 메도즈 vs McKinsey vs Munger vs Aristotle 분기를 *코드*로 박을 수 있는가, 아니면 "이 문제 분석해줘" 류 ambiguous 입력에서 후보로 띄우고 사용자 선택이 한계인가? 특히 "시간에 걸친 행동 패턴" 신호를 자동 감지할 수 있는가.
- system archetype 카탈로그(cut #1)를 후속 research로 정식 채번하면 `references/system-archetypes.md`로 분리할 가치가 있는가, 아니면 archetype 열거가 "카탈로그 훑기" 변질을 부르는가?
- deep/shallow 상호작용(tension #3)을 보강할 1차 출처가 있는가 — "shallow에서 deep으로 올라가는 경로"에 구체 규칙을 줄 수 있는가?
- C5/C6 비판을 1차 출처(Fischer & Riechers 2019, Solow *World Dynamics* 서평)로 보강하면 SKIP #3·9번째 anti-pattern의 근거가 단단해지는가?
- 한국어 1차/번역서 역어 대조 부재 — description의 한국어 트리거 표현("스톡 플로우" 등)이 국내 번역서 역어와 어긋나면 트리거가 새는가? application log로 관찰.
- description 자연어 트리거 표현 중 실전에서 작동 안 하는 것 가지치기.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - description 트리거 중 실제 호출에 기여한 표현 (특히 메도즈 명시 없이 자연어 — "미봉책인데 자꾸 재발" / "악순환" 류 — 로 호출된 비율).
  - master-router에서 메도즈 vs McKinsey vs Munger vs Aristotle 분기 정확도 — "이 문제 분석해줘" 류 ambiguous 입력이 어디로 가는가, "시간에 걸친 행동 패턴" 신호가 메도즈로 라우팅되는가.
  - Move 1(behavior-over-time 재프레이밍)이 실제로 사용자의 정지-사진 프레이밍을 뒤집는 빈도.
  - Move 6(12 leverage 랭킹)이 실제로 "관심 쏠린 곳(보통 #12)"과 "효과 있는 곳"의 괴리를 드러내는 빈도 — counterintuitive 경고가 결론을 *뒤집는* 비율.
  - Output의 "가설 형태 + 면책" 강제가 사용자가 진단을 처방으로 오용하는 것을 실제로 막는지.
  - deep-point만 강조해 "그래서 어디부터?"에서 좌절하는 케이스가 나오는지 (tension #1·#3의 실전 발현).
  - system archetype을 사용자가 요청하는데 스킬이 못 주는 케이스 빈도 (cut #1 분리 필요성 신호).
