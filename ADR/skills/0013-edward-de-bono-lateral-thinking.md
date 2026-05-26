# ADR 0013: Edward de Bono — Lateral Thinking (creative ideation as a reproducible divergence procedure)

- **Status**: Accepted
- **Date**: 2026-05-26
- **Related skill**: `.claude/skills/edward-de-bono-lateral-thinking/`
- **Source figure(s)**: Edward de Bono
- **Primary sources**: *Lateral Thinking: A Textbook of Creativity* (1970) · *Six Thinking Hats* (1985) · PO 정식화 (*Po: Beyond Yes and No*, 1972). 1차 회수 범위·미회수 항목은 research/edward-de-bono/lateral-thinking-summary.md 의 "Gaps inherited from raw" 참조.

## Context

mimesis 로스터는 그동안 *수렴 일색*이었다 — 맥킨지(MECE 분해), 아리스토텔레스(단일 수직 인과), 멍거(다학제 교차검증), 메도즈(동적 피드백 진단), 이어령(통설을 뒤집는 단일 본질 질문), 오웰(명료화 감사). 모두 "있는 것을 분해·검증·재정의·진단"하는 동작이다. 정작 사용자가 가장 자주 막히는 국면 — "아이디어가 안 나와 / 다 비슷한 안만 나와 / 다른 각도로 흔들어줘" — 에 대응하는 *발산(generative)* 동작은 비어 있었다. 특히 `mckinsey-structured-problem-solving`은 ADR 0003에서 "창의 발산엔 쓰지 말라"고 그 자리를 명시적으로 비워 두었다.

이 빈 *발산* 축을 채울 거장으로 드 보노를 골랐다. 그의 핵심 자산은 "창의는 재능"이라는 통념을 깨고 창의를 **누구나 돌릴 수 있는 재현 가능한 절차**(판단 끄기 → 도발 생성 → movement → 추출)로 환원한 것이다. mimesis가 "거장의 사고를 1턴 동작으로 박제"하는 레포라는 점에서, "절차화된 창의"는 정확히 박제하기 좋은 형태다.

## Decomposition

summary의 essence(Q4·Q9·Q11·Q12)는 다음으로 요약된다: **판단(NO)을 의도적으로 보류한 채, 당연한 것을 기계적으로 비틀어 *일부러 틀린* 디딤돌(provocation)을 만들고, 그 위에서 다시 능동적으로 움직여(movement) 정답이 아니라 *다른 배열*을 양산한다.** 이를 SKILL.md 절차로 재구성하면서 다음 구조를 추출했다.

- **토대 두 축** (procedure 본체 위에 먼저 박음):
  - *lateral vs vertical* (Q1, Q4) — 발산(생성)과 수렴(선택)은 *같은 머리 동작이 아니다*. vertical은 한 길을 고르려 다른 길을 배제하고 매 단계가 옳아야 하지만(Q3), lateral은 고르지 않고 최대한 많은 길을 열며 결론만 맞으면 중간 부품은 자기 지지적일 필요가 없다(bridge, Q3).
  - *movement vs judgment* (Q2, Q10, Q11) — PO는 판단을 *끄는* 진입 조건이고(Move 0), movement는 그 위에서 떠오른 (말 안 되는) 생각을 *연료로 써서* 나아가는 별도의 능동적 동작이다(Move 3). 둘은 모순이 아니라 순서(끈 다음 움직임)다 — summary Open tensions 1번의 해소를 그대로 채택.

- **실행 도구 묶음** (토대 위에 "도발 생성 → 디딤돌로 movement → 새 대안 추출" 형태로 배치):
  - *PO 모드 진입* (Move 0, Q9·Q10·Q11) — 즉시 판단 사이에 중간 코스를 끼움.
  - *challenge* (Move 1, Q17) — 가정의 *필요성*만 흔든다. 공격·반박 아님.
  - *provocation 5조작* (Move 2, Q12) — escape·reversal·exaggeration·distortion·wishful. 즉흥이 아니라 *기계적* 조작.
  - *random word / random entry* (Move 2-alt, Q14·Q15·Q22) — 진짜 무작위 주입. "selection을 random인 척"하기 금지가 핵심.
  - *movement 5추출법* (Move 3, Q11·Q13·Q14) — 원칙·차이·시뮬레이션·긍정·유용상황. noose→rope/loop 워크드 예시(Q14)를 Example 1로 승격.
  - *concept extraction / concept fan* (Move 4, Q18) — 좋은 안을 개념 층위로 끌어올려 다시 양산.

- **Six Thinking Hats는 발산 Green 하나가 아니라 6모드 전체가 한 도구 묶음** (Move 5, Q19·Q20·Q21) — 사용자 지시대로 6모드 식별/전환 질문 표 + parallel thinking + "한 번에 한 모자" + "Blue로 열고 닫는" 시퀀스 원칙으로 박았다. Move 0~4의 발산은 전부 Green 안에서 돌고, 나머지 5모자는 그 발산을 다른 모드와 시간으로 격리하는 관리 장치임을 명시.

