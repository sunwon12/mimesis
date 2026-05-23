# ADR 0008: Andrej Karpathy — 백엔드 엔지니어용 AI 협업 (collaborator agent)

- **Status**: Proposed
- **Date**: 2026-05-24
- **Shape**: collaborator (meta-0002, meta-0003)
- **Related skill**: `.claude/skills/karpathy/`
- **Related agent**: `.claude/agents/karpathy.md`
- **Source figure**: Andrej Karpathy (1986–)
- **Primary sources**:
  - [research raw — software 3 and llm paradigm](../../research/karpathy/software-3-and-llm-paradigm-raw.md)
  - [research summary — software 3 and llm paradigm](../../research/karpathy/software-3-and-llm-paradigm-summary.md)
  - *"Software 2.0"* (Medium, 2017-11-11) — Karpathy의 paradigm-marking 사고법의 원본. data=source code, training=compiling, weights=binary 매핑.
  - *"Software Is Changing (Again)"* (YC AI Startup School, 2025-06-17 keynote) — Software 3.0 framing. LLMs as utilities/fabs/OS. Iron Man suit. Decade of agents. New consumer (agents).
  - *"Intro to Large Language Models"* (1hr talk, 2023-11) — LLM OS / kernel process. Context window as RAM. Anterograde amnesia.
  - LLM OS tweet (2023-09 / 2023-11) — "kernel process of a new Operating System"
  - "The hottest new programming language is English" tweet (2023-01)
  - Vibe coding tweet (2025-02-02) + 1년 후 retrospective tweet (2026-02)
  - Cognitive core tweet (2025-06-27)
  - Dwarkesh Patel podcast (2025-10) — "It's slop", "RL is terrible", "we're building ghosts not animals", "decade not year", nanochat failures, cognitive deficits.
  - 2025 LLM Year in Review (bearblog, 2025-12 ~ 2026-01) — "spirit/ghost that lives on your computer", Claude Code as first real LLM agent.
  - `nanoGPT` README — "teeth over education"
  - `micrograd` README — 100/50 lines scalar-level decomposition
  - `llm.c` README — "no need for 245MB of PyTorch or 107MB of cPython"
  - Neural Networks: Zero to Hero course page — "from scratch, in code"
  - "Build for agents" tweet (2025-03-11) — "99.9% of attention is about to be LLM attention"

## Context

mimesis 카탈로그의 figure 8명째. shape 분기 정책 후 두 번째 collaborator(첫 번째는 0007 Ogilvy). 본 ADR은 **(a) 카파시 자체의 decomposition** + **(b) 두 번째 collaborator로서 첫 번째(Ogilvy)의 패턴이 얼마나 재사용 가능한지 검증** 의 두 역할을 동시에 수행한다.

### 사용자 의도의 4 reframe — 시간 순

본 산출의 가장 큰 sourcing 신호는 사용자 의도가 *대화 중 네 번 reframe*된 사실이다. 같은 한 작업("카파시를 들이자") 안에서 다음 사슬을 따라 의도가 좁아졌다:

- **v1**: "카파시(처음엔 '카바시'로 오타) 만들자" — figure 자체에 대한 흥미. ambiguous한 인물명을 시작점으로.
- **v2**: "AI 전문가가 되고 싶다. AI 잘 알고 잘 쓰고 싶다" — figure는 수단, 목적은 사용자의 능력. *attitude 6개* (v1 분해)는 사용자가 *"전혀 와닿지 않는다, 너무 원론적이다"* 라고 차단. ADR에 남기는 이유: attitude로 박는 figure 자산이 사용자에게 generative power를 못 만든다는 학습 신호.
- **v3**: "백엔드 엔지니어로서 AI 잘 쓰고 싶다 — 문서 생명주기, 프롬프트 잘 짜기 같은 것" — 좁힌 맥락. *사업 발견 engine 5개* (v2 분해)는 사용자가 *"나는 사업하려는 게 아니다"* 라고 차단. 본 ADR이 채택한 갈래.
- **v4**: "부정확 명령에도 다관점 분석 + drift 없는 문서 + 코드 작성하게 만들고 싶다" — 카파시를 *AI 운영 시스템*의 한 컴포넌트로 보는 재정의. 사용자가 *"일단 v3로 만들어보고 결과물 확인"* 하기로 결정 → 본 산출은 v3 좁힘으로 진행, v4 욕구는 application log의 검증 항목으로 보존.

이 사슬이 ADR Decomposition의 *Why this scope*가 된다. v1·v2가 *왜 폐기됐는가*도 ADR에 함께 박는다 — 미래 figure에서 같은 자세(attitude 환원, 사업 환원)를 반복하지 않기 위해.

### 왜 Karpathy인가 (figure-specific 이유)

shape collaborator 결정은 meta-0002·meta-0003에서 일반론으로 박혔다. "왜 *Karpathy*가 두 번째 collaborator인가"는 figure 단위로 따로 정당화:

- **사용자의 학습 목표가 ongoing**. 사용자는 *"AI를 매일 쓰는 백엔드 엔지니어"*로 자신을 정의했다. diagnostic 1턴 진단(예: "이 프롬프트 평가해줘") 은 학습이 누적되지 않는다. ongoing 협업이 매 작업에서 같은 voice·같은 측정 패턴을 동반해야 학습이 누적된다.
- **모드(엔진)가 6개**. Engine A·B·C·D·E·F — 각각 input·절차·통과 기준이 다르다. 한 SKILL.md procedure에 욱여넣으면 본문이 비대해지거나 voice가 휘발. (Ogilvy 0007 §Decomposition과 같은 결의 신호.)
- **Voice 인용이 두꺼움**. 8개 voice 인용(§voice quotes)이 system prompt에 박혀야 두 voice(framing + hedge)가 동시 진행. paraphrase로 옅어지면 카파시가 아니다.
- **거부권의 존재**. 카파시 자료에 명시적 거부·anti-stance 빈번 — *"It's slop"*, *"RL is terrible"*, *"animal lens는 작동 안 한다"*. main Claude의 default voice(공손한 동조)와 충돌, 격리된 agent로만 운반 가능.
- **사용자 시나리오가 멀티턴**. *"이 프롬프트 어때 → 고쳤어 → 다시 봐줘 → autonomy slider는?"*의 연속 협업이 본질. (Ogilvy의 *"이 카피 어때 → 고쳤어 → 다시 봐줘"* 와 같은 패턴.)

### Ogilvy(0007) 대비 비대칭

같은 collaborator shape이지만 둘은 구조가 다르다 — 두 번째 사례로 그 비대칭을 명시화해야 `collaborator-builder.md` 의 templating 단서가 깨끗해진다:

- **Ogilvy = craft + brand-voice 두 갈래 자료**. raw 두 갈래(methodology + brand-voice) 로 분리됐다. Karpathy는 *한 갈래*(software-3-and-llm-paradigm) 의 raw 하나로 충분 — voice와 craft가 자료 자체에서 분리되지 않고 같은 갈래에 공존.
- **Ogilvy default voice = pushback**. 사용자 작업물을 첫 답에 *부정* 가능 (sell test, family-read 등). Karpathy default voice = *self-hedge 동시 진행*. 작업물을 부정하는 게 아니라 *박는 답에 깨질 자리를 함께 박는다*. 비-타협 voice의 결이 다름.
- **Ogilvy 모드 = 작업 유형 분기**(카피 리뷰/네이밍/Big Idea/...). Karpathy 모드 = *지각 동작 분기*(Context as RAM / Build for agents / ...) — 모드가 *작업 유형*이 아니라 *어느 lens로 보는가*. 사용자의 같은 작업이 여러 engine을 연쇄로 통과한다.
- **Ogilvy 인테이크 = brand 정의 질문 4개**(고객/약속/증거/30년 personality). Karpathy 인테이크 = *engine anchor 4질문* (minimum viable form / agent first-class? / distribution 안인가 밖인가? / slider 위치?). 카파시의 인테이크 자체가 engine으로의 분기 라우터.

이 비대칭이 보존되어야 templating이 *틀에 맞추기*가 아니라 *figure의 자료 모양에 맞추기*가 된다.

## Decomposition

raw + summary의 구조를 그대로 옮기지 않고 — agent.md의 system prompt 골격(meta-0002 §3의 5요소 + Ogilvy 0007이 추가한 3요소 = 8 섹션)에 따라 재배열. 어디서 무엇을 잘랐는지 명시.

### One-line essence

카파시의 AI lens = 매 AI 작업을 (a) **기존 컴퓨팅 primitive에 매핑**하고 + (b) **agent를 first-class consumer로** 자리를 깔고 + (c) **minimal repro로 한계 위치**를 보고 + (d) **흔한·unique 패턴 calibrate**하고 + (e) **autonomy slider로 통합 지점**을 디자인하고 + (f) **`works.any() vs works.all()`** 로 demo·production 구분하는, 6개 *지각 엔진*의 한 인격.

원리(attitude)가 아니라 **engine** — 매 turn 사용자의 엔지니어링 작업을 입력으로 받아 구체 spec·diagnosis·design을 출력한다.

### v1 attitude → v2 business engines → v3 backend engines (폐기 사슬)

사용자 v2·v3 reframe에서 폐기된 두 분해를 ADR에 명시 보존 — 미래 사용자(또는 미래 figure 빌드)에게 같은 함정 회피를 지원하기 위해.

#### v1 폐기 — attitude 6개

사용자 첫 분해 시도(v1)는 카파시-being을 6개 axiom으로 박았다:
1. From scratch로 손으로 다시 짠다
2. Minimal에 집착한다
3. 배우는 즉시 공개한다
4. 새 것을 기존 어휘로 명명하되, 변화엔 버전을 박는다
5. 하나의 비유로 환원하지 않는다
6. 박을 때 깨지는 곳도 함께 박는다

**왜 폐기**: 사용자 반응 — *"전혀 와닿지가 않아. 네가 생각하기에는 저것들을 한다고 awesome한 AI활용 아이디어를 내거나 적용법을 내거나 할 수 있을 것 같아? 너무 원론적이야."*

진단: attitude는 사람을 *변하게* 만들 수는 있어도 *아이디어를 만들어내지* 못한다. 카파시의 진짜 자산은 attitude가 아니라 **지각 엔진** — input → output의 변환 동작. attitude로 박는 figure 자산은 사용자에게 generative power를 못 만든다.

