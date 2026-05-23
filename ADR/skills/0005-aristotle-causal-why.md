# ADR 0005: 아리스토텔레스 — Causal Why (4원인 + 제1원리/archē) 스킬

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/aristotle-causal-why/`
- **Source figure(s)**: Aristotle (lineage: Bacon의 자연 final cause 비판 → Descartes의 cogito 모델 → Ohno의 5 Whys → Mayr의 teleonomy → Musk의 first-principles 대중판 → Falcon의 "modes of explanation" 현대 해석)
- **Primary sources**:
  - [research raw](../../research/aristotle/causal-why-raw.md)
  - [research summary](../../research/aristotle/causal-why-summary.md)
  - Aristotle, *Physics* II.3 (194b16–195a3) — 4원인의 정식 정의
  - Aristotle, *Physics* I.1 (184a10–21) — "우리에게 알려진 것 → 본성상 알려진 것"의 인식 방향
  - Aristotle, *Physics* II.7 (198a21) — "네 원인 모두로 돌려야 한다"
  - Aristotle, *Posterior Analytics* I.2 (71b9–25) — 학문적 앎의 6 조건 (참·일차·즉각·더 알려진·선행·인과적)
  - Aristotle, *Posterior Analytics* I.3 (72b18–25) — 무한 후퇴 차단, archē는 indemonstrable
  - Aristotle, *Posterior Analytics* I.10 (76a37–40) — 공통 axiom vs 특수 원리 (archē의 도메인 복수성)
  - Aristotle, *Posterior Analytics* II.11 (94a20 ff.) — "원인은 middle term", eclipse·thunder 예시
  - Aristotle, *Metaphysics* I.3 (983a24–32) — 4원인의 metaphysical 재정식화
  - Aristotle, *Metaphysics* V.1–2 (1013a–1014a25) — archē의 다의성 + per se / per accidens
  - Aristotle, *Metaphysics* VIII.4 (1044b12) — "일식에는 목적인이 없다"
  - Andrea Falcon, "Aristotle on Causality," *Stanford Encyclopedia of Philosophy* — aitia를 "modes of explanation"으로 재해석
  - Francis Bacon, *Novum Organum* (1620) — 자연 탐구에서 final cause 추방
  - Taiichi Ohno, *Toyota Production System* (1988) p.17 — 5 Whys의 원전
  - Elon Musk, Kevin Rose Foundation 인터뷰 (2012) + Wired 인터뷰 (2012) — first principles의 현대 대중판
  - Ernst Mayr, teleonomy 개념 — *Teleological Notions in Biology* (SEP)

## Context

mimesis 스킬 셋은 ADR 0001~0004로 네 결의 막힘을 커버한다 — 통설 의심(이어령), 모드 진단(프롬), 평균 케이스 구조화(맥킨지), 평균 밖 개별 적합성(아리스토텔레스 phronesis). 그러나 다섯 번째 결의 막힘이 비어 있었다 — **"왜 이게 이렇게 됐는지 / 어디서 출발하는지를 끝까지 추궁하는 절차"**.

이 막힘은 위 네 스킬로 정확히 풀리지 않는다:

- 이어령의 정문(正問)은 통설을 한 번 뒤집어 의미를 재정의하지만, **원인의 두 축 좌표계**(수평 4분해 + 수직 추궁)는 다루지 않는다.
- 프롬의 having/being은 활동의 성공 기준 모드를 진단하지만, **현상의 원인 구조**를 분해하지 않는다.
- 맥킨지의 MECE는 문제를 구조화하지만 "왜?" 자체의 형식 유형(존재/속성/행위/고장)을 가르지 않는다. MECE 트리의 leaf가 4원인 중 어디에 속하는지를 묻지 않으면 분석이 작용인 한 갈래로 쏠릴 수 있다.
- **같은 인물의 phronesis 스킬과 트리거 표면이 명확히 다르다** — phronesis는 "이 개별 상황에서 뭘 할까"(보편의 어색함을 개별로 보정), causal-why는 "왜 이게 이렇게 됐지 / 어디서 출발하지"(원인의 좌표계로 분해·추궁). 사용자 발화 표면도 다르다.

특히 다음 막힘 패턴이 사용자에게 일관적으로 나타난다:

1. **5 Whys로 부족함을 느낄 때** — 토요타식 단일 선형 추궁이 작용인 한 갈래로 수렴해 "리뷰 프로세스 부재"에서 끝나지만, 형상인(시스템 구조)·질료인(인프라)·목적인(이 서비스의 telos)을 묻지 못해 답답함이 남는다.
2. **머스크식 first principles로 부족함을 느낄 때** — 재료비 분해(질료인)는 강력하지만 형상·작용·목적의 archē 추궁이 비어 있어 한 도메인(주로 하드웨어)에 갇힌다. SaaS·서비스·의사결정 영역에서 약함이 드러난다.
3. **"왜 그 선택을 했나"를 회고할 때** — 작용인(누가 추진)·목적인(무엇을 위해) 혼합이 정리되지 않아 합리화로 미끄러진다.
4. **본질적 정의가 필요한 분석** — "왜 X는 Y인가" 류는 형상인 추궁이 주축이지만, 4원인 좌표를 모르면 작용인으로 답이 떠밀려간다.

이 다섯 번째 결의 막힘에 답하는 사고법이 아리스토텔레스의 두 도구 — **4원인 doctrine과 archē/제1원리 doctrine** — 이다. 두 도구는 *Physics* + *Posterior Analytics* + *Metaphysics*에 걸쳐 한 좌표계로 작동하며, 후대 모든 first-principles 사고법(Bacon, Descartes, Ohno, Musk)은 이 좌표계의 **부분 채택** 또는 **부분 거부**다.

## Decomposition

summary의 구조를 그대로 옮기되, 스킬화에 필요한 5개 축으로 재정리한다.

### Core thesis (summary §One-line essence)

"왜?"는 한 번의 질문이 아니라 **두 축으로 동시에 작동하는 좌표계**다.
- **수평 축**: 한 층의 현상을 네 가지 원인(질료·형상·작용·목적)으로 분해한다 (*Physics* II.3).
- **수직 축**: 더 이상 증명 불가능한 출발점(archē)에 닿을 때까지 각 가지를 거슬러 올라간다 (*Posterior Analytics* I.2–3).
- **작동 조건**: "안다 = 그 원인을 파악했다"는 등식 (Q3, Q4, Q6, Q8, Q11).

### Generative structure — 8 core principles (summary §Core principles)

1. 앎 = 원인의 파악 (Q3, Q4, Q6, Q8, Q11)
2. "왜?"의 답은 4종류 — aitia의 다의성 (Q1, Q2, Q4, Q17)
3. aitia는 "원인"이 아니라 "설명 양식" (Q15, Falcon)
4. archē는 무한 후퇴를 끊는 지점 (Q7, Q8, Q9)
5. 인식 방향은 "우리에게 알려진 것" → "본성상 알려진 것" — **현상을 부정하고 시작하지 않음** (Q7)
6. archē는 도메인별로 복수다 (Q10)
7. 원인은 demonstration의 middle term이다 (Q11, Q12)
8. per se vs per accidens 필터로 사후 합리화·상관관계 오인을 거른다 (Q14)

이 8개 원칙이 스킬의 6 Move + 8 Heuristic + 9 Anti-pattern의 골격이다.

### Mental moves — 6 steps (summary §The mental moves)

스킬에는 summary의 Step 0(트리거 인지)을 제외한 Step 1~5에 자가 검증을 더해 6 Move로 압축했다.

(Q11/Q12 → Move 1 질문 형식 결정; Q1/Q2/Q4/Q17 → Move 2 4원인 분해; Q14 → Move 3 per se 필터; Q7/Q8/Q9/Q10 → Move 4 수직 추궁/멈춤 조건 5; Q11 → Move 5 통합/demonstration; Q19 → Move 6 자가 검증)

특히 **Move 3 (per se / per accidens 필터)** 는 summary가 Step 2 안의 sub-step으로 두었던 것을 별도 Move로 끌어올렸다. 이유: 사용자가 4원인 표를 "다이어그램 채우기"로만 쓰는 anti-pattern(C7, Falcon의 우려)을 차단하려면 필터가 명시적 단계로 보여야 한다. Aristotle 자신이 *Metaphysics* V.2(1013a24–1014a25)에서 *Physics*보다 정교한 4원인 분류에 이 필터를 추가했다는 사실이 그 위치 승격의 근거다.

### Heuristics (summary §Heuristics & decision rules)

운영 가능한 휴리스틱 8개를 살림 (R1~R8). R10(per se 필터)은 Move 3으로 승격되어 별도로 두지 않음. R9(archē 도메인 복수성)는 R7로 흡수.

### Anti-patterns (summary §Anti-patterns)

9개 모두 살림. 사용자 요구사항의 "5 Whys / Musk와의 차이"는 anti-pattern #1(단일 갈래)과 #7(Musk-shallow trap)로 표면화. anti-pattern #6(Cartesian doubt)·#5(telos creep)·#3(단일 universal archē)는 비적용 영역(When to use의 호출 금지 영역)과 짝지어진다.

### Boundaries (summary §When this thinking applies / does not)

스킬 본문 "When to use" 의 호출 금지 영역으로 옮김:
- 알고리즘적 단순 조회·계산 (C8 한국어 실무자 비판)
- 분 단위 reversible 실험 (인지 비용 회수 불가)
- 순수 자연 현상에 목적인 강요 (Q16 Aristotle 자신의 자가 한계 표명 + C1 Bacon)
- 진화·자연선택에 final cause 강요 (C3 Mayr/teleonomy)
- 단일 universal foundation 요구 (Q10, Q24 — Descartes 영역)
- Cartesian doubt 영역 (Q7 — 현상 부정 시작은 Aristotle 모델 아님)

### Open tensions (summary §Open tensions)

5개 tension 중 본문에 surface한 것:

- T1 (4원인의 보편 적용 vs 일식 N/A) → 본문 "권장 순서" + Move 2 "빈 칸 N/A 명시" + 휴리스틱 R3로 운영적 해소.
- T3 (4원인 = 설명 양식 vs 현실 구조) → 본문에 Falcon 인용 한 줄("aitia는 '설명 양식'") + anti-pattern #4(체크리스트 기계화)로 양 해석 균형. 학술 논쟁은 ADR에만 남김.

본문에 박지 않은 것:

- T2 (nous epistemology) — raw §Gaps에 명시된 Posterior Analytics II.19 수집 누락. 본문에서는 archē 멈춤 조건 5개로 우회. 후속 researcher pass가 II.19를 보강하면 Move 4가 더 정교해질 수 있음.
- T4 (도메인별 archē의 transferability) — 머스크식 transfer가 정당화되는 조건이 raw에 명시 안 됨. 본문 R7로 "import하지 않는다" 보수적 정책. ADR Consequences에 미해소로 적시.
- T5 (목적인 살아남는 영역의 경계) — 휴리스틱 R3로 부분 해결("자연엔 강제 안 함, 인공물엔 시작점"). "진화한 사회 제도, 학습한 AI 모델"의 경계는 미해소로 ADR에 적시.

## Decision

### 1) 왜 aristotle-phronesis와 분리했는가 — 같은 인물의 다른 method를 별도 스킬로 자르는 결정

mimesis의 figure-anchored 룰은 **"1스킬 1거장"**이지 **"1인 1스킬"이 아니다** (`.claude/skills/README.md` 네이밍 규칙 참조). 같은 거장의 다른 method가 트리거 표면이 명확히 다르면 별도 스킬로 가른다.

phronesis와 causal-why는 다음과 같이 다르다:

| | `aristotle-phronesis` | `aristotle-causal-why` |
| --- | --- | --- |
| **묻는 질문** | "이 개별 상황에서 뭘 할까" | "왜 이게 이렇게 됐지 / 어디서 출발하지" |
| **주요 트리거 표현** | "원칙대로 했는데 어색해", "이 환자/학생/팀에는 이상하다" | "왜 이게 이렇게 됐지", "근본까지 추궁", "first principles로 다시 보자" |
| **출력의 결** | 지금 할 행동 한 가지 (praxis) | 원인 좌표 + 멈춤 조건 충족된 archē + demonstration (epistēmē) |
| **Aristotle 원전 위치** | *Nicomachean Ethics* VI (윤리학, 변할 수 있는 인간사) | *Physics* + *Posterior Analytics* + *Metaphysics* (자연학·논리학·존재론, 모든 영역) |
| **호출 도메인** | 의료 bedside, 교육 코칭, 리더십, 양형 | 인공물·코드 설계, 시스템 RCA, 가격·구조 재설계, 본질적 정의 |
| **변할 수 있음 / 없음** | 변할 수 있는 인간사 전용 | 변하지 않는 것까지 포함 (자연 현상·논리 구조) |

두 스킬을 한 스킬로 묶으면 description이 비대해지고, "phronesis 영역에서 4원인을 펼치거나 / causal-why 영역에서 phronimos를 베끼는" 잘못된 매핑이 발생한다. Aristotle 자신이 *NE* VI.5–7에서 phronesis와 epistēmē/sophia를 명확히 분리했고(NE VI.7, 1141b14–18), causal-why 도구는 epistēmē/sophia 쪽 가족에 속한다.

분리의 또 다른 효과 — 후속으로 같은 인물의 또 다른 method(예: *Rhetoric*의 enthymeme, *De Anima*의 perception)를 별도 스킬로 가르는 패턴이 정해진다.

### 2) 왜 4원인과 First Principles(archē)를 한 스킬로 묶었는가

분리할 수도 있었다. 그러나 묶은 이유:

1. **두 도구가 좌표계로 함께 작동한다.** 4원인은 수평 분해, archē는 수직 추궁 — 한 좌표의 두 축이다. Aristotle 자신이 *Posterior Analytics* II.11(94a20 ff.)에서 두 도구를 **명시적으로 연결**했다: 4원인이 demonstration의 middle term이고, demonstration은 archē에서 출발한다. 분리하면 사용자가 "이건 4원인 영역인가, archē 영역인가"를 매번 골라야 하는데, 원전에서는 한 절차 안에서 함께 작동한다.

2. **절차의 자연스러운 흐름** — Move 2(4원인 분해, 한 층)에서 Move 4(수직 추궁, archē까지)로 이어진다. 분해 → 추궁이 한 호흡이다. 분리하면 사용자가 한 작업을 두 번 호출해야 한다.

3. **substantive task 트리거 요구** (7 Principles #5). "4원인만 적용해줘"라는 정확한 호출은 드물다. 실제 트리거는 "왜 이게 이렇게 됐지", "5 Whys로 부족해", "first principles로 보자" — 이 막힘은 두 도구가 함께 가야 풀린다.

4. **lineage 비교가 한 스킬 안에서 작동한다.** 5 Whys(작용인 단일 추궁), 머스크 first principles(질료인 분해 + 단층 추궁), Bacon(목적인 거부), Descartes(단일 universal archē) — 모두 4원인 + archē 좌표 위에서 차이가 드러난다. 분리하면 비교 자체가 어색해진다.

### 3) 5 Whys / Musk first principles와의 차이를 어떻게 표면화했는가

다음 자리들에서 명시적으로:

- **Anti-pattern #1 (단일 갈래 만족)** — Toyota 5 Whys의 구조적 한계를 직접 명명. 작용인 한 갈래만 거슬러 올라가는 절차임을 표면화.
- **Anti-pattern #7 (Musk-shallow trap)** — 머스크의 first principles가 사실상 질료인 단일 추궁임을 표면화. 형상·작용·목적의 archē까지 가지 않으면 절차의 절반.
- **Anti-pattern #8 (임의의 N단계 추궁)** — 5 Whys의 "5"는 휴리스틱이지 archē 판별 조건이 아님을 명시.
- **휴리스틱 R8** — 머스크식 강점(질료인 분해)을 살리되 그것을 가능하게 한 telos 재정의("화성")까지 보아야 함을 표면화.
- **Example 1 (시스템 다운)** — 5 Whys로 부족함을 느낀 사용자가 4원인으로 보완하는 walkthrough를 그대로 시연. "리뷰 프로세스 부재"에서 멈춘 단일 갈래에 형상인(스키마 가정)·질료인(인프라)·목적인(서비스 telos) 가지를 동시 확장.
- **Example 2 (SaaS 가격)** — 머스크식 질료인 분해가 SaaS에선 약함(한계비용 0)을 시연하고, 목적인·작용인 archē가 실제 lever임을 드러냄.

### 4) Final cause가 무의미한 영역에서의 적용 정책

비적용 영역으로 명시 (When to use의 호출 금지 영역):

- 순수 자연 현상의 기계적 설명 (일식·날씨·물리 법칙) — Aristotle 자신의 *Metaphysics* VIII.4 자가 한계 표명 + Bacon의 1620년 비판.
- 진화·자연선택의 기능 설명 — Mayr의 teleonomy 운동. final cause를 강요하면 teleology 오류.

운영적 처리는 휴리스틱 R3 ("자연 현상·물리 시스템에는 목적인을 강제하지 않는다") + Move 2의 "권장 순서" ("자연 현상 분석에선 Aristotle 원전 순서, 단 목적인이 N/A인 경우 많음") + Move 2의 "빈 칸이 있으면 N/A인지 모르는지 명시" 정책으로.

경계가 모호한 영역(진화한 사회 제도, 학습한 AI 모델, 자연발생한 시장 구조)은 **명시적 판단이 필요**한 회색 지대로 ADR Consequences에 남긴다.

### 5) 트리거 (description 설계)

사용자가 실제로 쓸 표현 + 인물·고유 개념 키워드를 명시:

- 인물·개념 키워드: "아리스토텔레스" / "4원인" / "사원인" / "four causes" / "질료인" / "형상인" / "작용인" / "동력인" / "목적인" / "aitia" / "first principles" / "제1원리" / "제일원리" / "archē" / "아르케"
- 자연어 표현 10개: "왜 이게 이렇게 됐지" / "근본까지 거슬러 올라가고 싶다" / "본질이 뭔지 알고 싶다" / "이게 왜 작동하는지 모르겠다" / "유추로만 답하고 있는 것 같다" / "왜 이 가격이어야 하지" / "왜 이 구조여야 하지" / "fuse가 끊겼다에서 멈추기 싫다" / "5 Whys로는 부족하다" / "first principles로 다시 보자"

명시적 인물명 없이도 트리거되도록 "사용자가 아리스토텔레스를 명시하지 않아도" 한 줄을 박았다. 단, 이 레포의 트리거 정책(meta-ADR 0001)에 따라 master-router를 먼저 호출하는 것이 권장 흐름이라는 한 줄을 동시에 박아 표면 충돌을 방지.

비적용 영역 6종(알고리즘 단순 조회 / reversible 실험 / 자연 현상에 목적인 강요 / 진화에 final cause 강요 / 단일 universal foundation / Cartesian doubt 영역)을 명시. 특히 같은 인물의 phronesis 스킬과의 표면 충돌을 명시한 한 줄을 description에 박았다 — master-router가 두 인물-스킬을 가를 수 있도록.

Triggering guide 5개 항목 통과:
- [x] 80자 이상 (실제 ~1000자)
- [x] 무엇을 하는 스킬인지 (도입 한 문장: "두 축으로 묻는 사고법 — 수평 4원인 + 수직 archē")
- [x] 사용자가 실제로 쓸 표현 10개+ 명시
- [x] 명시 안 해도 트리거 (한 줄 박힘)
- [x] should-NOT-trigger 경계 (6종 명시)

### 6) 잘라낸 것

- **Open tensions 5개 중 T2/T4/T5의 본문 노출 자제** — lean 원칙. nous epistemology, transferability, 목적인 살아남는 영역의 회색 지대 — 학술적 가치는 크지만 사용자 의사결정에 직접 영향이 적음. ADR Consequences에만 surface.
- **그리스어 원문 직접 인용** — 본문에는 transliteration + 표 안의 짧은 그리스어만. ADR Primary sources의 Bekker 행번호로 학술 참조 가능성 확보.
- **Falcon의 "modes of explanation" 학술 논쟁** — 본문에 anti-pattern #4 한 줄로만 박음. T3 학술 긴장은 ADR에만 남김.
- **De Partibus Animalium 생물체 분석 사례** — raw §Gaps의 G5. 1차 인용 확보 못 함. 본문에 박지 않음. 후속 보강 시 example 3으로 추가 가능.
- **소프트웨어 아키텍처 적용 사례 Deshpande 인용** — raw §Gaps의 G6. 본문 일부만 확보. Example 1·2를 자체 시나리오로 작성해 우회.
- **한국어 표준 학술 번역 verbatim 인용** — raw §Gaps의 G3. 김진성·조대호 번역 본문 미접근. 한국어 번역어("질료인/형상인/작용인(동력인)/목적인")는 일반 통용 표기 채택.
- **5단계 "트리거 인지(Step 0)"를 별도 Move로 두지 않음** — Move 1에서 흡수. SKILL.md의 "When to use" 섹션이 사실상 Step 0 역할.

### 7) Resource 분리 여부

references/scripts/assets 디렉토리를 만들지 않았다.

- 본문이 ~250줄 (500줄 임계 이하).
- 결정론적 helper(4원인 자동 분류, archē 자동 판별)는 불가능 — Falcon의 "modes of explanation" 해석상 4원인 분류는 도메인·맥락 의존적이고, archē 판별은 다섯 멈춤 조건 중 어떤 것이 충족됐는지를 사람이 판단해야 한다. 자동화하면 anti-pattern #4(체크리스트 기계화)로 미끄러진다.
- 4원인 표를 `assets/four-causes-template.md`로 빼는 것을 검토했으나, 도메인이 너무 다양해서(인공물/자연/코드/조직/가격) 한 템플릿보다 본문 표 + Example 2개가 강하다고 판단. application log 후 재평가.

### 8) Master-router와의 관계

`master-router`에 등록 시 다음 룰이 잡혀야 한다:

- 트리거 신호 = ("왜 이게 이렇게 됐지" + "근본 / 본질 / first principles / archē") 조합. 또는 ("5 Whys / 머스크 first principles로 부족하다" + 더 깊은 추궁 욕구).
- 같은 인물 스킬과의 분리:
  - `aristotle-phronesis`: 보편 원칙이 어색한 개별 상황에서 행동 한 가지. **인간사·실천 영역 전용**.
  - `aristotle-causal-why`: 현상의 원인 좌표 분해 + archē 추궁 + demonstration 재구성. **자연·논리·구조 영역 포함, 모든 도메인**.
- 다른 거장 스킬과의 분리:
  - `lee-eo-ryeong-questioning`: 통설 *자체*를 의심해 의미 재정의. causal-why는 통설을 *유지*하면서 그 원인 구조를 분해.
  - `mckinsey-structured-problem-solving`: MECE로 평균 케이스 구조화 (해결 lever 식별). causal-why는 원인 좌표 (이해/설명/archē 도달). 액션 우선이면 mckinsey, 이해 우선이면 causal-why.
  - `erich-fromm-having-vs-being`: 활동의 성공 기준 모드 진단. causal-why는 원인 좌표 분해. 직교축이라 표면 충돌 거의 없음.
- 호출 우선순위: "왜 / 근본 / 본질 / first principles / archē / 4원인" 류 표면이 명시되면 causal-why 우선. "이 상황 어떻게 풀까 / 어디서부터" 류면 mckinsey가 디폴트. "이 사람·이 시점·이 맥락" 류면 phronesis가 디폴트.

## Consequences

### Positive

- mimesis 스킬 셋이 "통설 의심 / 모드 진단 / 평균 구조화 / 평균 밖 적합성 / **원인 좌표 추궁**" 다섯 축으로 완비된다. 사용자 의사결정·이해 막힘 패턴을 더 넓게 커버.
- **5 Whys / 머스크 first principles의 한계를 사용자가 식별할 수 있는 도구**가 처음 생긴다. 두 도구 모두 현장에서 널리 쓰이지만, 작용인 단일 추궁 / 질료인 단일 추궁의 부분 채택임을 표면화하는 자리가 mimesis에 없었다.
- 같은 인물(Aristotle)의 다른 method를 별도 스킬로 가르는 **선례**가 0004(phronesis) + 0005(causal-why)로 정착된다. 후속으로 *Rhetoric*의 enthymeme, *De Anima*의 perception, *Politics*의 polis 같은 method를 별도 스킬로 가를 수 있는 패턴이 명확해진다.
- 인공물·코드·아키텍처·가격 구조 분석에서 **목적인부터 시작하는** 절차가 명시적으로 박혔다 — 휴리스틱 R2. 디자인·설계 회고에서 자주 빠지는 telos 명시화를 강제한다.
- Lineage(Bacon → Descartes → Ohno → Mayr → Musk → Falcon)를 ADR에 명시 — 후속 스킬이 이 lineage의 어느 갈래를 별도로 다룰지(예: Mayr의 teleonomy를 진화·AI 모델 분석 전용 스킬로) 결을 갈라낼 수 있다.

### Negative / Trade-offs

- **두 도구 묶음의 학습 곡선** — 4원인 + archē + per se 필터 + 멈춤 조건 5개 + 8 휴리스틱 + 9 anti-pattern을 한 번에 마주하면 압도된다. Move 1(질문 형식)과 Move 2(4원인 분해) 두 단계만 돌려도 사용자가 가치를 보도록 본문 구조를 짰지만, 풀 절차의 진입 비용은 phronesis보다 높다.
- **archē 도메인 transferability 미해소** (T4). 머스크식 transfer("물리학적 사고법을 다른 도메인에")가 정당화되는 조건이 원전에 없다. 휴리스틱 R7로 "import하지 않는다" 보수적 정책을 깔았지만, 실제 사용자는 transfer를 시도할 가능성이 크고 이 경우 ADR이 명시한 안전망이 없다.
- **목적인 살아남는 영역의 회색 지대** (T5). 휴리스틱 R3(자연엔 강제 안 함)와 R2(인공물엔 시작점)로 양극단은 처리되지만, 중간 영역(진화한 사회 제도, 자연발생한 시장 구조, 학습한 AI 모델)은 사용자 자가 판단에 맡겨진다. anti-pattern #5(telos creep)로 경계하지만 완전 차단은 어렵다.
- **nous epistemology 절차화 부재** (T2 + G1). archē 판별은 다섯 멈춤 조건으로 운영했지만, Aristotle의 원전 epistemology(nous의 직관적 이해, *Posterior Analytics* II.19)는 raw 단계에서 수집 누락. 사용자가 archē에 도달했을 때 "어떻게 그것을 안다고 확신할 수 있나"의 인식론적 단계가 절차에 박혀 있지 않다. 멈춤 조건 5개가 충족됐다는 외부 체크로만 운영.
- **체크리스트 기계화 위험** (anti-pattern #4). 사용자가 4원인 표를 빈칸 채우기로만 쓰는 케이스를 본문 anti-pattern + Move 3(per se 필터)로 차단했지만, 첫 사용 시 일어날 가능성이 가장 높은 오용 패턴이다. 특히 자동화 도구·LLM이 이 표를 단순 채우기로 다룰 우려.
- **같은 인물의 두 스킬 사이 호출 혼동** — phronesis와 causal-why의 트리거 표면이 다르지만, 사용자가 "왜 이 환자에게 이 가이드라인이 안 통하지" 같은 발화로 시작하면 두 스킬 모두 후보가 된다. master-router에서 인물·도메인 가르기로 분리하지만, 실전 표현이 더 섞일 가능성.
- **머스크식 first principles로 들어온 사용자가 4원인 확장을 거부할 위험.** 머스크의 명성과 단순성 때문에 "질료인 분해만으로 충분하다"는 자기 만족에 머물 가능성. anti-pattern #7(Musk-shallow trap)과 휴리스틱 R8로 표면화했지만 완전 차단은 어렵다.

### Open questions

- Example을 인공물·시스템 RCA·가격 외 도메인(생물체 기능, 진화한 사회 제도, AI 모델 분석)으로 더 늘려야 할까? — 비적용 영역과의 경계 회색 지대를 example로 시연하면 가치가 있지만 본문이 길어진다.
- per se / per accidens 필터를 Move 3으로 승격한 결정이 사용자에게 직관적으로 작동하는가 — application log로 검증. 만약 사용자가 이 필터를 매번 건너뛰면 Move 2 안의 sub-step으로 다시 내릴 수 있다.
- 머스크식 first principles로 들어온 사용자가 4원인 확장을 거부하는 빈도 — anti-pattern #7이 실제로 작동하는지 application log.
- 본문 표(4원인 정의)를 `assets/`로 분리할 것인지 — 도메인 다양성 vs 본문 lean 사이 trade-off. 첫 사용 후 재평가.
- AI 모델·진화한 시스템의 목적인 처리 — 별도 스킬(`mayr-teleonomy`?)로 분리할 가치가 있는가. Mayr의 작업이 충분히 독립적이지만 mimesis의 figure-anchored 룰을 따른다면 가능. 단, 이런 스킬을 만들면 같은 영역에서 causal-why와 트리거 표면이 겹친다 — master-router의 분기 룰이 더 복잡해진다.
- Aristotle 그리스어 원문 인용을 더 surface해야 하는가 — phronesis 스킬과 같은 정책(ADR Primary sources에 Bekker 행번호로만 박음)을 유지했지만, causal-why는 4원인이라는 더 명사적 개념이라 원어 노출의 학습 효과가 다를 수 있다.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - Move 1(질문 형식 결정)이 실제로 (a)(b)(c)(d) 4분기로 갈리는지, 사용자가 어떤 분기를 가장 많이 트리거하는지 (가설: (d) 고장 why가 가장 흔함 — 5 Whys 대체 수요).
  - Move 2(4원인 분해)에서 "권장 순서" — 인공물엔 목적인부터, 자연엔 질료인부터, 고장엔 작용인부터 — 의 분기가 실제로 사용자 도메인에 맞게 동작하는지.
  - Move 3(per se 필터)이 실제로 우연적 원인을 걸러내는 빈도 — 이게 작동하지 않으면 anti-pattern #4(체크리스트 기계화)로 미끄러진다.
  - Move 4(수직 추궁) 멈춤 조건 5개 중 어느 것이 가장 자주 충족되는지 — 만약 "5(도메인 정합)" 한 종류로만 수렴하면 archē 판별이 단조로워진 신호.
  - Example 1(시스템 다운, 5 Whys 보완) vs Example 2(SaaS 가격, Musk 확장) 중 어느 것이 사용자 self-recognition에 더 강하게 작동하는지.
  - 머스크식 first principles로 들어온 사용자가 4원인 확장을 받아들이는 비율 (anti-pattern #7 실효성 검증).
  - phronesis와의 호출 분기가 master-router에서 깔끔하게 작동하는지 — 같은 인물 두 스킬 사이 혼동 빈도.
  - 13개 트리거 키워드 + 10개 자연어 표현 중 실제 호출에 기여한 표현 (특히 명시적 인물명·개념 없이 자연어 표현만으로 호출되는 비율).
