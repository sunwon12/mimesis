# ADR 0011: 조지 오웰 — Writing with Clarity (유리창 같은 글) 스킬

- **Status**: Accepted
- **Date**: 2026-05-24
- **Related skill**: `.claude/skills/orwell-writing-clearly/`
- **Source figure(s)**: George Orwell (1903–1950)
- **Primary sources**:
  - [research raw](../../research/orwell/writing-with-clarity-raw.md)
  - [research summary](../../research/orwell/writing-with-clarity-summary.md)
  - *Politics and the English Language* (1946) — 여섯 규칙(Q11), 양심적 작가의 4+2 질문(Q7), 나쁜 습관 네 범주(Q6), 전도서 원문 vs 패러디 시연(Q8, Q9), "명료한 언어의 가장 큰 적은 위선"(Q4), 규칙은 본능 실패 시의 안전장치(Q10)
  - *Why I Write* (1946) — "좋은 산문은 유리창"(Q14), 글쓰기 동기는 거짓 폭로·사실 환기(Q15), 정치적 목적 없을 때 죽은 글을 썼다는 회고(Q16)
  - 비판 진영(SKIP 조건 재료): Geoffrey Pullum의 anti-passive·anti-idiom 논박(C1–C3), 오웰 자신이 에세이에서 수동태를 평균 이상 사용(C4), 오웰 본인의 한계 인정(C5), Ed Smith "plain ≠ honest"(C7, C8), Freedman 발 "평이=중립" 신앙 비판(C9)

## Context

mimesis 로스터에 **글쓰기/작업법(How they work)** 결의 거장이 처음 들어온다 — 지금까지는 사고법(맥킨지·아리스토텔레스·파인만·멍거)·태도(프롬·이어령)·협업(오길비·카파시·서튼)뿐이었고, "이미 쓴 글을 또렷하게 만드는" 자리가 비어 있었다. 백엔드 엔지니어도 ADR·PR·설계문서를 매일 쓰지만 — 이 스킬은 **명시적으로 범용**으로 설계한다(아래 Decision 참조). 사용자가 직접 박은 방향: "이 스킬은 백엔드 엔지니어에 한정된 게 아니라 모두가 범용되게 쓰게 하고 싶어."

거장 선택에서 헤밍웨이(iceberg·voice)·Zinsser(영미 논픽션)·오웰을 비교해 **오웰**을 골랐다. 이유: 글쓰기 거장 중 명료성을 가장 *사고법*으로 만든 사람이다 — 오웰의 핵심 주장은 "문체 다듬기"가 아니라 **흐릿한 언어가 진흙탕/불성실한 생각을 반영하고 *동시에 조장*한다**는 양방향 인과(Q2, Q3)이고, 그래서 흐린 문장은 *증상*으로 진단된다(Q3, Q13). 이건 figure-anchored 컨셉(거장 고유의 *사고 동작*이 자산)에 정확히 맞는다. 헤밍웨이는 스타일·voice 쪽이라 collaborator로 기울고 영역이 좁다.

shape 판정: **diagnostic**. 명료성은 브랜드 voice(주관·누적이라 오길비가 collaborator)와 달리 규칙-지배적이고, "초고 붙여넣기 → 진단 + 타이트한 다시쓰기"의 1턴 pass가 본질이다. 또 *범용/저마찰*(SKILL.md 한 장만 복사하면 누구나 사용)이라는 사용자 요구가 diagnostic을 직접 가리킨다 — collaborator는 agent 본체 + 라우팅이라 마찰이 크다. shape 분기 SSOT는 `ADR/meta/0002-collaborator-agent-shape.md`.

## Decomposition

summary의 구조를 스킬화 결정 축으로 재정리한다.

### One-line essence (summary §One-line essence)

"흐린 문장을 *증상*으로 읽어라 — 안개를 찾고, 그 안개를 만드는 습관에 이름 붙이고, 뜻을 구체적·평이한 말로 도로 밀어 넣고, 그 안개가 덜 정해진/숨기고 싶은 생각을 가렸는지 점검하고, 글이 이제 *유리창*처럼 뜻을 통과시키는지 본다." (근거: Q3, Q4, Q7, Q14)

### Core principles → Mental moves 매핑

summary의 5 core principles + 7 mental moves를 **7-step procedure**로 옮겼다. 핵심 설계 결정은 **여섯 규칙을 절차의 중심에 두지 않은 것**이다 — Step 1(진단 자세)과 Step 4(정직성 점검)를 *앞에* 놓고, 여섯 규칙은 Step 5의 *예시적 전술*로 내렸다.

