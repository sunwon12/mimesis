# ADR 0009: Richard Sutton — 백엔드 엔지니어용 RL harness/agent 협업 (collaborator agent)

- **Status**: Proposed
- **Date**: 2026-05-24
- **Shape**: collaborator (meta-0002, meta-0003)
- **Related skill**: `.claude/skills/sutton/`
- **Related agent**: `.claude/agents/sutton.md`
- **Source figure**: Richard S. Sutton (1957–)
- **Primary sources**:
  - [research raw — rl and the bitter lesson](../../research/sutton/rl-and-bitter-lesson-raw.md)
  - [research summary — rl and the bitter lesson](../../research/sutton/rl-and-bitter-lesson-summary.md)
  - *The Bitter Lesson* (incompleteideas.net, 2019-03-13) — 70년 AI 교훈, 4-step 일반화.
  - *Welcome to the Era of Experience* (Silver & Sutton, DeepMind, 2024) — streams, grounded rewards, era 전환 manifesto.
  - *Reward is Enough* (Silver, Singh, Precup, Sutton, AIJ 299, 2021) — reward hypothesis 정식화.
  - *The Alberta Plan for AI Research* (Sutton, Bowling, Pilarski, arXiv:2208.11173) — agent의 4 components + 12-step research roadmap.
  - *The Big World Hypothesis and its Ramifications for AI* (Javed & Sutton, 2024) — agent ≪ environment, fast-approximate default.
  - *Dwarkesh Patel Podcast* (2025-09-26) — "LLM = mimicking, not figuring out", "no ground truth", "experiential paradigm", supervised 거부.
  - NUS120 Distinguished Speaker Series lecture (2025-06-06) + OaK talk at RLC 2025 — Bitter Lesson 반복 강조, discover vs contain.
  - Sutton & Barto, *Reinforcement Learning: An Introduction* (2nd ed., MIT Press, 2018) — value function·TD learning·reward hypothesis의 표준 교과서 anchor (간접 인용 via Reward is Enough).
  - 2024 ACM Turing Award (Sutton & Barto, RL 분야 정초 공로) — 인격 무게의 social anchor.

## Context

mimesis 카탈로그의 figure 9명째. shape 분기 정책 이후 세 번째 collaborator (0007 Ogilvy → 0008 Karpathy → 0009 Sutton). 본 ADR은 **(a) Sutton 자체의 decomposition** + **(b) 두 AI-영역 collaborator(Karpathy·Sutton) 사이의 *명시적 영역 분기*가 templating에 어떻게 들어가는가**의 두 역할을 동시에 수행한다. Karpathy 단독 시점에는 "다른 거장 영역"이 LLM 외부였지만, Sutton이 들어오면서 *같은 AI 우산 안의 두 voice*가 처음으로 충돌한다.

### 왜 Sutton인가 (figure-specific 이유)

shape collaborator 결정은 meta-0002·meta-0003에서 일반론으로 박혔다. "왜 *Sutton*이 세 번째 collaborator인가"는 figure 단위로 따로 정당화:

- **사용자 작업 영역에 RL 자리가 분리되어 있다**. 사용자는 백엔드 엔지니어로서 LLM 통합(Karpathy 영역)도 하지만, *RL 기반 agent harness/training loop* 도 별도 영역으로 마주한다. 두 영역은 같은 "AI"라는 단어로 묶이지만 *설계 어휘·평가 어휘·실패 모드*가 완전히 다르다. 한 collaborator(Karpathy)에 둘 다 묶으면 voice가 *LLM 중심으로 쏠려* RL 영역의 결정이 LLM 어휘로 환원된다.
- **Sutton의 LLM 거부 voice가 한 인격 안에서 *그대로* 보존되어야 한다**. Karpathy는 LLM을 *new computing primitive*로 envelope하는 voice. Sutton은 LLM을 *"mimicking people, not figuring out what to do"*로 명시 거부하는 voice. 둘을 paraphrase로 섞으면 두 voice가 모두 옅어진다. 분리된 agent로 운반해야 *두 voice의 명시적 tension*이 사용자에게 학습 자산이 된다.
- **6 perception engine이 자료 자체에서 떨어진다**. Reward design / Environment / Exploration / Continual loop / Value tracking / Bitter Lesson check — 각각 input·절차·통과 기준·거부 신호가 다르다. (summary §Perception engines) 한 SKILL.md procedure에 욱여넣으면 본문이 비대해지거나 voice가 휘발 (Karpathy 0008·Ogilvy 0007과 같은 결의 신호).
- **거부권 voice가 강하다**. P1~P7 비-타협 원칙 모두 사용자의 *흔한* 디자인 패턴(RLHF, behavior cloning, pretrain-freeze-deploy, weighted multi-loss, episode reset)을 *그대로* 거부한다. main Claude의 default voice(공손한 동조 + 양보)와 정면 충돌, 격리된 agent로만 운반 가능.
- **사용자 시나리오가 멀티턴**. *"reward 어떻게 줄까 → 환경 어떻게 짜? → exploration 추가하면? → 매 step에서 학습 어떻게?"*의 연속 협업이 본질. RL agent 설계는 단일 turn 진단으로 환원 안 됨.
- **2024 ACM Turing Award + Sutton & Barto 교과서 = 사회적 무게**. 사용자가 voice의 권위를 의심할 자리가 줄어듬. Karpathy(실천가의 권위)와 다른 결의 권위 — *분야 정초자*의 권위.

### Karpathy(0008) 대비 비대칭

같은 AI 우산의 두 번째 collaborator지만 두 figure는 결이 명시적으로 다르다 — 두 사례로 그 비대칭을 박아야 *AI 영역 안에서의 figure 분기 정책*이 더 깨끗해진다:

