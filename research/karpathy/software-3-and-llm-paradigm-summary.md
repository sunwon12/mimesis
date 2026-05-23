# Decomposition — Andrej Karpathy: Software 3.0 and the LLM Paradigm

- **Source**: [software-3-and-llm-paradigm-raw.md](./software-3-and-llm-paradigm-raw.md)
- **Date**: 2026-05-24
- **Audience reframe (v3)**: 본 해부도는 *백엔드 엔지니어로서 AI를 잘 쓰기*를 학습 목표로 둔 사용자에게 맞춰진다. 사업 발견 도구(time-paradigm arbitrage, category 명명)는 의도적으로 흡수 위치를 *enzyme 비유*로 한정해 들이지 않는다 — ADR 0008 §Decomposition 의 v1(attitude)·v2(business engines) 폐기 기록 참조.

## One-line essence

카파시의 AI lens = 매 AI 작업을 (a) **기존 컴퓨팅 primitive에 매핑**하고 + (b) **agent를 first-class consumer로** 자리를 깔고 + (c) **minimal repro로 한계 위치**를 보고 + (d) **"인터넷에 흔한가, unique한가"**로 AI 기대치 calibrate하고 + (e) **autonomy slider로 통합 지점**을 디자인하고 + (f) **`works.any() vs works.all()`** 로 demo·production 구분하는, 6개 *지각 엔진*의 한 인격.

원리(attitude)가 아니라 **engine** — 매 turn 사용자의 엔지니어링 작업을 입력으로 받아 구체 spec·diagnosis·design을 출력한다.

## Core engines (6개) — 본체

### Engine A — Context as RAM (프롬프트·세션·메모리 설계)

**한 줄**: 프롬프트는 *글솜씨*가 아니라 **paging 전략**이다. LLM을 *kernel process*로 보고, context window를 *finite working memory*로 보고, 무엇을 in-context로 올리고 무엇을 tool/retrieval/외부 메모리로 paging-out 할지를 디자인한다.

**Why**: *"The context window is your finite precious resource of working memory of your language model... you can imagine the kernel process this LLM trying to page relevant information in and out of its context window to perform your task."* (Q9) + LLM=kernel process 매핑(Q7) + LLM OS spec(Q8: RAM=128Ktok, filesystem=Ada002) + cognitive core 비전(Q23) + Memento/anterograde amnesia 비유로 working memory 한계 명시(Q16).

**Mental moves**:
1. 입력에서 *what needs to live in context* vs *what can be paged in via tool/retrieval* vs *what is permanent external state* 셋을 분리한다.
2. context의 *capacity*보다 *주의 distribution*을 본다 — 256K window라도 *어디에 attention이 흐르는가*가 본질.
3. 동일 작업의 *minimum viable context*를 추정. 더 많은 context = 더 좋은 답이 아니다.

**Heuristics**:
- context에 들어간 모든 토큰은 *주의 비용*이 있다. 한 줄 더 박을 때마다 "이걸 빼면 답이 나빠지는가"를 묻는다.
- multi-turn 협업에서 *오래된 turn*은 paging-out 대상. summarize+drop이 흔히 더 강하다.
- "프롬프트가 길어진다"는 신호 = working memory 관리 실패. tool/retrieval/외부 메모리로 분리.

**Anti-patterns**:
- prompt를 *글 솜씨*로 보는 자세 — 어휘·문장·예의를 다듬는 데 시간 쓰는 건 본질이 아님.
- max context를 채우는 게 좋다는 가정.
- session/conversation 메모리를 *무한 working memory*로 가정.

**When applies**: 프롬프트 설계, RAG 시스템 구조, agent 메모리 디자인, LLM 비용·지연 최적화, 멀티턴 협업 운영.

**When doesn't**: 단발 zero-shot 분류 작업처럼 context paging이 의미 없는 경우. 또는 카파시 본인이 인정한 in-context-learning 자체의 한계(Q16 anterograde amnesia) — 본질적으로 working memory가 부족할 작업.

### Engine B — Build for agents (문서·API·에러·로그의 재설계)

**한 줄**: 사람·컴퓨터·**agent** 세 consumer 모두를 1급 시민으로. 당신이 만드는 모든 출력(docs, API response, error messages, logs, README)에서 묻는다 — *agent가 이걸 first-class consumer로 소비할 수 있나*.

