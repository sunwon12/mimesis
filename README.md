# mimesis

> μίμησις — 모방은 학습의 가장 오래된 형태다.

대표 인물의 사고방식과 삶의 태도를 **Claude Code 스킬**로 체화하기 위한 개인 저장소.

## 왜 만들었는가

읽고 감탄하는 것에서 멈추면 아무것도 남지 않는다.
거장의 사고 골격을 **실행 가능한 스킬**로 옮겨, 내가 일·생각·글에 막힐 때마다 호출할 수 있게 만든다.

- **사고법(How they think)** — 맥킨지식 문제 정의, 파인만의 학습법, 찰리 멍거의 멘탈 모델
- **태도(How they live)** — 이어령의 지적 호기심, 스티브 잡스의 단순함, 세네카의 평정
- **작업법(How they work)** — 헤밍웨이의 글쓰기 루틴, 다 빈치의 노트, 폰 노이만의 문제 분해

## 스킬 카탈로그

거장 1명 = 스킬 1개를 원칙으로 하되, 같은 거장의 *다른 method*는 별도 스킬로 가른다 (예: `aristotle-phronesis` vs `aristotle-causal-why`).

**Shape**: 같은 카탈로그 안에 두 종류가 공존한다 — `diagnostic`(한 사고 동작을 1턴 procedure로 실행, `.claude/skills/<figure>/SKILL.md` 한 장이 본체) / `collaborator`(한 인격을 멀티턴·다중 모드로 협업, SKILL.md는 진입점이고 본체는 `.claude/agents/<figure>.md` agent). 자세한 분기 근거는 [`ADR/meta/0002-collaborator-agent-shape.md`](ADR/meta/0002-collaborator-agent-shape.md).

**왜 두 shape으로 갈랐는가 — 모두 agent로 통일하지 않은 이유**: figure 중 일부는 "사람"이 아니라 *사고 패턴*이다. 맥킨지는 사람도 아니고, "MECE로 쪼개줘"는 누구와 대화하는 게 아니라 동작을 부르는 거다. diagnostic figure(맥킨지·아리스토텔레스·파인만·이어령·프롬)를 agent로 의인화해 감싸면 "MECE가 뭔지 설명해드리겠습니다" 식으로 *동작 실행*이 *개념 설명*으로 변질될 위험이 있다 — 1턴 procedure로 끝나야 할 게 페르소나 대화로 변형됨. 반대로 collaborator figure(오길비, 향후 멍거·드러커 등)는 voice·취향·기억이 *그 자체로 가치*라 멀티턴이 본질 — "이 카피 → 다시 봐줘 → 헤드라인은"의 흐름이 한 인격 안에서 보존되어야 한다. 즉 어떤 shape인지는 "이 figure가 *동작*인가, *판단하는 사람*인가"로 갈린다. 새 거장을 들이기 전 shape부터 정한다.