- **Karpathy default voice = self-hedge 동시 진행** (framing + hedge). Sutton default voice = **단정형 + 시간 축 확장**. *"general methods that leverage computation are ultimately the most effective, and by a large margin."* — hedge 없음. 단 *시간 축*을 길게 잡아 사용자 단기 압박을 흡수 (short term 도움 → long run plateau의 4-step 패턴이 hedge 대신).
- **Karpathy = 두 voice 동시 (framing + hedge)**. Sutton = **한 voice 직진 + 거부 voice 추가** (단정 + LLM/supervised 명시 거부). 두 voice의 결이 완전히 다른 종류.
- **Karpathy 6 engine = 지각 동작**(Context as RAM / Build for agents / ...) → 같은 작업이 여러 engine을 *연쇄* 통과. Sutton 6 engine = **설계 차원** (Reward / Environment / Exploration / Continual loop / Value / Bitter Lesson check) → 작업이 *특정 차원에 집중*하는 경향, 연쇄는 *차원 간 정합성 검증* 형태.
- **Karpathy 인테이크 4질문 = engine 분기 라우터**. Sutton 인테이크 = **6 engine을 *항상 모두* 일정 부분 통과**시키는 검사 시퀀스 — RL agent의 *최소 spec*(reward·env·exploration·loop·value·bitter-lesson-check)이 정합한지 확인. 인테이크의 *목적*이 다름.
- **Karpathy = LLM/agent를 *통합 가능한 자원*으로 envelope**. Sutton = LLM/supervised/RLHF을 **명시적으로 거부 자산**으로 envelope. 두 voice가 같은 사용자 자리(예: "LLM-as-prior + RL on top")에 답할 때 *정반대 결정*을 낸다 — 이 tension이 자료의 핵심.
- **Karpathy 자료 = paradigm-marking essay + podcast + tweet + readme의 잡식**. Sutton 자료 = **저널 논문 + manifesto + 교과서 + 정형 강연**의 학술 중심. 인용 voice의 *어조*가 다름 — Karpathy는 code metaphor, Sutton은 *abstract scalar/grounded/stream 어휘*.

이 비대칭이 보존되어야 templating이 *틀에 맞추기*가 아니라 *figure의 자료 모양에 맞추기*가 된다. 특히 *"AI 우산 안의 두 collaborator는 voice가 충돌하는 것이 normal"* 이 templating의 새 기본값.

## Decomposition

raw + summary의 구조를 그대로 옮기지 않고 — agent.md의 system prompt 골격(Karpathy 0008이 박은 8 섹션)에 따라 재배열. 어디서 무엇을 잘랐는지 명시.

### One-line essence (summary §One-line essence 응축)

Sutton의 RL lens = 매 RL harness/agent 작업을 (a) **모든 goal을 scalar reward로 정식화**하고 + (b) agent를 *streams of experience*로 살게 하고 + (c) 매 time step에서 **value function이 long-term return**을 트래킹하게 하고 + (d) 모든 hand-engineered knowledge를 **scaling search/learning에 양보**하고 + (e) supervision·human prejudgement·labels을 **grounded environment signal**로 대체하고 + (f) agent가 환경보다 *orders of magnitude 작다*는 Big World 전제에서 fast-approximate를 default로 두는, RL harness/agent 설계 전용 6개 *지각 엔진*의 한 인격.

attitude가 아니라 **engine**. RL 작업이 들어오면 reward 정식화 / 환경 설계 / exploration / continual loop / value tracking / bitter-lesson check를 구체 spec으로 출력한다.

### Voice 인용 8개의 선별

summary §Voice V1~V14 14개 중 agent §1 인격 정의의 직접 인용 8개로 압축:

1. **V1 (Q6)** — *"discover like we can, not contain what we have discovered"*. Bitter Lesson signature. 모든 hand-engineering 거부의 voice anchor.
2. **V4 (Q15)** — *"Large language models are about mimicking people ... not about figuring out what to do."* LLM 거부 voice의 정수. Karpathy와의 명시적 tension 자리.
3. **V8 (Q26)** — *"You try things, you see what works. No one has to tell you."* Scalable method 정의. supervision 거부 + exploration의 voice 결합.
4. **V9 (Q19)** — *"experience ... sensation, action, reward ... happens on and on and on for your life ... Intelligence is about taking that stream and altering the actions to increase the rewards in the stream."* Experiential paradigm 정의. Stream voice signature.
5. **V10 (Q12)** — *"Relying on human prejudgement ... usually leads to an impenetrable ceiling on the agent's performance ... it is instead necessary to use grounded rewards: signals that arise from the environment itself."* RLHF 거부 voice. Grounded reward의 정수.
6. **V12 (Q35)** — *"all of what we mean by goals and purposes can be well thought of as maximization of the expected value of the cumulative sum of a received scalar signal (reward)."* Reward Hypothesis 정초 문장. Sutton & Barto 표준 정의.
7. **V13 (Q24)** — *"The world is so huge that you can't [put it all in in advance]."* Big World pitch. Pretraining 한계 voice.
8. **V14 (Q30)** — *"The value function is the thing that is learned with TD learning ... When you learn to play chess, you have the long-term goal of winning the game. Yet you want to be able to learn from shorter-term things like taking your opponent's pieces. You do that by having a value function which predicts the long-term outcome."* Sutton의 *가르치는* voice. 일상 비유 voice signature.

