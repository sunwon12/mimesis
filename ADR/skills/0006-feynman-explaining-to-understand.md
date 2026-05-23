# ADR 0006: 파인만 — Explaining to Understand (이해의 자기-감사) 스킬

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/feynman-explaining-to-understand/`
- **Source figure(s)**: Richard Feynman (1918–1988)
- **Primary sources**:
  - [research raw](../../research/feynman/first-principles-and-learning-raw.md)
  - [research summary](../../research/feynman/first-principles-and-learning-summary.md)
  - *Cargo Cult Science* (1974 Caltech commencement address) — "you must not fool yourself, and you are the easiest person to fool"
  - *The Feynman Lectures on Physics* Vol I, Preface (1963) — "the system is a failure" + "atoms in motion" 한 문장 (Lecture 1)
  - 1966 NSTA talk "What Is Science?" — 아버지 일화: "you'll only know about humans in different places, and what they *call* the bird"
  - BBC *Fun to Imagine* (1983) interview — 자석을 고무줄로 환원하기를 거부 ("I can't explain that attraction in terms of anything more familiar to you, because I don't understand it…")
  - David Goodstein, *Feynman's Lost Lecture* (1996) — spin-½ Fermi-Dirac 일화: "I couldn't reduce it to the freshman level. That means we don't really understand it"
  - James Gleick, *Genius* (1992), Ch 12 — Caltech 시절 "Notebook of Things I Don't Know About" 묘사
  - 1979 Auckland lecture (QED preview) — "If it disagrees with experiment, it's wrong. That's all there is to it"

## Context

mimesis 스킬 셋이 자라면서 *같은 입에서 나온 표현*("first principles", "근본부터", "본질이 뭔지")이 여러 스킬의 트리거 표면을 동시에 건드리는 일이 발생했다. 특히 `aristotle-causal-why` (ADR 0005 skills) 가 이미 **인공물·시스템·아키텍처를 외부에서 분해하는 first-principles** 결을 가져갔다 — 4원인 분해 + archē 수직 추궁 + 머스크식 axioms-up 재설계. 그 description은 "왜 이 가격이어야 하지", "왜 이 구조여야 하지", "first principles로 다시 보자" 까지 모두 받는다.

파인만을 새 스킬로 들이려고 보니 표면이 정면충돌한다. raw 1차 자료에서도 파인만 본인은 "first principle"이라는 단어를 *epistemic posture* — "you must not fool yourself" — 의미로만 한 번 썼다 (Q2). Musk-style "axioms-up first-principles thinking" 라벨은 사후에 파인만에게 붙은 frame이다. raw §Open tension 6번이 이 사실을 보존한다.

그러므로 파인만 스킬을 "first-principles thinking 전반"으로 잡으면 `aristotle-causal-why` 와 무한 충돌하면서 둘 다 흐려진다. 파인만에게 *고유한 결*만 분리해야 한다.

해부도(summary)와 Open tension 마지막 항목을 보면 파인만 고유의 결은 다음과 같이 좁혀진다:

- "내가 진짜 이해했는가"의 **자기-감사 (learning self-audit)** — *이미 안다고 믿는 것*에 적용되는 방향성.
- **Brazil-bay 진단** (Q9) — 이름은 아는데 창밖 바다에 적용 못함.
- **Freshman-level reduction** (Q16) — 못 줄이면 *우리가* 모르는 것이라는 *공동체-차원* 진단.
- **Cargo Cult Science** (Q3, Q4) — 자기를 속이지 않는 자세.
- **Notebook of Things I Don't Know** (Q15) — 자기 무지의 지도.
- **권위·공식의 ignorance** (Q17) — "science의 권위를 provenance로 대체."

→ 파인만 스킬은 "**이미 안다고 믿는 것**을 자기-감사" + "fluent하지만 비어 있을 수 있는 설명을 까발리기"에 좁힌다. 새 문제를 아키텍처 차원에서 분해하는 작업은 `aristotle-causal-why`에 양보한다.

## Decomposition

summary의 구조를 그대로 옮기되, 이 스킬화 결정에 직결된 축으로 재정리한다.

### One-line essence (summary §One-line essence)

"이름을 가진 무언가를 기계적 동작으로 분해해 *눈앞의 사례*에 대고 시험하라. 자기 자신은 가장 속이기 쉬운 청중이다." 이 한 줄이 first-principles 결과 learning 결을 묶는 동일한 동작이다 (근거: Q2, Q5, Q6, Q7, Q11, Q15).

### Core principles → Mental moves 매핑

summary의 6 core principles + 11 mental moves를 스킬화하면서 **9-step procedure** 로 압축했다 (Move 1–9). 압축 근거:

- summary Move 1(floor) → SKILL Move 1 (근거: Q2, Q3)
- summary Move 2(strip names) → SKILL Move 2 (근거: Q5, Q6, Q8, Q9)
- summary Move 3(notebook) → SKILL Move 3 (근거: Q15)
- summary Move 4(kernels) → SKILL Move 4 (근거: Q1, Q15)
- summary Move 5(explicit frame) → SKILL Move 5 (근거: Q12, Q14)
- summary Move 6+7(guess→consequence→look + apply to thing in front) → SKILL Move 6 (Brazil-bay) (근거: Q7, Q9, Q11)
- summary Move 8(freshman reduction) → SKILL Move 7 (근거: Q16, C2)
- summary Move 9(refuse false analogy) → SKILL Move 8 (근거: Q12, Q13, C5)
- summary Move 10(disclose what could make you wrong) → SKILL Move 9 (근거: Q4)
- summary Move 11(restart from kernel) → SKILL Move 4의 일부로 흡수 (자기-감사 모드에 핵심 손실 없음, lean 원칙)

### Heuristics (summary §Heuristics)

7개 휴리스틱 중 7개 모두 SKILL.md에 살림 (jargon → name only; can't predict concrete case → cargo; freshman fail → *we* don't know; false-analogy refuse; provenance over authority; smoothness suspect; experiment-disagreement-final). 각 휴리스틱의 Why 한 줄이 summary Q번호에 직결한다.

### Anti-patterns (summary §Anti-patterns)

8개 anti-pattern 중 7개를 SKILL.md에 흡수 (memorization without bridge, credentialed jargon, cargo-cult form, bending truth, false-analogy, smoothness pass, freshman-fail-as-shaming, reality-check skipped). 잘라낸 것: "stopping at why without frame" — Move 5에 흡수됐고 별도 anti-pattern으로 또 적으면 중복. "privileging frontier over foundational" — 사용자 현장 사고에 직접 활용도가 낮음 (학자적 자세론), ADR에만 남김.

### When this thinking applies / boundaries (summary §When this thinking applies)

5개 적용 영역 + 5개 boundary를 SKILL.md "When to use"에 옮김. boundary 중 두 개 (false-analogy 영역, reality-check 불가 영역, 평균 학습자에 강의로 전달)는 description에도 should-NOT-trigger 한 줄로 명시 — Triggering guide 체크리스트 5번 항목 통과.

### Open tensions (summary §Open tensions)

6개 tension 중:

- "first-principles 결 vs learning 결의 미세한 차이" (tension #2) → **이 ADR Decision의 "잘라낸 것"의 1번 항목으로 살림** (first-principles 결을 `aristotle-causal-why`로 라우팅).
- "방법은 작동하는데 가르치는 형태로는 실패" (tension #3) → SKILL.md "When to use"의 호출하지 말 것 4번 (평균 학습자에 강의 형태로 전달)에 surface.
- "explain it simply 테스트의 방향" (tension #4) → SKILL.md Move 7의 Why 한 줄("진단의 방향이 자기-비난이 아니라 무지 지도") + Anti-pattern "freshman-fail-as-shaming" 두 곳에 박힘.
- "간단한 설명이 환상을 만들 위험" (tension #5) → SKILL.md Heuristic "매끄러움이 의심되면 시험하라" + Anti-pattern "자기-감사를 매끄러움으로 통과시킴" 으로 박힘.
- "Aggressive simplification vs aggressive refusal" (tension #1) → SKILL.md Move 4 (커널 환원)와 Move 8 (거짓 친숙 환원 거부)의 *분업* 으로 surface — 파인만 본인 안에서는 모순이 아니라 kernel reduction과 false-analogy reduction의 구분이라는 점이 두 Move의 Why에 박힘.
- "'first principles' 라벨 자체" (tension #6) → 이 ADR Context와 아래 Decision의 "잘라낸 것"의 핵심 근거.

## Decision

### 트리거 (description 설계)

description에 박은 사용자 표현 14개:

1. (인물·개념 명시) "파인만 / Feynman / Feynman technique / 파인만 학습법 / 파인만 노트 / cargo cult / self-audit"
2. "쉽게 설명 못 하면 모르는 거다"
3. "freshman한테 설명해봐"
4. "이거 진짜 이해한 거 맞나"
5. "이름만 외운 것 같다"
6. "용어는 아는데 적용을 못 하겠다"
7. "공식은 아는데 메커니즘은 모르겠다"
8. "유창하게 설명은 하는데 내가 정말 아는지 모르겠다"
9. "내가 나를 속이는 것 같다"
10. "권위·교과서에 기대고 있다"
11. "이 개념을 누구한테 설명할 수 없다"

명시적 인물명 없이도 트리거되도록 "사용자가 파인만을 명시하지 않아도" 한 줄을 박았다. should-NOT-trigger 경계 4종 (false-analogy 영역, reality-check 불가 영역, 평균 학습자에 강의 형태, 새 문제를 아키텍처 차원으로 분해하는 작업)을 명시했다. 특히 마지막 경계가 `aristotle-causal-why`와의 분담이다 — `master-router` 경유 권장을 description에 한 줄로 박았다. Triggering guide 5개 항목 모두 통과.

### 스킬명 — 왜 `feynman-explaining-to-understand`인가

후보 비교:

- `feynman-explaining-to-understand` (선택) — gerund, Feynman technique 결 강조. "explain"이 곧 *이해 검증*임을 이름이 직접 운반.
- `feynman-rebuilding-from-scratch` — first-principles + learning 통합 결. 그러나 "rebuilding"이 *새 문제 공격*을 연상시켜 `aristotle-causal-why`와 트리거 표면 충돌 가능성이 크다.
- `feynman-first-principles` — 잘 알려진 명칭이지만 (a) gerund 아님 (b) 정확히 `aristotle-causal-why` 와 정면충돌 (c) raw §Open tension #6이 보존한 사실 — 파인만 본인은 이 라벨로 부르지 않았다 — 을 위반.

따라서 `feynman-explaining-to-understand`. Hard rules의 figure-anchored + gerund 권장 둘 다 충족. ASCII lowercase + hyphens, 32자, 룰 통과.

### 잘라낸 것 (의도적 제외)

이 결정이 ADR의 핵심이다. 파인만 스킬에서 의도적으로 양보·제외한 영역:

1. **Musk-style "axioms-up first-principles thinking" 결 — `aristotle-causal-why` 로 라우팅.** 가격 재설계, 시스템 RCA, 4원인 분해, "왜 이 구조여야 하지" 류의 *새 문제를 아키텍처 차원에서 분해하는 작업*은 파인만 description에서 명시적으로 제외한다 (should-NOT-trigger 라인). 근거:
   - raw §Open tension #6: 파인만 본인의 코퍼스에서 "first principle"은 epistemic posture 의미로 한 번만 쓰였다 (Q2). Musk frame은 사후 적용.
   - `aristotle-causal-why` description이 이미 머스크식 first-principles ("왜 이 가격이어야 하지", "fuse가 끊겼다에서 멈추기 싫다", "5 Whys로는 부족하다") 표현을 받고 있다.
   - 두 스킬을 같은 표면에 두면 master-router 부담만 늘어나고 두 description이 흐려진다.
   - ambiguous한 자연어 표현("first principles로 다시 보자")만 있을 때는 master-router가 분기 — 명시적 인물·개념이 있을 때만 직접 호출.

2. **학습 자기-감사 + cargo-cult 자기-기만 방지 + freshman-reduction 자기-진단에 좁힌 이유.** 파인만 코퍼스의 *고유한* 기여는 — 4원인이나 axioms-up과는 달리 — *이미 안다고 *느끼는* 것*을 까발리는 self-audit 동작이다. Brazil-bay 진단(Q9), freshman-reduction(Q16), notebook of things I don't know(Q15), "you are the easiest person to fool"(Q2) — 이 네 가지는 외부 분석이 아니라 *내부 점검* 도구다. 이 결은 mimesis 기존 셋(lee-eo-ryeong 통설의심 / fromm 모드진단 / mckinsey 구조화 / aristotle-causal-why 외부분해 / aristotle-phronesis 개별적합성)에서 비어 있다.

3. **"Notebook of Things I Don't Know"를 별도 references/로 분리하지 않음.** Principle #2 (progressive disclosure)의 분리 기준 ("SKILL.md가 300줄 넘어가거나 도메인 변종이 여러 개일 때")에 미달. 노트북은 SKILL.md Move 3 안에서 *mental move* 로 충분히 운반된다. 별도 references/notebook-of-things-i-dont-know.md를 만들면 (a) 본문이 분산되고 (b) 사용자가 *템플릿 채우기*로 받아들여 cargo-cult 형식주의에 빠질 위험이 있다. 노트북의 본질은 양식이 아니라 *질문을 정리하는 동작*이라는 raw §Open tension #2를 보존하기 위해 별도 자료화는 의도적으로 회피.

4. **`feynman-rebuilding-from-scratch` (= first-principles + learning 통합) 네이밍 회피.** 파인만 안에서는 두 결이 같은 동작이라는 essence는 보존하되, *스킬 트리거 단위*에서는 좁혀야 했다. summary §Open tension #2가 그 분기점: "스킬화할 때 어느 모드인가 — 새 문제 공격인가 자기-감사인가 — 를 명시하면 트리거가 명확해진다." 자기-감사 모드만 살림.

5. **Lectures *서문*의 "system failure" 인정을 본문 깊이 박지 않음.** raw Q19/Q20의 자기-비판은 ADR Consequences §Negative에 옮기고, SKILL.md "When to use" 호출하지 말 것 4번 ("평균 학습자에게 강의 형태로 전달") 한 줄로만 surface. 본문에서 이걸 깊게 다루면 학습 자기-감사 도구의 자신감을 깎는다.

6. **Cargo Cult Science 원본 PDF 1차 검증을 후속으로 넘김.** raw §Gaps 3에 명시된 한계. SKILL.md는 2차 채널 인용을 사실로 전제하고 작성됐다 — 인용된 핵심 구절("you must not fool yourself", "you are the easiest person to fool", "bending over backwards") 이 잘못 인용된 사실이 확인되면 SKILL.md Move 1 + Move 9의 wording을 수정해야 한다.

7. **Lineage(머스크·맥킨지·Khan Academy의 "Feynman technique" 변용)를 본문에서 surface하지 않음.** figure-anchored 룰 + lean 원칙. lineage 언급은 ADR Primary sources와 Context에만.

### Resource 분리 여부

references / scripts / assets 디렉토리를 만들지 않았다.

- SKILL.md 본문이 ~180줄 (500줄 임계 이하).
- 결정론적 helper는 파인만 사고법의 본질상 만들 수 없다 — *자기-기만은 패턴화하면 다음 자기-기만의 매개가 된다* (Principle #3와 raw §Anti-patterns의 cargo-cult 비판 둘 다 동일 결).
- 진단 템플릿(Brazil-bay 적용 체크리스트, freshman 환원 체크리스트)을 assets/로 빼는 것을 검토했으나, 사용자가 *템플릿 채우기*로 받아들이면 정확히 cargo-cult anti-pattern을 install하게 된다. example 2개(코드 학습 자기-감사 + 코드리뷰 권위 인용)가 템플릿보다 강하다고 판단. application log 후 재평가.

### Master-router와의 관계

`master-router`에 등록 시 다음 룰이 잡혀야 한다:

- 트리거 신호 = (이미 안다고 *느끼는* 것 + 메커니즘 의심) 조합. *새 문제*가 아니라 *이미 가진 이해*에 대한 self-audit이라는 방향성이 결정적.
- 다른 스킬과의 분리:
  - `aristotle-causal-why`: 인공물·시스템·아키텍처를 *외부에서* 분해 (새 문제 / 설계 검토 / RCA / 가격 재설계). 파인만은 *자기 내부 이해*를 self-audit. 같은 "first principles" 표현이 양쪽에 떨어지면 master-router가 분기.
  - `lee-eo-ryeong-questioning`: 통설을 의심해 폐기·재정의. 파인만은 통설의 *메커니즘 부재*를 점검하지만 통설 자체를 폐기하지 않는다 — Q11의 "guess can be wrong"이지만 default는 검증 가능한 메커니즘이다.
  - `aristotle-phronesis`: 보편 원칙이 *이 사례*에 안 맞을 때 개별 적합성 진단. 파인만은 보편 원칙을 *내가 정말 안다고 할 수 있는가* 진단. 둘 다 "보편 원칙"이라는 표면을 공유하지만 진단 방향이 다르다.
  - `mckinsey-structured-problem-solving`: 평균 케이스 구조화. 파인만은 평균 케이스의 *이해 자체*를 점검.
- 호출 우선순위: 사용자가 "이해했는가" 류를 명시하면 파인만 우선. "왜 이렇게 됐지 / 본질이 뭔지" 류면 `aristotle-causal-why` 우선. ambiguous하면 master-router가 둘을 후보로 띄우고 사용자 선택.

## Consequences

### Positive

- mimesis 스킬 셋이 "통설 의심 / 모드 진단 / 구조화 / 외부 분해 / 개별 적합성 / **내부 self-audit**" 6축으로 완비된다. 가장 흔한 학습·이해 막힘 ("공부했는데 진짜 안 거 같지 않다") 패턴을 처음 커버.
- `aristotle-causal-why` 와의 트리거 분담이 깔끔해진다 — *외부 분해* vs *내부 self-audit*. 동일 표현("first principles")이 떨어져도 master-router가 결단할 축이 명확해짐.
- 코드 학습·시스템 이해·온보딩 점검·코드리뷰의 권위 인용 자가-진단 같은 일상적인 엔지니어링 사고에 호출 가능한 스킬이 처음 생긴다.
- Brazil-bay 진단 + freshman reduction이라는 *2-기둥 출력 판정 룰*이 illusion of explanatory depth 안티-패턴을 차단한다 — "매끄러움 = 통과 신호"라는 가장 흔한 자기-기만 모드를 막는다.
- raw §Open tension #6의 보존 — "파인만 본인은 'first principles'라고 부르지 않았다" 라는 1차 자료의 사실을 ADR Decision에 박아 사후 lineage 라벨로 figure를 왜곡하지 않는 mimesis 운영 원칙의 선례를 만든다.

### Negative / Trade-offs

- **Self-audit이 또 다른 cargo가 될 위험.** 사용자가 9-step procedure를 *형식적으로* 돌리고 "통과했다"로 자기-인증할 수 있다. SKILL.md Move 1(floor) + Anti-pattern "매끄러움 통과"가 이를 막으려 하지만 완전한 차단은 불가능. raw §Open tension #5의 illusion of explanatory depth 비판이 이 스킬 자체에 그대로 적용되는 *자기-적용 위험*.
- **Freshman reduction이 자기-shaming 도구로 변질 위험.** 파인만의 원본은 "*we* don't understand"인데 사용자가 "*나는* 게으르다"로 받아들이면 진단 데이터가 자기-비난으로 흡수된다. SKILL.md Move 7의 Why와 Anti-pattern "freshman-fail-as-shaming" 두 곳에 박았지만, 한국 학습 문화의 자기-shaming 디폴트와 충돌할 가능성. application log로 모니터링 필요.
- **`aristotle-causal-why` 와의 경계 모호함.** "first principles" 표현은 양쪽 description에 모두 떠 있다. master-router가 분기를 잘못하면 잘못된 스킬이 호출된다. 사용자가 *내가 이해했는가*(파인만) vs *이게 왜 이렇게 됐는가*(아리스토텔레스)의 차이를 본인도 인지하지 못한 채 입력하는 경우가 가장 자주 일어날 것이다.
- **Reality-check 불가 영역에서 무용.** boundary로 명시했지만 사용자가 boundary를 무시하고 호출하면 첫 다섯 step만 돌고 *cargo를 더 정교하게 짓는 도구*가 된다 — raw §When this thinking applies의 마지막 항목 (Q11, C6)이 정확히 이 위험을 짚는다.
- **9-step procedure의 학습 곡선.** Move 1~9를 한 번에 돌리는 건 압도적이다. 사용자가 일부만 적용해도 가치가 나오도록 Move 6(Brazil-bay)과 Move 7(freshman reduction)을 핵심 출력 판정 두 기둥으로 박았다. 이 둘만 돌려도 "이해했다 vs 이름만 안다"의 80%는 잡힌다.
- **raw §Gaps 5에 명시된 빈자리** — 파인만 본인이 *학습 자기-감사*에서 어떻게 reality-check 단계를 수행했는지 1차 자료가 부족하다. SKILL.md는 Q11(과학적 가설의 reality-check)을 학습 모드에 *전용*해 박았지만 — 이게 파인만 본인의 실천이었는지 우리의 재구성인지가 보강이 필요하다. application log에서 사용자의 reality-check 단계가 어떻게 작동하는지 관찰해 후속 researcher pass로 보강.

### Open questions

- master-router에서 파인만 vs aristotle-causal-why 분기 룰을 *코드*로 박을 수 있는가, 아니면 ambiguous한 자연어 표현에서 둘을 *후보로 띄우고 사용자에게 선택*시키는 게 한계인가? 후자라면 사용자 인지 부담이 늘어난다.
- Example 2(코드리뷰 권위 인용)이 사용자의 self-recognition에 작동하는가? 학습 자기-감사가 *혼자 공부할 때*만이 아니라 *팀 상호작용*에서도 호출되어야 가치가 크다.
- Move 3(노트북) 의 작동 방식 — Gleick의 2차 서술만 있고 (raw §Gaps 2) 원본 노트북 내용 미확보. application 후 사용자들이 노트북을 *질문 정리* 용도로 쓰는지 *답 정리* 용도로 쓰는지 모니터링.
- Lineage 별도 스킬 분리 가능성: Khan Academy / Tim Ferriss / Anders Ericsson 류의 "Feynman technique" 변용이 충분히 독립적인 lineage를 형성한다면 별도 figure-anchored 스킬(`khan-explain-it-to-a-child`?)로 분리 가능. 단 mimesis 룰상 "method-only는 금지"이므로 그 lineage의 *대표 한 명*을 골라야 한다.
- description 14개 트리거 표현 중 실전에서 작동하지 않는 표현이 있을 것이다 — application log로 가지치기.
- 자기-적용 위험 (self-audit이 또 다른 cargo) 을 차단할 두 번째 게이트를 추가해야 하는가? — 현재는 Move 1(floor) + Anti-pattern 두 개만 박았다. 부족하면 별도 *meta-audit* heuristic을 7번 휴리스틱으로 추가 검토.

## Application log

- TBD — 첫 사용 후 갱신. 특히 모니터링할 항목:
  - Move 6(Brazil-bay)이 실제 self-audit에서 작동하는 빈도 vs Move 7(freshman reduction)이 작동하는 빈도 — 두 기둥 중 어느 것이 더 자주 *통과/실패* 신호를 만드는가.
  - description 14개 트리거 표현 중 실제 호출에 기여한 표현 (특히 인물명 없이 자연어 표현만으로 호출된 비율).
  - master-router에서 파인만 vs `aristotle-causal-why` 분기 정확도 — "first principles로 다시 보자" 류의 ambiguous 표현이 들어왔을 때 어디로 가는가.
  - Anti-pattern "freshman-fail-as-shaming"이 실제로 자기-비난 모드를 차단하는가, 아니면 한국 학습 문화 디폴트에 묻히는가.
  - Example 1(useEffect cleanup 자기-감사) vs Example 2(코드리뷰 권위 인용) 중 어느 쪽이 사용자 self-recognition에 더 강하게 작동하는지.
  - 9-step procedure 중 사용자가 *건너뛰는* step (특히 Move 5 frame 명시, Move 9 반례 노출) — 자주 건너뛰는 step이 나오면 lean 원칙에 따라 흡수·삭제 검토.
  - Self-audit 자체가 cargo가 되는 사례 — "다 통과했다고 적었는데 실은 매끄러움만 확인한 케이스" 가 얼마나 자주 나오는지. 빈도 높으면 meta-audit heuristic 추가.