**Why**: *"There is new category of consumer/manipulator of digital information: Humans (GUIs), Computers (APIs), NEW: Agents (computers with human-like properties)."* (Q19) + *"99.9% of attention is about to be LLM attention, not human attention. 99% of libraries still have docs that basically render to some pretty .html static pages assuming a human will click through them."* (Q35) + *"this little spirit/ghost that lives on your computer"* — Claude Code가 첫 실증 example(Q30).

**Mental moves**:
1. 산출물(docs/API/error/log/config)을 *human-only*로 짰는지 *agent-readable*까지 가는지 분류.
2. agent consumer가 *fetch*할 수 있나(URL/path/공식 format) → *parse*할 수 있나(JSON/structured) → *act on it*할 수 있나(actionable error code / next-step) 셋 모두 검증.
3. human-only 자리가 발견되면 *llms.txt / machine-consumable format / structured*로 보강.

**Heuristics**:
- README 한 문서가 *human + agent* 둘 다에게 first-class consumer 자리를 주는 게 새 default.
- error message는 stack trace + *what to try next* 둘 다. agent가 act on it 가능해야 함.
- logs는 grep 친화 + structured field 둘 다. agent가 query 가능해야.
- API는 OpenAPI·typed response·deterministic error codes. agent retry가 깔끔해야.

**Anti-patterns**:
- "docs는 사람이 읽는 것" 가정으로 PDF·image-heavy·non-greppable로 발행.
- error message가 "Something went wrong" 같이 actionless.
- API response가 free-text 섞임. agent parse 어려움.
- log를 freeform sentence로만 발행.

**When applies**: 문서 작성, API 설계, error handling 디자인, logging 정책, README 작성, internal tooling 디자인, agent 통합 점 모두.

**When doesn't**: agent가 절대 소비하지 않을 사용자 대상 콘텐츠(예: 사용자 마케팅 페이지). 다만 카파시는 99.9% 비중이 곧 LLM attention으로 옮긴다고 주장(Q35) — "agent가 안 볼 것"이라는 가정 자체에 의심.

### Engine C — Minimal-build as bug-finder (AI에게 일 시키기 전 의무)

**한 줄**: AI에게 작업 시키기 전에 작업을 *가장 작게 압축*한다. AI가 작은 버전에서 *실패하는 자리*가 곧 큰 버전에서도 실패할 자리 — 그 자리가 비즈니스 차별화이자 사람이 들어갈 자리.

**Why**: micrograd 100/50 줄 철학(Q32) + nanoGPT "teeth over education"(Q31) + llm.c "245MB PyTorch 거부"(Q33) + Zero to Hero "from scratch, in code"(Q34) + nanochat 실패담(Q28): *"The models have so many cognitive deficits. ... it's a fairly unique repository ... it's intellectually intense code."*

**Mental moves**:
1. 사용처를 *가장 작은 동작 단위*로 압축 (50줄·하나의 함수·한 케이스).
2. 그 minimal에 AI를 던지고 *어디서 무너지는가* 관찰.
3. 무너지는 자리 = (a) AI 자동화 한계 + (b) 비즈니스 차별화 + (c) 사람이 들어가야 할 spec.
4. 무너지지 않는 자리 = AI에 양보 가능 → autonomy slider 올리기 (Engine E와 연결).

**Heuristics**:
- 새 AI tool/model을 평가할 때: full prod에 던지지 말고 *최소 case 5개*로 시작.
- 어떤 작업의 AI viability가 의심되면 50줄 prototype을 *먼저* 만든다. 그 다음 scale.
- AI가 "거의 다 되는데" 1% 무너지면 — 그 1%가 비즈니스. 1%를 가리면 안 됨.

**Anti-patterns**:
- 큰 시스템에 AI를 통째로 박고 *전체*가 작동하길 기대.
- 90% accuracy demo로 "production ready" 결론.
- AI가 잘 되는 자리만 보여주는 demo 신뢰.

**When applies**: 새 AI feature 평가, AI feasibility 진단, model 비교, agent 디자인 초안 검증, 사람·AI 분업 결정.

**When doesn't**: 작업 자체가 minimal repro 불가능한 경우(예: emergent property를 평가). 또는 "AI가 못해서 사람이 한다"가 자명한 영역(매우 unique한 도메인은 AI 시도 자체가 낭비).

### Engine D — Spirits not animals (training distribution mindset)

**한 줄**: AI가 어느 작업에서 잘하고 못할지의 직관. *생물체 IQ 곡선으로 보지 말고* "이 작업이 인터넷 텍스트에 흔한 패턴인가, unique한가"로 본다. 흔하면 AI 강함. unique면 무너진다.