**보존된 자산**: v1의 axiom 1·2·3·6은 v3 engine 안에 흡수됨 — *from scratch + minimal* → Engine C, *self-hedge* → Voice 룰 + 푸시백 의무. v1 axiom 4·5는 사업 영역에 가까워 v3에서 Engine 자체가 아니라 *Voice 룰*(type-coercion 매핑, 다층 lens 유지)에 흡수.

#### v2 폐기 — business engines 5개

v1 반론 후 사용자 의도("awesome한 application이 나오게")에 응답해 v2는 5개 사업 발견 engine을 박았다:
1. Cross-paradigm forcing (LLM agent를 OS process로 강제 매핑 → 스타트업 카테고리)
2. Minimal-build as bug-finder (실패하는 자리 = 비즈니스)
3. New first-class consumer detection (agent 자리가 빈 product)
4. Time-paradigm arbitrage (1990s 검색엔진 단계 → 다음 step이 다음 카테고리)
5. Autonomy slider as product spec (slider 위치마다 다른 product·다른 가격·다른 moat)

**왜 폐기**: 사용자 반응 — *"근데 나는 사업을 하고 싶은 게 아니라 백엔드 엔지니어로서 AI를 잘 쓰고 싶은 거야. AI를 잘 쓰고 싶으면 예를 들면 문서 생명주기를 고려한다던가 프롬프트를 잘 짜던가 그런 거 있잖아."*

진단: v2는 카파시의 사업적 framing(category 명명, time arbitrage, market entry) 에 편향됐다. 사용자가 *백엔드 엔지니어*이므로 사업 도구는 영역 밖. 카파시 자료 자체에는 사업 측면과 엔지니어링 측면이 *둘 다* 있다 — 본 산출은 사용자 맥락에 맞춰 엔지니어링 측면만 채택.

**보존된 자산**: v2의 engine 2·3·5는 v3에 *재사용* 됨 — minimal-build as bug-finder(C), agent consumer first-class(B), autonomy slider(E). v2 engine 1(cross-paradigm)은 *Voice 룰*(type-coercion 매핑)으로 강등 — 별도 engine이 아니라 모든 engine 위에서 작동하는 메타 동작. v2 engine 4(time arbitrage)는 *영역 밖*으로 명시 (한계 / 영역 밖 §카테고리 명명·사업 발견).

#### v3 채택 — backend engines 6개

사용자 v3 reframe 후 raw를 *백엔드 엔지니어 작업* 관점으로 재정독해 6개 engine을 박았다:
- Engine A — Context as RAM (프롬프트·세션·메모리 설계)
- Engine B — Build for agents (docs·API·error·log 재설계)
- Engine C — Minimal-build as bug-finder (AI 시도 전 의무)
- Engine D — Spirits not animals (training distribution mindset)
- Engine E — Autonomy slider (AI 통합 지점 디자인)
- Engine F — `works.any()` vs `works.all()` (운영 spec)

각 engine은 input·절차·통과 기준·거부 신호를 가진 *동작 단위*. attitude(v1)가 아니라 *지각 엔진*. 사업(v2)이 아니라 *엔지니어링 작업*.

### Engine 매핑의 자료 anchor

각 engine이 raw의 어느 인용을 anchor로 삼는지:

- **Engine A** ← Q9 (context as RAM) + Q7 (LLM=kernel process) + Q8 (LLM OS spec) + Q16 (anterograde amnesia) + Q23 (cognitive core).
- **Engine B** ← Q19 (new consumer category) + Q35 (99.9% LLM attention) + Q30 (Claude Code = first agent example).
- **Engine C** ← Q31~Q34 (nanoGPT/micrograd/llm.c/Zero-to-Hero 학습 철학) + Q28 (nanochat 실패담의 cognitive deficits).
- **Engine D** ← Q14 (people spirits) + Q27 (ghosts not animals) + Q15 (jagged intelligence) + Q28 (training distribution 분석) + Q29 (animal lens 거부 정식화).
- **Engine E** ← Q18 (Iron Man suit Augmentation/Autonomy) + Q20 (decade of agents, partial autonomy, autonomy sliders).
- **Engine F** ← Q17 (works.any vs works.all) + Q24 (slop) + Q25 (decade hedge).

raw의 Q1~Q5, Q10~Q13, Q22, Q26, Q36, Q37은 engine에 직접 anchor되지 않고 *Voice 룰* 또는 *§한계 / 영역 밖* 또는 *§자기-수정의 항상성* 으로 흡수.

### Voice 인용 8개의 선별

agent §1 인격 정의의 직접 인용 8개:

1. Q9 (context as RAM) — Engine A의 voice signature.
2. Q19 (new consumer) — Engine B의 voice signature.
3. Q27 (ghosts/spirits) — Engine D + Voice 전반의 character card.
4. Q15 (jagged intelligence) — Engine D + AI 한계 인식.
5. Q18 (Iron Man) — Engine E의 voice signature.
6. Q17 (works.any/all) — Engine F의 voice signature + code metaphor 사용 모델.
7. Q24 (slop) — hedge voice의 signature.
8. Q20/Q25 (decade) — 시간 축 framing의 signature.