- **경계(인접 사고법과의 구분)** — summary의 "경계" 섹션(Q1·Q10·Q11·Q16)을 기준으로 가르는 동작 정체성 = **"판단을 보류한 채 새 대안을 양산/점프"**. 단, summary가 명시했듯 이어령·McKinsey·Munger 쪽 1차 비교 자료는 raw 범위 밖이라, 드 보노 쪽 증거로만 분기선을 그었다(아래 Decision).

## Decision

**Shape: diagnostic.** SKILL.md 한 장이 procedure 본체다. `.claude/agents/` agent 파일은 만들지 않는다(collaborator 아님).

- **왜 diagnostic인가**: 점유 축이 "1턴 발산 procedure로 끝나는 것"이다 — 사용자가 "다른 각도로 흔들어줘"라고 하면 그 자리에서 PO→provocation→movement→추출을 한 번 돌려 *다른 배열의 후보 목록*을 내놓으면 동작이 완결된다. 멀티턴 페르소나 협업(collaborator)이 필요한 영속 voice가 아니라, 막힌 사고를 흔드는 *재현 가능한 자극 절차*다. 드 보노 자산의 정체성("창의를 절차로 환원")이 곧 diagnostic의 정의와 일치한다.

- **트리거 계약** (이 레포의 figure-anchored 정책 + ADR/meta/0001-master-router 분담):
  - *명시 호출*: "드 보노 / 에드워드 드 보노 / Edward de Bono / de Bono / lateral thinking / 수평적 사고 / 수평 사고 / Six Thinking Hats / 여섯 색깔 모자 / 6개의 모자 / six hats / PO / provocation / random word / 랜덤 워드".
  - *인물 미명시 트리거 표면*: "아이디어가 안 나와 / 다 비슷한 안만 나와 / 뻔한 답만 나와 / 발상을 못 벗어나겠어 / 브레인스토밍 하는데 막혔어 / 이 문제 다른 각도로 흔들어줘 / 새 대안이 필요해 / 창의적으로 접근하고 싶어". (Principle #1 — under-trigger를 막기 위해 자연어 변형을 넓게.)
  - *ambiguous 분기*: 발산 vs 수렴 vs 의미생성 vs 다학제 의도가 불분명하면 master-router 경유 권장 한 줄을 description에 박음.

- **입력**: 발산이 막힌 *하나의 열린 문제/주제* (정답이 여럿이거나 아직 정의되지 않은 것).

- **출력 계약**: (1) 판단 보류 선언 → (2) 사용한 도발 기법 + 도발문 → (3) movement 흔적(도발→디딤돌→새 대안 경로) → (4) 양산된 *다른 배열*의 대안 목록 → (5) 선택적 concept extraction → (6) 그룹이면 Six Hats 시퀀스 → (7) "이건 검증된 해법이 아니라 자극 절차" 면책 한 줄.

- **인접 스킬과의 분기** (should-NOT-trigger 경계로 박음):
  - vs `lee-eo-ryeong-questioning`(이어령): 이어령은 통설을 뒤집어 새 *의미*를 빚는 메타·의미론(단일 본질 질문)이다. 드 보노의 reversal은 *옳은 반전을 찾지 않고* 어떤 반전이든 패턴 교란용 자극으로만 쓴다(Q16) — 의미 생성이 아니라 패턴 교란, 단일 본질이 아니라 *다수* 대안 양산.
  - vs `mckinsey-structured-problem-solving`(맥킨지): 맥킨지는 수렴·MECE 분해(발산 금지 영역)다. 드 보노는 명시적으로 *generate for the sake of generating*, 매 단계 옳을 필요 없음(Q1·Q3) — 구조화의 정반대 극. 두 스킬은 상보적이다(lateral로 양산 → 수렴으로 선택).
  - vs `charlie-munger-latticework`(멍거): 멍거는 검증된 외부 *학문 모델*을 차용해 교차검증한다. 드 보노의 외부 자극은 검증된 모델이 아니라 *무관할수록 좋은 무작위 자극*(Q6·Q15) — 차용이 아니라 교란.

- **잘라낸 것**:
  - *효능 주장 / "검증된 방법" 포지셔닝*. summary Gaps·Open tensions 4번에 따라, 효과가 통제 연구로 입증되지 않았으므로(C2·C3·C4) "재현 가능한 자극 절차"로만 포지셔닝하고 효능을 주장하지 않는다.
  - *그룹 퍼실리테이션 운영론*. Six Hats를 "한 번에 한 모자 + Blue로 열고 닫기"의 식별/전환 도구로만 채택하고, 진행자 권력·집단사고 관리 같은 운영론은 1턴 diagnostic 범위 밖으로 잘랐다(C6).
  - *parallel thinking의 "논쟁 전면 폐기" 주장*. 갈등의 생산성을 제거한다는 비판(C5, Open tensions 3)은 미해소이므로, 발산을 한 모드로 격리하는 선까지만 채택하고 "adversarial argument 자체를 폐기"하는 강한 주장은 넣지 않았다(Example 2에 Black 구간 필수 배정으로 봉합).
  - *patterning-mind 신경과학 메커니즘의 강한 정당화*. 1970년판 챕터로만 커버되고 근거가 빈약해(Gaps), SKILL.md에는 "마음은 자기조직화 패턴 시스템"을 *왜 무관 자극이 필요한가*의 동기로만 얕게 쓰고 신경과학적 사실 주장으로 박지 않았다.

- **resource 분리 판단**: 분리하지 않았다(SKILL.md 한 장). 본문이 ~140줄로 Principle #2의 분리 임계(300줄)에 한참 못 미치고, provocation 5조작·movement 5추출법·Six Hats 6모드가 모두 한 절차 흐름 안에서 함께 참조되므로 references/로 떼면 오히려 흐름이 끊긴다. scripts/도 불필요(결정론적 반복 helper 없음 — random word 추출은 사용자가 직접 무작위로 뽑는 행위 자체가 핵심이라 자동화하면 의미가 죽는다).

## Consequences

- **Positive**:
  - mimesis 로스터에 *발산* 동작이 처음 들어와, 수렴 일색이던 도구 세트가 "발산→수렴" 페어로 완성된다. 맥킨지가 비워 둔 자리를 정확히 채운다.
  - 창의를 재능이 아닌 절차로 다루므로, "아이디어가 안 나온다"는 호소에 *기계적으로 실행 가능한* 자극 절차(PO→provocation→movement→추출)를 1턴에 돌려줄 수 있다.
  - 그룹 발산이 논쟁으로 죽는 흔한 실패(Example 2)에 Six Hats 시퀀스라는 즉시 처방을 준다.

- **Negative / Trade-offs**:
  - **실증 증거 부족** (C2·C3·C4): lateral thinking·CoRT의 효과는 통제된 연구로 입증된 적이 거의 없고, 일반화·신뢰성을 요구하면 약하다. 이 스킬은 "효과가 입증된 방법"이 아니라 "막힌 사고를 흔드는 재현 가능한 자극 절차"로만 포지셔닝해야 한다(드 보노 본인도 "증명이 아니라 시동"이라 했다).
  - **self-promotion / derivative 비판** (C1): lateral thinking이 기존 창의 연구의 재포장이라는 지적이 있다. 따라서 이 스킬의 자산은 *독창성*이 아니라 *절차화라는 형태*에 둔다 — 독창성 주장을 절제했다.
  - **Six Hats 과잉단순 비판** (C6): 사고를 6색으로 가르는 것이 과잉단순이고, Blue를 쥔 진행자가 비판을 봉쇄하거나 집단사고를 유발할 수 있다. SKILL.md는 "한 번에 한 모자 + Blue로 열고 닫기"만 채택하고 Black 구간 필수 배정으로 일부 봉합했으나, 진행자 권력 문제는 1턴 diagnostic으로는 다루지 못한다.
  - **patterning-mind 신경과학 주장의 근거 빈약**: "마음은 자기조직화·자기최대화 패턴 시스템"이라는 메커니즘 주장은 근거가 약하므로 동기 설명으로만 얕게 썼다. 메커니즘 정당화를 강하게 박으려면 추가 researcher가 필요하다(*Po* 1972 / *I Am Right You Are Wrong* 1990 1차 인용 미확보, Aeon/Melechi 전문 미회수).
  - **정직한 위치 매김**: 드 보노는 "사상 깊이"보다 "유용한 발상 기법의 발명가"에 가깝다. 이 스킬은 그 점에서 깊은 철학이 아니라 *작동하는 절차*로서 정직하게 쓴다.

- **Open questions**:
  - parallel thinking의 "갈등 제거 vs 갈등의 생산성"은 미해소(C5). 발산 격리 선까지만 채택했으나, 갈등이 생산적인 국면에서 이 도구가 오히려 탐색을 줄이는지 사용 사례로 검증 필요.
  - 인접 스킬 분기(이어령·McKinsey·Munger)는 드 보노 쪽 1차 증거로만 그었다 — 해당 인물 research와 교차해 분기선을 양방향으로 검증하면 더 단단해진다.
  - "1턴 diagnostic"이 random word의 *진짜 무작위성*을 어떻게 보장하는가 — 모델이 "그럴듯한 단어"를 selection하는 anti-pattern으로 미끄러지지 않는지 application log로 관찰 필요.

## Application log

(아직 없음 — 첫 적용 후 채운다. 특히 관찰할 것: (1) 모델이 random word를 진짜 무작위로 뽑는가 vs "그럴듯한 단어"를 selection하는가, (2) 도발에서 movement 없이 멈추는 anti-pattern을 피하는가, (3) 수렴이 필요한 문제에 발산을 강요하지 않고 SKIP 경계를 지키는가.)
