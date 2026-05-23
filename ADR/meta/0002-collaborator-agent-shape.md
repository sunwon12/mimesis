# ADR meta-0002: 거장 페르소나를 "단일 진단 스킬"이 아닌 "상주 협업 에이전트"로 도입

- **Status**: Proposed
- **Date**: 2026-05-23
- **Scope**: 레포의 figure 자산 shape 정책. `.claude/skills/`와 `.claude/agents/`의 역할 분리, 카탈로그 분류, 파이프라인 종착점에 영향.
- **Affected skills / files**:
  - 신규(예정): `.claude/agents/<figure>.md` — 거장 페르소나 에이전트의 본체 (~~`figures/<figure>.md`~~ — Erratum 참조)
  - 신규(예정): `.claude/skills/<figure>/SKILL.md` — agent로의 진입점 스킬 (얇음)
  - 수정(예정): `README.md` — 카탈로그 표에 shape 컬럼 추가, 사용 흐름에 협업자 분기 추가
  - 수정(예정): `.claude/agents/` 디렉토리 구조 — ~~기존 파이프라인 에이전트와 figure 페르소나 에이전트를 하위로 분리 (`pipeline/` vs `figures/`)~~ → **평면 유지 + 네이밍 컨벤션으로 구별** (Erratum 참조)
  - 영향: 파이프라인 종착점(`skill-builder`) — 결과물이 항상 SKILL.md라는 가정이 깨짐. agent.md를 만드는 분기 필요(별도 ADR 후속 가능)

## Erratum — 2026-05-23 (작성 당일)

본 ADR 작성·실행 직후 발견된 기술적 제약으로 §1(디렉토리 재구조 부분)이 폐기됨.

**제약**: Claude Code의 subagent 디스커버리는 `.claude/agents/`의 **top-level `.md` 파일만** 스캔한다. `.claude/agents/figures/ogilvy.md` 같은 nested 경로는 디스커버리되지 않는다 (공식 docs 확인: "Each subagent is a single `.md` file at the project or personal `.claude/agents/` directory" — code.claude.com/docs/en/sub-agents.md).

**영향**:
- 본 ADR §Decision의 §2 ("디렉토리 구조") 가 무효. 기존 3개 pipeline agent를 `pipeline/`으로, figure agent를 `figures/`로 분리하려던 계획 폐기.
- `.claude/agents/figures/ogilvy.md` 는 `.claude/agents/ogilvy.md` 로 즉시 이동 완료.
- `.claude/skills/<f>/SKILL.md` 는 본래부터 표준 패턴(skill당 1폴더)이라 영향 없음.

**대안 결정 — 네이밍 컨벤션으로 두 종류를 구별**:
- pipeline agent: `researcher.md`, `summarizer.md`, `skill-builder.md` (역할 기술어 — 공통 명사)
- figure agent: `ogilvy.md`, `munger.md`, ... (figure 이름 — 고유 명사)
- figure-anchored 네이밍 메모리 룰이 이미 이 구별을 강제하고 있어, 네이밍 컨벤션 추가 비용은 없음.
- 본문 아래의 §Decision §2, §Migration notes의 디렉토리 재구조 항목, §Consequences의 "위치 비대칭" 항목은 본 Erratum에 의해 모두 무효. 다른 부분(shape 분기 정책, hybrid 패턴, 카탈로그 shape 컬럼 등)은 그대로 유효.

이 Erratum은 ADR의 사고 흐름 자체를 무효화하지 않는다 — *figure 자산을 두 shape으로 분기한다*는 본 ADR의 본질 결정은 그대로. *어떻게 물리적으로 분리하느냐*만 디렉토리 → 네이밍으로 바뀜.

## Context

기존 mimesis의 모든 figure 자산은 **단일 진단 스킬(diagnostic skill)** shape이다:

- 입력: 사용자 발화 한 덩어리
- 처리: 거장의 한 사고 동작을 procedure로 실행 (4원인 분해, freshman test, having↔being 진단 등)
- 출력: 한 번의 응답
- 상태: 무상태. 한 turn으로 종결.

이 shape은 0001~0006 모든 ADR의 암묵 전제였다. 그러나 새 거장 후보군을 들이는 과정에서 다른 형태의 요구가 표면화됐다.