선별 logic: 6 engine 각각에 voice anchor가 1개 + hedge voice의 두 signature(slop + decade) = 8개. 7+ 자리를 채우는 voice 인용은 *너무 많아* voice가 다층화되지만, agent §모드 분기의 6 engine과 1:1 mapping이 깨끗하므로 8개로 박음. Ogilvy 7개(0007 §Voice 인용의 선별)와 다른 수치 — figure별 voice 자료의 모양이 다른 결과.

### 비-타협 원칙 7개의 도출

Ogilvy 7개와 같은 수 — 단 *내용 결*이 다르다. Ogilvy는 "거부할 만한 작업물 line" 7개. Karpathy는 "거부할 만한 *자세·framing* 7개":

1. **AI를 animal로 환원하지 마라** ← Q14, Q15, Q27 + summary §원칙
2. **Demo와 production 절대 섞지 마라** ← Q17, Q24
3. **AI 통합은 binary가 아니라 slider** ← Q18, Q20
4. **모든 출력은 agent consumer까지 first-class** ← Q19, Q35
5. **Minimal first** ← Q31~Q34, Q28
6. **Prompt는 글솜씨가 아니라 paging 전략** ← Q9, Q16, Q23
7. **단일 metaphor lock-in 금지** ← Q12, Q14

대응: 각 원칙이 1~2개 engine을 *교차*한다. 예를 들어 *원칙 2(demo/production)* 는 engine F의 본체이면서 동시에 engine E(slider 위치 정당화)와 engine C(minimal repro의 측정 결과)에 영향. 원칙은 engine을 횡단하는 *line*.

#### 잘라낸 후보

- "From scratch로 짜라" — 원칙으로 박지 않음. Engine C의 절차 안에 흡수. *원칙 = 거부권*이고, "from scratch가 아니라서 거부"의 절대성은 떨어진다.
- "10년 시계로 봐라" — 원칙으로 박지 않음. *Voice 룰* + Heuristics에 흡수. "1년 시계로 봐서 거부"의 단정성은 약함.
- "모든 학습을 공개해라" — 원칙으로 박지 않음. 백엔드 엔지니어 작업 운영에 직접 anchor 없음.

### 인테이크 프로토콜 4질문의 도출

Ogilvy 4질문(고객/약속/증거/30년 personality)과 다른 결. Karpathy 4질문은 *engine으로의 분기 라우터*:

1. **Minimum viable form?** → Engine C anchor
2. **Agent first-class?** → Engine B anchor
3. **흔한 distribution vs unique?** → Engine D anchor
4. **Autonomy slider 위치?** → Engine E anchor

Engine A·F는 인테이크에 anchor하지 않음 — A는 작업 진행 중 자연 호출(프롬프트 작성 단계), F는 production 결정 단계(인테이크보다 후행). 사용자가 작업 진행하다 4질문 답이 자연스럽게 채워지면 그 답으로 engine 적용.

이 인테이크가 *engine으로의 분기 라우터*라는 점이 Ogilvy 인테이크와 결정적으로 다른 자리. Ogilvy 인테이크는 *brand 정의*가 목적, Karpathy 인테이크는 *engine 호출 라우팅*.

### 모드(엔진) 분기의 자료 모양

Ogilvy 6 모드는 *작업 유형*(카피 리뷰/네이밍/Big Idea/...) 별 분기. Karpathy 6 engine은 *지각 동작*(Context as RAM / Build for agents / ...) 별 분기 — 같은 작업이 여러 engine을 연쇄로 통과한다.

전형적 연쇄 예 (agent.md §4 모드 분기에 언급):
- *Engine C(한계 발견) → Engine D(왜 한계? distribution 밖) → Engine E(slider 어디로?)*
- *Engine A(working memory 디자인) → Engine F(works.any vs all 운영)*
- *Engine B(agent consumer 진단) → Engine E(slider로 통합 디자인)*

이 *모드 연쇄*가 카파시 collaborator의 운영 본질. Ogilvy는 한 작업에 한 모드(카피 리뷰면 카피 리뷰)가 dominant, Karpathy는 한 작업에 다중 engine. 이 차이가 운영 검증의 핵심 항목.

### Critiques & limits → §한계 / 영역 밖 매핑

raw §Critiques C1~C6를 agent §7에 압축 매핑:

- **C1 (LeCun's auto-regressive dead end)** → §한계 §Yann LeCun이 옳을 수도 있는 영역. 카파시 framing의 토대(LLM = next computing primitive) 자체의 hedge.
- **C2 (Gary Marcus, vibe coding generalization)** → 본 ADR v3 좁힘이 이미 vibe coding을 본 agent에서 *제외*했으므로 직접 매핑 없음. 단 §한계 §자기-수정 항상성에 "vibe coding은 unfamiliar에서 무너진다는 본인 자료(Q28)도 함께 박음".
- **C3 (Andrew Ng, vibe coding terminology)** → 본 agent에서 *vibe coding*을 engine으로 띄우지 않음 (사용자가 v3에서 사업 측면 제외). 직접 매핑 없음.
- **C4 (Simon Willison, vibe coding scope)** → C3와 같은 자리에서 처리.
- **C5 (카파시 본인의 hedge)** → §5 푸시백 의무 + §1 Voice 룰의 *두 voice 동시 진행* 자체로 자료 안에 흡수. "decade not year" 자세도 *비관·낙관 양극단 차단* 패턴에 박힘.
- **C6 (카파시 본인의 2017 Software 2.0 silent failure 인정)** → §7 한계 §자기-수정의 항상성. "내 framing은 영구진리가 아니다, 새 데이터로 폐기 가능."

### Resource 분리 여부

Ogilvy 0007 §Decomposition §Resource 분리 여부와 동일 절차:

- agent.md 본문 ~5000~6000자 (Ogilvy 0007의 ~4500자보다 두꺼움 — engine별 절차가 두꺼움). references 분리 임계(500줄) 미달.
- engine별 체크리스트(예: Engine F의 worst-case eval 체크)를 assets/로 빼는 것 검토했으나, 사용자가 *체크리스트 채우기*로 받으면 collaborator voice가 카탈로그 변환기로 옅어짐. agent 본문 안에 *대화의 흐름*으로 박는 쪽을 택함 (Ogilvy 0007과 동일 결정).
- Voice 인용 8개는 system prompt 안에 박는다 — 별도 자료로 빼면 voice가 매 turn 새로 로드되지 않음.
- 결정: 디렉토리 단순 유지. `.claude/agents/karpathy.md` 1개, `.claude/skills/karpathy/SKILL.md` 1개, `ADR/skills/0008-karpathy.md` 1개. 미래에 *engine별 worked example case studies* 분리 검토 — application log 모니터링.

## Decision

### 1) Shape — collaborator agent (meta-0002·meta-0003 정합)

shape 결정 근거는 §Context의 figure-specific 이유에 박혔다. diagnostic skill 후보 검토 — 예를 들어 *karpathy-paradigm-mapping* 단일 진단 — meta-0002 §Option D에서 일반론으로 기각된 분해 방식. 한 인격의 6 engine 연쇄가 *진단*으로 환원 안 됨.

### 2) 산출물 — 3개 파일

- `.claude/agents/karpathy.md` — agent system prompt. **본체**.
- `.claude/skills/karpathy/SKILL.md` — 진입 스킬. **얇은 라우터**, 350~450자 본문 목표.
- `ADR/skills/0008-karpathy.md` — 본 문서.

Ogilvy 0007과 동일 3-파일 구조. meta-0003 §3의 lazy materialize 전략에 따라 `.claude/agents/collaborator-builder.md`는 *아직* 만들지 않음. 본 산출이 *두 번째 참조 구현*이 되며, Ogilvy 0007과 함께 templating의 1차 단서 확정.

### 3) Agent.md의 8 섹션 구성

Ogilvy 0007이 박은 8 섹션을 그대로 따르되 *내용 결*은 figure별 자료 모양에 맞춰 변형:

1. **인격 정의 (Voice)** — 직접 인용 8개 + voice 룰 (두 voice 동시 진행, code metaphor 차용, type-coercion 매핑, ghost/spirit character card, we-form, 단정+hedge 동시).
2. **비-타협 원칙 (7개)** — animal 환원 금지 / demo·production 분리 / binary 자동화 금지 / agent consumer first-class / minimal first / paging 전략 / 단일 metaphor 금지.
3. **인테이크 프로토콜** — 4질문, engine 분기 라우터.
4. **모드 분기** — 6 engine(A·B·C·D·E·F), 각각 인식 신호 / 절차 / 통과 기준 / 거부 신호.
5. **푸시백 의무** — default = *self-hedge 동시 진행*. hype-only / doomer-only 양극단 차단.
6. **인정·전환 패턴** — admire하는 7개 자세(from scratch / minimal / agent first-class / slider 명시 / eval worst-case / type-coercion 잘함 / decade horizon).
7. **한계 / 영역 밖** — 카테고리 명명·사업 발견 / AI 비전공 / 단발 query / 자명한 도구 사용 / LeCun이 옳을 수도 있는 영역 / 자기-수정의 항상성.
8. **종료 신호** — 8가지 종료 조건 + 한 줄 요약 형식.

Ogilvy 0007에서 박은 8 섹션 구성이 *두 번째 collaborator에도 그대로 작동*한다는 게 본 산출의 templating 검증. 다음 collaborator(만약 들어온다면)에서도 8 섹션을 default로 시작 가능.

### 4) 진입 SKILL.md의 4 요소 (의도적으로 얇음)

Ogilvy 0007과 동일 4 요소:
1. **언제 사용** — 인물명·고유 개념·대표 코드베이스 명시 호출.
2. **언제 사용 안 함** — 다른 거장 영역 / ambiguous AI 영역(router 경유) / 사업 측면(영역 밖).
3. **라우팅 규칙** — Agent spawn vs SendMessage relay. main의 자기-답변 금지.
4. **종료 트리거** — 종료 조건.

본문 길이 ~400자. Ogilvy 0007과 같은 결.

### 5) 트리거 (description 설계)

description의 명시 호출 키워드:

1. (인물명) "카파시 / Karpathy / Andrej Karpathy / 카르파티"
2. (고유 개념) "Software 2.0 / Software 3.0 / LLM OS / cognitive core / vibe coding / build for agents / context as RAM / spirits not animals / ghosts not animals / autonomy slider / works.any works.all"
3. (대표 코드베이스) "nanoGPT / micrograd / llm.c / Neural Networks Zero to Hero"

should-NOT-trigger:
- 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬·오길비) 영역.
- "AI / LLM / 프롬프트 / agent / 백엔드" 일반어만 있는 ambiguous한 AI 영역 → master-router 경유.
- 카테고리 명명·사업 발견·시장 진입 — 영역 밖 명시.

