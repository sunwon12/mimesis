# ADR meta-0001: 거장 스킬 추천 라우터 (master-router)

- **Status**: Accepted
- **Date**: 2026-05-23
- **Scope**: 레포 전체의 figure 스킬 트리거 아키텍처. 모든 `.claude/skills/<figure-name>/SKILL.md`의 frontmatter description 정책에 영향.
- **Affected skills / files**:
  - 신규: `.claude/skills/master-router/SKILL.md`
  - 수정: `.claude/skills/lee-eo-ryeong-questioning/SKILL.md` (description 좁힘)
  - 수정: `.claude/skills/erich-fromm-having-vs-being/SKILL.md` (description 좁힘)
  - 수정: `.claude/skills/mckinsey-structured-problem-solving/SKILL.md` (description 좁힘)
  - 수정: `README.md` (권장 흐름 추가)
  - 디렉토리 분리: `ADR/` → `ADR/skills/` + `ADR/meta/` (이 결정의 부수 효과)

## Context

mimesis 레포는 거장 스킬을 점진 추가하는 구조다. 0001~0003 세 스킬을 추가한 시점에서 다음 문제가 표면화됐다:

- **트리거 표면 충돌**. 한 사용자 발화가 여러 figure 스킬의 description에 동시에 매핑되는 일이 빈번해진다. 예:
  - "이번 분기에 산 책이 12권인데 다 못 읽었어. 다 들어둔 강의는 또 어떻게 정리하지?" → fromm(축적 호소) + 가능하면 mckinsey(scope 정리)
  - "키노트 도입이 진부한데 어떻게 풀어야 할지 모르겠어" → lee-eo-ryeong(통설 의심) + mckinsey(메시지 구조화)
- **description의 자기학대적 비대화**. trigger 누락을 막으려고 한국어 자연 표현을 description에 박는 패턴(0001/0002/0003 모두 채택)이, 스킬이 늘어날수록 표면이 겹쳐 모델의 자동 매핑 신뢰도를 떨어뜨린다.
- **"반드시 호출한다" 조항의 부작용**. 0002/0003 description 끝에 박힌 "사용자가 'X'라고 명시하지 않아도 반드시 호출한다" 조항은 단일 스킬 시대에는 under-trigger를 막아줬지만, 여러 스킬에 같은 조항이 박히면 모델이 어느 쪽을 먼저 부르는지 무작위에 가까워진다.
- **확장 압력**. 로스터(README의 인물 추가 계획)에 Munger, Feynman, Jobs, Naval 등이 줄을 서 있어 5~10개 스킬이 되는 시점이 멀지 않다. 그 시점이 오기 전에 트리거 아키텍처를 정해두지 않으면 매번 description을 미세 조정하는 부채가 누적된다.

거장 한 명을 더 해부하는 문제가 아니라, **레포 전체의 트리거 정책**을 정하는 문제다. 그래서 `skills/` 가 아니라 `meta/` 디렉토리에 새로 ADR을 둔다 (이 결정 자체가 ADR 디렉토리 분리의 트리거).

## Options considered

### Option A — 현 상태 유지: 거장 스킬마다 "반드시 호출" auto-trigger
- **장점**: 추가 마찰 없음. 사용자가 일상 표현만 던져도 자동 호출.
- **단점**: 스킬 N개 시점에 충돌이 N(N-1)/2로 증가. 모델이 어느 쪽을 먼저 잡는지 비결정적. 가장 큰 비용은 "잘못된 자동 호출"이 한 번 일어나면 raw 스킬 신뢰가 통째로 깎인다는 점.
- **결론**: 단기에는 가장 싸지만 5~10개 스킬 도달 시 회복 비용이 너무 크다.

### Option B — 거장 스킬을 explicit-only로 좁히고, 라우터 스킬 추가 (auto+explicit)
- **장점**:
  - 거장 스킬 description은 인물명·고유 개념 명시 호출에만 반응 → 표면 충돌 제로.
  - 라우터가 "ambiguous한 모든 상황"을 받아서, 사용자 컨텍스트를 짧게 진단하고 1~3개 후보를 그 이유와 함께 보여준다.
  - 사용자가 "왜 이 인물이 이 상황에 맞는가"의 매핑을 한 박자 의식적으로 학습 — mimesis의 본래 의도(거장 사고를 자기 것으로 만들기)와 부합.
  - 라우터 description만 갱신하면 신규 거장 스킬을 추가할 때마다 다른 스킬 description을 안 만져도 된다 (확장 비용이 라우터 한 곳으로 집중).