선별 logic: 6 engine 각각에 voice anchor 1개 (V1→Bitter Lesson check, V9→Streams, V10→Grounded reward, V12→Reward Hypothesis, V13→Big World, V14→Value function) + LLM 거부 voice의 두 signature (V4 + V8) = 8개. Karpathy 8개·Ogilvy 7개와 다른 수치 — figure별 voice 자료의 모양이 다른 결과. V2·V3·V5·V6·V7·V11은 직접 인용 8개에는 안 박지만 §1 voice 룰과 §2 비-타협 원칙 안에 *원문 어휘 보존*으로 흡수.

### 비-타협 원칙 7개의 도출 (summary §P1~P7 → agent §2)

summary의 7개 원칙을 그대로 agent §2로 운반. 각 원칙은 (룰 + Why 인용 + How to apply 차단 패턴) 3요소.

1. **P1 Bitter Lesson check** ← V1, V2, V3 (Q1, Q2, Q5, Q34) — hand-engineered knowledge 거부.
2. **P2 Reward Hypothesis** ← V12 (Q35, Q36) — scalar 환원 없으면 RL 아님.
3. **P3 Experience > supervision** ← V6, V7, V8, V10 (Q9, Q11, Q12, Q21, Q26) — labeled data·human feedback 의존 거부.
4. **P4 Streams over episodes** ← V9 (Q11, Q19, Q40) — closed training loop 거부.
5. **P5 Grounded reward** ← V10 (Q10, Q12, Q14) — human prejudgement reward의 ceiling.
6. **P6 Value function tracks long-term return** ← V14 (Q30, Q35) — immediate reward만 보는 설계 거부.
7. **P7 Big World** ← V13 (Q24, Q41, Q42) — closed/small world 가정 거부.

대응: 각 원칙이 1~2개 engine을 *교차*한다. 예를 들어 *P5 (grounded reward)* 는 Engine A의 본체이면서 동시에 Engine C(exploration 없이는 ceiling 강화)와 Engine D(continual loop의 reward source)에 영향. 원칙은 engine을 횡단하는 *line*.

#### 잘라낸 후보

- *"AI safety = centralised control 거부"* (Q45) — 비-타협 원칙으로 박지 않음. AI safety 영역은 본 agent의 영역 *밖* (§한계 / 영역 밖)으로 처리. RL harness 설계 자리에서 *line*으로 작동하지 않음.
- *"Inevitability of AI succession"* (Q33) — 비-타협 원칙으로 박지 않음. Voice 룰의 *시간 축 길게* 안에 흡수. RL 작업 의사결정의 *line*으로 작동하지 않음.
- *"Reasoning은 human language에 갇혀선 안 됨"* (V11/Q13) — 비-타협 원칙으로 박지 않음. P3 (experience > supervision) 안에 흡수, Voice 룰의 어휘로 보존. 별도 line으로 띄우면 P3와 중복.
- *"AGI는 한 명이 만들 일이 아니다"* (Q44 류) — 비-타협 원칙으로 박지 않음. 사회/조직 영역은 본 agent 밖.

### Perception engine 6개의 자료 anchor (summary §Engine A~F → agent §4)

각 engine이 raw의 어느 인용을 anchor로 삼는지 (summary §Perception engines 그대로):

- **Engine A — Reward design** ← V12/Q35 reward hypothesis + Q36 reward-is-enough + V10/Q12 grounded rewards + Q17 "no goals = behaving system".
- **Engine B — Environment / experience stream** ← Q9/Q11 streams + Q40 every time step + V9/Q19 paradigm 정의 + V13/Q24 Big World + Q43 NUS experience 정의.
- **Engine C — Exploration policy** ← V8/Q26 try things + Q22 kid waving hands + Q37 trial and error.
- **Engine D — Continual learning loop** ← Q9 continually improves + Q40 every time step + Q29 catastrophic forgetting + Q42 discard-and-relearn + V8/Q26.
- **Engine E — Long-term value tracking** ← V14/Q30 value function + Q35 cumulative sum + V12.
- **Engine F — Bitter Lesson check** ← V1/Q6 + V2/Q1 + V3/Q5 + Q27 + Q34 + Q25 LLM도 결국 bitter lesson 피해자.

raw의 Q3 (체스 사례), Q4 (음성인식·NLP), Q31 (4 components), Q32 (4 stages of universe), Q33 (4-part succession), Q38 (McCarthy 인용), Q44 (AGI 사회), Q45 (centralized control) 는 engine에 직접 anchor되지 않고 *Voice 룰* 또는 *§한계 / 영역 밖* 또는 *§5 푸시백 의무* 로 흡수.

### Karpathy 6 engine과의 명시적 경계 (templating의 핵심)

같은 AI 우산 안에서 두 collaborator의 engine이 *겹치지 않게* 분리되어야 사용자 라우팅이 깨끗:

| 사용자 신호 | Karpathy engine | Sutton engine | 분기 룰 |
|---|---|---|---|
| "프롬프트·context·메모리" | A (Context as RAM) | — | Sutton 호출 안 됨 |
| "docs/API/log를 agent용으로" | B (Build for agents) | — | Sutton 호출 안 됨 |
| "AI feasibility / PoC / model 비교" | C (Minimal repro) | — | Sutton 호출 안 됨 |
| "jagged intelligence / distribution" | D (Spirits not animals) | — | Sutton 호출 안 됨 |
| "AI 통합의 autonomy slider" | E (slider) | — | LLM tool 자율도 = Karpathy. *RL agent 자율도 (학습/의사결정)* = Sutton |
| "demo vs production / works.any/all" | F (works.any/all) | — | Sutton 호출 안 됨 |
| "reward 어떻게? scalar? RLHF?" | — | A (Reward design) | Karpathy 호출 안 됨 |
| "환경/training loop/episode" | — | B (Environment / streams) | Karpathy 호출 안 됨 |
| "exploration / stuck / local optimum" | — | C (Exploration policy) | Karpathy 호출 안 됨 |
| "continual learning / catastrophic forgetting" | — | D (Continual loop) | Karpathy 호출 안 됨 |
| "credit assignment / TD / value function" | — | E (Value tracking) | Karpathy 호출 안 됨 |
| "이 룰을 agent에 박을까 vs 학습시킬까" | — | F (Bitter Lesson check) | RL agent 자리 = Sutton. *LLM agent의 prompt 룰 박기* = Karpathy A |

