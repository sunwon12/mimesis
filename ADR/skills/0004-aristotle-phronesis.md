# ADR 0004: 아리스토텔레스 — Phronesis (실천적 지혜) 스킬

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/aristotle-phronesis/`
- **Source figure(s)**: Aristotle (lineage: Aquinas의 *prudentia* → Gadamer의 hermeneutics 부활 → MacIntyre의 *After Virtue* → Nussbaum의 perception-of-particulars 강조 → Pellegrino·Kaldjian·Kinghorn의 의료 phronesis 운동 → Vallor의 technomoral phronesis)
- **Primary sources**:
  - [research raw](../../research/aristotle/phronesis-raw.md)
  - [research summary](../../research/aristotle/phronesis-summary.md)
  - Aristotle, *Nicomachean Ethics* Book VI (≈ Bekker 1139a–1145a), 특히:
    - VI.5 (1140a24–b30) — phronesis 정의 + 페리클레스 예시
    - VI.7 (1141a20–22, 1141b14–18) — sophia와의 위계 + 보편·개별 결합
    - VI.8 (1142a11–20) — 젊은이는 phronimos가 될 수 없다 (경험 필요성)
    - VI.12 (1144a6–9, 1144a23–29) — 덕은 목적, phronesis는 수단 / deinotes 구분
    - VI.13 (1144b30–1145a2) — 덕과 phronesis의 분리불가능
  - Jessica Moss, "Virtue Makes the Goal Right" (NYU)
  - Joseph Dunne, *Back to the Rough Ground*
  - Martha Nussbaum, *Love's Knowledge* / *The Fragility of Goodness*
  - Hans-Georg Gadamer, *Truth and Method* II.II.2.b "The Hermeneutic Relevance of Aristotle"

## Context

mimesis의 기존 스킬은 각각 결이 다른 막힘을 풀어준다:

- `lee-eo-ryeong-questioning` (ADR 0001) — 통설·관용어가 자명하게 받아들여질 때 한 번 뒤집어 의미를 다시 짓는다.
- `erich-fromm-having-vs-being` (ADR 0002) — 활동의 성공 기준이 "축적/보유"로 굳어 있을 때 동사·과정으로 재구성한다.
- `mckinsey-structured-problem-solving` (ADR 0003) — 복잡·모호한 의사결정에서 MECE/가설/Pyramid로 구조화한다.

그러나 사용자가 자주 마주치는 또 다른 결의 막힘이 비어 있었다 — **"보편 원칙·베스트프랙티스를 따랐는데 결과가 어색하거나 어긋났을 때"**. 이는 위 세 스킬로는 정확히 풀리지 않는다:

- 이어령식 질문은 통설 자체를 의심하지만, phronesis 케이스에선 원칙이 옳다(95% 케이스에선 맞다). 의심해야 할 것은 "이 사례가 원칙의 평균 가정 밖에 있다"는 개별성이다.
- Having/being 진단은 활동의 성공 기준 모드를 다루지만, phronesis 케이스에선 목적은 정해진 상태에서 수단의 적합성이 흔들린다 — 다른 축이다.
- 맥킨지의 MECE는 문제를 구조화하지만 "이 사람·이 시점·이 맥락" 같은 비-MECE한 개별성에는 약하다. 맥킨지가 *average* 케이스를 다룬다면 phronesis는 *this particular* 케이스를 다룬다.

특히 의료의 bedside judgment, 교육·코칭의 한 학생 판단, 리더십의 한 팀·이 시점 결정, 법관 양형, 윤리적 딜레마, 돌봄·치료 같은 영역에서 사용자가 막히는 양상은 일관적이다 — (1) 가이드라인·매뉴얼·체크리스트는 적용했고, (2) 그게 의학적/논리적으론 맞는데, (3) 이 환자·이 학생·이 사람에게는 어색하고, (4) "왜 어색한가"를 logos로 풀지 못해 침묵하거나 자의(自意)로 빠진다.

이 4-step 막힘을 풀어주는 사고법이 아리스토텔레스의 phronesis다. 2300년 동안 의료·법·교육·정치학에서 반복적으로 부활해온 까닭이 여기 있다.

## Decomposition

summary의 구조를 그대로 옮기되, 스킬화에 필요한 5개 축으로 재정리한다.

### Core thesis (summary §Core thesis)

Phronesis는 "변할 수 있는 인간사(*τὰ ἐνδεχόμενα ἄλλως ἔχειν*)에서 좋은 삶에 이르는 길을 그때그때 식별·숙고·행위하는 품성 상태(*hexis*)"이다 (Q1, NE VI.5 1140a24–b6). 보편 원칙(*episteme*)도, 산출물을 만드는 기술(*techne*)도, 영원한 것을 관조하는 이론지(*sophia*)도 아니다 (Q3, Q9, Q10).

### Generative structure — 5층 진단 (summary §Generative structure)

phronesis는 다섯 층의 결합으로 성립한다. 한 층이라도 빠지면 phronesis가 아니라 다른 무엇이 된다 — 이 5층이 스킬의 Move 1~7의 골격이다.

1. **올바른 목적(*skopos*)을 지향하는 품성** (Q6, Q7, Q8) — 덕(*ethike arete*)이 목적을 올바르게 설정한다. 이 층이 없으면 영리해도 *deinotes*일 뿐.
2. **보편 원칙의 보유** (Q4) — "건강에 가벼운 고기가 좋다" 같은 일반화 가능한 명제.
3. **개별을 지각하는 능력** (Q4, Q16) — "이 닭고기가 가벼운 고기다"처럼 보편을 이 사례에 매핑하는 지각. Nussbaum은 여기에 감정도 인지적 지각으로 포함시킨다.
4. **숙고(*bouleusis*)** (Q1, Q9, Q12) — 목적을 향한 수단들을 비교·계산하는 활동. 변할 수 있는 것에만 작동한다.
5. **시간이 만든 경험(*empeiria*)** (Q4, Q5) — 개별 지각은 다양한 상황에 반복 노출되어야 발달한다. 그래서 젊은이는 기하학자는 될 수 있어도 phronimos는 될 수 없다 (NE VI.8, 1142a11–20).

이 다섯이 결합하면 phronesis, 결합하지 않으면 다른 것: *episteme*(2만), *techne*(2+4지만 목적이 외부 산출물), *deinotes*(2+4지만 1이 없음), 자연적 덕(1만, 2~4 없음) (Q3, Q7, Q8).

### Mental moves — 7 steps (summary §Mental moves)

스킬에는 7개 step을 모두 살렸다. 7±2 cognitive load 제약 안에 있고, 어느 step도 빠지면 진단 구조가 무너진다.

(Q9/Q11 → Move 1 Domain check; Q6 → Move 2 Telos diagnosis; Q4/Q16/Q18 → Move 3 Particular perception; Q1/Q9/Q12 → Move 4 Deliberation about means; Q7 → Move 5 Deinotes guard; Q19 → Move 6 Logos check; Q2/Q5/Q21 → Move 7 Exemplar check)

특히 **Move 5 (Deinotes guard)** 는 요구사항에서 명시적으로 요청된 별도 체크다 — summary §Mental moves의 5단계를 그대로 보존하면서, "수단 효율성만 좋고 목적은 흔들리는 영리한 villainy" 패턴을 식별하는 게이트로 박았다. Aristotle 자신의 1144a23–29 구분("clever villain은 deinotes를 가지나 phronesis는 없다")을 진단 단계로 옮긴 것.

### Heuristics (summary §Heuristics & decision rules)

운영 가능한 휴리스틱 7개를 살림: 베스트프랙티스의 암묵적 telos 명시화 / 규칙이 어색하면 규칙의 평균 가정을 의심 / 경험 없는 영역에선 phronimoi에서 빌려라 / 감정을 신호로 다뤄라 / 동일 수단이 다른 목적에도 작동하면 deinotes 의심 / 수단까지만 숙고하라 / 규칙은 디폴트 트랙, phronesis는 예외 트랙. (각 Q번호 — Q4/Q5/Q6/Q7/Q15/Q16/Q17/Q18/Q21 — 은 SKILL.md Why 줄에 직결.)

### Anti-patterns (summary §Anti-patterns)

8개 모두 살림: 원칙 단순 거부(Q4), 즉흥 판단을 phronesis라 부르기(Q19), deinotes 머묾(Q7), 자연적 덕에 머묾(Q8/Q15), phronimos 결론 복사(Q2/Q21), 목적과 수단 동시 흔들기(Q6), 경험 없는 영역에서 phronesis 자처(Q5), 알고리즘화 가능 영역에 호출(Q22). 사용자 요구사항의 "감(感)을 phronesis라 부르는 것", "권위자 흉내내기"는 각각 anti-pattern #2, #5로 흡수됨.

### Boundaries (summary §Boundaries)

스킬 본문 "When to use" 의 호출 금지 영역으로 옮김: 불변·필연(수학·물리)(Q9/Q10), 외부 산출물 제작(Q3), safety-critical SOP(Q22 + Q11), 대규모 반복 결정(Q22), 경험 자본 없는 단독 판단(Q5), reversible 실험(application 판단). 특히 **safety-critical SOP의 경계는 사용자 요구사항대로 "절차 안의 미세 조정은 OK, 절차 자체 무력화는 anti-pattern"으로 분리 명시**.

### Open tensions (summary §Open tensions)

본문에 5개 tension을 모두 박지 않았다 — lean 원칙 + 사용자 의사결정에 직접 영향을 안 주는 학술 긴장이라. 단 다음 두 점은 본문 Move/Heuristic의 Why에 녹였다:

- "phronesis가 sophia보다 낮은가 vs 자기 영역에서 architectonic인가" 긴장 → Move 1 "이 사안이 phronesis 영역인가" 판정과 boundaries로 실용적 해소.
- "medicine은 techne인가 phronesis인가" 긴장 → Example 1(bedside judgment)에서 "production 측면 = techne, this patient 판단 = phronesis" 분업으로 surface.

순환성(phronimos가 phronesis를, phronesis가 phronimos를 정의), elitism 비판, 알고리즘 시대 phronesis의 위치 — 이 세 tension은 ADR Consequences §Negative에 별도로 박는다.

## Decision

### 트리거 (description 설계)

사용자가 실제로 쓸 표현을 9개 박았다:
1. "원칙대로 했는데 어색해"
2. "베스트프랙티스대로 했는데 안 맞아"
3. "매뉴얼에는 이렇게 적혀 있는데 이 사람한텐 안 통해"
4. "체크리스트는 맞는데 뭔가 어긋난다"
5. "규칙은 알겠는데 이 상황에선 다르게 해야 할 것 같다"
6. "이게 정답인 건 알겠는데 이 환자/이 학생/이 팀에는 이상하다"
7. "감으론 이게 아닌데 왜 그런지 설명을 못 하겠다"
8. "두 원칙이 충돌하는데 어떻게 골라야 하지"
9. (인물·개념 명시) "아리스토텔레스 / phronesis / 프로네시스 / 실천적 지혜 / phronimos / prudentia / practical wisdom / bedside judgment / 현장 판단"

명시적 인물명 없이도 트리거되도록 "사용자가 아리스토텔레스를 명시하지 않아도" 한 줄을 박았다. should-NOT-trigger 경계 3종(알고리즘 영역 / safety-critical SOP의 정형 부분 / reversible 실험) + 1 (경험 자본 없는 단독 판단)을 명시. 기존 스킬들(`erich-fromm-having-vs-being`, `mckinsey-structured-problem-solving`)의 description 구조 — 도입 한 문장 + 호출 표현 나열 + master-router 협력 한 줄 + 적용 영역 + boundaries — 를 그대로 따랐다. Triggering guide 5개 항목 통과.

### 스킬 단위 — 왜 7-Move 묶음을 한 스킬로

Domain check만, Telos diagnosis만, Deinotes guard만 — 각각을 분해하는 안도 검토했다. 그러나:

1. **substantive task에서 트리거되어야 한다** (Principle #5). 사용자가 "deinotes 체크해줘"라고 정확히 말하는 경우는 없다. 실제 호출 신호는 "원칙대로 했는데 어색해" 같은 복합 막힘이다. 그 막힘을 풀려면 7 Move가 함께 가야 한다 — Domain만 체크하고 Telos 분리를 안 하면 합리화로 미끄러지고, Telos만 다루고 Particular perception이 없으면 개별 신호를 못 본다.
2. **Aristotle 원전이 이미 묶음으로 작동한다.** NE VI.5–13이 한 호흡으로 phronesis를 정의→차별화→구성요소→오용 사례→타 지혜와의 관계로 짠다. 인위적으로 자르면 원본 사고가 왜곡된다.
3. **figure-anchored 룰을 깔끔하게 따른다** — phronesis는 Aristotle의 고유 개념이고 후속 lineage(Aquinas, MacIntyre, Nussbaum)는 모두 Aristotle에 귀속해 발전시켰다. 메모리의 [mimesis-naming-figure-anchored](#) 규칙과 정합.

### 스킬명 — 왜 `aristotle-phronesis`인가

mimesis Hard rules는 method-slug에 gerund(-ing)를 권장하지만 "인물 고유 개념명은 예외" 허용. `phronesis`는:
- Aristotle의 고유 그리스어 용어이며 영어·한국어에 표준 등가어가 없다 (prudentia / practical wisdom / 실천적 지혜는 모두 부분적 번역).
- gerund 후보(`deliberating`, `perceiving-particulars`, `judging-in-context`)들이 각각 5층 중 하나만 가리켜 묶음을 표현하지 못한다.
- "phronesis"라는 단어 자체가 트리거 키워드로 작동 — 의료·교육·철학 커뮤니티에서 이 단어를 쓰는 사람이 늘고 있다.

따라서 인물 고유 개념명 예외 적용. `aristotle-phronesis`로 figure-anchored 원칙 유지.

### 포함한 mental moves

7 Move 전부 + 7 heuristic + 8 anti-pattern + 2 example (의료 bedside + 리더십 1on1). Example을 의료와 매니징의 두 도메인으로 결을 넓힌 것은 "phronesis = 의료 윤리 강의" 라는 좁은 연상으로 호출이 갇히지 않게 하기 위함이다. 실제로 phronesis가 가장 자주 필요한 곳은 평범한 매니저·코치·리더의 한 사람 판단이라는 가설을 example로 박았다.

### 의도적으로 잘라낸 것

- **Open tensions 5개를 본문에 노출하지 않음** — lean 원칙. "phronesis vs sophia 위계", "medicine = techne or phronesis", 순환성, elitism, 알고리즘 시대 phronesis — 이 5개는 학술적 가치는 크지만 사용자의 의사결정에는 직접 영향이 거의 없다. ADR Consequences에서만 surface.
- **Heidegger / Gadamer / MacIntyre 본문 직접 인용** — raw에 충분히 인용되어 있지만 SKILL.md에 그들의 해석사를 박으면 본문이 학술 논문이 된다. Move 6(Logos check)의 Why에 "Heidegger처럼 phronesis를 결단의 순간으로 축소하면" 한 줄로만 surface.
- **EE VIII.1의 본문 부패 문제와 그로 인한 "phronesis가 목적도 파악하는가" 해석 긴장** — raw §Gaps에 명시. SKILL.md는 NE VI.12의 분업 구도(덕=목적, phronesis=수단)를 기본 채택. 후속 researcher pass가 EE를 보강하면 Move 2가 수정될 수 있음을 ADR에 적시.
- **Greek 원문 직접 인용 (φρόνησις, σκοπός, ἕξις, βούλευσις, ἐμπειρία)** — 본문에는 라틴 transliteration만 사용. ADR Primary sources의 Bekker 행번호로 학술 참조 가능성 확보.
- **Schwartz의 청소부 일화 (Q18)** — raw에 1차 출처 미확보. example로 박지 않고 Heuristic의 추상 표현("규칙이 어색하면 규칙의 평균 가정이 어긋난 것")으로만 흡수.

### Resource 분리 여부

references/scripts/assets 디렉토리를 만들지 않았다.

- 본문이 ~210줄 (500줄 임계 이하).
- 결정론적 helper(목적-수단 분리 자동화, deinotes 분류 등)는 phronesis의 본질상 불가능 — Aristotle 자신이 명제로 환원되지 않는다고 했고, 환원하는 순간 anti-pattern이 된다.
- 진단 템플릿(Domain → Telos → Particulars → Deliberation → Deinotes → Logos → Exemplar 흐름)을 `assets/diagnostic-template.md`로 빼는 것을 검토했으나, 사용자 도메인이 너무 다양해서(의료 / 교육 / 리더십 / 법) 한 템플릿보다 example 2개가 강하다고 판단. application log 후 재평가.

### Master-router와의 관계

`master-router`에 등록 시 다음 룰이 잡혀야 한다:

- 트리거 신호 = (베스트프랙티스/매뉴얼/체크리스트 + 어색함/어긋남) 조합.
- 다른 스킬과의 분리:
  - `lee-eo-ryeong-questioning`: 통설 *자체*를 의심 → 통설을 폐기·재정의. phronesis는 통설을 *유지*하면서 이 사례만 보정.
  - `erich-fromm-having-vs-being`: 활동의 성공 기준 모드 진단. phronesis는 모드가 아니라 적합성 진단.
  - `mckinsey-structured-problem-solving`: 평균 케이스에 대한 구조화. phronesis는 평균 밖 개별에 대한 진단.
- 호출 우선순위: 사용자가 "원칙대로 했는데 안 맞아" 류를 명시하면 phronesis 우선. "이 문제 어디서부터" 류면 mckinsey가 디폴트.

## Consequences

### Positive

- mimesis 스킬 셋이 "통설 의심 / 모드 진단 / 구조화 / 개별 적합성" 4축으로 완비된다. 사용자 의사결정의 가장 흔한 막힘 패턴을 모두 커버.
- 의료·교육·리더십 같은 high-stakes 도메인에서 호출 가능한 스킬이 처음 생긴다 — 기존 셋은 비즈니스·기획·자기진단 위주였다.
- 7-Move 진단 구조가 사용자에게 "어색함을 logos로 풀어내는" 명시적 훈련 도구가 된다. "감으론 이게 아닌데 왜 그런지 설명을 못 하겠다"는 막힘이 가장 흔한 호소이며, Move 3+6이 이걸 푼다.
- Lineage(Aquinas → Gadamer → MacIntyre → Nussbaum → Pellegrino → Vallor)를 ADR에 명시 — 후속 스킬(예: Vallor의 technomoral phronesis를 AI 윤리 스킬로 분리, MacIntyre의 *practice* 개념을 별도 스킬로 분리)이 이 ADR을 참조해 결을 갈라낼 수 있다.

### Negative / Trade-offs

- **순환성 문제 — phronimos가 phronesis를, phronesis가 phronimos를 정의** (Q21). Aristotle 자신의 해법은 페리클레스 같은 ostensive identification + 덕과 phronesis의 분리불가능 thesis(Q8). 그러나 결정 절차로서 "누가 진짜 phronimos인가"를 외부에서 검증할 길이 없다 — Move 7(Exemplar check)이 "공동체가 phronimos로 식별하는 사람" 에 의존하는데, 그 공동체적 식별 자체가 phronesis를 전제한다. 사용자는 이 순환을 받아들여야 한다.
- **Elitism 비판** (Q20, Politics 1260a12–14에서 Aristotle 자신이 노예·여성·아이는 phronesis 능력이 없다고 했음). 현대 부활자(Nussbaum, Kristjánsson)는 이를 "역사적 우연으로서의 오류"로 분리하지만, "형식 구조와 사회적 배제가 정말 분리되는가"는 미해소. 스킬은 보편 적용 가능성을 전제로 짰지만, 이 전제가 깨질 가능성을 ADR에 적시.
- **알고리즘 시대의 phronesis 위치** (Q22). Vallor 등은 알고리즘이 phronesis 발달 기회 자체를 박탈한다고 본다. 스킬의 "디폴트 트랙 = 알고리즘, 예외 트랙 = phronesis" 분업은 부분 해소책이지만, **예외 식별 자체가 phronesis이므로 알고리즘으로 완결되지 않는다** — 어디까지 알고리즘에 맡길지를 phronesis가 정해야 하는 메타 회귀가 남는다.
- **신비주의 변질 위험.** Move 6(Logos check)을 박았지만, 사용자가 "결단했다 / 그냥 느낌이다"로 정당화하고 그게 phronesis라고 자처하는 케이스를 완전히 막을 순 없다. 특히 본인 권위가 높은 시니어 사용자가 후배에게 "phronesis로 결정했다"고 말하는 식의 오용 위험.
- **묶음 스킬의 학습 곡선** — 7 Move + 7 heuristic + 8 anti-pattern을 한 번에 마주하면 압도된다. 사용자가 일부만 적용해도 가치가 나오도록 Move 1(Domain)과 Move 2(Telos)를 핵심 진단점으로 박았다. 이 둘만 돌려도 "이게 phronesis 영역인가 / 빗나간 게 목적인가 수단인가"의 80%는 잡힌다.

### Open questions

- Example을 의료·리더십 외 도메인(법관 양형, 교육 코칭, 정책 결정)으로 더 늘려야 할까? — 도메인 다양성이 호출 표면을 넓히지만 본문이 길어진다는 trade-off.
- Move 3(Particular perception)의 "감정도 인지적 지각" 부분이 사용자에게 직관적으로 전달되는지 — Nussbaum의 *Love's Knowledge*가 깊게 다루는 지점인데, 본문에는 한 줄로만 박았다. application log로 검증.
- Master-router에서 phronesis와 mckinsey의 트리거 표면 겹침(둘 다 "어떻게 결정하지" 류)을 어떻게 분기할 것인가 — 현재는 "원칙대로 했는데 어색" vs "어디서부터 풀지"로 분리했지만 실전 표현은 더 섞일 가능성.
- Aristotle 그리스어 원전 인용을 더 surface해야 하는가 — 학술적 권위는 올라가지만 본문 가독성은 떨어진다. 현재는 ADR Primary sources에 Bekker 행번호로만 박았다.
- AI 시대 phronesis의 위치를 별도 스킬(`vallor-technomoral-phronesis`?)로 분리할 가치가 있는가 — Vallor의 작업이 충분히 독립적이지만 mimesis가 거장 한 명에 귀속하는 룰을 따른다면 분리 가능. application 후 판단.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - Move 1(Domain check)이 실제로 phronesis 호출을 차단하는 빈도 (false positive 방지)
  - Move 2(Telos diagnosis)가 "이건 phronesis가 아니라 덕 레이어"로 사용자를 보내는 빈도 — 이게 정확히 작동하면 phronesis가 합리화로 미끄러지는 가장 큰 위험을 막는다
  - 9개 트리거 표현 중 실제 호출에 기여한 표현 (특히 명시적 인물명 없이 자연어 표현만으로 호출되는 비율)
  - 의료 example vs 리더십 example 중 어느 것이 사용자 self-recognition에 더 강하게 작동하는지
  - Move 5(Deinotes guard)가 실제로 "영리한 villainy"를 차단한 사례
  - Move 7(Exemplar check)의 "결론이 아니라 그가 본 개별을 베껴라"가 결론 복사 anti-pattern을 막는 빈도
