# research/

`researcher` → `summarizer` 에이전트의 **중간 산출물** 저장소.
스킬을 만들기 전 거장의 사고를 raw → summary 두 단계로 정제한 결과가 인물별로 쌓인다.

## 구조

```
research/
└── <figure-slug>/
    ├── <topic>-raw.md       # researcher 산출물: 1차 자료 + 직접 인용
    └── <topic>-summary.md   # summarizer 산출물: 재현 가능한 절차로 해부
```

- `<figure-slug>` — 인물 이름 kebab-case (예: `charlie-munger`, `lee-eo-ryeong`).
- `<topic-slug>` — 토픽 kebab-case (예: `inversion`, `intellectual-curiosity`).
- 디렉토리가 없으면 `mkdir -p` 로 만든다.
- 동일 인물·토픽 raw가 이미 존재하면 덮어쓰지 말고 `-raw-v2.md` 처럼 버전 suffix를 붙인다.

## raw.md 템플릿 (researcher 산출물 SSOT)

researcher 에이전트가 작성하는 파일은 **반드시** 이 형식을 따른다.

```markdown
# Raw Research — <Figure>: <Topic>

- **Date**: YYYY-MM-DD
- **Assumptions** (입력 부족 시): ...
- **Search queries used**:
  - ...

## Primary sources
1. <제목> — <저자/매체>, <연도>
   - URL/ISBN: ...
   - 신뢰도: high | medium | low + 한 줄 이유
2. ...

## Quotes & evidence

### Q1
> "<원문 인용>"
>
> — <출처 + 정확한 위치 (페이지/타임스탬프/단락)>

**Context**: 어떤 상황에서 한 말인지 1–2문장.
**Translation (ko)**: <한글 번역, 원문이 한글이 아닐 때>

### Q2
...

## Critiques & limits (raw, 평가 금지)

> 거장의 프레임이 어디서 깨지는가 — 후속 단계가 스킬의 SKIP 조건·경계 조항을 짤 재료. "X가 더 낫다"는 판단 금지.

### C1
> "<반론 인용 원문>"
>
> — <반박자 + 출처 + 정확한 위치>

**Target**: 거장의 어떤 주장·프레임을 겨냥한 반박인지 1문장.
**Context**: 어떤 맥락에서 나온 반박인지 1–2문장.
**Translation (ko)**: <한글 번역, 원문이 한글이 아닐 때>

### C2
...

## Recurring observations (raw, 해석 금지)
- 여러 인용에서 반복되는 표현·구조·키워드만 기록. "그래서 핵심은 X다"류 결론 금지.

## Gaps / open questions
- 찾고 싶었지만 못 찾은 것
- 출처가 모호해서 채택하지 않은 것
- 추가 조사 추천 방향
```

### raw 작성 hard rules
- **요약·해석·종합 절대 금지** — 그건 summarizer의 일이다. raw는 증거만 모은다.
- **출처 없는 인용 금지** — "유명한 명언" 류는 검증 안 되면 본문에 넣지 말고 `Gaps`에 적는다.
- 최소 **5개 이상의 인용**을 목표로 하되, 부족하면 그대로 둔다 (가짜로 채우지 마라).
- **반론은 raw 증거로만** — `Critiques & limits` 섹션은 "어디서 깨지는가"의 자료다. "거장보다 X가 옳다"는 평가 금지. 출처·맥락 규칙은 1차 자료와 동일.

## summary.md 템플릿 (summarizer 산출물 SSOT)

summarizer 에이전트가 작성하는 파일은 **반드시** 이 형식을 따른다.

```markdown
# Decomposition — <Figure>: <Topic>

- **Source**: [<topic>-raw.md](./<topic>-raw.md)
- **Date**: YYYY-MM-DD

## One-line essence
이 인물의 이 사고법을 한 문장으로. 시·찬사 금지, **작동 원리**로 적는다.

## Core principles
1. **<원칙명>** — 한 문단 설명. (근거: Q3, Q7)
2. ...

## The mental moves (재현 가능한 절차)
거장이 실제로 머릿속에서 하는 동작을 순서로:
1. <Move 1>: 무엇을 / 왜 / 어떻게 (근거: Q?)
2. <Move 2>: ...
...

## Heuristics & decision rules
- "X이면 Y한다" 형식의 룰들 (근거: Q?)

## Anti-patterns (이 인물이 거부하는 것)
- ... (근거: Q?)

## When this thinking applies
- **잘 맞는 상황**: ...
- **안 맞는 상황**: ...

## Open tensions
- 인용들 사이에서 모순처럼 보이는 지점. 해소 시도 + 미해소 표시.

## Gaps inherited from raw
- raw의 Gaps 중 이 decomposition에 영향을 준 것
```

### summary 작성 hard rules
- 모든 주장은 raw의 Q번호로 **근거를 단다**. 근거 없는 일반론 금지.
- **raw에 없는 사실 추가 금지** — 새 자료가 필요하면 `Gaps`에 적고 researcher를 다시 돌리라고 알린다.
- `Anti-patterns`와 `Open tensions`를 비워두지 마라. 비어 있다면 raw가 부족하다는 신호 — `Gaps`에 명시.
- `One-line essence`는 **작동 원리**를 적는다. "그는 위대했다" 같은 평가/찬사 금지.

## 원칙

- **raw는 절대 손으로 고치지 않는다** — researcher를 다시 돌려 v2를 만든다 (`-raw-v2.md`).
- **summary는 raw의 Q번호 근거를 보존한다** — summary만 보고 raw를 추적할 수 있어야 한다.
- 이 폴더의 파일들은 **최종 스킬(.claude/skills/) + ADR**로 이어지는 원재료다. 지우지 마라.
