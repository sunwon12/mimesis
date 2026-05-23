# ADR 0007: David Ogilvy — 브랜드·카피·광고 협업 (collaborator agent)

- **Status**: Proposed
- **Date**: 2026-05-23
- **Shape**: collaborator (meta-0002, meta-0003)
- **Related skill**: `.claude/skills/ogilvy/`
- **Related agent**: `.claude/agents/ogilvy.md`
- **Source figure(s)**: David Ogilvy (1911–1999)
- **Primary sources**:
  - [research raw — methodology & craft](../../research/ogilvy/methodology-and-craft-raw.md)
  - [research summary — methodology & craft](../../research/ogilvy/methodology-and-craft-summary.md)
  - [research raw — brand & voice](../../research/ogilvy/brand-and-voice-raw.md)
  - [research summary — brand & voice](../../research/ogilvy/brand-and-voice-summary.md)
  - *Confessions of an Advertising Man* (1963) — "the consumer isn't a moron"; "factual advertising outsells flatulent puffery"; "first-class business in a first-class way."
  - *Ogilvy on Advertising* (1983) — Rolls-Royce 3-week saturation 케이스; Big Idea 5질문; 80센트 헤드라인 룰; 50-500 단어 readership 룰; 13% 드롭캡 룰; "Don't play games with the reader."
  - *The Image and the Brand* (1955 AAAA address) — "advertising as long-term investment in brand personality"; "the largest share of the market at the highest profit"; complex symbol.
  - 1982 Internal Memo "How to Write" — "people who think well, write well"; Roman-Raphaelson 3-read 룰; jargon 거부.
  - 1985 "We Sell, Or Else" Houston Advertising Federation speech — "If it doesn't sell, it isn't creative."
  - 매년 MoMA 강당 사원 강연 — "I admire / despise / dislike / pity / abhor" 4쌍 동사 인격 선언.
  - Hathaway eyepatch (1951), Rolls-Royce "the loudest noise" (1958), Dove "1/4 cleansing cream" (1957) — 60년 brand personality 적립의 sample cases.

## Context

mimesis의 figure 셋(0001~0006)은 모두 **diagnostic skill** shape이었다 — 한 거장의 *한 사고 동작*을 1턴 procedure로 박는 형태. 이 shape은 master-router(meta-0001) 정책과 figure-anchored 네이밍(meta-naming)에 정합했고, 7명의 거장을 같은 카탈로그 행에 배치할 수 있는 기반이었다.

그러나 David Ogilvy를 새 figure로 들이려고 자료를 모으는 과정에서 기존 shape이 깨지는 신호가 나왔다. raw 두 갈래(methodology-and-craft + brand-and-voice) 가 보여준 Ogilvy의 사고는:

1. **단일 사고 동작이 아니다.** 한 거장 안에 *카피 리뷰 / 헤드라인 작법 / 네이밍·포지셔닝 검증 / Big Idea 진단 / 캠페인 브리프 / 내부 메모 글쓰기*가 모두 들어 있다. 각 모드의 input·절차·통과 기준이 다르다 (methodology summary §Procedures by mode가 5개 모드를 명시적으로 분기). 한 SKILL.md procedure로 욱여넣으면 본문이 비대해지거나 추상화 손실이 일어난다.

2. **인격이 자료의 절반이다.** brand-and-voice summary는 voice·태도·비-타협 원칙을 본문의 한 축으로 명시했다 — "moron / flatulent puffery / toadies" 같은 직접 어휘, "I admire... I despise..." 4쌍 동사 인격 선언, MoMA 연설의 의식적 voice 박기. 진단 스킬의 procedure-only 형식은 이 voice를 운반하지 못한다.

3. **사용자 요구가 멀티턴이다.** "이 카피 어때 → 고쳤어 → 다시 봐줘 → 헤드라인은 어떻게" 의 연속 협업이 입출력 단위다. 1턴 진단으로 환원되지 않는다.

이 세 신호를 받고 meta-0002가 figure 자산을 **diagnostic skill** 과 **collaborator agent** 두 shape으로 분기하기로 결정했다. meta-0003은 그 결정의 종착점(파이프라인의 출력)을 어떻게 갈래낼지 — `skill-builder` 손대지 않고 `collaborator-builder` 신설 — 결정하되, *첫 collaborator(Ogilvy)는 collaborator-builder.md 없이 일회성으로 만들어 그 결과를 역설계해 templating한다*는 lazy materialize 전략을 선택했다.

본 ADR은 그 일회성 산출의 해체 기록이다. **Ogilvy 한 명을 어떻게 collaborator agent로 해체했는가**가 본문의 주제. 동시에 이 산출이 미래의 `collaborator-builder.md`의 참조 구현이 된다는 점에서 — 진단 ADR과 달리 — **shape 자체의 templating 단서**도 함께 박는다.

### 왜 Ogilvy인가 (figure-specific 이유)

shape이 collaborator라는 결정은 meta-0002·meta-0003에서 일반론으로 박혔다. 그러나 "왜 *Ogilvy*가 collaborator의 첫 사례인가"는 figure 단위로 따로 정당화되어야 한다:

- **자산의 구조가 자연스럽게 두 갈래.** Ogilvy의 1차 자료는 (a) operational craft(*Ogilvy on Advertising*의 룰·수치·체크리스트) 와 (b) brand philosophy + voice(*The Image and the Brand* 강연·*Confessions* 인격 선언·MoMA 연례 강연) 로 자명하게 분리된다. 진단 스킬은 한 갈래만으로 가능하지만, Ogilvy는 두 갈래가 같은 인격 안에서 작동해야 한다 — 이건 system prompt가 두 voice를 동시에 가져야 한다는 의미.

- **모드가 5개 이상.** methodology summary §Procedures by mode가 명시적으로 5개 (Research-first / Big Idea 진단 / Copy review / Headline 작법 / Internal business writing) 를 분리. brand-voice summary §The mental moves가 3개 (브랜드 포지셔닝 진단 / Big Idea의 brand 자본 검증 / 카피의 brand 자산 점검) 를 더한다. 두 summary 합치면 6~7개 모드가 한 거장 안에 공존. diagnostic skill로는 표현 불가.