- **단점**:
  - 마찰 한 단계 추가 — 사용자가 라우터 호출 → 추천 → 명시 호출의 2 turn이 든다.
  - 라우터 자체의 auto-trigger 정의가 또 하나의 description 작업.
  - 라우터가 자동 호출 안 하면 사용자가 첫 사용에서는 "왜 추천만 하고 안 풀어주지?"의 마찰을 한 번 겪는다.
- **결론**: 선택. 이유는 Decision 참조.

### Option C — 라우터도 auto-호출하고, 거장 스킬도 그대로 auto 유지
- **장점**: 명시 호출이 들어왔을 때는 거장이 잡히고, 그 외에는 라우터가 잡혀 표면적으로 깔끔.
- **단점**: 결국 두 layer의 description이 또 겹친다. "어느 쪽이 먼저 잡히는가"가 다시 비결정적. Option A의 문제를 다른 자리에 옮긴 것에 불과.
- **결론**: 기각.

### Option D — 라우터 explicit-only, 거장 스킬 auto 유지
- **장점**: 사용자가 직접 부를 때만 라우터.
- **단점**: 사용자가 어떤 거장이 적합한지 모를 때 도움받을 기본 흐름이 사라진다. 라우터의 가장 큰 가치(ambiguity 해소)가 죽는다.
- **결론**: 기각.

## Decision

**Option B**를 선택한다. 구체 형태:

### 1) 라우터 스킬 신규: `.claude/skills/master-router/`
- **이름**: `master-router` — figure-anchored 네이밍 규칙([mimesis-naming-figure-anchored](../../memory/...) 메모리)에서 의도적으로 면제. 메타 스킬이기 때문.
- **트리거**: auto + explicit. description 본문에 "사용자가 라우터를 명시적으로 부르지 않아도 호출한다" 조항 박음.
- **자동 호출 조건**: 사용자가 거장 영역에 걸리지만 (1) 어떤 인물·고유 개념도 명시 안 함, (2) 두 개 이상의 figure 표면에 겹침, (3) "어떤 스킬", "스킬 추천", "거장 골라줘" 류 직접 요청 중 하나.
- **호출하지 않을 조건**: 인물명/고유 개념 명시, 코드/실행/조회 작업, 단일 figure에 자명히 떨어지는 경우.
- **동작**: 컨텍스트 진단(활동/기준/신호 3축) → 부족하면 1~3개의 좁은 단일 선택지 질문 → 매칭 1~3개를 "왜 이 상황에 맞는지"와 함께 반환 → **자동 호출하지 않고 사용자가 명시 호출하도록 트리거 문구를 알려준다**.

### 2) 거장 스킬 description은 명시 호출 + 라우터-경유로 좁힌다
- 인물명·고유 개념(예: "프롬", "having mode", "이어령", "정문", "맥킨지", "MECE", "pyramid principle")이 발화에 있을 때만 자동 호출.
- 일상 자연 표현은 description에서 빼지 않고 "적용 영역"으로 보존하되 — 표면이 겹칠 가능성이 있을 때는 master-router를 먼저 호출한다는 안내 한 줄을 박는다.
- 기존 "반드시 호출한다"는 모두 제거.

### 3) 추천 후 자동 호출은 의도적으로 하지 않는다
가장 논쟁적인 선택. 트레이드오프:
- **자동 호출 시**: 마찰 1 turn 절약. 그러나 사용자가 "왜 이 거장인가"를 의식 못 하고 그냥 결과만 받게 됨 — mimesis의 본래 의도("거장 사고를 자기 것으로 만들기")가 라우터에 가려진다. 또 추천이 잘못됐을 때 사용자가 멈출 기회 없이 그 figure 스킬의 procedure가 발화된다.
- **명시 호출만**: 마찰 1 turn 추가. 그러나 사용자가 매번 "○○ 스킬로 다음 turn에 부르면 돼" 같은 안내를 받으면서 figure-situation 매핑을 학습한다. 그리고 다음에 비슷한 상황이 오면 라우터를 거치지 않고 곧장 명시 호출이 된다 — 라우터는 점점 빈도가 줄어드는 게 정상이다.
- 명시 호출 쪽을 선택. README의 권장 흐름 멘트와 정합한다.

### 4) ADR 디렉토리 구조도 동시에 바꾼다
- 기존: `ADR/0001-...md`, `0002-...md`, `0003-...md` 평면
- 신규: `ADR/skills/0001~0003-...md` + `ADR/meta/0001-master-router.md`
- 두 결의 ADR이 한 번호 체계에 섞이면 "거장 해부" 사고 흐름과 "레포 가꾸기" 사고 흐름이 서로의 노이즈가 된다. 디렉토리로 물리적으로 분리.
- 각 디렉토리는 자기 0001부터 독립 번호.