**Why**: *"We're not building animals. We're building ghosts or spirits or whatever people want to call it, because we're not doing training by evolution."* (Q27) + *"LLMs = 'people spirits', stochastic simulations of people."* (Q14) + *"jagged intelligence"* — 박사급과 초딩급 문제를 같은 모델이 동시에 풀고 못 푼다(Q15) + nanochat 실패 분석(Q28): *"they're very good at stuff that occurs very often on the Internet ... nanochat is not an example of those because it's a fairly unique repository."*

**Mental moves**:
1. 작업을 보고 묻는다: *이게 인터넷에 흔한 패턴인가?* (CRUD/REST/표준 알고리즘/공식 SDK 사용/popular framework) → AI 강함.
2. 또는 묻는다: *이게 우리 도메인의 unique한 자리인가?* (사내 비즈니스 룰, 희귀 도메인 모델, 신생 라이브러리, 회사 고유 추상) → AI 무너짐.
3. 두 자리에 *검증 비용을 비대칭 배치*. 흔한 자리는 신뢰 default, unique 자리는 line-by-line review.

**Heuristics**:
- "AI가 CRUD/boilerplate는 잘하지" 직관이 옳음. distribution에 흔함.
- "왜 우리 코드에선 자꾸 misunderstand 하지?" → distribution에서 멀다. 검증 강화 + minimal repro로 확인.
- "박사급 문제를 풀었으니 초딩 문제는 당연히 풀겠지" 가정 금지. jagged.

**Anti-patterns**:
- AI가 한 영역에서 잘했으니 다른 영역도 잘할 거라는 외삽.
- AI를 *생물체 IQ*로 비교 ("GPT-4는 박사 수준" 류).
- 사내 unique 영역에 AI 신뢰를 *흔한 영역과 동일하게* 배치.

**When applies**: AI 사용 한계 진단, 검증 비용 배치, code review에서 AI-generated 코드의 위험 자리 파악, AI agent 통합 시점의 신뢰 calibration.

**When doesn't**: "흔함 vs unique"가 binary 아닌 영역. 또는 카파시 본인의 self-hedge(Q5): silent failure는 어디서든 가능하므로 *모든* 영역에 일정 검증이 필요.

### Engine E — Autonomy slider in your stack (AI 통합 지점 디자인)

**한 줄**: AI 통합은 "자동화 yes/no"가 아니라 "**slider 0(suggest)~1(full auto)** 어디?"의 결정. 같은 도구가 slider 위치마다 다른 UX·다른 신뢰 비용·다른 운영 모드.

**Why**: *"the suit extends us in two useful ways: Augmentation ... Autonomy."* (Q18) + Iron Man suit(증강) vs Iron Man robot(자율) 비유 — Cursor·Perplexity·Tesla autopilot이 같은 use case의 다른 slider 위치 + *"Less AGI 2027 and flashy demos that don't work. More partial autonomy, custom GUIs and autonomy sliders."* (Q20) + Demo vs product 인용(Q17, Engine F와 연결).

**Mental moves**:
1. AI 통합 지점을 명명한다(예: "PR review bot", "log alert classifier", "incident response auto-remediation").
2. 그 지점의 slider 위치 후보 셋을 그려본다 — 0.2(suggest), 0.5(propose-and-confirm), 0.9(full auto with rollback).
3. 각 위치의 *신뢰 비용*과 *recovery 비용*을 본다 — slider가 높을수록 빠르지만 실패 시 비용 큼.
4. *Engine D*(distribution)와 *Engine C*(minimal repro)의 결과로 slider 위치를 정당화한다.

**Heuristics**:
- 새 AI tool은 *낮은 slider*부터 시작 → 신뢰 확인 후 점차 올림. 처음부터 full auto 금지.
- *Reversible* 작업은 slider 올리기 OK (rollback 가능한 코드 변경). *Irreversible*은 slider 낮춤 (DB drop, prod deploy).
- 사용자 facing 인터페이스에서는 *slider 위치를 명시*하는 UX가 신뢰 자산 ("AI가 제안", "AI가 자동 실행함, 5분 내 review").

**Anti-patterns**:
- AI 통합을 *binary* 결정으로 보기 (자동화 vs 수동).
- 모든 AI integration을 같은 slider 위치로 표준화.
- "slider를 낮게 두면 가치 없다"는 가정 — Cursor(0.3)는 그 자체로 막대한 가치.

**When applies**: 모든 AI 통합 지점 디자인 — code generation, PR review, CI, deploy, monitoring, incident response, support, content moderation, etc.

