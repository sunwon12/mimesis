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

## 원칙

- **raw는 절대 손으로 고치지 않는다** — researcher를 다시 돌려 v2를 만든다 (`-raw-v2.md`).
- **summary는 raw의 Q번호 근거를 보존한다** — summary만 보고 raw를 추적할 수 있어야 한다.
- 이 폴더의 파일들은 **최종 스킬(.claude/skills/) + ADR**로 이어지는 원재료다. 지우지 마라.