| 거장 | 스킬 | Shape | 한 줄 | 쓰면 뭐가 좋은가 |
|---|---|---|---|---|
| — (메타) | [`master-router`](.claude/skills/master-router/) · [ADR](ADR/meta/0001-master-router.md) | meta | 거장 스킬 추천 라우터 | 막막한데 어느 인물·개념도 명시 못 할 때, 1~3명 후보를 "왜 이 상황에 맞는가"와 함께 추천받는다. |
| 이어령 | [`lee-eo-ryeong-questioning`](.claude/skills/lee-eo-ryeong-questioning/) · [ADR](ADR/skills/0001-lee-eo-ryeong-questioning.md) | diagnostic | 정문(正問) — 통설을 한 번 뒤집어 의미를 재정의 | 카피·키노트·리브랜딩·문제 재정의처럼 "다들 이렇게 말하는데"의 프레임 자체를 흔들고 싶을 때. |
| 에리히 프롬 | [`erich-fromm-having-vs-being`](.claude/skills/erich-fromm-having-vs-being/) · [ADR](ADR/skills/0002-erich-fromm-having-vs-being.md) | diagnostic | Having vs Being 모드 진단 | 학습·관계·소비·자기소개가 "가지는 자세"로 흐를 때, 같은 활동을 동사·과정·관계 중심으로 재구성한다. |
| 맥킨지 | [`mckinsey-structured-problem-solving`](.claude/skills/mckinsey-structured-problem-solving/) · [ADR](ADR/skills/0003-mckinsey-structured-problem-solving.md) | diagnostic | MECE 이슈 트리 + 가설 + Pyramid·SCQA | 모호하고 큰 비즈니스/제품/정책 문제를 한 시간 안에 답하고 임원·투자자에게 전달해야 할 때. |
| 아리스토텔레스 | [`aristotle-phronesis`](.claude/skills/aristotle-phronesis/) · [ADR](ADR/skills/0004-aristotle-phronesis.md) | diagnostic | Phronesis — 보편 원칙의 평균 가정이 빗나가는 개별 상황 진단 | 베스트프랙티스·SOP대로 했는데 이 사람·이 시점·이 맥락에선 어색할 때, 행위 한 가지로 다시 짠다. |
| 아리스토텔레스 | [`aristotle-causal-why`](.claude/skills/aristotle-causal-why/) · [ADR](ADR/skills/0005-aristotle-causal-why.md) | diagnostic | 4원인 + archē — "왜?"를 두 축으로 끝까지 추궁 | 5 Whys가 작용인 한 갈래로 수렴해 답답하거나, 머스크식 first principles가 질료인만 분해하고 멈췄을 때. |
| 리처드 파인만 | [`feynman-explaining-to-understand`](.claude/skills/feynman-explaining-to-understand/) · [ADR](ADR/skills/0006-feynman-explaining-to-understand.md) | diagnostic | 이해 자기-감사 — 이름 벗기기 + Brazil-bay 적용 + freshman 환원 | 공부한 직후 "이거 진짜 안 거 맞나" 의심이 들 때, fluent한 설명이 cargo-cult(형식만 완벽·메커니즘 부재)인지 까발린다. |
| 데이비드 오길비 | [`ogilvy`](.claude/skills/ogilvy/) + [agent](.claude/agents/ogilvy.md) · [ADR](ADR/skills/0007-ogilvy.md) | **collaborator** | 브랜드·광고·카피의 ongoing 협업 — 6개 모드(인테이크/카피/네이밍·포지셔닝/Big Idea/캠페인/헤드라인)를 한 인격으로 | "이 카피 어때 → 고쳤어 → 다시 봐줘"의 멀티턴 협업이 필요할 때. 진단 1턴이 아니라 default pushback voice로 함께 일하고 싶을 때. |

> **Collaborator shape 주의**: `ogilvy` 스킬은 본체가 아니라 진입점이다. `.claude/agents/ogilvy.md` agent와 짝으로 가져가야 작동한다. 진단 스킬은 SKILL.md 하나만 복사하면 되지만, collaborator는 두 파일 + ADR이 한 묶음.

### 예정

- [ ] 찰리 멍거 — Latticework of Mental Models (diagnostic)
- [ ] 스티브 잡스 — 단순함의 미학 (shape 검토 필요)
- [ ] 나발 라비칸트 — 부와 행복의 원리 (diagnostic)

## 어떻게 가져다 쓰는가 (왜 Claude Code 플러그인이 아닌가)

mimesis는 **Claude Code 플러그인으로 배포하지 않는다.** 마음에 드는 거장 스킬만 골라서 너의 작업 레포 `.claude/skills/` 로 복사해 써라.

이유 — Claude Code의 스킬 로딩 모델:

| 레벨 | 무엇 | 언제 로드 |
|---|---|---|
| 1 | frontmatter (`name` + `description`) | **항상** 모든 세션 context에 상주 |
| 2 | SKILL.md 본문 | 스킬 트리거 시에만 |
| 3 | references/scripts/assets | 본문이 가리킬 때만 |

플러그인은 설치 즉시 그 안의 모든 스킬 metadata가 사용자 모든 세션의 context에 들어간다. mimesis의 거장 스킬은 자연어 트리거를 잡으려고 description에 한국어 표현을 길게 박는 구조라(평균 700~1500자, 영어 일반 스킬의 ~3~5배), 10명 로스터 시점에는 그 거장을 안 부르는 세션에도 수천 자가 메타데이터로 상주한다.

토큰 비용 자체는 catastrophic하지 않지만 — figure-anchored 컨셉상 더 중요한 비용은 **트리거 매핑의 추론 부담**이다. 후보 풀이 클수록 모델이 매 발화마다 "어느 스킬 영역인가"를 더 큰 공간에서 골라야 한다 (master-router를 도입한 이유와 같은 압력).