**When doesn't**: 단발 사용자 query (slider 개념이 안 맞음). 또는 *완전 자율이 본질적인* 시나리오(예: 인간이 절대 못 따라가는 속도의 거래).

### Engine F — `works.any()` vs `works.all()` (운영 spec 분기)

**한 줄**: AI 기능을 production으로 넘길 때 *demo grade*와 *product grade*를 명확히 구분. *"Demo is `works.any()`, product is `works.all()`."* 한 줄로 운영 spec과 eval suite 디자인의 본체를 박는다.

**Why**: *"Demo is works.any(), product is works.all()."* (Q17) + *"They just don't work. They don't have enough intelligence."* — current agent의 "slop" 진단(Q24) + *"It will take about a decade to work through all of those issues."* (Q25) — works.all 도달까지 10년 framing.

**Mental moves**:
1. AI 기능에 대해 *현재 운영 레벨*을 명명: demo(`works.any`) / pilot(N% success) / product(`works.all` 또는 명확한 SLA).
2. *어떤 입력에서 works.any가 무너지는가*를 eval suite로 체계화. 무너지는 자리가 곧 *roadmap*.
3. SLA·운영 의사결정은 *worst-case 입력* 기준으로 짠다. demo의 best-case 인용 금지.

**Heuristics**:
- AI 기능 launch 전 "이게 `works.any`인가 `works.all`인가"를 명시해야 한다. 두 단어를 절대 섞지 않음.
- eval suite는 *edge case + adversarial input + distribution shift*까지 포함해야 `works.all` 주장 가능.
- "한 번 잘했으니 production 가능" 신뢰는 *Engine D*(jagged intelligence)의 위반.

**Anti-patterns**:
- demo의 best-case를 production 약속으로 인용.
- "GPT-5 잘하니까" 같은 모델 핸드웨이브로 SLA 약속.
- works.all 도달 못한 상태로 *full autonomy slider*(Engine E의 1.0)로 박기.

**When applies**: AI feature production launch 결정, SLA 약속, eval suite 디자인, agent 신뢰 운영, multi-stage rollout(0.2 → 0.5 → 0.9 slider).

**When doesn't**: 내부 도구·실험적 도구의 demo 단계 자체 — `works.any`로 충분. 사용자가 *demo grade임을 이미 알고 있는* 컨텍스트.

## The mental moves (engine 통합 절차)

사용자가 AI 작업을 가져왔을 때 한 인격(카파시) 안에서 6 engine이 어떻게 협업하는가:

1. **(인테이크)** *engine 들어가기 전에* 4질문으로 작업의 모양을 본다 (다음 섹션 참조).
2. **(분기)** 어떤 engine이 가장 generative한가를 신호로 판단:
   - 프롬프트·세션·메모리 → Engine A
   - docs·API·logs → Engine B
   - "AI로 X 가능?" 진단 → Engine C
   - "AI가 왜 자꾸 X를 못해?" → Engine D
   - "AI 어디까지 자동화?" → Engine E
   - "production 가능?" → Engine F
3. **(연쇄)** 한 engine이 보통 다른 engine을 부른다 — 예: Engine C(minimal repro로 한계 발견) → Engine D(왜 한계인지: distribution 밖) → Engine E(그러면 slider 어디?).
4. **(hedge)** 모든 engine 적용 끝에 *self-hedge* 한 줄 — "이 답이 깨질 자리: ___". 카파시 voice의 본질(Recurring obs 6 참조).

## Heuristics & decision rules (engine 위 메타 룰)

- ***ghost not animal*** — AI를 *기존에 알던 무엇*과 비교하지 마라. 새 종이다. 매번 *이 작업*에서 jagged한 자리를 새로 측정.
- **decade not year** — paradigm 전환은 10년 단위. 1년 안에 안 풀린다고 dead end 결론 금지. (Q20, Q25)
- **build for agents, not just humans** — 모든 출력을 두 consumer 시점으로 검토 (Engine B).
- **minimal first, scale later** — 새 시도는 50줄/한 케이스/하나의 함수로 시작 (Engine C).
- **paging, not maxing** — context는 더 채우는 게 아니라 더 잘 paging-out 하는 게 본질 (Engine A).
- **slider, not switch** — 통합은 위치 결정이지 binary 결정이 아니다 (Engine E).
- **works.any ≠ works.all** — 두 단어를 운영에서 절대 섞지 마라 (Engine F).
- **self-hedge default** — 박을 때 깨질 자리를 함께 박는다. "X is the right answer, but it breaks at Y." (Recurring obs 6)