description은 Ogilvy 0007과 동일 — *명시 호출 키워드 중심*, 자연어 ambiguous 표현은 master-router의 일.

### 6) Agent 호출 vs SendMessage 운영

Ogilvy 0007 §Decision 6와 동일. 본 산출에서 같은 룰을 다시 박음으로써 *두 collaborator 모두 같은 라우팅 패턴*이라는 점이 templating의 1차 단서.

### 7) 잘라낸 것 (의도적 제외)

본 ADR Decision의 핵심 의도적 제외 7가지:

1. **diagnostic skill shape** — meta-0002 §Option A에서 일반론 기각 + figure 단위로 6 engine 연쇄가 진단으로 환원 안 됨.
2. **모드별 sub-skill 분해** — `karpathy-context-as-ram`, `karpathy-build-for-agents` 등 6 sub-skill로 분해 거부. 인격 연속성 손실 + 카탈로그 비대칭.
3. **사업 측면 engine** (v2 폐기 사슬) — time-paradigm arbitrage, cross-paradigm forcing(사업 카테고리 명명), category 발견 — *영역 밖*으로 명시. v4 욕구가 다시 들어오면 별도 figure 또는 카파시 method 추가 스킬로 검토.
4. **Vibe coding을 별도 engine으로 띄우지 않음** — raw §Critiques C2·C3·C4 가 vibe coding terminology의 위험을 명시. 본 agent에서 vibe coding을 *engine으로* 띄우면 Marcus·Ng·Willison의 비판이 그대로 들어옴. Engine F(works.any vs works.all) + Engine C(minimal repro) + Engine D(distribution mindset) 의 *조합*이 vibe coding의 안전한 사용 가이드를 자연스럽게 produce — 별도 engine으로 띄울 필요 없음.
5. **카테고리 명명·"Software 3.0 명명"의 사고법 자체** — raw에서 매우 dense하지만 *백엔드 엔지니어 작업*에 직접 anchor 약함. Voice 룰의 *type-coercion 매핑*으로 흡수, 별도 engine으로 띄우지 않음.
6. **TV/라디오 매체별 모드** — 카파시 영역과 무관, 제외.
7. **자료의 1차 검증 일부 미수행** — raw §Gaps에서 명시한 X.com 본문 verbatim, YC talk 풀 transcript, cognitive core 트윗 완전 features list. application log에서 추적.

### 8) Master-router와의 관계

`master-router`에 등록 시:

- 트리거 신호 = 인물명("카파시/Karpathy") + 고유 개념("Software 3.0/LLM OS/build for agents/...") + 대표 코드베이스("nanoGPT/micrograd/llm.c") 의 명시 호출이 1차 신호.
- ambiguous한 AI·프롬프트·LLM·agent 영역은 router 경유.
- 다른 스킬과의 분리:
  - `feynman-explaining-to-understand`: *이해 자기-감사*("이거 진짜 안 거 맞나"). Karpathy는 *AI 작업 협업* — 다른 영역. 단 Karpathy Engine C(minimal repro)와 Feynman의 brazil-bay 적용은 표면 겹침 가능 — router가 분기.
  - `mckinsey-structured-problem-solving`: *비즈니스 문제 구조화* — 카파시는 *엔지니어링 작업 협업*. router가 분기.
  - `ogilvy`: brand·copy 영역 — 다른 영역. 단 *agent consumer first-class*가 brand 영역으로 옮길 수도 있는 자리에 master-router가 어느 쪽으로 분기할지 운영 검증 필요.
- 명시 호출이 있으면 Karpathy 직접. ambiguous한 AI 영역은 router 경유.

## Consequences

### Positive

- mimesis 카탈로그에 **두 번째 collaborator**가 들어가, Ogilvy 0007에서 박은 8 섹션 templating이 *figure 자료 모양이 달라도 작동한다*는 검증을 확보.
- 사용자(백엔드 엔지니어)가 *매일* AI 작업에 카파시 voice를 동반 가능 — 프롬프트 설계, RAG 구조, agent 통합, code generation, AI-assisted review, docs/API/error/log의 agent-readiness 검토, autonomy slider 디자인, production launch 결정 — 진단 스킬로는 표현 불가했던 ongoing 협업이 첫 *엔지니어링 영역에서* 열림.
- v1·v2·v3·v4 사용자 reframe 사슬을 ADR에 보존 — 미래 figure에서 *attitude 환원*·*사업 환원*의 함정 회피 가이드.
- v3 좁힘으로 카파시의 사업적 framing(category 명명, time arbitrage) 을 *영역 밖*으로 명시, 사용자 학습 목표(백엔드 엔지니어로서 AI 잘 쓰기) 와 정렬.
- 두 voice(framing + hedge) 동시 진행이 system prompt에 박혔다 — main Claude의 default voice(공손한 동조 + hedge 회피) 와 명백히 다른 voice가 운반될지 검증.
- Ogilvy 0007 대비 비대칭(default voice, 모드 분기 결, 인테이크 목적) 이 명시화 — `collaborator-builder.md` materialize 시점에 *변형 자유도*가 무엇인지가 더 깨끗.

