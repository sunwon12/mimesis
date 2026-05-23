# mimesis

> μίμησις — 모방은 학습의 가장 오래된 형태다.

대표 인물의 사고방식과 삶의 태도를 **Claude Code 스킬**로 체화하기 위한 개인 저장소.

## 왜 만들었는가

읽고 감탄하는 것에서 멈추면 아무것도 남지 않는다.
거장의 사고 골격을 **실행 가능한 스킬**로 옮겨, 내가 일·생각·글에 막힐 때마다 호출할 수 있게 만든다.

- **사고법(How they think)** — 맥킨지식 문제 정의, 파인만의 학습법, 찰리 멍거의 멘탈 모델
- **태도(How they live)** — 이어령의 지적 호기심, 스티브 잡스의 단순함, 세네카의 평정
- **작업법(How they work)** — 헤밍웨이의 글쓰기 루틴, 다 빈치의 노트, 폰 노이만의 문제 분해

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

1. [인물 로스터](#인물-로스터-점진-추가)에서 자기에게 울림이 있는 거장 1~3명을 고른다.
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
│   ├── agents/              # 3단계 파이프라인 에이전트
│   │   ├── researcher.md       # 1차 자료 수집
│   │   ├── summarizer.md       # 사고 해부도 작성
│   │   └── skill-builder.md    # SKILL.md + ADR 생성
│   └── skills/              # 실행 가능한 스킬 (Claude Code가 호출)
│       ├── master-router/      # ★ 거장 스킬 추천 라우터 (메타 스킬)
│       └── <figure-name>/      # 거장 1명 = 스킬 1개 (figure-anchored)
│           └── SKILL.md     # frontmatter(name, description) + 본문
├── research/                # 에이전트 중간 산출물
│   └── <figure-slug>/
│       ├── <topic>-raw.md
│       └── <topic>-summary.md
├── ADR/                     # 사고의 로그
│   ├── skills/              # 거장 1명을 어떻게 해체했는가
│   │   └── NNNN-<figure>.md
│   └── meta/                # 레포 전체를 어떻게 가꿀 것인가
│       └── NNNN-<topic>.md
└── README.md
```

- **`.claude/agents/`** — 거장을 해체하는 3단계 파이프라인.
- **`.claude/skills/`** — 결과물. figure-anchored 스킬은 명시 호출되거나 라우터의 추천을 거쳐 발화한다. `master-router`만 메타 스킬로 figure-anchored 룰에서 면제.
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

## 인물 로스터 (점진 추가)

- [x] 이어령 — 지의 거인, 질문으로 사고하기 ([skill](.claude/skills/lee-eo-ryeong-questioning/) · [ADR](ADR/skills/0001-lee-eo-ryeong-questioning.md))
- [x] Erich Fromm — Having vs Being 모드 진단 ([skill](.claude/skills/erich-fromm-having-vs-being/) · [ADR](ADR/skills/0002-erich-fromm-having-vs-being.md))
- [x] McKinsey — 구조적 문제 해결 (MECE, Pyramid, SCQA) ([skill](.claude/skills/mckinsey-structured-problem-solving/) · [ADR](ADR/skills/0003-mckinsey-structured-problem-solving.md))
- [x] Aristotle — Phronesis (실천적 지혜) ([skill](.claude/skills/aristotle-phronesis/) · [ADR](ADR/skills/0004-aristotle-phronesis.md))
- [ ] Charlie Munger — Latticework of Mental Models
- [ ] Richard Feynman — 첫 원리적 사고와 학습법
- [ ] Steve Jobs — 단순함의 미학
- [ ] Naval Ravikant — 부와 행복의 원리

## 새 스킬 추가 절차

1. `ADR/skills/NNNN-<slug>.md` 작성 — **먼저 사고 과정을 남긴다**. 왜 이 스킬인가, 어떤 트리거에 호출되어야 하는가, 어떤 입출력 계약을 가지는가.
2. `.claude/skills/<skill-name>/SKILL.md` 작성 — ADR의 결론을 실행 가능한 형태로 옮긴다. description은 인물명·고유 개념 명시 호출에 반응하도록 좁히고, ambiguous한 상황은 `master-router`가 받도록 한 줄을 박는다.
3. 직접 사용해보고 ADR의 *Consequences*에 적용 결과를 추가한다.
4. 레포 전체 아키텍처에 손이 가는 결정이라면 `ADR/skills/` 가 아니라 `ADR/meta/`로 간다.