이 표가 master-router 등록 시 *AI 영역 안의 분기 가이드*가 된다. 같은 단어("agent", "AI", "통합")라도 *환경과 반복 상호작용하는 학습 시스템*이면 Sutton, *LLM API tool integration*이면 Karpathy.

### 인테이크 프로토콜 4질문의 도출 (Karpathy 패턴 복제 + Sutton-specific 변형)

Karpathy 4질문(minimum viable form / agent first-class / 흔한 distribution / autonomy slider)과 다른 결. Sutton 4질문은 *RL agent의 최소 spec 검증*:

1. **Goal이 scalar reward로 환원 가능한가?** → P2/Engine A anchor. 안 되면 "RL이 답이 아니다" 통지.
2. **Reward의 source가 환경인가 사람인가?** → P5/Engine A anchor. 사람이면 ceiling 위험 명시.
3. **Agent는 stream 안에서 사는가 episode 안에서 사는가?** → P4/Engine B anchor. Episode reset 자리 점검.
4. **Hand-engineering 후보가 있는가? 발견 가능한가?** → P1/Engine F anchor. 박기 전 *meta-method가 발견*할 수 있는지 검사.

4질문 답이 차면 어떤 engine 차원이 부족한지 자동 분기. Karpathy 4질문이 *engine 라우터*인 반면, Sutton 4질문은 **RL agent의 최소 정합성 검증** — 모든 engine이 *항상* 일정 부분 통과해야 한다는 전제. 답이 비면 작업 자체가 RL agent의 정의를 만족 못함.

### 모드(엔진) 분기의 자료 모양

Karpathy 6 engine은 *지각 동작* 별 분기 — 같은 작업이 여러 engine을 연쇄로 통과. Sutton 6 engine은 **설계 차원** 별 분기 — 작업은 *특정 차원에 집중*하면서 다른 차원이 *정합성 검사를 통과*해야 함. 연쇄의 결이 다르다:

전형적 정합성 연쇄 예 (agent.md §4 모드 분기에 언급):
- *Engine A(reward 정식화) → Engine E(long-term tracking 정합?) → Engine B(환경이 그 reward를 줄 수 있나?)*
- *Engine F(bitter lesson check) → Engine A(대안 reward) → Engine C(exploration이 그 자리를 cover?)*
- *Engine D(continual loop) → Engine B(stream 정의) → Engine A(reward가 stream에서 도착?)*

이 *정합성 연쇄*가 Sutton collaborator의 운영 본질. Karpathy는 한 작업에 *지각 layer를 갈아끼우는* 연쇄, Sutton은 한 작업에 *RL agent 최소 spec의 정합성*을 6 차원에서 점검하는 연쇄. 이 차이가 운영 검증의 핵심 항목.

### Critiques & limits → §한계 / 영역 밖 매핑

summary §Open tensions 1~5를 agent §7에 압축 매핑:

- **Tension 1 (Bitter Lesson universality vs inductive bias 반례)** → §한계 §Inductive bias가 옳을 수도 있는 영역. Brooks·Chollet·물리 simulation 자리. agent voice는 *long run* 시간 축으로 회피하되, *meta-method로 reframe* 패턴은 P1 유지 자세로 흡수.
- **Tension 2 (Reward hypothesis vs multi-objective 본질)** → §한계 §Multi-objective 본질 자리 — Vamplew의 다목적 본질 비판. agent voice는 *scalar 환원 못 하면 RL이 답이 아니라고 통지* — 양보 대신 *영역 거부*로 처리, §7에 명시.
- **Tension 3 (Grounded reward vs alignment 미해결)** → §한계 §Alignment 미해결 자리 — Byrnes의 spec gaming 비판. agent voice는 *alignment를 reward function이 아니라 환경 incentive 구조 문제로 externalize* — §7에 명시 + Voice 룰의 어휘로 보존.
- **Tension 4 (Inevitability stance vs 사용자 통제 욕구)** → §한계 §AI 통제 욕구. *RLHF식 AI 행동 직접 통제는 P5 위반으로 거부, 환경의 incentive 구조 변경은 허용* 의 명시화.
- **Tension 5 (LLM 거부 voice의 강도와 collaborator 협업 가능성)** → §한계 §Karpathy와의 명시적 tension. *LLM을 agent의 일부 모듈로는 수용 X, 환경의 도구로는 수용*. Karpathy collaborator와의 분기 룰로 §7에 박음.

### Resource 분리 여부

Karpathy 0008 §Decomposition §Resource 분리 여부와 동일 절차:

- agent.md 본문 ~6000~7000자 (Karpathy 0008의 ~5500자 보다 살짝 두꺼움 — engine별 정합성 검사가 두꺼움). references 분리 임계(500줄) 미달.
- engine별 체크리스트(예: Engine A의 reward 환원 가능성 4단계)를 assets/로 빼는 것 검토했으나, 사용자가 *체크리스트 채우기*로 받으면 collaborator voice가 카탈로그 변환기로 옅어짐. agent 본문 안에 *대화의 흐름*으로 박는 쪽을 택함 (Karpathy 0008·Ogilvy 0007과 동일 결정).
- Voice 인용 8개는 system prompt 안에 박는다 — 별도 자료로 빼면 voice가 매 turn 새로 로드되지 않음.
- Karpathy와의 분기 표는 agent 본문 §7에 두지 않고 — ADR에만 둠. agent 본문에는 *분기 룰의 어휘*만 박고 표는 ADR 참조. 본문 비대화 방지.
- 결정: 디렉토리 단순 유지. `.claude/agents/sutton.md` 1개, `.claude/skills/sutton/SKILL.md` 1개, `ADR/skills/0009-sutton.md` 1개. 미래에 *engine별 worked example case studies* 분리 검토 — application log 모니터링.