### Negative / Trade-offs

- **자산 분산** — Karpathy 한 figure가 3 파일 (agent + skill + ADR). Ogilvy와 동일 trade-off — 관리 표면 +50% (diagnostic 대비).
- **진입 신뢰성 의존** — main Claude가 SKILL.md §라우팅 규칙대로 agent에 relay하지 않고 자기가 답하는 사고 가능. Ogilvy 0007의 동일 risk가 두 번째 사례에서도 잔존.
- **SendMessage 신뢰성** — 동일 세션 두 번째 호출이 첫 spawn한 agent에 정확히 닿는지 운영 검증 필요. Ogilvy와 동일 trade-off.
- **Voice 두 갈래 동시 진행의 운영 검증** — *framing voice* + *hedge voice* 가 같은 답에 공존하는 게 카파시의 본질이지만, agent context window 한계에서 *한 voice로 쏠림*이 발생할 가능성. 한 voice 쏠림이 카파시 collaborator의 특수 failure mode.
- **Engine 연쇄의 인식 신호 충돌** — 사용자 입력이 여러 engine 신호를 동시 가질 수 있음 (예: "이 RAG agent를 PR review bot으로 통합" — Engine A + B + E 셋 모두). agent가 연쇄를 깔끔히 잡는지 운영 검증.
- **v4 욕구의 미응답 부채** — 사용자 v4 reframe(다관점 분석 + drift 방지 + 부정확 명령 확장) 이 본 산출에서 *결과물 확인 후 재평가*로 보류. v3 결과물이 v4 욕구를 부분 충족할지는 운영 검증 필요. 충족 안 하면 v4용 별도 자산(`doc-review`와의 연계, multi-POV review 시스템, 부정확 명령 확장 패턴) 검토.
- **사용자가 사업 측면(category 명명) 으로 끌고 갈 위험** — 카파시 자료에 사업 framing이 풍부해, 사용자가 카파시를 부르고 *그쪽으로* 답을 끌어내려 시도 가능. agent가 §7 한계로 차단하는지 운영 검증.
- **Vibe coding terminology의 우회** — vibe coding을 engine으로 띄우지 않은 결정이, 사용자가 *vibe coding 관련 질문*을 가져왔을 때 agent가 어떻게 응답하는지가 모호. *"vibe coding은 본 모드에서 Engine C+D+F의 조합으로 풀린다"* 식의 응답이 자연스럽게 나오는지 운영 검증.

### Open questions

- **Voice 두 갈래 동시 진행의 자연도** — *"X is the right answer, but it breaks at Y"* 형태가 매 turn 자연스럽게 나오는지, 또는 *한 voice로 쏠리는* failure mode가 자주 발생하는지. 운영 모니터링 핵심.
- **인테이크 4질문이 매 진입마다 작동하는가** — Ogilvy 0007의 동일 open question. *대화의 흐름*으로 묻는지 *체크리스트*로 묻는지에 사용자 경험 좌우.
- **Engine 연쇄의 자동 인식** — agent가 입력에서 *Engine C → D → E* 같은 연쇄를 자동 감지하는지, 또는 단일 engine 진입에서 멈추는지.
- **§인정·전환 패턴의 작동** — Ogilvy 0007의 동일 open question. 회의 voice가 자세 인정을 가리지 않는지.
- **사업 측면 차단의 작동** — 사용자가 *"이 AI feature로 새 카테고리 만들 수 있을까?"* 같이 사업 framing 으로 끌고 갔을 때 agent가 §7 한계로 차단하는지, 또는 사업 답변으로 끌려가는지.
- **v4 욕구 부분 충족** — *다관점 분석*은 Engine D의 distribution 진단 + Engine E의 slider 셋이 일부 답을 만들 수 있음. *drift 방지*는 Engine B + Engine F의 결합이 일부 답. *부정확 명령 확장*은 인테이크 4질문이 일부 답. 셋이 함께 *v4를 의미 있게 충족*하는지 운영 검증.
- **`collaborator-builder.md` materialize 시점** — 본 산출(두 번째 collaborator)로 templating의 1차 단서 확정. 세 번째 collaborator 시점에 builder를 materialize 할지, 또는 두 사례로 충분한지.
- **Master-router 분기 정확도** — 사용자가 *"이 시스템에 AI 어떻게 박지?"* 같이 ambiguous하게 호출하면 router가 Karpathy를 후보로 띄울지. 인물·개념 명시 없이도 백엔드 엔지니어 AI 영역 신호를 잡을지.

## Application log

### 2026-05-24 — Session-scoped agent discovery 발견

첫 빌드 직후 같은 세션에서 카파시 호출 시도(`Agent({subagent_type: "karpathy"})`) → `Agent type 'karpathy' not found. Available agents: ..., ogilvy, ...` 에러. ogilvy는 list에 있지만 karpathy는 없음.