### 표면화된 요구

브랜딩·마케팅 영역의 거장(David Ogilvy)을 검토하던 중, 사용자가 원한 사용 패턴이 기존 진단 스킬과 다른 모양임을 확인했다:

> "그 거장과 함께 일을 한다는 개념으로 그 스킬을 계속 호출하면 답을 구하거나 대화를 하거나 일을 시킬 것 같아"

이 요청에는 세 가지 차이가 있다:

1. **다중 모드** — 한 거장 안에서 카피 리뷰 / 네이밍 평가 / 포지셔닝 검증 / 빅 아이디어 진단 / 캠페인 브리핑이 모두 하나의 인격으로 묶여야 한다. 진단 스킬처럼 "한 동작"으로 환원되지 않는다.
2. **지속 대화** — "이 카피 어때 → 고쳤어 → 다시 봐줘 → 헤드라인은 어떻게 → 그럼 이건"의 멀티턴 협업. 한 turn으로 종결되지 않는다.
3. **인격 일관성** — 사용자가 "함께 일한다"고 느끼려면 voice·태도·기준이 모든 turn에 걸쳐 동일해야 한다. main Claude의 기본 voice와 섞이면 페르소나가 깨진다.

이 세 차이는 자료(Ogilvy의 책·메모·인터뷰)에서 추출되는 사고 동작의 문제가 아니라 — **결과물의 shape이 다른 종류**라는 의미다.

### 왜 skill로는 부족한가

Claude Code의 skill은 본질적으로 **main 세션에 procedure를 얹는 것**이다. 그래서 거장 페르소나를 skill로 구현하면 다음이 일어난다:

- **Voice 오염**. main 세션엔 CLAUDE.md, 다른 스킬, 시스템 reminder, 메모리가 동시에 떠 있다. "Ogilvy로 답하라"는 지시는 매 turn 이 모든 신호와 경쟁한다. 페르소나가 빠르게 옅어진다.
- **상태 부재**. skill은 호출 시 procedure를 얹지만, 다음 turn에서 자동으로 재발화되지 않는다. 멀티턴 협업을 위해서는 사용자가 매번 재호출하거나 description의 auto-trigger에 의존해야 하는데, 이는 master-router 도입의 동기였던 트리거 표면 충돌을 정확히 다시 키운다.
- **모드 분기의 비대화**. 한 거장 안에 5~7개 작업 모드를 procedure로 박으면 SKILL.md 본문이 진단 스킬의 3~5배가 된다. 본문은 트리거 시에만 로드되니 토큰 비용은 아니지만, **단일 진단 스킬과 같은 카탈로그 행에 있으면 사용자가 같은 도구로 오해한다**.

### 왜 agent shape이 더 맞나

Claude Code의 agent는 **독립 인스턴스**다 — 자기 system prompt, 자기 context window, 자기 voice. 페르소나를 깨끗하게 격리할 수 있다.

- **Voice 순도**. agent의 system prompt만이 인격을 정의한다. main 세션의 다른 신호와 섞이지 않는다.
- **상태 유지**. SendMessage 패턴으로 같은 agent에게 연속 호출이 가능하다. "이 카피 → 다시 봐줘 → 헤드라인은"의 흐름이 한 인격 안에서 보존된다.
- **모드 분기의 자연성**. agent는 본질적으로 multi-step. 모드 분기를 system prompt + 첫 turn 인테이크로 처리하면 진단 스킬보다 자연스럽다.
- **mimesis의 본래 의도와 부합**. "거장과 함께 일한다"는 framing은 *다른 인격이 옆에 있다*는 감각을 요구한다. agent는 그걸 문자 그대로 구현한다 — mimesis(모방)의 의미와 정합.

### 함정

그러나 사용자는 항상 **main 세션**에 타이핑한다. agent에 직접 말할 수 없다. 그래서 흐름은 항상:

```
사용자 → main Claude → SendMessage → 거장 agent → 답 → main이 relay
```

매 turn "거장한테 이거 물어봐줘"를 명시하는 건 마찰. 그러므로 진입 트리거와 라우팅 규칙이 main Claude 측에 있어야 하고, 이건 결국 **얇은 skill**이 자연스럽다.