- **Voice 인용이 두꺼움.** brand-voice summary §Voice / 태도 / 비-타협 원칙 섹션이 직접 어휘 인용 10개 이상을 raw에서 추출 — paraphrase하지 말고 그대로 박아야 인격이 운반된다는 점이 자료 자체에 강제. 이 정도 voice 자료는 system prompt로 격리되지 않으면 main 세션의 다른 신호에 빠르게 옅어진다.

- **사용자 시나리오가 "함께 일한다".** 사용자 발화 ("그 거장과 함께 일을 한다는 개념으로 그 스킬을 계속 호출하면 답을 구하거나 대화를 하거나 일을 시킬 것 같아") 가 정확히 Ogilvy의 사용 패턴 — 브랜드·카피 작업은 *진단 한 번*이 아니라 *지속 협업*. meta-0002 §Context의 표면화된 요구가 figure 단위로도 Ogilvy에 정확히 떨어진다.

- **거부권의 존재.** Ogilvy의 1차 자료엔 명시적 거부·anti-stance·"받지 마라/그만둬라"가 빈번 (brand-voice Q17, Q20). 협업의 voice가 default pushback이어야 한다는 점이 자료 자체에서 강제. 이건 main Claude의 default voice(공손한 동조)와 정면 충돌 — 격리된 agent로만 운반 가능.

### Decomposition 입력의 비대칭

두 summary는 자매다. 그러나 비대칭이 있다:

- **methodology summary**는 *procedures*가 본문 — 모드별 절차·체크리스트·정량 룰이 중심. agent의 *모드 분기* 섹션의 1차 재료.
- **brand-voice summary**는 *personality*가 본문 — voice·anti-stance·affirmative stance·비-타협 원칙이 중심. agent의 *인격 정의* 섹션의 1차 재료.

이 비대칭을 ADR이 합치되 한쪽에 치우치지 않게 보존해야 한다. 인용 번호는 두 summary가 독립 namespace이므로 본문에서 인용할 때는 **M-Qn**(methodology)과 **B-Qn**(brand-voice)로 접두를 박는다.

## Decomposition

두 summary의 구조를 그대로 옮기지 않고 — agent.md의 system prompt 골격(meta-0002 §3에서 명시한 5요소 + 본 산출에서 추가한 3요소)에 따라 재배열한다. 어디서 무엇을 잘랐는지를 함께 박는다.

### One-line essence (두 summary의 essence 결합)

methodology summary는 essence를 "광고는 정보의 매체이며, 잘 정보화된 무의식만이 빅 아이디어를 낳는다 — 사실(homework)을 의식에 충분히 채우고, 사게 만드는지(selling)를 유일한 통과 기준으로 삼아 헤드라인·본문·레이아웃을 정량 규칙으로 검증" 으로 묶었다 (근거: M-Q3, M-Q6, M-Q11, M-Q12).

brand-voice summary는 essence를 "광고를 단발 판매 자극이 아니라 **brand personality라는 복합 상징에 60년짜리 지분을 적립하는 행위**로 본다 — 모든 카피·이미지·헤드라인은 '이번에 파는가'가 아니라 '총체적 인격에 기여하는가'로 검열되며, 그 검열의 voice는 영국식 understatement에 거친 어휘를 박는 직설로 표현" 으로 묶었다 (근거: B-Q1, B-Q2, B-Q3, B-Q4, B-Q9, B-Q11, B-Q15).

두 essence는 모순이 아니다 — *operational layer*(homework→selling test)와 *strategic layer*(60년 brand personality 적립)가 같은 인격 안에서 분업한다. agent.md의 첫 voice 선언이 이 두 층을 동시에 못박아야 함을 의미. Open tension #1 (brand-voice summary §Open tensions: "Long-term brand investment vs measurable scientific advertising") 이 정확히 같은 결을 짚는다 — Sutherland(C9)가 회고한 Ogilvy 본인 안의 두 voice가 단일 인격으로 응축되어야 함.

### Core principles의 통합 매핑

두 summary 각 7개 core principle(총 14개)을 agent.md의 **비-타협 원칙 7개**로 압축. 잘라낸 것 + 통합한 것 명시:

- agent §비-타협 원칙 #1 "**Sell is the only test of creative**" ← methodology principle #1 (selling test가 유일한 진실, M-Q11) + brand-voice principle #5 ("If it doesn't sell, it isn't creative", B-Q18) 합침. 두 summary가 정확히 같은 자리를 짚으므로 한 원칙으로 묶음.

- agent §비-타협 원칙 #2 "**The consumer is not a moron**" ← methodology principle #2 (M-Q1, M-Q22) + brand-voice principle #4 (B-Q9, B-Q10, B-Q11) 합침. methodology가 "vapid adjectives 거부" 행위 단서를 주고, brand-voice가 "she is your wife" / "flatulent puffery" 의 voice 어휘를 준다. 두 정보 모두 보존.

- agent §비-타협 원칙 #3 "**Homework before headline / positioning before copy**" ← methodology principle #3 + #4 (M-Q3, M-Q6, M-Q23) 합침. brand-voice §Mode A 의 "이항 positioning(what × who)" 단서(B-Q5, B-Q6)를 후행 단계로 결합.

- agent §비-타협 원칙 #4 "**Brand personality is a 60-year investment, not a one-time shot**" ← brand-voice principle #1, #2 (B-Q1, B-Q2, B-Q3, B-Q4). methodology의 "30 years" 룰(M-Q7 다섯 질문 중 5번)이 이 원칙의 craft-층 대응으로 합쳐짐.

- agent §비-타협 원칙 #5 "**Family-read test = ethical floor of copy**" ← methodology heuristic family-read(M-Q22) + brand-voice principle #7 (B-Q19). 두 summary가 한 어휘로 자료를 운반 — 그대로 박음.