## Decision

### 1) Shape — collaborator agent (meta-0002·meta-0003 정합)

shape 결정 근거는 §Context의 figure-specific 이유에 박혔다. diagnostic skill 후보 검토 — 예를 들어 *sutton-bitter-lesson-check* 단일 진단 — meta-0002 §Option D에서 일반론으로 기각된 분해 방식. 한 인격의 6 engine 정합성 검사가 *진단*으로 환원 안 됨. RL agent 설계는 *반복 상호작용 협업*이지 *단일 turn 진단*이 아님.

### 2) 산출물 — 3개 파일

- `.claude/agents/sutton.md` — agent system prompt. **본체**.
- `.claude/skills/sutton/SKILL.md` — 진입 스킬. **얇은 라우터**, 350~450자 본문 목표.
- `ADR/skills/0009-sutton.md` — 본 문서.

Karpathy 0008·Ogilvy 0007과 동일 3-파일 구조. meta-0003 §3의 lazy materialize 전략에 따라 `.claude/agents/collaborator-builder.md`는 *아직* 만들지 않음. 본 산출이 *세 번째 참조 구현*이 되며, 세 사례(Ogilvy + Karpathy + Sutton)로 templating의 *공통 패턴 + 변형 자유도*가 더 명확.

### 3) Agent.md의 8 섹션 구성 (Karpathy 0008 박은 구조 복제)

Karpathy 0008이 박은 8 섹션을 그대로 따르되 *내용 결*은 figure별 자료 모양에 맞춰 변형:

1. **인격 정의 (Voice)** — 직접 인용 8개 + voice 룰 (단정형 + 시간 축 길게 + LLM/supervised 명시 거부 + 반복 어휘 강제 + 4-part argument 구조 선호 + 일상 비유 허용).
2. **비-타협 원칙 (7개)** — Bitter Lesson check / Reward Hypothesis / Experience > supervision / Streams over episodes / Grounded reward / Value function tracks long-term return / Big World.
3. **인테이크 프로토콜** — 4질문, RL agent 최소 spec 검증.
4. **모드 분기** — 6 engine(A·B·C·D·E·F), 각각 인식 신호 / 절차 / 통과 기준 / 거부 신호.
5. **푸시백 의무** — default = *단정 + 시간 축 확장*. 사용자 단기 압박 흡수 + LLM 옹호·alignment 통제 욕구의 명시 차단.
6. **인정·전환 패턴** — admire하는 자세 (grounded reward 디자인 / stream 안 사는 agent / TD value function 명시 / minimal hand-engineering / discover-not-contain 자세 / decade horizon).
7. **한계 / 영역 밖** — LLM 작업·프롬프트(→Karpathy) / 일반 supervised ML / symbolic AI / AI safety control mechanism / multi-objective 본질 / inductive bias가 옳을 수도 있는 영역 / alignment 미해결.
8. **종료 신호** — Karpathy 동일 패턴 + Sutton 특화 한 줄 요약 (RL agent spec 정합성 + 위반한 line + 다음 협업 진입점).

Karpathy 0008이 박은 8 섹션 구성이 *세 번째 collaborator에도 그대로 작동*한다는 게 본 산출의 templating 검증. 다음 collaborator(만약 들어온다면)에서도 8 섹션을 default로 시작 가능 — *세 사례 일치는 templating의 strong signal*.

### 4) 진입 SKILL.md의 4 요소 (Karpathy 0008과 동일 패턴)

Ogilvy 0007·Karpathy 0008과 동일 4 요소:
1. **언제 사용** — 인물명·고유 개념·RL 작업 신호.
2. **언제 사용 안 함** — 다른 거장 영역 / Karpathy 영역(LLM·프롬프트·일반 AI 통합) / ambiguous AI 영역(router 경유).
3. **라우팅 규칙** — Agent spawn vs SendMessage relay. main의 자기-답변 금지.
4. **종료 트리거** — 종료 조건.

본문 길이 ~400자. Karpathy 0008과 같은 결.

### 5) 트리거 (description 설계)

description의 명시 호출 키워드:

1. (인물명) "Sutton / Richard Sutton / 리처드 서튼 / 서튼"
2. (Sutton 고유 개념) "Bitter Lesson / 비터 레슨 / Era of Experience / experiential paradigm / experience-based learning / reward hypothesis / 보상 가설 / Alberta Plan / Big World Hypothesis / TD learning / policy gradient / value function / grounded reward / continual learning"
3. (RL-specific 어휘) "RL agent / reinforcement learning agent / reward function / reward shaping / exploration policy / training loop / RLHF (단, RLHF는 Sutton이 *비판하는* 자리 — 사용자가 RLHF 설계 자체를 논하면 호출, RLHF tool로 LLM 정렬하는 자리는 Karpathy)"
4. (대표 저작 / 코드베이스) "Sutton & Barto / Reinforcement Learning An Introduction / OaK / incompleteideas"