### 왜 meta-ADR인가

이 결정은 Ogilvy 한 명을 어떻게 해체할지의 문제가 아니다. 다음을 결정한다:

- figure 자산은 두 shape — **diagnostic skill** 과 **collaborator agent** — 으로 분기한다
- 각 shape마다 디렉토리·진입점·카탈로그 표현이 다르다
- 신규 거장을 들일 때 어느 shape인지 먼저 정해야 한다 (Ogilvy는 collaborator, Aristotle/Feynman은 diagnostic, Munger는 검토 필요)
- 파이프라인(researcher → summarizer → skill-builder)의 종착점이 항상 SKILL.md라는 가정이 깨진다

그래서 `skills/`가 아니라 `meta/`. 그리고 master-router(meta-0001) 다음 마일스톤이다.

## Options considered

### Option A — Diagnostic skill shape에 욱여넣기

협업 요구를 무시하고 Ogilvy도 단일 진단 스킬로 만든다.

- **장점**: 기존 shape·디렉토리·파이프라인을 그대로 쓴다. 카탈로그 분류가 단순.
- **단점**:
  - 5~7개 모드를 한 SKILL.md procedure로 박으면 본문이 비대해진다.
  - Voice 오염 문제는 해결되지 않는다 — main 세션의 다른 신호와 항상 경쟁.
  - 사용자가 원한 "함께 일한다"의 감각이 구조적으로 불가능. skill은 한 turn에 한 동작.
  - 멀티턴 대화를 시뮬레이션하려면 결국 description의 auto-trigger에 의존 → master-router 도입 동기와 충돌.
- **결론**: 기각. 요구의 본질을 부정하는 선택.

### Option B — Pure agent (skill 진입 없음)

`.claude/agents/ogilvy.md` 하나만 두고, 사용자가 매번 Agent 도구 호출 또는 SendMessage로 직접 의사소통.

- **장점**:
  - 가장 순수한 격리. main 세션과 완전 분리.
  - 카탈로그·skill 디렉토리에 흔적 없음. 표면 충돌 zero.
- **단점**:
  - 진입 마찰이 크다. 사용자가 "Agent 도구로 ogilvy를 spawn"을 매번 의식해야 한다.
  - main Claude가 "지금 ogilvy를 부르세요"를 트리거할 신호가 없다 — skill의 description이 그 역할을 했는데, 그걸 없앤 셈.
  - 사용자 입장에서 "다른 figure는 `/lee-eo-ryeong` 같이 명시 호출하는데 ogilvy만 다른 방식"이라는 일관성 결손.
- **결론**: 기각. 격리의 가치는 살리지만 진입점 부재가 너무 큰 비용.

### Option C — Hybrid: 얇은 진입 skill + 본체 agent

`.claude/skills/<figure>/SKILL.md` 는 진입점만 정의(명시 호출에만 반응, 본문은 "agent를 spawn하거나 기존 세션에 SendMessage"의 라우팅). 본체는 `.claude/agents/<figure>.md`.

- **장점**:
  - 사용자 진입 UX는 진단 스킬과 동일 — `/ogilvy` 호출.
  - 페르소나는 agent의 system prompt에 깨끗하게 격리.
  - 카탈로그 표에서도 일관되게 한 행 = 한 거장.
  - skill description은 인물명·고유 개념 명시 호출에만 반응하도록 좁혀, master-router 정책(meta-0001)과 정합.
  - 미래에 같은 거장의 다른 method가 추가될 때(예: `ogilvy-positioning` vs `ogilvy-copy-review`) 진단 vs 협업 shape이 같은 카탈로그 안에서 공존 가능.
- **단점**:
  - 자산 두 곳에 분산. 한 거장이 skill + agent 두 파일을 가진다. 관리 표면이 늘어남.
  - main Claude가 SendMessage를 정확히 라우팅하는지에 진입 신뢰성이 걸린다. 진입 skill의 본문이 빈약하면 main이 agent를 호출 안 하고 자기가 답하는 사고가 발생할 수 있음.
  - 파이프라인(skill-builder)의 종착점이 SKILL.md 한 종류라는 가정이 깨진다 — collaborator는 agent.md도 만들어야 함. 후속 ADR로 파이프라인 갱신 필요.