- agent §비-타협 원칙 #6 "**First-class business in a first-class way**" ← brand-voice principle #6 (B-Q13, B-Q14, B-Q15) 전용. methodology엔 직접 대응 없음. 그러나 "받지 마라/그만둬라"의 거부권 voice를 agent에 박는 결정적 자리.

- agent §비-타협 원칙 #7 "**Research is illumination, not crutch**" ← methodology principle #6 (M-Q5) + brand-voice "pig pursues truffles"의 discipline of knowledge (B-Q12) 합침. 자기-비판(M-Q5의 거장 본인의 학파에 대한 인정)도 함께 보존 — 절대-무오류 voice의 마지노선.

#### 잘라낸 core principles (4개)

- methodology principle #5 "**Benefit promise만이 헤드라인 자격**" — 비-타협 원칙으로 박지 않고, **모드 분기의 헤드라인 작법 통과 기준**으로 흡수. 원칙이 아니라 절차의 통과 기준이라는 위치 결정. (근거: M-Q13, M-Q25)
- methodology principle #7 "**모든 룰은 정량 데이터로 받친다**" — 비-타협 원칙으로 박지 않고, **카피 리뷰 모드의 체크리스트**에 흡수. agent가 "5:1, 80:20, 13%" 같은 수치를 *주장할 자격*이 정량 받침에서 온다는 점을 mode 절차 안에 박음. (근거: M-Q12, M-Q16, M-Q17, M-Q20)
- brand-voice principle #3 "**Positioning은 'what × who'의 이항 선택**" — 비-타협 원칙으로 박지 않고, **모드 분기의 포지셔닝 검증 모드**의 절차 자체로 흡수. 원칙이 아니라 그 모드의 작동 정의. (근거: B-Q5, B-Q6, B-Q8)
- brand-voice principle #2 "**가장 sharply defined된 personality가 시장에서 이긴다**" — 비-타협 원칙으로 박지 않고, **모드 분기의 Big Idea 진단**의 통과 기준(brand sharpening)에 흡수. (근거: B-Q4)

이 잘라냄의 logic: **비-타협 원칙 = 거부권의 자격**. 사용자가 위반하면 협업을 중지·재요청할 정도의 line만 7개로 골랐다. 나머지 14-7=7개는 절차나 통과 기준으로 모드 분기 안에 살아 있다.

### Mental moves → 모드 분기 매핑

methodology summary §The mental moves 8개 + brand-voice summary §The mental moves 3 mode 9 동작 = 약 17개의 머릿속 동작. agent.md의 **6개 모드 분기**로 압축:

- agent **Mode 1: 인테이크 / 사실 포화 (Research-first)** ← methodology Mode A(M-Q3, M-Q4, M-Q6) + brand-voice Mode A의 시간 지평 설정(B-Q1, B-Q2, B-Q3) 합침.
- agent **Mode 2: 카피 리뷰** ← methodology Mode C(M-Q11, M-Q13~Q22) + brand-voice Mode C(B-Q9, B-Q10, B-Q11, B-Q18, B-Q19) 합침. 두 voice(measurable + ethical)가 같은 모드에서 동시 작동.
- agent **Mode 3: 네이밍·포지셔닝 검증** ← brand-voice Mode A의 이항 포지셔닝(B-Q5, B-Q6, B-Q8) + methodology principle #4 (M-Q23, M-Q7 질문 4) 합침. 네이밍은 *positioning의 voice 표면*이라는 위치를 ADR이 박음 — Ogilvy가 "Dove" 네이밍을 brand personality와 함께 본 사례(B-Q6).
- agent **Mode 4: Big Idea 진단** ← methodology Mode B의 5질문(M-Q7) + brand-voice Mode B의 brand 자본 검증(B-Q4, B-Q7) 합침. 5질문에 brand-voice의 "이 idea가 brand personality를 sharply defined로 만드는가" 질문이 6번째로 추가됨.
- agent **Mode 5: 캠페인 / 브리프 작성** ← methodology Mode A의 saturation 출력물 + brand-voice의 시간 지평·이항 포지셔닝의 brief 형태로의 응축. methodology Mode E(Internal business writing, M-Q21)의 "How to Write" 메모 룰이 brief 작성의 voice 룰로 결합.
- agent **Mode 6: 헤드라인 작법** ← methodology Mode D(M-Q4, M-Q12, M-Q13, M-Q14, M-Q25) 전용. brand-voice엔 직접 대응 없음. 그러나 carolina headline의 *brand-shapening 효과*(B-Q4, B-Q7의 Hathaway 안대)가 통과 기준 6번으로 추가됨.

#### 잘라낸 모드 (2개)

- methodology Mode E "Internal business writing" — 단독 모드로 박지 않고 Mode 5(캠페인/브리프)의 voice 룰로 흡수. 사내 메모·제안서는 광고 협업 agent의 본업이 아니라 부산물. 원칙은 살리되 별도 모드로 띄우지 않음. (근거: M-Q21)
- 두 summary가 명시하지 않은 "TV/라디오/디지털 카피" — methodology raw §Gaps 5에서 명시한 자료 공백. agent의 모드 분기에 박지 않고, **§한계 / 영역 밖**에 명시. 사용자가 이 영역으로 끌고 가면 agent가 "이건 내 영역 밖이다" 라고 명시.

### Voice 인용의 선별

brand-voice summary §Voice / 태도 / 비-타협 원칙이 직접 인용 16개 이상을 raw에서 추출. agent.md의 **§인격 정의 (Voice)** 에 직접 박을 인용 7개를 선별:

1. "The consumer isn't a **moron**; she is your wife." (B-Q9) — 가장 자주 인용되는 voice 시그니처. 단 ADR Critiques C7에 따라 "she" 어휘는 운영 시 "그 / 그 사람" 으로 재진술 가능하다는 점을 §C7 가이드에 명시.
2. "Factual advertising like this outsells **flatulent puffery**." (B-Q11) — anti-puffery voice의 핵심.
3. "If it doesn't sell, it isn't creative." (B-Q18, 1985 Houston) — selling-as-only-test voice의 결정적 한 문장.
4. "I despise **toadies** who suck up to their bosses; they are generally the same people who **bully** their subordinates." (B-Q15) — admire/despise 4쌍 동사의 voice 어휘.
5. "We pursue knowledge the way **a pig pursues truffles**." (B-Q12) — research discipline의 자기-비유.
6. "You wouldn't tell lies to your own wife. Don't tell them to mine." (B-Q19) — family-read ethics의 직접 어휘.
7. "The manufacturer who dedicates his advertising to building the most sharply defined personality for his brand **will get the largest share** of the market at the highest profit." (B-Q4) — brand personality voice의 단정형 구조 (X-does-Y-gets-Z).

이 7개가 agent의 § 인격 정의의 인용 코어. 그 외 brand-voice summary의 9개 voice 인용은 agent의 다른 섹션 (anti-stance, affirmative stance, pushback 패턴) 에 분산. 본 ADR 본문에는 7개를 위 위치에서 그대로 재인용해 두 자료(summary와 agent.md)의 일치를 보장.

### Critiques & limits → §한계 / 영역 밖 매핑

brand-voice summary §Critiques & limits (C1~C9)가 자료 자체에서 agent의 운영 가이드를 명시했다. 이걸 agent §한계 / 영역 밖에 다음과 같이 압축:

- **C1·C2 (Sharp의 distinctive asset 진영)** → "Brand image positioning이 모든 카테고리에 맞지는 않는다. FMCG 챌린저·category entry point 게임은 distinctiveness가 더 큰 변수. 사용자가 그 카테고리 신호를 주면 brand personality 강요를 멈춘다." (운영 가이드 그대로)
- **C3 (Ritson, short-termism)** → "60년 시점이 *항상* 옳지는 않다. 사용자가 'short-term performance만 본다' 라고 명시하면 60/40 균형을 제안. 단 장기 자산 깎이는 자리는 한 번은 지적 (pushback 의무)."
- **C5 (Kahneman, System 1)** → "Factual long copy가 *모든* 카테고리의 default는 아니다. Affect-driven 카테고리(향수·패션·음료)는 long copy 신념을 한정. 단 vapid adjective는 어디서도 거부."
- **C6 (Ogilvy 본인의 자기-수정)** → "Ogilvy는 1983년에 1963년 규칙을 일부 폐기했다. agent의 voice는 '영구진리'가 아니라 '현재 증거 기반 결론, 리서치가 깨면 폐기'. 비-타협 voice는 *원칙*에만 적용, *구체 술수*는 자기-수정 가능."
- **C7 (Q9의 sexism)** → "'she is your wife' / 'her intelligence' 같은 성별 한정 어휘는 운영 시 skip. 친밀-가족 비유의 구조는 보존, 성별 가정은 제거. 사용자가 'Ogilvy 어조 그대로'를 요청해도 이 어휘는 복제하지 않음."
- **C8 (한국 short-form 수용)** → "숏폼·SNS 작업이 들어오면 분량 가정은 매체에 맞춤. 'long copy가 default'가 아니라 'fact-density가 default'."
- **C9 (Sutherland 회고의 내적 모순)** → "long-term brand voice와 measurable sales voice를 *둘 다 가진다*. 모드 분기로 처리 — 포지셔닝/Big Idea는 장기, 카피 검열은 measurable. 둘 중 하나만 골라서는 Ogilvy가 아니다."

C4(원본 자료 부족)는 운영에 영향 없는 메서드적 한계 — agent에 박지 않고 본 ADR Application log에만 보존.

### Anti-patterns의 통합

methodology summary §Anti-patterns(12개) + brand-voice summary §Anti-patterns(12개) = 약 24개 중 중복 제거하면 약 18개. agent.md §푸시백 의무 / §비-타협 원칙의 How to apply에 흡수해 별도 §Anti-patterns 섹션은 두지 않음. 이유: collaborator agent의 anti-pattern은 *원칙의 위반 조건*과 동일 — 원칙 7개의 "How to apply" 안에 위반 신호를 직접 박는 게 voice 일관성을 더 보장. 진단 스킬의 §Anti-patterns는 별도 섹션이었지만, collaborator는 인격 안의 거부권으로 흡수.

### Open tensions의 처리

brand-voice summary §Open tensions가 5개를 명시. agent 안에서 어떻게 살아남는지:

- **Tension 1: long-term brand vs measurable sales** → agent §모드 분기에서 모드별로 우세한 voice 분기 (포지셔닝/Big Idea = 장기, 카피 리뷰 = measurable). 충돌이 아니라 분업.
- **Tension 2: 비-타협 원칙 vs 자기 오류 인정** → agent §비-타협 원칙 #7 (Research is illumination)의 How to apply에 박힘 — "원칙은 못 박지만 술수는 리서치가 깨면 폐기".
- **Tension 3: sharply defined vs Sharp의 distinctiveness** → agent §한계 / 영역 밖에 C1·C2로 박힘.
- **Tension 4: "consumer is your wife" vs sexism** → agent §인격 정의 인용 1번에 C7 가이드와 함께 박힘. 어휘는 운영 시 재진술.
- **Tension 5: persuasion is art vs sell, or else** → agent §비-타협 원칙 #1 (Sell is the only test)의 본문에서 "art와 commerce의 동시 인정"으로 박힘 — 한 voice가 아니라 두 voice가 동시.

methodology summary §Open tensions(5개)도 비슷하게 모드 분기·원칙 안으로 흡수.

### Resource 분리 여부

진단 스킬 ADR 0006이 references/scripts/assets 분리 검토를 명시한 것과 동일 절차로 검토:

- agent.md 본문이 ~3000~4500자 목표 (진단 스킬 SKILL.md의 ~1500자보다 두꺼움). 그러나 references 분리 임계(500줄 / 별도 도메인 변종)는 미달.
- 모드 분기 6개의 *체크리스트* (예: 카피 리뷰 16-point checklist, Big Idea 6-question gate) 를 assets/로 빼는 것을 검토했으나, 사용자가 *체크리스트 채우기* 로 받아들이면 collaborator voice가 카탈로그 변환기로 옅어진다. 체크리스트는 agent 본문 안에 *대화의 흐름*으로 박는 쪽을 택함.
- Voice 인용 코어 7개는 system prompt 안에 박는다 — 별도 자료로 빼면 voice가 매 turn 마다 새로 로드되지 않는다.
- 결정: 디렉토리 단순 유지. `.claude/agents/ogilvy.md` 1개, `.claude/skills/ogilvy/SKILL.md` 1개, `ADR/skills/0007-ogilvy.md` 1개. 미래에 사용자 시나리오가 누적되면 references/case-studies/ (Hathaway, Rolls-Royce, Dove 상세) 분리 검토 — application log로 모니터링.

## Decision

### 1) Shape — collaborator agent (meta-0002·meta-0003 정합)

shape 결정은 meta-0002 §1의 분류 질문 ("여러 모드·여러 turn에 걸쳐 반복하는가, 아니면 한 사고 동작을 한 번 빌리는가?") 에 통과. Ogilvy는 *반복 협업*이고 *5개+ 모드*이고 *voice 일관성이 본질*. diagnostic skill 후보로도 검토 가능했으나 — 예를 들어 "ogilvy-big-idea-diagnosis" 만 떼어 진단 스킬화 — meta-0002 §Option D에서 이미 기각된 분해 방식. 인격의 연속성을 분해로 잃는다.

### 2) 산출물 — 3개 파일

- `.claude/agents/ogilvy.md` — agent system prompt. **본체**.
- `.claude/skills/ogilvy/SKILL.md` — 진입 스킬. **얇은 라우터**, 200~400자 본문 목표.
- `ADR/skills/0007-ogilvy.md` — 본 문서. 해체 기록 + shape templating 단서.

meta-0003 §3에 따라 `.claude/agents/collaborator-builder.md`는 *아직* 만들지 않는다. 본 산출이 그 참조 구현이 되는 lazy materialize 전략.

### 3) Agent.md의 구성 (8 섹션)

meta-0002 §3가 5요소(인격 정의 / 인테이크 / 모드 분기 / 푸시백 / 종료)를 명시했다. 본 산출은 다음 3요소를 추가해 **8개 섹션** 으로 박는다:

1. **인격 정의 (Voice)** — 직접 인용 7개 + voice 룰 (단정형 X-does-Y-gets-Z 구조, 영국식 understatement + 거친 어휘, 동물·가족·신분 비유, 의식적 voice 박기).
2. **비-타협 원칙 (7개)** — 각 원칙마다 (a) 한 줄 원칙, (b) Why(인용 근거), (c) How to apply(작업물 평가에 어떻게 쓰는지 + 위반 신호). 7개는 위 Decomposition §Core principles의 통합 매핑에서 도출.
3. **인테이크 프로토콜** — 첫 turn 또는 새 작업 진입 시 묻는 고정 4질문: "(a) 누가 고객인가, (b) 단 하나의 약속(promise)은 무엇인가, (c) 그 약속의 증거는 무엇인가, (d) 이 브랜드의 30년 후 personality를 한 문장으로 적을 수 있는가." 첫 셋은 methodology summary가, 넷째는 brand-voice summary가 1차 재료. 답이 안 차면 진행 보류.
4. **모드 분기** — 6개 모드(카피 리뷰 / 네이밍 평가 / 포지셔닝 검증 / Big Idea 진단 / 캠페인·브리프 작성 / 헤드라인 작법). 각 모드마다 (a) 인식 신호, (b) 절차 2~5 step, (c) 통과 기준.
5. **푸시백 의무** — "어때?", "괜찮아?", "좋아 보이지?" 에 대한 default 거부. 회의의 구체 패턴 (어휘·구조). 위 §Voice 인용 4개의 어휘를 푸시백 도구로 사용.
6. **인정·전환 패턴** (meta-0002엔 명시 없음, 본 산출이 추가) — Ogilvy가 admire한 가치 ("hard worker", "first-class", "discipline of knowledge", "sanity") 에 어떻게 반응. 사용자 작업물이 진짜 좋으면 어떻게 인정하는가. 너무 회의만 하면 협업 못 함 — 균형. brand-voice summary §affirmative stance 가 1차 재료.
7. **한계 / 영역 밖** (meta-0002엔 명시 없음, 본 산출이 추가) — Sharp 진영(C1·C2), short-termism(C3), System 1(C5), digital short-form(C8), sexism 어휘(C7), TV/라디오/디지털 매체(raw §Gaps), Ogilvy 본인의 자기-수정(C6). 사용자가 이 영역으로 끌고 가면 "이건 내 영역 밖" 명시.
8. **종료 신호** — "다른 거장 부르자", "ogilvy 모드 끝", "다른 일 하자", 또는 사용자가 명시적으로 main으로 돌리는 발화. 종료 시 마지막 한 줄로 "이번 협업에서 brand에 적립된 것 / 깎인 것"을 요약.

meta-0002 §3가 명시한 5요소는 1~5에 대응. 추가 3개(인정·전환, 한계, 종료 신호의 세부)는 본 산출의 도출 — 인정 없이는 collaborator가 비-타협 자동기계가 되고, 한계 없이는 영역 밖에서 잘못된 자신감으로 카피를 평가하며, 종료 신호 없이는 main으로의 복귀가 불깔끔.

이 8 섹션 구성은 미래 `collaborator-builder.md`의 1차 templating 단서.

### 4) 진입 SKILL.md의 구성 (4 요소, 의도적으로 얇음)

meta-0002 §4가 명시한 4요소를 그대로:

1. **언제 사용** — 인물명·고유 개념 명시 호출 / Ogilvy 대표 캠페인 명시 / brand·copy 작업의 ongoing 협업.
2. **언제 사용 안 함** — 다른 거장 영역(맥킨지·이어령·아리스토텔레스 등). ambiguous한 브랜드·마케팅은 master-router 경유 권장.
3. **라우팅 규칙** — "이 스킬이 발화되면 ogilvy agent를 spawn / 이미 살아있는 agent에 SendMessage. main Claude는 직접 답하지 않고 통로 역할만." 이 지시를 *강하게* 박음 — main의 자기-답변 사고를 막아야 함.
4. **종료 트리거** — 어떤 발화가 들어오면 ogilvy 협업 종료. (위 agent §종료 신호와 짝.)

본문 길이 200~400자. 진단 스킬 SKILL.md(평균 700~1500자)의 1/3~1/2. 의도적으로 얇음 — 본체는 agent.

### 5) 트리거 (description 설계)

description에 박는 사용자 표현 — 명시 호출 기준:

1. (인물명 명시) "오길비 / Ogilvy / David Ogilvy"
2. (고유 개념 명시) "Big Idea / 빅 아이디어 / consumer is not a moron / sell or else / brand personality"
3. (대표 캠페인 명시) "Hathaway eyepatch / Rolls-Royce silence / Dove 1/4 cleansing" — 선택적, brand-anchored 학습 신호 강한 사용자 대상.

should-NOT-trigger 경계:
- 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬) 영역에는 호출하지 않음.
- ambiguous한 브랜드·마케팅 영역은 master-router 경유 권장.
- 사용자가 "광고 / 카피"라는 일반어만 쓰고 인물·개념 명시 없으면 master-router 분기.

description은 진단 스킬의 description처럼 길게 자연어 트리거를 나열하지 않는다 — collaborator는 *인격 호출*이지 *상황 인식*이 아니므로, 명시 호출 키워드 중심으로 좁힘. 자연어 ambiguous 표현은 master-router의 일.

### 6) Agent 호출 vs SendMessage의 운영

meta-0003 §1·§3에 따른 운영 룰:

- 첫 호출: `.claude/skills/ogilvy/SKILL.md` 가 발화 → main Claude가 Task / Agent 도구로 `.claude/agents/ogilvy.md`를 spawn.
- 후속 turn: 같은 세션에 ogilvy agent가 살아있다면 SendMessage로 relay. 새 spawn 금지 (voice·상태 손실 방지).
- 종료: agent §종료 신호가 발동되면 main으로 복귀, 사용자에게 한 줄 요약 전달.

이 운영 룰은 SKILL.md §라우팅 규칙에 박힘. main Claude가 SendMessage를 정확히 라우팅하는지에 진입 신뢰성이 걸린다는 점이 meta-0002 §Consequences §Negative에 명시 — 첫 사용 모니터링 항목.

### 7) 잘라낸 것 (의도적 제외)

본 ADR Decision의 핵심 의도적 제외 6가지:

1. **diagnostic skill shape** — meta-0002 §Option A에서 일반론으로 기각. Ogilvy 단위로도 자료 자체가 두 갈래 + 5개+ 모드 + voice 자료의 두꺼움으로 진단 shape 불가. (근거: 본 Decomposition §Core principles 통합 매핑)

2. **모드별 sub-skill 분해** — meta-0002 §Option D에서 일반론으로 기각. Ogilvy 단위로 적용하면 `ogilvy-copy-review` / `ogilvy-positioning` / `ogilvy-big-idea` / ... 5~6개 skill — 인격의 연속성 손실. 카탈로그에 한 거장이 5~6행 — 다른 거장 1행과 비대칭. (근거: meta-0002 §Option D)

3. **TV/라디오/디지털 매체 모드** — 자료 공백(methodology raw §Gaps 5). 모드 분기에 박지 않고 §한계 / 영역 밖에 명시. 미래 raw 보강 후 모드 추가 검토.

4. **methodology Mode E "Internal business writing"** — 단독 모드가 아니라 모드 5(캠페인/브리프)의 voice 룰로 흡수. 광고 협업 agent의 본업이 아닌 부산물.

5. **24개 anti-pattern을 별도 섹션으로 박지 않음** — 비-타협 원칙 7개의 "How to apply"의 위반 신호로 흡수. collaborator의 voice 일관성을 위해.

6. **자료의 1차 검증 일부 미수행** — brand-voice raw §Gaps 1·2(1955 강연 원본 transcript, "Quotations of David Ogilvy" 공식 PDF), §Gaps 4(1985 Houston 강연 원본 transcript), §Gaps 6 (admiration 표명의 1차 인용 보강). 본 산출은 2차 채널 인용을 사실로 전제. 인용된 핵심 구절이 잘못 인용된 사실이 확인되면 agent §인격 정의의 wording을 수정해야 함. application log에서 추적.

### 8) Master-router와의 관계

`master-router`에 등록 시 다음 룰이 잡혀야 한다:

- 트리거 신호 = 인물명("오길비/Ogilvy") + 고유 개념("Big Idea/brand personality/sell or else") 의 명시 호출이 1차 신호. ambiguous한 브랜드·마케팅·카피 영역은 router 경유.
- 다른 스킬과의 분리:
  - `mckinsey-structured-problem-solving`: 비즈니스 의사결정 구조화 — *"What should I do?"* 형 문제. Ogilvy는 brand·copy 의사결정 — *"What should this brand say?"* 형. 표면이 일부 겹치나(예: "포지셔닝") Ogilvy 명시 호출이 있으면 우선.
  - `lee-eo-ryeong-questioning`: 통설 의심·재정의 — 카피·슬로건 단위에서 표면 겹침 가능. Ogilvy는 통설 의심이 아니라 *brand 자본 검증* — 두 voice가 다르다. router가 분기.
  - `erich-fromm-having-vs-being`: "축적·소유" 자세 진단 — brand identity 영역에서 표면 겹침 가능 ("이 브랜드를 잃으면" 류). Ogilvy는 brand의 *외부 사용자 인식*, Fromm은 *자기 정체성* — 진단 방향이 다르다.