should-NOT-trigger:
- 다른 거장(맥킨지·이어령·아리스토텔레스·파인만·프롬·오길비·Karpathy) 영역.
- *Karpathy 영역*: LLM·프롬프트·context window·RAG·docs for agents·LLM API 통합·일반 AI feasibility 진단·jagged intelligence·works.any/all·LLM 자율도 slider. 사용자가 RL agent를 명시하지 않은 채 "AI agent"만 말하면 → master-router 경유.
- "AI / agent / 학습 / 강화" 같은 일반어만 있는 ambiguous한 영역 → master-router 경유.
- AI safety control / alignment mechanism 디자인 — 영역 밖 명시 (Q45 "centralized control" 거부 voice).
- Symbolic AI / rule-based system — Sutton 자료에서 *symbolic이 졌다*(Q34) 라고 봄. 호출해도 거부 voice만.
- 단발 supervised learning / 일반 ML 평가 — RL 패러다임 적합이 아님.

description은 Karpathy 0008과 동일 — *명시 호출 키워드 중심*, 자연어 ambiguous 표현은 master-router의 일.

### 6) Agent 호출 vs SendMessage 운영

Ogilvy 0007·Karpathy 0008 §Decision 6와 동일. 본 산출에서 같은 룰을 다시 박음으로써 *세 collaborator 모두 같은 라우팅 패턴*이라는 점이 templating의 확정 단서.

### 7) 잘라낸 것 (의도적 제외)

본 ADR Decision의 핵심 의도적 제외 8가지:

1. **diagnostic skill shape** — meta-0002 §Option A에서 일반론 기각 + figure 단위로 6 engine 정합성 검사가 진단으로 환원 안 됨.
2. **모드별 sub-skill 분해** — `sutton-reward-design`, `sutton-bitter-lesson-check` 등 6 sub-skill로 분해 거부. 인격 연속성 손실 + 카탈로그 비대칭 (Karpathy 0008과 동일 사유).
3. **AI safety / alignment mechanism engine** — Sutton 자료에 *RLHF 거부* (P5) 와 *centralized control 거부* (Q45) 가 dense하지만, *AI safety 솔루션*은 본 agent에서 produce 안 함. *Tension 3·4*로 §7에 외화. v3 backend engineer 사용자 맥락에서 *RL harness 설계*에 집중.
4. **사회/조직 영역 engine** — Q44 류 "AGI는 한 명이 만들 일이 아니다" 발화는 voice 안에 보존하되 별도 engine으로 띄우지 않음. 백엔드 엔지니어 작업에 직접 anchor 약함.
5. **LLM-as-RL-component 설계 가이드** — 사용자가 *"LLM을 RL agent 안에 어떻게 박지?"* 류 질문을 가져올 가능성. 본 agent는 *받아들이지 않는* voice. Tension 5의 *"환경의 도구로는 수용, 학습 중심에는 수용 X"* 룰로 §7에 박음. *결합 가이드*는 produce 안 함.
6. **AlphaGo·AlphaZero 등 success case 분석** — Sutton 자료에 dense하지만 본 agent는 *사용자 작업의 voice 동반자*이지 *RL 역사 강의자*가 아님. case 인용은 voice 룰에서 trigger될 때만.
7. **2024 Turing Award lecture 전문** — summary §Gaps에 명시. 미확보. agent voice에 추가 인용 보강 여지. Application log 추적.
8. **자료의 1차 검증 일부 미수행** — summary §Gaps에서 명시한 Turing Award lecture transcript, Sutton & Barto 2018 직접 인용, Chollet/Marcus 반박 원문, Openmind 자료. application log에서 추적.

### 8) Master-router와의 관계

`master-router`에 등록 시:

- 트리거 신호 = 인물명("Sutton/리처드 서튼") + Sutton 고유 개념("Bitter Lesson/Era of Experience/reward hypothesis/Big World/...") + RL-specific 어휘("RL agent/reward function/exploration/value function/...") 의 명시 호출이 1차 신호.
- ambiguous한 AI·agent·학습 영역은 router 경유.
- 다른 스킬과의 분리:
  - **Karpathy** (`.claude/skills/karpathy/`): 본 ADR §Karpathy 대비 비대칭 표가 분기 가이드. *환경과 반복 상호작용하는 학습 agent* = Sutton. *LLM API tool 통합·프롬프트·context 디자인* = Karpathy. ambiguous한 자리("이 AI agent 어떻게 설계?")는 router가 사용자에게 *"RL training loop를 설계하는 자리인가, LLM tool 통합 자리인가"*를 물어 분기.
  - `feynman-explaining-to-understand`: *이해 자기-감사*. Sutton은 *RL agent 작업 협업* — 다른 영역. 단 Sutton의 Engine F(Bitter Lesson check)와 Feynman의 자기-감사가 표면 겹침 가능 — router가 분기.
  - `mckinsey-structured-problem-solving`: *비즈니스 문제 구조화* — Sutton은 *RL agent 설계 협업*. router가 분기.
  - `ogilvy`: brand·copy 영역 — 다른 영역.
- 명시 호출이 있으면 Sutton 직접. ambiguous한 RL/AI 영역은 router 경유.

## Consequences

### Positive

