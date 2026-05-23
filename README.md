# mimesis

> μίμησις — 모방은 학습의 가장 오래된 형태다.

대표 인물의 사고방식과 삶의 태도를 **Claude Code 스킬**로 체화하기 위한 개인 저장소.

## 왜 만들었는가

읽고 감탄하는 것에서 멈추면 아무것도 남지 않는다.
거장의 사고 골격을 **실행 가능한 스킬**로 옮겨, 내가 일·생각·글에 막힐 때마다 호출할 수 있게 만든다.

- **사고법(How they think)** — 맥킨지식 문제 정의, 파인만의 학습법, 찰리 멍거의 멘탈 모델
- **태도(How they live)** — 이어령의 지적 호기심, 스티브 잡스의 단순함, 세네카의 평정
- **작업법(How they work)** — 헤밍웨이의 글쓰기 루틴, 다 빈치의 노트, 폰 노이만의 문제 분해

## 디렉토리 구조

```
mimesis/
├── .claude/skills/          # 실행 가능한 스킬 (Claude Code가 호출)
│   └── <skill-name>/
│       └── SKILL.md         # frontmatter(name, description) + 본문
├── ADR/                     # 스킬 설계 의사결정 기록
│   └── 0001-<slug>.md       # Context / Decision / Consequences
└── README.md
```

- **`.claude/skills/`** — 결과물. Claude Code가 트리거 키워드로 자동 호출하는 실행 단위.
- **`ADR/`** — 사고 과정. 왜 이 스킬을 만들었고, 왜 이런 형태로 잘랐는지를 남긴다.
  결과물만 보면 "이미 정해진 답"처럼 보이지만, ADR을 남기면 **거장을 해체한 우리의 사고 흐름** 자체가 또 하나의 자산이 된다.

## 작성 원칙

1. **요약하지 말고 해체하라** — "무엇을 말했는가"가 아니라 "어떤 구조로 사고했는가"를 스킬화한다.
2. **출처를 남겨라** — 원문/페이지/영상 타임스탬프. 검증되지 않은 명언은 받아들이지 않는다.
3. **스킬은 ADR과 짝으로** — 모든 스킬은 동일 번호의 ADR이 짝지어 존재한다.
4. **회의하라** — 거장도 틀린다. 동의하지 않는 지점은 ADR의 *Consequences*에 명시한다.

## 인물 로스터 (점진 추가)

- [ ] McKinsey — 구조적 문제 해결 (MECE, Pyramid, SCQA)
- [ ] 이어령 — 지의 거인, 생각의 탄생
- [ ] Charlie Munger — Latticework of Mental Models
- [ ] Richard Feynman — 첫 원리적 사고와 학습법
- [ ] Steve Jobs — 단순함의 미학
- [ ] Naval Ravikant — 부와 행복의 원리

## 새 스킬 추가 절차

1. `ADR/NNNN-<slug>.md` 작성 — **먼저 사고 과정을 남긴다**. 왜 이 스킬인가, 어떤 트리거에 호출되어야 하는가, 어떤 입출력 계약을 가지는가.
2. `.claude/skills/<skill-name>/SKILL.md` 작성 — ADR의 결론을 실행 가능한 형태로 옮긴다.
3. 직접 사용해보고 ADR의 *Consequences*에 적용 결과를 추가한다.