- **결론**: 선택. 이유는 Decision 참조.

### Option D — Sub-skill 분해 (모드별 개별 skill)

Ogilvy의 5~7개 모드를 각각 별개 skill로 만든다 (`ogilvy-copy-review`, `ogilvy-positioning`, `ogilvy-big-idea-diagnosis`, ...).

- **장점**: 기존 shape 그대로 유지. 각 skill이 진단 단위로 작고 명확.
- **단점**:
  - "함께 일한다"의 감각이 완전히 사라진다. 매 작업마다 다른 skill을 명시 호출해야 함.
  - figure-anchored 네이밍 룰의 압력 — 한 거장에 5~7개 skill이 붙으면 카탈로그가 불균형해진다(다른 거장은 1~2개인데).
  - master-router의 후보 풀이 인물 단위가 아니라 모드 단위로 폭증.
  - 같은 거장의 모드 간 voice 일관성을 보장할 메커니즘이 없음 (각 skill이 독립).
- **결론**: 기각. 협업 요구의 핵심(인격의 연속성)을 분해로 잃는다.

## Decision

**Option C(Hybrid)**를 선택한다. 구체 형태:

### 1) figure 자산은 두 shape으로 명시 분기

각 거장을 들이기 전에 다음 질문으로 shape을 정한다:

> **"이 거장과 같은 작업을 여러 모드·여러 turn에 걸쳐 반복하는가, 아니면 한 사고 동작을 한 번 빌리는가?"**

| Shape | 언제 | 예 |
|---|---|---|
| **Diagnostic skill** | 한 사고 동작 1턴. 무상태. | Aristotle 4원인, Feynman freshman test, Fromm having↔being |
| **Collaborator agent** | 다중 모드 + 멀티턴 + 페르소나 일관성. | Ogilvy (브랜딩·카피), 검토 후보: Hemingway(글쓰기 협업), Jobs(제품 평가) |

shape 판단이 모호하면 default는 diagnostic skill — agent는 인격 일관성이 본질적으로 요구될 때만.

### 2) 디렉토리 구조 (Erratum 적용 후 — 평면 + 네이밍 컨벤션)

```
.claude/
├── agents/                      # 평면 유지 — Claude Code가 top-level만 스캔
│   ├── researcher.md                # pipeline (역할 기술어 — 공통 명사)
│   ├── summarizer.md                # pipeline
│   ├── skill-builder.md             # pipeline
│   └── <figure-name>.md             # ★ figure 페르소나 (figure 이름 — 고유 명사)
└── skills/
    ├── master-router/
    └── <figure-name>/           # diagnostic이면 procedure, collaborator면 얇은 진입점
        └── SKILL.md
```

> **변경 사유**: 본 ADR 최초 작성 시 `pipeline/` + `figures/` 두 하위 디렉토리로 분리할 계획이었으나, 디스커버리 제약(top-level만 스캔)으로 폐기. Erratum 참조. 두 종류의 구별은 figure-anchored 네이밍 메모리 룰이 이미 강제하는 *고유명사 vs 역할 기술어* 컨벤션이 흡수.

~~기존 `.claude/agents/` 평면 구조를 `pipeline/`과 `figures/`로 분리. 두 종류의 에이전트가 한 디렉토리에 섞이면 역할이 흐려진다.~~ → Erratum: 디스커버리 제약으로 폐기. 두 종류의 구별은 *고유명사 vs 역할 기술어* 네이밍 컨벤션이 흡수.

### 3) Collaborator agent의 구성 요소 (system prompt 골격)

agent.md는 다음을 명시한다:

1. **인격 정의** — voice, 태도, 비-타협 원칙 5~7개. 1차 자료에서 추출한 인용으로 뒷받침.
2. **인테이크 프로토콜** — 첫 turn에 항상 묻는 고정 질문 세트. 예: Ogilvy는 "누가 고객? 단 하나의 약속? 증거?" 3가지.
3. **모드 분기** — 들어오는 작업 타입 인식 규칙. 각 모드의 고유 procedure.
4. **푸시백 의무** — "어때?"에 칭찬으로 답하지 않는다. 비-타협 원칙으로 회의한다.
5. **종료 조건** — 어떤 신호가 들어오면 협업을 종료하고 main으로 돌려보내는가.