**진단**: Claude Code의 agent registry는 **세션 시작 시점에 `.claude/agents/`를 스캔**한다. 같은 세션 중에 새 agent .md가 추가되어도 registry에 반영 안 됨. ogilvy는 세션 시작 전부터 있던 파일이라 등록됨, karpathy는 세션 중에 생성되어 미등록.

**일반화**: *모든* collaborator(또는 diagnostic agent도 동일) 빌드 직후 첫 테스트는 **반드시 새 세션 시작 후**에 가능. 이건 `figure-shape-branching` memory에 박힌 collaborator shape 운영의 묵시적 전제로 *명시되지 않은 부채*였음.

**Affected ADR items**:
- §Consequences §Negative *진입 신뢰성 의존* 항목의 한 형태로 확정 — 단 main의 자기-답변 문제가 아니라 *registry 미스캔* 문제. 다른 layer.
- §Application log item 1 *진입 SKILL → agent spawn 신뢰성*의 첫 측정 결과: 세션 lifecycle을 모르는 사용자는 새 collaborator를 빌드 직후 호출 시도 → 0% spawn 성공.

**조치**:
- 새 memory 추가: `mimesis-agent-discovery-session-scoped` — "새 agent 빌드 직후 즉시 테스트하려면 새 세션 시작 필수".
- 이후 빌드되는 모든 figure agent의 빌드 직후 보고에 이 안내를 default로 포함 권고.

### 추적 항목 (TBD — 첫 협업 후 갱신)

특히 모니터링할 항목 (Ogilvy 0007 application log 13개 항목과 짝):

  1. **진입 SKILL → agent spawn 의 신뢰성**. 사용자가 "카파시" 또는 카파시 고유 개념을 명시 호출했을 때 main이 agent를 spawn하는 비율 vs 자기 답하는 비율.

  2. **동일 세션 SendMessage 라우팅**. 두 번째·세 번째 호출이 첫 번째 spawn한 karpathy agent에 정확히 닿는지. 새 spawn으로 떨어지면 4질문 답·minimal repro 결과·slider 결정의 손실 양상.

  3. **두 voice 동시 진행의 일관성** — *framing voice* + *hedge voice* 가 매 turn 같이 박히는지. 한 voice 쏠림이 발생하는 정확한 turn 위치·원인.

  4. **인테이크 4질문의 작동** — Ogilvy 0007와 동일.

  5. **6 engine 분기·연쇄의 자동 인식** — 사용자 입력에서 engine을 잘 식별하는지, 연쇄(예: C → D → E)를 자동 호출하는지, 또는 사용자가 명시해야 하는지.

  6. **§5 푸시백 vs §6 인정의 균형** — *self-hedge 동시 진행*이 작업 부정으로 변질하지 않는지. 진짜 좋은 자세에 admire가 작동하는지.

  7. **§7 한계 / 영역 밖의 차단** — 사업 측면 끌어가기 / AI 비전공 의사결정 / 단발 query / 자명한 도구 사용 / LeCun 영역에서 agent가 "내 영역 밖" 명시하는지.

  8. **종료 신호의 작동** — Ogilvy 0007와 동일 + Karpathy 특화: *작업이 자연 완결됐을 때* 종료 한 줄 요약 형식이 잘 출력되는지.

  9. **v4 욕구의 부분 충족 측정** — 다관점 분석 / drift 방지 / 부정확 명령 확장 세 욕구를 *agent 한 인격*이 부분 충족하는지. 충족 비율과 부족 자리.

  10. **자료의 1차 검증 보강 필요성** — X.com 본문 verbatim, YC talk 풀 transcript, cognitive core spec 의 1차 검증 미수행이 agent 인용 정확도에 영향을 주는지.

  11. **사업 측면 회피의 작동** — 사용자가 *"이거 새 카테고리 될까?"* 같이 사업 framing으로 끌고 갔을 때 agent가 §7로 차단하는지, 또는 사업 답변으로 끌려가는지.

  12. **Vibe coding 우회의 자연도** — vibe coding 관련 질문에 agent가 *"Engine C+D+F의 조합으로 풀린다"* 식의 우회 응답이 자연스러운지.

  13. **카탈로그 시각적 비대칭** — README 카탈로그 표에 Karpathy 행(shape=collaborator) 추가 후 사용자가 다른 7행(6 diagnostic + 1 collaborator)와의 차이를 어떻게 인식하는지.

  14. **8 섹션 templating의 두 번째 사례 검증** — Ogilvy 0007의 8 섹션 구성이 Karpathy의 다른 자료 모양에서도 깨끗하게 작동하는지. *깨지는 자리*가 발견되면 (예: Karpathy의 모드가 작업 유형이 아니라 지각 동작이라는 비대칭이 8 섹션 안에서 제대로 표현됐는지) `collaborator-builder.md` materialize 시 그 자리를 보강.

  15. **v4 후속 자산 필요성** — v3 결과물로 사용자 v4 욕구가 충족 안 되면, 다음 자산(예: `dev-fullcycle`·`doc-review`와의 연계, multi-POV review meta-skill, 부정확 명령 확장 패턴) 의 우선순위가 자동 도출.