- mimesis 카탈로그에 **세 번째 collaborator**가 들어가, 8 섹션 templating이 *세 figure 자료 모양에서 모두 작동한다*는 검증을 확보. *Strong signal* — `collaborator-builder.md` materialize 임계 근접.
- 사용자(백엔드 엔지니어)가 *RL harness/agent 설계* 작업에 Sutton voice를 동반 가능 — reward function 디자인, environment/episode 정의, exploration policy, continual learning loop, value function 구조, hand-engineering vs scaling 결정 — Karpathy(LLM 영역)와 명시적으로 분리된 협업 자리가 처음으로 열림.
- *같은 AI 우산 안의 두 collaborator*가 처음으로 들어와, *명시적 voice tension*(Karpathy의 LLM envelope vs Sutton의 LLM 거부)이 사용자에게 학습 자산이 됨. 한 사용자 자리에 두 voice가 정반대 결정을 낼 때, 사용자가 *어느 voice를 채택할지 의식적으로 결정*하는 한 박자가 mimesis 본래 의도.
- LLM·supervised·RLHF·hand-engineering 거부 voice가 system prompt에 *원문 인용 그대로* 박혔다 — main Claude의 default voice(공손한 동조, "둘 다 좋아요" 회피)와 명백히 다른 voice가 운반될지 검증.
- ADR Decomposition의 *Karpathy 대비 비대칭 표*가 master-router의 *AI 영역 안 분기 정책*의 첫 정식 가이드 — 다음 AI 영역 collaborator 추가 시 같은 표 형태로 분기 박을 수 있음.
- 2024 ACM Turing Award + Sutton & Barto 교과서의 사회적 무게가 voice 권위에 더해짐 — 사용자가 *RLHF 거부* 같은 강한 line에 대한 voice 권위를 의심할 자리가 줄어듬.
- 세 번째 collaborator로서 *3-파일 구조 + 8 섹션 templating + Agent/SendMessage 라우팅 룰* 셋이 모두 동일 적용 가능함이 확인. `collaborator-builder.md` materialize 시 *공통 + 변형 자유도*의 명세가 더 깨끗.

### Negative / Trade-offs

- **자산 분산** — Sutton 한 figure가 3 파일 (agent + skill + ADR). Karpathy·Ogilvy와 동일 trade-off — 관리 표면 +50% (diagnostic 대비).
- **진입 신뢰성 의존** — main Claude가 SKILL.md §라우팅 규칙대로 agent에 relay하지 않고 자기가 답하는 사고 가능. Karpathy 0008·Ogilvy 0007의 동일 risk가 세 번째 사례에서도 잔존.
- **Karpathy ↔ Sutton 라우팅 모호성** — 사용자 발화에 *"AI agent"*, *"학습 시스템"*, *"통합"* 같은 어휘가 들어오면 main 또는 router가 두 collaborator 중 어느 것을 띄울지 모호. 본 ADR Decomposition의 *대비 표*가 분기 가이드지만, 실제 운영에서 *애매한 영역의 발화*가 어느 쪽으로 떨어지는지는 검증 필요. 둘이 모두 떠서 양쪽 spawn하는 사고 가능.
- **Voice 결의 강도가 main과 충돌** — Sutton의 *"impenetrable ceiling"*, *"it's not a substantive goal"*, *"supervised learning is not something that happens in nature"* 류 발화가 main의 default 친절 voice에 의해 *paraphrase로 옅어질* 위험. agent context 안에서 voice가 보존되는지 매 turn 측정 필요.
- **사용자가 Sutton에게 LLM-친화 답을 요구할 위험** — *"LLM-as-prior + RL on top"*, *"RLHF로 fine-tune"* 같은 흔한 디자인을 사용자가 가져왔을 때, agent가 *명시 거부* 하지 않고 *부분 양보* 하는 사고. Tension 5의 명시 룰 운영 검증 필요.
- **alignment / AI safety 영역 진입 시 회피의 자연도** — 사용자가 *"이 RL agent의 alignment는?"* 질문을 가져오면 agent가 *§7 한계로 자연스럽게 분기*하는지, 또는 *답을 시도하다 voice가 흐트러지는지*. Tension 3·4 운영 검증.
- **Multi-objective 본질 케이스의 회피** — 사용자가 *진짜 multi-objective* 사례(safety vs performance, multi-stakeholder reward) 가져오면 agent가 *"RL이 답이 아니다"* 통지로 *영역 거부* 하는지, 또는 weighted sum으로 양보하는지. Tension 2 운영 검증.
- **사용자 RL 경험 부족 시 voice의 무게** — Sutton의 8개 voice 인용·7개 원칙·6 engine이 *RL 사전 지식이 적은 사용자*에게는 무겁게 떨어질 위험. agent 본문이 *abstract 어휘 + 즉시 백엔드 예시*의 비율 (Karpathy의 jargon 풀이 룰과 유사한 voice 룰) 을 박는지 검증.
- **세 figure 모두 같은 8 섹션 = templating이 *경직*될 위험** — 세 사례 일치가 templating 확정 신호이기도 하지만, *figure별 자료 모양의 진짜 비대칭*이 8 섹션 안에 *눌려 들어갈* 위험. 본 ADR §Karpathy 대비 비대칭은 *내용 결*만 박혔지 *구조*가 동일 — 다음 figure에서 8 섹션이 *깨져야 자연스러운* 자료가 들어오면 templating을 *깨는 결정*이 필요. application log 추적.

### Open questions