## Consequences

- **Positive**:
  - 거장 스킬 description 끼리의 표면 충돌이 사라진다 — 각자 인물명·고유 개념에만 반응.
  - 라우터가 figure-situation 매핑을 사용자에게 노출해, **거장 사고를 자기 것으로 만든다**는 mimesis 본래 의도가 도구 레벨에서 강화됨.
  - 신규 거장 스킬 추가 비용이 라우터 한 곳으로 집중 — 다른 스킬을 안 만져도 된다.
  - ADR 디렉토리 분리로 두 결의 사고 흐름이 각자의 진척도를 시각화한다 (`skills/`는 로스터 진행, `meta/`는 레포 진화).
- **Negative / Trade-offs**:
  - **마찰 1 turn 추가**. 사용자가 라우터 호출 → 추천 → 명시 호출의 2 turn 흐름. 자주 쓰는 거장은 사용자가 곧장 명시 호출하게 되어 라우터를 안 거치게 되지만, 새 거장이 추가될 때마다 첫 만남에서는 라우터를 거치게 된다.
  - **거장 스킬 under-trigger 위험**. 명시 호출에만 반응하게 좁혔기 때문에, 사용자가 인물명을 모르는 상황에서 라우터를 거치지 않고 곧장 작업을 던지면 거장 스킬이 누락될 수 있다. 라우터의 auto-trigger 신뢰도에 의존하게 됨.
  - **라우터 자체의 description이 부풀 위험**. 라우터의 auto-trigger 정의가 또 하나의 description 비대화 자리가 될 수 있음. heuristic으로 "후보 4개 이상이면 진단 부족"을 박았지만 첫 사용에서 검증 필요.
  - **figure-anchored 네이밍 룰의 첫 예외**. `master-router`는 인물에 귀속되지 않는다. "메타 스킬은 figure-anchored 면제"라는 보조 룰이 암묵적으로 생긴다 — 이 자체를 별도 meta-ADR로 박을지 검토 필요.
- **Open questions**:
  - 자동 호출 안 하기로 한 결정이 사용자 실제 사용에서 마찰로만 작동하는지, 학습 효과를 살리는지 — 첫 사용 후 검증.
  - 라우터가 매칭 0개를 솔직히 반환할 때 사용자가 "스킬 시스템이 비어 있다"고 오해하지 않는지.
  - 라우터 description에 박은 "거장 트리거 표면" 키워드 목록이 신규 거장 추가될 때마다 갱신되어야 하는지, 아니면 추상화된 형태(예: "깊은 사고/진단/구조화 영역")로 두면 충분한지.
  - 라우터 자체의 procedure가 도구의 가치보다 길어지면 사용자가 우회할 가능성 — 1~3 질문 상한선이 실효성 있는지.

## Migration notes

- `ADR/0001-lee-eo-ryeong-questioning.md` → `ADR/skills/0001-lee-eo-ryeong-questioning.md` (이번 커밋에서 이동, `git mv`로 히스토리 보존)
- `ADR/0002-erich-fromm-having-vs-being.md` → `ADR/skills/0002-erich-fromm-having-vs-being.md`
- `ADR/0003-mckinsey-structured-problem-solving.md` → `ADR/skills/0003-mckinsey-structured-problem-solving.md`
- 이동된 파일의 research 링크는 `../research/...` → `../../research/...`로 한 단계 깊은 상대경로로 갱신.
- `ADR/README.md`는 두 종류의 ADR(스킬/메타)을 모두 설명하도록 갱신.
- 루트 `README.md`에 권장 흐름(상황 → master-router → 명시 호출)을 한 단락 추가.
- 거장 스킬 description은 3개 모두 "명시 호출 + 라우터 경유" 형태로 한 번에 갱신. 향후 추가될 거장 스킬의 description도 같은 패턴 따른다.

## Application log

- TBD — 첫 사용 후 갱신. 특히 다음 다섯 가지를 기록한다:
  1. 라우터가 ambiguous한 상황을 실제로 잡는지 (under-trigger 여부).
  2. 사용자가 명시 호출 안내를 받았을 때 다음 turn에 그 스킬을 부르는 비율.
  3. 라우터가 "매칭 0개"를 반환한 빈도와 그게 로스터 확장 신호로 작동했는지.
  4. 두 거장 표면 충돌 케이스에서 라우터가 명료화 질문을 1개로 끝냈는지, 3개까지 갔는지.
  5. 거장 스킬 description을 좁히고 나서 under-trigger 사례가 늘었는지 (특히 사용자가 인물명을 모르는 상황).
