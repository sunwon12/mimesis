# .claude/skills

이 폴더의 각 하위 디렉토리는 하나의 **거장 스킬**이다.
스킬은 모두 동일 형식을 따르지만, **목적·트리거·입출력은 스킬마다 다르다**.

```
.claude/skills/
└── <skill-name>/
    └── SKILL.md     # frontmatter(name, description) + 본문
```

각 스킬은 짝이 되는 `ADR/NNNN-<slug>.md` 를 가진다 (필수).
스킬을 추가하기 전 ADR을 먼저 쓴다 — *결과물보다 사고 과정이 먼저다*.