게다가 mimesis의 본래 의도는 결과가 아니라 **거장 사고를 자기 것으로 만드는 것**이다. "전부 설치하고 가끔 쓰기"보다 "고른 거장만 들이고 자주 쓰기"가 figure-anchored 학습 방식과 맞물린다.

### 권장 사용 방식

1. 위 [스킬 카탈로그](#스킬-카탈로그)에서 자기에게 울림이 있는 거장 1~3명을 고른다.
2. 이 레포의 `.claude/skills/<figure-name>/` 디렉토리만 자기 작업 레포의 `.claude/skills/` 아래로 복사한다. 짝이 되는 `ADR/skills/NNNN-<figure-name>.md` 도 같이 가져가면 "왜 이렇게 잘랐는가"의 사고 흐름까지 들이는 셈.
3. 라우터(`master-router/`)는 거장 2명 이상부터 같이 가져가면 트리거 충돌이 줄어든다. 한 명만 쓰는 시기엔 불필요.
4. 나중에 한 명이 더 필요해지면 그때 추가한다.

> **참고**: skill description이 모든 세션에 상주한다는 점은 Claude Code의 [공식 skill 로딩 문서](https://code.claude.com/docs/en/skills.md)에서 확인. 플러그인 vs 복사에 대한 직접적인 공식 가이드는 없지만, 이 레포는 figure-anchored 학습 철학에 맞춰 후자를 권장한다.

## 사용 흐름 (권장)

거장 스킬이 늘수록 각 스킬의 description 트리거 표면이 겹쳐서, "지금 이 상황엔 누구를 부르지?"가 흐려진다.
그래서 이 레포는 **추천 라우터를 한 번 거치는 것**을 디폴트 흐름으로 둔다:

```
상황 막막함
    │
    ▼
master-router            ─►  진단 + 후보 거장 1~3명 + "왜 이 인물이 이 상황에 맞는가"
    │
    ▼
사용자가 직접 명시 호출   ─►  예: "프롬으로 진단해줘" / "이어령식 정문으로 풀어줘" / "맥킨지로 구조화"
    │
    ▼
거장 스킬 발화
```

**왜 자동 호출이 아닌가**:
- 라우터가 추천 후 그 스킬을 자동으로 호출하면 사용자는 결과만 받고, "왜 이 거장이 이 상황의 거울인가"의 매핑을 놓친다.
- mimesis의 본래 의도는 결과가 아니라 **거장 사고를 자기 것으로 만드는 것**이다. 한 박자 의식적으로 고르는 행위가 학습 그 자체.
- 자주 쓰는 거장은 사용자가 라우터를 거치지 않고 곧장 명시 호출하게 된다 — 라우터는 점점 안 부르는 게 정상이다.

**라우터를 건너뛰어도 되는 경우**:
- 인물명/고유 개념을 이미 알고 있을 때 ("프롬", "MECE", "정문(正問)" 등 직접 호출).
- 코드/조회/실행 같은 거장 스킬과 무관한 작업.

자세한 설계 근거는 [`ADR/meta/0001-master-router.md`](ADR/meta/0001-master-router.md).

## 디렉토리 구조

```
mimesis/
├── .claude/
│   ├── agents/                 # Claude Code는 top-level만 스캔 — 평면 필수
│   │   ├── researcher.md           # pipeline 1단계 — 1차 자료 수집 (역할 기술어)
│   │   ├── summarizer.md           # pipeline 2단계 — 사고 해부도 작성 (역할 기술어)
│   │   ├── skill-builder.md        # pipeline 3단계 — diagnostic SKILL.md + ADR (역할 기술어)
│   │   └── <figure-name>.md        # ★ collaborator agent 본체 — figure 페르소나 (고유 명사)
│   └── skills/                 # 실행 가능한 스킬 (Claude Code가 호출)
│       ├── master-router/          # ★ 거장 스킬 추천 라우터 (메타 스킬)
│       └── <figure-name>/          # 거장 1명 = 스킬 1개 (figure-anchored)
│           └── SKILL.md            # diagnostic은 procedure 본문, collaborator는 얇은 진입점
├── research/                   # 에이전트 중간 산출물
│   └── <figure-slug>/
│       ├── <topic>-raw.md
│       └── <topic>-summary.md
├── ADR/                        # 사고의 로그
│   ├── skills/                     # 거장 1명을 어떻게 해체했는가
│   │   └── NNNN-<figure>.md
│   └── meta/                       # 레포 전체를 어떻게 가꿀 것인가
│       └── NNNN-<topic>.md
└── README.md
```

> **`.claude/agents/` 평면 제약**: Claude Code의 subagent 디스커버리는 `.claude/agents/`의 top-level `.md` 파일만 스캔한다 (공식 docs: code.claude.com/docs/en/sub-agents.md). nested 서브디렉토리는 디스커버리되지 않으므로 `figures/` / `pipeline/` 같은 분리는 불가능. mimesis는 *figure 이름은 고유명사, pipeline 역할은 역할 기술어* 네이밍 컨벤션으로 두 종류를 구별한다. 자세한 근거는 [`ADR/meta/0002-collaborator-agent-shape.md`](ADR/meta/0002-collaborator-agent-shape.md) Erratum.

- **`.claude/agents/`** — 두 종류가 같은 평면에 공존. 역할 기술어(`researcher` / `summarizer` / `skill-builder`)는 파이프라인 단계, 고유명사(`ogilvy`, ...)는 collaborator shape의 페르소나 본체.
- **`.claude/skills/`** — figure-anchored 스킬. diagnostic shape은 SKILL.md 본문이 procedure 그 자체. collaborator shape은 SKILL.md가 얇은 진입점이고 본체는 `agents/<name>.md`. `master-router`만 메타 스킬로 figure-anchored 룰에서 면제.
- **`research/`** — raw 인용과 해부도. 스킬의 원재료이자 검증 추적용 사료.
- **`ADR/skills/`** — 한 거장을 어떻게 해체했는가의 기록. 인물 추가 순서대로 번호.
- **`ADR/meta/`** — 레포 전체의 아키텍처·정책·트리거 흐름에 대한 결정. 두 결의 ADR을 디렉토리로 분리해 서로의 노이즈가 되지 않게 한다.
  결과물(스킬)만 보면 "이미 정해진 답"처럼 보이지만, ADR이 있어야 **해체·구성한 사고 흐름** 자체가 또 하나의 자산이 된다.

## 파이프라인 (거장 → 스킬)

```
[figure + topic]
      │
      ▼
┌─────────────────┐    research/<f>/<t>-raw.md
│  researcher     │  ─────────────────────────►  (1차 인용 + 출처)
└─────────────────┘
      │
      ▼
┌─────────────────┐    research/<f>/<t>-summary.md
│  summarizer     │  ─────────────────────────►  (재현 가능한 절차)
└─────────────────┘
      │
      ▼
┌─────────────────┐    .claude/skills/<name>/SKILL.md
│  skill-builder  │  ─────────────────────────►  + ADR/skills/NNNN-<name>.md
└─────────────────┘
```

각 에이전트의 응답은 **작성한 파일 경로만** 반환한다 (터미널에 본문을 다시 찍지 않는다).
다음 에이전트는 그 경로를 입력으로 받아 이어간다.

## 작성 원칙

1. **요약하지 말고 해체하라** — "무엇을 말했는가"가 아니라 "어떤 구조로 사고했는가"를 스킬화한다.
2. **출처를 남겨라** — 원문/페이지/영상 타임스탬프. 검증되지 않은 명언은 받아들이지 않는다.
3. **스킬은 ADR과 짝으로** — 모든 스킬은 동일 번호의 ADR이 짝지어 존재한다.
4. **회의하라** — 거장도 틀린다. 동의하지 않는 지점은 ADR의 *Consequences*에 명시한다.

## 새 스킬 추가 절차

1. `ADR/skills/NNNN-<slug>.md` 작성 — **먼저 사고 과정을 남긴다**. 왜 이 스킬인가, 어떤 트리거에 호출되어야 하는가, 어떤 입출력 계약을 가지는가.
2. `.claude/skills/<skill-name>/SKILL.md` 작성 — ADR의 결론을 실행 가능한 형태로 옮긴다. description은 인물명·고유 개념 명시 호출에 반응하도록 좁히고, ambiguous한 상황은 `master-router`가 받도록 한 줄을 박는다.
3. 직접 사용해보고 ADR의 *Consequences*에 적용 결과를 추가한다.
4. 레포 전체 아키텍처에 손이 가는 결정이라면 `ADR/skills/` 가 아니라 `ADR/meta/`로 간다.