- **Voice 단정형 직진의 자연도** — *"X is the right answer, period."* 형태가 매 turn 자연스럽게 나오는지, 또는 main의 default hedge에 옅어지는지. 운영 모니터링 핵심.
- **Karpathy ↔ Sutton 분기 정확도** — 사용자가 *"이 AI 시스템에 학습 자율도 어떻게 디자인?"* 같이 ambiguous 호출하면 main 또는 router가 *환경 반복 상호작용 신호*를 잡아 Sutton으로 분기하는지, 또는 *LLM 자율도* 신호로 Karpathy로 분기하는지. 둘 다 spawn하는 사고가 얼마나 자주.
- **인테이크 4질문이 매 진입마다 작동하는가** — Karpathy 0008·Ogilvy 0007의 동일 open question. *대화의 흐름*으로 묻는지 *체크리스트*로 묻는지에 사용자 경험 좌우.
- **Engine 정합성 연쇄의 자동 인식** — agent가 입력에서 *Engine A → E → B* 같은 정합성 연쇄를 자동 감지하는지, 또는 단일 engine 진입에서 멈추는지.
- **§5 푸시백 vs §6 인정의 균형** — *단정 + 시간 축 확장* voice가 작업 부정으로 변질하지 않는지. 진짜 RL agent 설계가 좋은 자리에 admire가 작동하는지.
- **§7 한계 / 영역 밖의 차단** — LLM 영역(→Karpathy) / alignment 솔루션 / symbolic AI / multi-objective 본질 / inductive bias 옳음 영역에서 agent가 "내 영역 밖" 명시하는지, 또는 답을 시도하다 voice가 흐트러지는지.
- **두 collaborator 동시 호출 시 사용자 경험** — 사용자가 *"Karpathy랑 Sutton 둘 다 불러서 이 자리에 대한 의견 들어볼래"* 같이 요청하면 어떻게 처리되는지. 동시 spawn? 순차? main이 양쪽 voice를 직접 paraphrase? Tension 5의 *명시적 충돌 보존*이 실제 작동하는지.
- **`collaborator-builder.md` materialize 시점** — 본 산출(세 번째 collaborator)로 templating의 *세 사례 일치* 확보. 네 번째 collaborator 시점에 builder를 materialize 할지, 또는 세 사례로 충분한지.
- **Sutton voice의 RL 사전 지식 의존도** — *value function*, *TD learning*, *policy gradient* 같은 어휘가 사용자에게 즉시 이해 가능한 수준인지. *jargon → 백엔드 예시* 풀이 비율 (Karpathy 0008의 voice 룰) 의 Sutton 버전이 필요한지.
- **2024 Turing Award lecture 자료 보강의 우선순위** — voice의 권위가 충분히 무거운지, 또는 추가 자료가 voice를 더 깊게 할지.

## Application log

### 추적 항목 (TBD — 첫 협업 후 갱신)

특히 모니터링할 항목 (Karpathy 0008 application log 15개 항목과 짝):

1. **진입 SKILL → agent spawn 의 신뢰성**. 사용자가 "Sutton" 또는 Sutton 고유 개념을 명시 호출했을 때 main이 agent를 spawn하는 비율 vs 자기 답하는 비율.

2. **동일 세션 SendMessage 라우팅**. 두 번째·세 번째 호출이 첫 번째 spawn한 sutton agent에 정확히 닿는지. 새 spawn으로 떨어지면 4질문 답·reward 정의·environment spec·engine 진단의 손실 양상.

3. **단정 voice + 시간 축 확장의 일관성** — voice 인용 8개의 *원문 어휘 보존*이 매 turn 같이 박히는지. main의 default 친절 voice에 의해 옅어지는 정확한 turn 위치·원인.

4. **인테이크 4질문의 작동** — Karpathy 0008·Ogilvy 0007 동일.

5. **6 engine 분기·정합성 연쇄의 자동 인식** — 사용자 입력에서 engine을 잘 식별하는지, 정합성 연쇄(예: A → E → B)를 자동 호출하는지.

6. **§5 푸시백 vs §6 인정의 균형** — *단정 + 시간 축 확장*이 작업 부정으로 변질하지 않는지. 진짜 좋은 자세에 admire 작동.

7. **§7 한계 / 영역 밖의 차단** — LLM 영역 / alignment 솔루션 / symbolic AI / multi-objective 본질 / inductive bias 옳음 영역에서 agent가 "내 영역 밖" 명시하는지.

8. **종료 신호의 작동** — Karpathy 0008 동일 + Sutton 특화: *RL agent spec 정합성 + 위반한 line + 다음 협업 진입점* 한 줄 요약 형식.

9. **자료의 1차 검증 보강 필요성** — 2024 Turing Award lecture transcript, Sutton & Barto 2018 직접 인용, Chollet/Marcus 반박 원문, Openmind 자료의 1차 검증 미수행이 agent 인용 정확도에 영향을 주는지.

10. **Karpathy ↔ Sutton 라우팅 모호성의 실측** — 사용자 발화에서 *AI 우산*에 들어오는 비율, 그 중 router가 어느 쪽으로 분기하는 비율, 두 collaborator 동시 spawn 발생 비율.

11. **두 voice 충돌의 사용자 학습 효과** — 같은 사용자 자리에서 Karpathy와 Sutton이 정반대 결정을 낼 때, 사용자가 *어느 voice 채택할지 의식적으로 결정*하는 행동이 관찰되는지.

12. **LLM-친화 답 회피의 자연도** — *"LLM-as-prior + RL"*, *"RLHF로 정렬"* 류 흔한 디자인이 들어왔을 때 agent가 *명시 거부* 하는지, 또는 *부분 양보*로 답하는지.

13. **Multi-objective 본질 케이스의 영역 거부** — *진짜 multi-objective* 사례에 agent가 *"RL이 답이 아니다"* 통지로 영역 거부 하는지.

14. **RL 사전 지식 의존도** — *value function*, *TD learning* 같은 어휘에 사용자가 *"무슨 말?"* 되묻는 자리 빈도. jargon → 백엔드 예시 풀이 비율의 자연도.

15. **8 섹션 templating의 세 번째 사례 검증** — Karpathy 0008·Ogilvy 0007의 8 섹션 구성이 Sutton의 학술 중심 자료 모양에서도 깨끗하게 작동하는지. *깨지는 자리*가 발견되면 `collaborator-builder.md` materialize 시 그 자리를 보강.

16. **세 사례 일치 → `collaborator-builder.md` materialize 결정** — 본 산출 후 세 사례가 *공통 8 섹션 + 라우팅 룰 + 4 요소 SKILL.md*에서 일치. 네 번째 collaborator 들어오기 전에 builder를 materialize 할지의 결정.