### 4) 진입 skill의 구성 요소 (얇음)

SKILL.md는 다음만 정의:

1. **트리거** — 인물명·고유 개념 명시 호출에만 반응 (예: "오길비", "Ogilvy", "Big Idea", "permission marketing"이면 Seth Godin 등).
2. **라우팅 규칙** — "현재 세션에 같은 figure의 agent가 살아있는지 확인 → 있으면 SendMessage, 없으면 spawn".
3. **main의 역할** — 진입 후 main Claude는 사용자 입력을 agent로 relay하는 통로 역할. 자기가 답하지 않는다.
4. **종료 트리거** — 사용자가 명시적으로 "다른 거장 부르자" / "ogilvy 모드 끝" 같은 신호를 보내면 relay 종료.

진단 스킬의 SKILL.md는 평균 700~1500자였다. 진입 skill은 200~400자 수준으로 의도적으로 얇게 둔다 — 본체는 agent다.

### 5) 카탈로그 표에 shape 컬럼 추가

기존 표 컬럼: 거장 · 스킬 · 한 줄 · 쓰면 뭐가 좋은가
신규 컬럼: **shape** (diagnostic / collaborator)

사용자가 "이 행은 어떤 모양의 도구인가"를 한눈에 본다. master-router는 `meta`로 표기.

### 6) 파이프라인 종착점 갱신 — 후속 ADR로 분리

기존 `skill-builder` agent는 종착점이 항상 `SKILL.md + ADR`였다. Collaborator인 경우 종착점이 `agent.md + 얇은 SKILL.md + ADR` 세 파일이다. 이 갱신은 다음 중 하나:

- **6-A**: `skill-builder`에 shape 분기 추가 (한 agent가 두 종착점 모두 만듦)
- **6-B**: `collaborator-builder` agent 별도 신설 (skill-builder는 diagnostic 전용으로 좁힘)

이 결정은 첫 collaborator(Ogilvy)를 실제 파이프라인으로 만들 때 검증 후 후속 ADR로 박는다. 본 ADR에서는 분기 가능성만 명시하고 결정 보류.

## Consequences

- **Positive**:
  - 거장 페르소나의 voice 순도가 격리로 보장됨. main 세션의 다른 신호와 경쟁하지 않음.
  - 멀티턴 협업 요구를 자연스럽게 처리. SendMessage 패턴이 그 자체로 적합한 abstraction.
  - 카탈로그에 shape 컬럼이 명시되어 사용자가 "이 도구는 어떻게 쓰는 도구인가"를 한눈에 안다.
  - 진단 스킬과 협업 에이전트가 한 레포 안에 공존할 수 있는 정책 기반이 생긴다 — 향후 figure 다양성이 늘어도 카탈로그가 일관되게 분류됨.
  - master-router의 정책(인물명·고유 개념 명시 호출, ambiguous는 라우터 경유)과 정합 — collaborator도 같은 트리거 규칙을 따르므로 라우터 description을 거의 안 만져도 됨.

- **Negative / Trade-offs**:
  - **자산 분산**. 한 거장이 `.claude/skills/<f>/`와 `.claude/agents/<f>.md` 두 위치에 흩어진다. 관리·갱신 시 짝을 의식해야 함.
  - **진입 신뢰성 의존**. main Claude가 진입 skill의 라우팅 규칙대로 agent에 relay하지 않고 자기가 답하는 사고가 가능. 진입 skill 본문에 "main은 답하지 않는다"를 강하게 박아도 모델의 자기-답변 경향이 0이 아님.
  - **파이프라인 복잡도 증가**. skill-builder의 종착점이 두 종류가 된다. 후속 ADR로 처리 보류했지만, 첫 collaborator를 만들 때 실제 마찰로 표면화될 가능성.
  - **shape 판단의 모호함**. "Munger Latticework는 진단인가 협업인가?" 같은 경계 사례. shape 판단 기준을 더 정교화해야 할 수 있음.
  - **카탈로그 비대칭의 위험**. 현재 카탈로그 7행은 전부 diagnostic. collaborator가 추가되면 표에서 시각적으로 이질적이라 "왜 다른 모양인가" 설명을 README에서 한 단락 더 들여야 함.
  - ~~**`.claude/agents/` 디렉토리 재구조의 부수 영향**. 기존 pipeline 에이전트 3개를 `pipeline/` 하위로 이동해야 함.~~ → Erratum: 디스커버리 제약으로 디렉토리 재구조 자체가 폐기. 이 trade-off는 사라짐. 대신 figure agent와 pipeline agent가 같은 평면에 공존하는 *시각적 비대칭*이 새 trade-off (네이밍 컨벤션이 의미적으로는 흡수하나, 디렉토리 listing에서는 한 줄로 섞임).

