# .claude/skills

이 폴더는 두 종류의 스킬을 담는다:

```
.claude/skills/
├── master-router/         # 메타 스킬 — 상황에 맞는 거장 스킬을 추천하는 디스패처
└── <figure-name>/         # 거장 스킬 — figure-anchored, 인물 1명에 1개
    ├── SKILL.md           # frontmatter(name, description) + 본문 (필수)
    ├── references/        # (선택) 필요시 로드하는 보조 문서
    ├── scripts/           # (선택) 결정론적 반복 작업용 실행 코드
    └── assets/            # (선택) 산출물에 들어가는 템플릿/예시
```

- **거장 스킬** (`<figure-name>/`) — figure-anchored 룰 적용. 인물명·고유 개념을 명시 호출하거나 라우터의 추천을 거쳐 발화한다. 짝이 되는 `ADR/skills/NNNN-<figure>.md` 를 가진다 (필수).
- **메타 스킬** (`master-router/`) — figure-anchored 룰 면제. 거장 스킬 description끼리의 트리거 표면 충돌을 흡수해, ambiguous한 상황을 진단·추천한다. 짝이 되는 ADR은 `ADR/meta/` 아래.

스킬을 추가하기 전 ADR을 먼저 쓴다 — *결과물보다 사고 과정이 먼저다*. 사용자 입장의 권장 흐름은 루트 [`README.md`](../../README.md#사용-흐름-권장) 참조.

---

## SKILL.md 템플릿 (skill-builder 산출물 SSOT)

skill-builder 에이전트가 작성하는 거장 스킬은 **반드시** 이 형식을 따른다.

```markdown
---
name: <skill-name>
description: 80자 이상. 무엇을 하는지 + 언제 호출되어야 하는지(사용자 표현 5개+) + "명시 안 해도 트리거" 한 줄. Triggering guide 체크리스트 통과해야 함.
---

# <Skill title>

> 출처 인물: <Figure>. 한 줄 본질 (summary의 essence).

## When to use
- 다음 상황에 호출:
  - …(구체적)
- 다음에는 호출하지 말 것:
  - …

## The procedure
1. <Move 1>: <행동> — **Why:** <왜 이걸 이 시점에 하는가 1줄>
2. <Move 2>: …
…

## Heuristics
- <휴리스틱>. **Why:** <왜 이게 작동하는가>

## Examples
**Example 1 — <상황 라벨>:**
- Input: <사용자가 줄 법한 prompt 또는 데이터>
- Output (이 스킬을 통과한 후): <어떻게 변환·구조화되는가>

**Example 2 — <다른 결의 상황>:** (선택, 두 번째 예시가 결을 넓혀줄 때만)
…

## Anti-patterns (피할 것)
- <안 좋은 패턴>. **Why:** <왜 이게 무너지는가>

## Output expected
이 스킬 실행 후 사용자에게 돌려줄 산출물의 형태.
(예: "문제 정의 1문장 + MECE로 쪼갠 하위 이슈 트리 + 각 가지의 첫 검증 액션")
```

---

## 7 Principles (skill 작성의 핵심 원칙)

Anthropic 공식 `skill-creator`에서 추출. SKILL.md를 쓰기 전 매번 본다.

### 1. Description은 "약간 pushy"하게 써라
Claude는 스킬을 **under-trigger** 하는 경향이 있다 — 도움이 되는 상황에도 호출 안 하고 지나간다.
- ❌ "맥킨지식 문제 분해 스킬."
- ✅ "맥킨지식 문제 분해 스킬. 사용자가 'MECE', '구조화', '문제 정의', '이슈 트리', '어떻게 접근하지' 같은 말을 하거나 모호한 비즈니스/제품 문제를 던지면 — 사용자가 명시적으로 '맥킨지 방식'이라고 말하지 않아도 — 반드시 이 스킬을 사용한다."

**트리거 키워드는 사용자가 실제로 쓸 법한 표현으로.** 직역체("MECE", "이슈 트리")보다 자연어 변형("어떻게 풀지 모르겠어", "정리 좀 해줘")이 더 강하게 잡힌다.

### 2. Progressive disclosure로 구성한다
스킬은 3-level 로딩이다:
1. **Metadata (name + description)** — 항상 context에 있음 (~100 단어)
2. **SKILL.md body** — 스킬 트리거 시 로드 (500줄 미만이 이상적)
3. **Bundled resources** — 필요할 때만 로드 (무제한)

**언제 쪼개나:**
- SKILL.md가 300줄 넘어간다 → 도메인/변종별로 `references/<variant>.md` 로 분리하고 SKILL.md에선 "X면 references/aws.md를 읽어라" 식 포인터만 남긴다.
- 같은 helper 코드를 매 호출마다 다시 만든다 → `scripts/` 에 박제하고 "use scripts/foo.py" 라고 지시한다.
- 산출물 템플릿이 길다 → `assets/template.md` 로 빼고 SKILL.md에선 경로만 가리킨다.

mimesis 스킬은 대부분 작아서 SKILL.md 한 장으로 충분. 큰 거장(예: 파인만 학습법 전체)일 때만 분리.

### 3. WHY를 설명한다. ALWAYS/NEVER는 yellow flag.
오늘의 LLM은 똑똑하다. 강제 명령(ALWAYS/NEVER 캡스)은 일관성 없이 따라지고 엣지 케이스에서 깨진다. 대신 **왜 그렇게 하는지** 를 설명하면 모델이 스스로 판단해서 더 우아하게 따른다.
- ❌ "ALWAYS start with problem statement. NEVER skip this step."
- ✅ "먼저 problem statement 1문장을 쓴다 — 이 1문장이 어색하면 보통 문제 정의 자체가 안 끝난 거다. 어색함이 나침반이다."

빡빡한 MUST가 3개 이상이면 → 다시 쓴다. 거장의 사고를 "강요"가 아니라 "전염"시키는 게 목표.

### 4. 구체적 예시(Input → Output)를 1-2개 박는다
거장의 사고는 추상 원칙만으론 전염되지 않는다. **실제 사례 한 줄**이 원칙 10줄보다 강하다. summary의 인용/사례 중 가장 강한 1-2개를 SKILL.md "Examples" 섹션에 옮긴다.

### 5. Substantive task에서만 트리거됨을 인지한다
Claude는 자기가 단독으로 쉽게 처리할 수 있는 task에는 스킬을 호출하지 않는다 — description이 완벽하게 매치해도 마찬가지. 다중 단계 사고가 필요한 복잡한 task일 때만 호출된다.
→ 너무 사소한 단위로 자르지 마라. 거장의 mental moves가 진짜 가치를 갖는 task에서 호출되도록 description을 쓴다.

### 6. lean 하게 유지한다
"있으면 좋은" 섹션은 빼라. 모델이 매번 무시하거나 잘못 적용하는 부분이 보이면, 그 부분을 잘라내는 게 더 효과적인 경우가 많다. 부풀리지 마라.

### 7. 반복되는 helper는 scripts/로 박제한다
스킬을 여러 번 쓰다 보면 같은 보조 작업(파일 변환, 포매팅, 체크리스트 생성 등)을 매번 새로 한다는 게 보일 거다. 그러면 `scripts/<helper>.py` 로 박제하고 SKILL.md에서 호출하게 한다. 토큰·시간 둘 다 아낀다.

---

## Triggering guide (description 작성 체크리스트)

description은 스킬의 **유일한** 트리거 메커니즘이다. Claude는 description만 보고 호출 여부를 결정한다.

- [ ] 80자 이상
- [ ] 무엇을 하는 스킬인지 (1문장)
- [ ] 언제 호출되어야 하는지 — 사용자가 실제로 쓸 표현 5개 이상 (`"X" 같은 말을 하거나`, `"Y" 같은 상황에서`)
- [ ] **명시 안 해도 트리거**되어야 하는 경우를 한 문장으로 박는다 (단, 거장 스킬은 인물명·고유 개념 명시 호출 + master-router 경유로 좁힌다 — 이 레포의 트리거 정책)
- [ ] should-NOT-trigger 경계가 있다면 "단, … 에는 사용 안 한다" 한 줄

이 레포의 트리거 정책 (라우터와의 분담)은 `ADR/meta/0001-master-router.md` 의 Decision 섹션 참고.

---

## 네이밍 규칙 (Hard rules)

- **figure-anchored**: 스킬명은 `<figure-slug>-<method-slug>` 형식, 항상 한 거장에 귀속한다. 여러 거장이 함께 발전시킨 사고법(예: first-principles thinking — 아리스토텔레스/파인만/머스크)이라도 가장 대표적인 한 명을 골라 figure-anchored 로 만든다. mimesis 레포의 컨셉(거장 귀속) 자체가 핵심 자산이라 method-only 네이밍은 금지. lineage는 본문/ADR Decomposition에서 언급한다.
- **메타 스킬은 예외**: `master-router` 처럼 인물에 귀속되지 않는 디스패처/인프라성 스킬은 figure-anchored 룰에서 면제. 메타 스킬임을 ADR/meta/에 별도로 기록한다.
- **ASCII lowercase + numbers + hyphens 만, 최대 64자**: Claude Code 공식 검증 룰. Unicode/한글 사용 시 skill 로드 실패. 한국어는 description / 본문 H1 제목 / 본문 절차에 자유롭게 쓴다.
- **method-slug는 가능하면 gerund(-ing 동명사)** — 예: `questioning`, `decomposing`, `inverting`, `explaining-simply`. Anthropic 공식 권장 (행위 단위가 더 자연스럽게 트리거됨). 단, 약어(`mece`, `swot`)나 인물 고유 개념명(`having-vs-being`)은 예외 허용.

---

## 스킬 작성 워크플로우

1. ADR 먼저 — `ADR/skills/NNNN-<skill-name>.md` (템플릿은 `ADR/README.md`). 스킬이 레포 아키텍처에 손이 가는 결정이면 `ADR/meta/`로 간다.
2. SKILL.md를 위 템플릿대로 쓴다. 7 Principles와 Triggering guide 통과 필수.
3. 거장 스킬 description은 인물명·고유 개념 명시 호출에 좁히고, ambiguous한 상황은 master-router가 받도록 한 줄을 박는다. (이 레포의 트리거 정책 — 자세히는 `ADR/meta/0001-master-router.md`.)
4. 보조 자료가 필요할 때만 `references/`, `scripts/`, `assets/` 디렉토리를 만든다 (Principle #2 조건 충족 시).
5. 직접 사용해보고 ADR의 *Application log*를 채운다.