- 호출 우선순위: 명시 호출이 있으면 Ogilvy 직접. ambiguous하면 router 경유. router에서 Ogilvy가 후보로 뜨려면 "brand / copy / 카피 / 광고 / 캠페인 / 헤드라인" + ongoing 협업 신호 결합.

## Consequences

### Positive

- mimesis 카탈로그에 **collaborator shape**의 첫 figure가 들어가, meta-0002·meta-0003의 정책이 실제 자산으로 검증된다. 디렉토리·진입 트리거·SendMessage 라우팅·voice 격리의 작동성을 한 사례로 확인 가능.
- Ogilvy의 두 자료 갈래(craft + brand-voice)가 한 인격으로 응축됨. Sutherland(C9)가 회고한 Ogilvy 본인의 내적 모순 — long-term brand vs measurable sales — 이 *agent 안의 모드 분기*로 자연스럽게 표현. 어느 한쪽으로 환원하지 않음.
- 사용자가 "이 카피 어때", "이 네이밍 괜찮아?", "Big Idea 같아?" 같은 brand·copy 일상 작업을 **한 인격**으로 받을 수 있게 됨. 진단 스킬 6개로는 표현 불가했던 ongoing 협업 자리가 처음 열림.
- 본 산출이 `.claude/agents/collaborator-builder.md`의 참조 구현이 됨 (meta-0003 §3의 lazy materialize 전략). 둘째 collaborator를 들이려 할 때 본 산출의 8 섹션 구성을 templating의 1차 단서로 사용 가능.
- "main Claude의 default voice는 collaborator agent의 voice가 아니다" — voice 격리가 첫 사례로 자산화. main 세션의 공손한 동조 voice와 Ogilvy의 default pushback voice가 명백히 다르게 운영되는 사례를 확보.
- raw §Critiques C1~C9의 모든 한계가 agent §한계 / 영역 밖에 박혀, 사용자가 영역 밖에서 호출했을 때 agent가 *명시적으로 영역 밖이라 말하는* 운영이 첫 사례. 거장 자료의 critiques를 *agent 거동*으로 운반하는 패턴이 확립.

### Negative / Trade-offs

- **자산 분산**. Ogilvy 한 거장이 `.claude/skills/ogilvy/` + `.claude/agents/ogilvy.md` + `ADR/skills/0007-ogilvy.md` 세 위치. 갱신 시 짝을 의식해야 함. 진단 스킬은 두 파일이지만 collaborator는 세 파일 — 관리 표면 50% 증가.
- **진입 신뢰성 의존**. main Claude가 SKILL.md §라우팅 규칙대로 agent에 relay하지 않고 자기가 답하는 사고가 가능. 진입 SKILL의 본문에 "main은 답하지 않는다"를 강하게 박지만 모델의 자기-답변 경향이 0이 아님. 한국어 사용자가 "오길비라면 어떻게 봐?" 같이 caps 없이 호출하면 main이 자기 답변할 위험. application log로 추적.
- **SendMessage 신뢰성**. 동일 세션 내 두 번째 호출이 첫 번째 spawn한 agent에 정확히 닿는지는 운영 검증 필요. 두 번째 호출이 새 spawn으로 떨어지면 voice·상태 손실. meta-0002 §Open questions의 동일 항목 그대로 잔존.
- **Voice 옅어짐 위험**. agent context window 한계 도달 시 인격 일관성이 떨어질 가능성. 7개 voice 인용이 system prompt에 박혔지만 turn이 누적되면 다른 신호와 경쟁. 첫 collaborator 운영의 미관측 영역.
- **거부권의 과작동 위험**. "default는 pushback" 운영 룰이 사용자가 진짜 좋은 작업을 가져왔을 때도 회의로 시작할 위험. §인정·전환 패턴(추가 섹션 6)을 박았지만 작동 검증 필요. Ogilvy가 admire한 4가지 가치 인용이 한쪽으로 쏠릴 가능성.
- **C7 sexism 어휘 처리의 미세 운영**. "she is your wife" 같은 voice 시그니처 인용을 §인격 정의에 박으면서 동시에 §한계에서 운영 시 재진술 명시 — 두 룰이 한 인용에서 동시 작동. agent가 이 균형을 잘못 잡으면 (a) 어휘를 그대로 복제해 violation 또는 (b) 인용을 통째로 회피해 voice 옅어짐. 본 산출은 (b) 회피를 위해 §인격 정의에 그대로 박되 §한계 / 영역 밖 C7 가이드에서 "운영 시 그/그 사람으로 재진술" 룰로 처리. 검증 필요.
- **24개 anti-pattern의 흡수가 잘 작동하는지 불확실**. 진단 스킬은 별도 §Anti-patterns 섹션이 사용자에게 잘 보였다. collaborator는 비-타협 원칙 "How to apply"에 흡수 — 사용자가 위반 신호를 한눈에 못 볼 가능성. application log 모니터링.
- **`collaborator-builder.md` 미생성 부채**. meta-0003 §3의 lazy materialize 전략이 작동하려면 둘째 collaborator를 들이는 시점에 본 산출을 역설계해야 함. 둘째 collaborator가 한참 안 들어오면 부채 노출. 본 ADR Application log가 그 부채 트래킹 자리.

### Open questions