- summary Move 1 (diagnostic stance) → SKILL Step 1 (근거: Q3, Q4, Q13)
- summary Move 2 (locate the fog, 4 habit categories) → SKILL Step 2 (근거: Q6)
- summary Move 3 (scrupulous-writer interrogation) → SKILL Step 3 (근거: Q7)
- summary Move 4 (honesty check) → SKILL Step 4 (근거: Q4, Q5, Q16)
- summary Move 5 (cut/rewrite via six rules, *not* a filter) → SKILL Step 5 (근거: Q10, Q11)
- summary Move 6 (before/after test) → SKILL Step 6 (근거: Q8, Q9)
- summary Move 7 (re-read for transparency) → SKILL Step 7 (근거: Q14, C8)

Core principle 4 (decide-meaning-first, Q16)는 별도 Move 없이 Step 3의 자문 1번("나는 무엇을 말하려는가")과 Step 4 honesty check에 흡수 — lean 원칙. Core principle 5 (rules-are-servants, Q10/Q11-vi)는 Step 5 Why + Heuristic("규칙은 명료성에 진다") + Anti-pattern("기계적 린터") 세 곳에 분산해 박았다(가장 오용되기 쉬운 지점이라 중복 강조 허용).

### Heuristics (summary §Heuristics)

summary 7개 휴리스틱 전부 SKILL.md에 살림 (can't-answer-what-am-I-saying / long-word-at-weakest-point / cut-with-no-loss / prefer-everyday-word / replace-dead-metaphor / break-rule-if-barbarous / diagnose-by-category).

### Anti-patterns — SKIP 조건의 핵심 (summary §Anti-patterns + Open tensions)

이 스킬의 가장 큰 위험은 **여섯 규칙을 dumb 린터로 변질**시키는 것이라, anti-pattern 7개를 비판 진영 근거(C1–C9)에 직결해 박았다:

- 기계적 린터 (Q10, Q11-vi)
- "수동태 전부 삭제" 패스 거부 (C1, C2, C4 — Pullum + 오웰 본인 20% 수동태)
- "익숙한 표현 일괄 금지" 거부 (C3 — "insane and unfollowable")
- "평이=참" 동일시 거부 (C7, C8 — Ed Smith, plain ≠ honest)
- "평이=중립" 가정 거부 (C9 — Freedman)
- 환원 불가능한 복잡성에 평이함 강요 거부 (C7 — "new puritanism")
- 빈 자리를 장식으로 메우기 거부 (Q16)

### When this thinking applies / boundaries (summary §When this thinking applies)

인접 3종 경계를 SKILL.md "When to use"와 description 둘 다에 박았다 — `ogilvy`(설득·판매, collaborator) / `lee-eo-ryeong-questioning`(새 의미 빚기) / `feynman-explaining-to-understand`(개념 이해 자체 감사). 세 경계 모두 *"이미 정해진 뜻을 또렷이 옮긴다"*는 오웰 고유 동작을 기준으로 가른다.

### Open tensions (summary §Open tensions)

- "처방 vs 자기-한정" (tension #1) → 절차를 *진단 자세·정직성 점검을 앞세우고 규칙은 종속*시키는 구조로 해소(Step 1·4가 Step 5 앞).
- "명료한 언어 ⇒ 명료한 사고, 주장됐으나 미보장" (tension #2) → 진단 가치(안개가 진흙탕 생각을 *자주* 드러낸다)는 살리되, "평이=정직 증명"의 추론은 명시 거부. SKILL.md Step 4·7 Why와 Output #5의 *면책 한 줄*("명료해졌다 ≠ 옳아졌다")로 박음.
- "앵글로색슨 고유 규칙 vs 언어 보편 동작" (tension #3) → **이 스킬의 범용화 핵심.** 절차를 언어 보편 동작으로 짜고 여섯 규칙은 영어 예시 전술로 내렸다. 한국어 산문에 그대로 작동(Examples 둘 다 한국어).

## Decision

### 범용 positioning (이 스킬의 정의적 결정)

레포 방향(메모리: skills-universal-not-backend)에 따라 **명시적으로 도메인 중립**으로 설계했다:
- Examples 2개가 *코딩이 아닌* 일상 산문 — 사내 공지 문단 + 동료에게 보낼 이메일 한 문장.
- description 트리거의 자연어 표현에서 직무 한정어 제거.
- 절차를 언어 보편 동작으로 framing(아래 cut #3).

### 트리거 (description 설계)

1. (인물·개념 명시) "조지 오웰 / George Orwell / 오웰 / Orwell / 정치와 영어 / Politics and the English Language / 좋은 글은 유리창 / windowpane prose / 오웰 6규칙 / 오웰의 여섯 규칙 / plain language / 평이한 언어"
2. (자연어, 오웰 명시 없이도) "이 글 더 명료하게 해줘" / "문장이 뭔가 흐릿해" / "글이 장황해/늘어져" / "군더더기 빼줘" / "무슨 말인지 모르게 쓴 것 같아" / "너무 추상적이고 모호해" / "이 문단 다듬어줘" / "문장이 무겁고 딱딱해" / "전문용어로 떡칠한 것 같아"

should-NOT-trigger 경계:
- 인접 3종(`ogilvy` 설득·판매 / `lee-eo-ryeong-questioning` 새 의미 / `feynman-explaining-to-understand` 개념 이해)과 구별을 description·본문 둘 다에 명시.
- SKIP 2종(환원 불가능한 복잡성 / 진실 측정기 오용)을 비판 진영 근거(C7·C8·C9)와 함께 박음.
- 그냥 "글 좀 봐줘"처럼 명료성 vs 설득 vs 의미-만들기 의도가 불분명하면 master-router 경유 권장 한 줄.

Triggering guide 5개 항목 통과(80자 이상 / 무엇을 / 언제·표현 5개+ / 명시 안 해도 트리거 한 줄 / should-NOT 한 줄).

### 스킬명 — 왜 `orwell-writing-clearly`인가

- `orwell-writing-clearly` (선택) — figure-anchored + gerund-leaning("writing"). 동작이 곧 이름. 누구나 쓰는 자연어("명료하게 써줘")와 트리거 표면이 직접 겹친다.
- `orwell-plain-language` — 기각: "plain language"는 비판 진영(Ed Smith)이 *함정*으로 지목한 바로 그 표현이라, 스킬명으로 쓰면 "평이=좋음"이라는 우리가 거부하는 등식을 이름에 박는 셈.
- `orwell-windowpane` — 고유 개념명이라 매력적이나 너무 비유적이라 자연어 트리거가 약하다.

ASCII lowercase + hyphens, 21자, Claude Code 검증 룰 통과.

### 입력 / 출력 계약

- **입력**: 이미 (대충) 뜻이 정해진 *완성된 초고* — 이메일·보고서·정책 문단·에세이·초록 등 평이한 산문.
- **출력 계약** (SKILL.md "Output expected"): (1) 안개 지도(흐린 자리 + 습관 범주), (2) 자문 1번의 답("진짜 말하려는 것" 한 줄, 못 나오면 정직하게 멈춤), (3) 정직성 점검 결과, (4) 다시 쓴 텍스트 + before/after 자기-판정, (5) 투명성 판정 + **면책 한 줄**("명료해졌다 ≠ 옳아졌다").

### 잘라낸 것 (의도적 제외)

1. **여섯 규칙을 절차의 중심에 두지 않음.** 규칙은 Step 5의 예시 전술로 내리고 진단 자세·정직성 점검을 앞세웠다. **Why:** 오웰 본인(Q10)이 "여섯 규칙을 다 지켜도 나쁜 글"이라 했고, 규칙 중심 스킬은 Pullum이 논박한(C1–C3) dumb 린터로 변질된다. 규칙을 가운데 두면 정확히 그 실패 모드를 install한다.

2. **"수동태 삭제" 류 결정론적 린터 미구현(scripts/ 없음).** **Why:** anti-passive 조언은 언어학적으로 혼란스럽고(C1) 오웰 자신이 20% 수동태를 쓴다(C4). 스크립트로 박으면 거장이 *경고한* 함정을 자동화하는 셈.

3. **여섯 규칙의 영어 고유성 → 언어 보편 동작으로 재framing.** **Why:** 규칙 i(인쇄 상투구)·ii·v(라틴어계 vs 앵글로색슨)·iv(영어 수동태)는 앵글로색슨 색이 강하다(tension #3). 사용자가 주로 한국어로 쓰므로, 절차를 "안개 찾기 → 습관 명명 → 뜻을 구체어로 → 정직성 점검 → 투명성 확인"의 보편 동작으로 짜고 여섯 규칙은 영어 예시로 보존. Examples 둘 다 한국어 산문.

4. **"평이=정직/참" 추론 차단을 절차에 내장.** **Why:** 비판 진영(C7·C8·C9)이 가장 단단하게 때린 지점. 진단 가치는 살리되, Output #5에 면책 한 줄을 *강제*해 스킬이 진실 측정기로 오용되는 것을 막았다.

### Resource 분리 여부

references / scripts / assets **만들지 않았다.**
- SKILL.md 본문 ~117줄 (Principle #2의 300줄 임계 이하).
- scripts/(예: 수동태·상투구 탐지기)는 **안티-패턴을 install**하므로 의도적으로 거부 — cut #2 참조. 결정론적 텍스트 린터는 오웰이 경고한 dumb 필터 그 자체다.
- 여섯 규칙·나쁜 습관 카탈로그를 references로 빼는 것도 기각: 규칙은 *예시 전술*로 본문에 인라인으로 충분하고, 별도 문서로 빼면 "규칙 체크리스트"라는 잘못된 무게중심을 준다.

### Master-router와의 관계

- 트리거 신호 = (이미 뜻이 정해진 글) + (명료성/장황함/흐릿함 호소). *설득*(오길비)도 *새 의미*(이어령)도 *개념 이해*(파인만)도 아닌 "이미 가진 뜻을 또렷이"가 결정적.
- 분리: "팔리게 해줘/카피 봐줘"는 오길비, "통념 뒤집어줘/새 프레임"은 이어령, "이거 내가 진짜 이해한 거 맞나"는 파인만, "이 글 명료하게/장황해"는 오웰.
- ambiguous("글 좀 봐줘"만)하면 master-router가 오웰 vs 오길비 vs 이어령을 후보로 띄우고 사용자 선택.

## Consequences

### Positive

- mimesis에 **작업법(글쓰기)** 결이 처음 들어와 사고법·태도·협업 3결에 4번째 축이 붙었다.
- **첫 명시적 범용 스킬** — Examples·트리거를 도메인 중립으로 설계해 "거장 사고는 모두의 거울"이라는 컨셉을 강화. 이후 스킬의 범용화 레퍼런스.
- 비판 진영(Pullum·Smith·Freedman)을 SKIP 조건으로 흡수해, 거장을 *맹신*이 아니라 *회의와 함께* 박았다 — 작성 원칙 #4("거장도 틀린다") 실천 사례.
- "명료해졌다 ≠ 옳아졌다" 면책을 출력 계약에 강제해, 글쓰기 도구가 진실·논리 보증으로 오용되는 흔한 실패를 차단.

### Negative / Trade-offs

- **여섯 규칙을 내렸지만 완전 차단은 불가능.** main Claude가 절차를 돌릴 때 여전히 규칙을 dumb하게 적용할 여지가 있다 — Step 5 Why·Anti-pattern 2개로 막았으나 행동 보증은 아니다.
- **영어 고유 규칙의 한국어 전이가 검증 안 됨.** 절차를 언어 보편 동작으로 짰지만, 한국어 산문에서 "늘리기 구문"·"허세 어휘"의 실제 탐지 품질은 application log로 봐야 안다(한국어 1차 출처도 미확보 — raw Gaps).
- **SKIP 조건 일부가 2차 출처 기반.** 환원 불가능한 복잡성 경계(C7)·"평이≠중립"(C9)이 Wikipedia 경유라 1차 검증 전(summary Gaps). SKIP 룰의 근거가 단단하지 않다.
- **진단 코어는 반박이 *없어서* 단단한 게 아니라 비판이 *집중되지 않아서* 단단하다.** 비판은 규칙 iv·i에 몰렸고 "뜻을 먼저 정하라/군더더기 빼라"엔 직접 반박이 없다(summary Recurring obs) — 부재가 정당화는 아니다.

### Open questions

- 한국어 산문에서 4개 습관 범주(특히 "허세 어휘"·"무의미어")가 영어만큼 또렷이 진단되는가? 안 되면 한국어 전용 습관 카탈로그가 필요할 수 있다.
- master-router에서 오웰 vs 오길비 분기 — "이 글 좀 봐줘"가 명료성인지 설득인지 사용자가 명시 안 할 때 후보 띄우기 외에 더 좁힐 수 있나?
- 환원 불가능한 복잡성 SKIP을 법률/과학/시 1차 출처로 보강하면 "어디까지 평이하게"의 선을 줄 수 있는가?
- (skill-builder 미완) 이 ADR은 skill-builder agent가 SKILL.md 작성 후 API 에러로 중단되어 **사람(main Claude)이 직접 작성**했다 — 파이프라인 산출 일관성에서 벗어난 유일 케이스. 후속 파이프라인은 정상 3-에이전트 흐름 복귀.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - description 트리거 중 실제 호출에 기여한 표현(특히 오웰 명시 없이 "글이 장황해" 류로 호출된 비율).
  - Examples(공지 문단 / 이메일 한 문장) 중 어느 쪽이 사용자 self-recognition에 강한가.
  - Step 4(정직성 점검)가 실제로 "안개가 못 정함/숨김을 덮은" 자리를 잡아내는 빈도 — 이게 단순 교열과 가르는 핵심 동작이라.
  - 한국어 산문에서 습관 범주 진단이 작동하는지 (영어 규칙의 한국어 전이 검증).
  - "평이=참" 오용이 면책 한 줄로 실제로 차단되는지.
  - master-router에서 오웰 vs 오길비 vs 이어령 분기 정확도.