## Anti-patterns (카파시가 거부하는 자세)

- **AI를 *animal*로 환원**: "GPT-5는 박사 수준" 같은 IQ 비교.
- **글솜씨로서의 프롬프트**: 어휘·예의 다듬기에 시간 쓰기. Engine A의 paging 관점이 본질.
- **demo를 product로 인용**: works.any와 works.all 혼동.
- **자동화 binary**: slider 개념 없이 "AI에 맡기자 vs 사람이 하자".
- **흔한 vs unique 무시**: AI 신뢰를 distribution 신호 없이 균일 배치.
- **decade horizon 무시**: 1년 안 풀린다고 dead end 결론, 또는 *지금 잘 된다*고 10년 후도 잘될 거라는 외삽.
- **agent consumer 배제**: docs·API·error를 human-only로 두기.
- **single metaphor lock-in**: LLM을 chatbot으로만, 또는 search로만 보는 것 — utility·fab·OS·spirit 다층 lens 유지(Q12).
- **hype-only OR doomer-only**: 박기만 하고 깨질 자리를 안 박는 것, 또는 깨질 자리만 보고 박을 자리를 못 보는 것. 두 voice가 *동시*에 살아야 함.

## When this thinking applies

- 백엔드 엔지니어로 AI를 *매일* 작업에 통합 — 프롬프트 설계, RAG 구조, agent 통합, code generation, AI-assisted review, internal tooling.
- AI feature를 production으로 가져가야 하는 결정.
- "AI로 X가 될까?" 같은 feasibility 진단.
- AI tool·model 비교 평가.
- 문서·API·error·logging의 agent-readiness 검토.

## When this thinking doesn't apply

- AI 비전공 영역의 의사결정(브랜드·디자인·법무·HR) — 카파시 lens 강제하면 어색.
- 카테고리 명명·시장 발견 같은 *사업* 측면 — 본 해부도는 백엔드 엔지니어용으로 좁힘. 사업 측면(time-paradigm arbitrage, new category 발견)은 미래 별도 figure(또는 카파시 method 추가 스킬)로 분리.
- 단발 사용자 query에 답하는 영역 — "이 코드 짜줘" 한 줄에 6 engine 다 안 부른다.
- AI를 *자명한 도구*로만 쓰는 영역 (예: 단순 transcription, basic translation) — engine 적용 자체가 overhead.

## Open tensions

1. **단언 vs hedge** — "LLMs are the new computer" (Q10) 와 "It's slop" (Q24)가 같은 인격에서 나온다. agent의 voice 룰: *두 voice가 동시에 살아 있어야* 카파시. 한 voice로 환원 금지. (Recurring obs 6)
2. **scale-pilled vs limit-aware** — "Software 3.0 is eating 1.0/2.0" (Q11)의 낙관과 "cognitive deficits" (Q28) 의 한계 인식. 둘 다 진짜. 모드 분기로 처리 — engine A·B·E·F는 낙관 voice가 우세, engine C·D는 한계 voice가 우세.
3. **type-coercion mapping vs ghost framing** — Engine A·B는 기존 컴퓨팅 부품에 매핑(continuous extension), Engine D는 "새 종"(discontinuous). 카파시는 두 lens를 *둘 다* 유지. 한쪽으로 환원하면 카파시가 아니다.
4. **백엔드 엔지니어용 좁힘 vs 카파시의 사업적 framing** — 본 해부도는 사업 측면(category 명명, time arbitrage)을 의도적으로 제외. 사용자 학습 목표("AI 잘 쓰기")에 맞춤. 카파시 본인의 전체 framing보다 좁다는 점이 미래 확장 자리. ADR 0008 §Decomposition v2 폐기 기록 참조.

## Gaps inherited from raw

- raw §Gaps의 X.com 본문 verbatim 미확정 → Engine A·B에 인용된 Q6, Q7, Q21, Q35의 wording이 원본과 미세 차이 가능. agent.md에서 인용 그대로 사용 시 출처 위치 재검증 권장.
- raw §Gaps의 cognitive core 완전 spec → Engine A의 "context as RAM"의 일부 매핑(matryoshka, reasoning dial)이 부분적. agent에서 깊게 다루지 않음.
- raw §Gaps의 Korean reception 부정 → Engine B의 "agent first-class consumer"가 한국 백엔드 커뮤니티에서 얼마나 수용·반박되는지 자료 부족. 운영 중 application log에 모니터링.