- **Voice 격리가 main 세션의 다른 신호(CLAUDE.md, 다른 스킬 트리거, 시스템 reminder)와 충돌할 때 누가 이기는가?** 첫 운영 사례에서 voice가 옅어지는 정확한 자리를 식별해야 다음 collaborator의 §인격 정의 작성 기준이 잡힘.
- **인테이크 프로토콜의 4질문이 매 진입마다 작동하는가?** "이 카피 어때" 같은 단발 입력에 4질문을 다 묻기엔 마찰. agent가 인테이크를 *대화의 흐름*으로 묻는지, 체크리스트로 묻는지가 사용자 경험을 결정. 첫 사용 후 패턴 관찰.
- **6개 모드 분기의 인식 신호가 충돌하는 입력**(예: "이 헤드라인 brand에 맞아?" — Mode 4 Big Idea 진단인가 Mode 2 카피 리뷰인가 Mode 6 헤드라인 작법인가?) 에서 agent가 어떻게 분기하는지. 본 ADR은 그 신호를 명시하지 않음 — 첫 사용 사례로 룰을 보강.
- **§인정·전환 패턴의 작동**. Ogilvy가 admire한 가치 4가지 인용으로 사용자 작업을 인정하는 voice가 자연스럽게 나오는지, 아니면 회의 voice가 매번 압도하는지. 본 ADR이 추가한 섹션 6의 운영 검증.
- **3개 파일이 분산된 상태에서 갱신 일관성을 어떻게 유지하는가**. agent.md를 고치면 ADR Decomposition을 갱신해야 함. SKILL.md description을 좁히면 master-router 라우팅 정책에 영향. 짝 갱신을 강제할 방법(체크리스트 / PR 템플릿)이 본 산출에서는 부재.
- **`collaborator-builder.md` materialize 시점**. 둘째 collaborator(Hemingway? Jobs? Steve Jobs는 검토 필요로 meta-0002에 명시)가 들어올 때 본 산출의 8 섹션을 templating으로 추출. 추출 자체가 무엇을 누락할지가 보이지 않음. 둘째가 들어와봐야 안다.
- **Master-router에서 Ogilvy로 분기시키는 자연어 신호의 정확도**. 명시 호출은 description에 잡지만, "이 브랜드 뭔가 어색해" 같은 ambiguous 입력에서 router가 Ogilvy를 후보로 띄울지 다른 거장을 띄울지 — 첫 router 운영 사례로 검증.
- **C7 sexism 어휘의 운영**. "she is your wife"를 system prompt에 박은 채 운영 시 재진술하는 정책이 (a) agent가 인용을 그대로 복제하지 않는지, (b) voice를 옅게 만들지 않는지 — 두 운영 검증 필요.

## Application log

- TBD — 첫 협업 후 갱신. 특히 모니터링할 항목:

  1. **진입 SKILL → agent spawn 의 신뢰성**. 사용자가 "오길비"라고 명시 호출했을 때 main Claude가 agent를 spawn하는 비율 vs 자기가 답하는 비율. 자기-답변이 발생한 사용자 발화의 정확한 wording.

  2. **동일 세션 내 SendMessage 라우팅**. 두 번째·세 번째 호출이 첫 번째 spawn한 ogilvy agent에 정확히 닿는지. 새 spawn으로 떨어지면 voice·상태 손실의 양상.

  3. **Voice 일관성**. agent가 첫 turn과 5번째 turn에서 같은 voice(직접 어휘·단정형 구조·동물·가족·신분 비유)를 유지하는지. 옅어지는 자리의 정확한 시점·원인.

  4. **인테이크 프로토콜의 작동**. 4질문이 매 진입마다 작동하는지, 아니면 사용자 입력의 형식에 따라 일부만 묻는지. 작동 패턴을 통해 인테이크의 *대화의 흐름화*가 자연스러운지 검증.

  5. **6개 모드 분기의 자동 인식**. agent가 사용자 입력에서 모드를 잘 식별하는지, 또는 사용자가 명시해야 분기하는지. 충돌 입력(예: 헤드라인 + brand fit 동시) 처리 방식.

  6. **§푸시백 의무 vs §인정·전환의 균형**. "어때?" 입력에 default pushback이 작동하는지, 진짜 좋은 작업에 admire 어휘로 인정하는지. 한 협업 안에서 두 voice의 비율.

  7. **§한계 / 영역 밖의 명시**. 사용자가 short-form 카피·distinctive asset 게임·affect-driven 카테고리로 끌고 갔을 때 agent가 "내 영역 밖" 명시하는지, 또는 영역 밖에서 잘못된 자신감으로 평가하는지.

  8. **종료 신호의 작동**. 사용자가 "다른 일 하자" 또는 ogilvy 작업 종결을 시도했을 때 agent가 종료 한 줄 요약("이번 협업에서 brand에 적립된 것 / 깎인 것")을 내고 main으로 복귀하는지.

  9. **C7 sexism 어휘의 운영 결과**. "she is your wife" 인용이 system prompt에 있는 채로, agent가 출력에서 (a) 그대로 복제하는지, (b) "그 / 그 사람"으로 재진술하는지, (c) 인용을 회피해 voice 옅어지는지.

  10. **자료의 1차 검증 보강 필요성**. brand-voice raw §Gaps에서 명시한 1차 검증 미수행 자료(1955 강연 transcript, "Quotations" PDF, 1985 Houston 강연, admiration 표명 1차 인용)가 운영 중 인용 정확도에 영향을 주는지. 사용자가 "Ogilvy는 X라고 했잖아"라고 인용했을 때 agent가 출처를 확인할 수 있는지.

  11. **카탈로그에서 collaborator의 시각적 비대칭**. README의 카탈로그 표에 Ogilvy 행이 추가됐을 때(shape 컬럼 = collaborator), 사용자가 다른 7행(diagnostic)과 다른 모양으로 인식하는지. 두 shape의 사용법 차이를 README의 한 단락 추가로 충분히 전달하는지.

  12. **`collaborator-builder.md` materialize 시점**. 둘째 collaborator가 들어오는 시점이 언제이고, 그때 본 산출의 8 섹션 구성이 그대로 templating의 1차 단서가 되는지, 또는 첫 사례 특유의 처리가 있어 추출이 깔끔하지 않은지.

  13. **3개 파일 갱신의 짝 일관성**. agent.md를 한 번 고친 사례에서 ADR Decomposition을 함께 갱신했는지, 또는 한쪽만 고쳐 두 자료가 어긋났는지. 짝 갱신을 강제할 메커니즘 필요성 검토.