- **Open questions**:
  - 진입 skill에서 main이 자기-답변하는 사고를 막는 가장 신뢰성 있는 표현은 무엇인가. 첫 collaborator 적용 후 검증.
  - 같은 거장이 diagnostic + collaborator 양쪽 shape을 가질 수 있는가 (예: Ogilvy의 "Big Idea 진단"을 진단 스킬로, 전체 협업을 agent로). 가능하다면 figure-anchored 네이밍 룰을 어떻게 확장하는가.
  - SendMessage로 살아있는 agent를 식별하는 신뢰성 — 같은 세션 안에서 두 번째 호출이 정확히 첫 번째 agent에 닿는지.
  - Collaborator agent 안에서 모드 분기를 system prompt에 박을지, 첫 turn 인테이크에서 결정할지 — 두 방식의 voice 일관성 차이 검증.
  - 협업이 길어졌을 때 agent context window 한계 도달 시 어떻게 자연스럽게 종료·요약하는가.

## Migration notes

이 ADR은 Proposed 단계 — 실제 적용은 첫 collaborator(Ogilvy) 파이프라인 가동 시점에 동반된다. 그 시점에 일괄 수행할 작업:

1. ~~**디렉토리 재구조**~~ → Erratum: 폐기. 평면 + 네이밍 컨벤션으로 대체:
   - 기존 pipeline agent(`researcher.md`, `summarizer.md`, `skill-builder.md`)는 평면 그대로.
   - 신규 figure agent는 `.claude/agents/<figure>.md` 평면에 추가.
   - 디렉토리 이동 없음 — 상호 참조 경로 갱신도 없음.
2. **README 갱신**:
   - 카탈로그 표에 shape 컬럼 추가, 기존 7행은 모두 `diagnostic` 표기
   - 사용 흐름에 collaborator 분기 추가 — "막막함 → router → 거장 추천" 흐름은 동일하되 호출 후 거동이 다르다는 점을 명시
   - 디렉토리 구조 다이어그램 갱신
3. **신규 ADR**:
   - `ADR/meta/0003-pipeline-shape-branching.md` (가칭) — skill-builder의 종착점 분기 결정. 6-A vs 6-B 중 선택.
   - `ADR/skills/0007-ogilvy-...md` — 첫 collaborator의 해체 기록. shape: collaborator 명시.
4. **기존 7개 skill은 손대지 않는다** — diagnostic shape으로 이미 일관. 카탈로그 표의 shape 컬럼만 채우면 충분.

## Application log

- TBD — 첫 collaborator(Ogilvy) 적용 후 갱신. 특히 다음 일곱 가지를 기록한다:
  1. 진입 skill 호출 후 main Claude가 정확히 agent로 relay하는 비율. 자기-답변 사고 발생 빈도.
  2. 동일 세션 내 두 번째 호출이 같은 agent에 닿는지(SendMessage 신뢰성).
  3. Agent의 voice가 멀티턴에 걸쳐 일관 유지되는지, 어디서 옅어지는지.
  4. 모드 분기가 첫 turn 인테이크에서 자연스럽게 결정되는지, system prompt에 박힌 분기 규칙이 작동하는지.
  5. 사용자가 협업 종료를 어떻게 신호하는지, 종료 후 main으로의 복귀가 깔끔한지.
  6. 진단 스킬과 협업 에이전트가 같은 카탈로그에 공존했을 때 사용자가 두 shape을 헷갈리지 않는지.
  7. shape 판단 기준("다중 모드 + 멀티턴 + 페르소나 일관성")이 경계 사례(Munger, Naval, Jobs)에서 명료하게 작동하는지.
