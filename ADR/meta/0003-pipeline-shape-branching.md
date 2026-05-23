# ADR meta-0003: 파이프라인 종착점을 collaborator shape에 어떻게 분기시킬 것인가

- **Status**: Proposed
- **Date**: 2026-05-23
- **Scope**: `.claude/agents/`의 파이프라인 종착점 정책. 신규 figure가 어떤 shape인지에 따라 종착점 에이전트가 달라지는 규칙. meta-0002 §6에서 보류한 결정의 후속.
- **Affected files**:
  - 신규(예정): `.claude/agents/collaborator-builder.md` — *단, 첫 collaborator 적용 검증 후에 materialize* (Decision §3 참조)
  - 영향: `.claude/agents/skill-builder.md` — 손대지 않음 (diagnostic 전용으로 사실상 좁아짐, 문서상 명시는 추후)
  - 후속 산출물: `.claude/agents/ogilvy.md`, `.claude/skills/ogilvy/SKILL.md`, `ADR/skills/0007-ogilvy.md`

## Context

meta-0002에서 figure 자산을 두 shape(diagnostic skill / collaborator agent)으로 분기하기로 정했다. 그러나 그 ADR은 "파이프라인 종착점을 어떻게 갈래낼지"는 의도적으로 보류하고, 첫 collaborator 적용 시점에 후속 ADR로 박기로 했다.

지금이 그 시점이다:
- Ogilvy의 raw 자료 2개(`methodology-and-craft-raw.md`, `brand-and-voice-raw.md`) 수집 완료, 인용 45개.
- summary 2개 완료. 다음 단계가 종착점.
- 기존 `skill-builder` agent는 1개 입력 → 1개 SKILL.md + 1개 ADR을 만드는 형태. collaborator는 2개 입력(자매 raw/summary) → 3개 산출물(`.claude/agents/<f>.md`, 얇은 `.claude/skills/<f>/SKILL.md`, `ADR/skills/NNNN-<f>.md`)이 필요.

이 차이가 너무 커서 skill-builder를 그대로 쓸 수 없다는 점은 자명하다. 남은 결정은 **갈래내는 방식**이다.

## Options considered

### Option A — skill-builder를 확장해서 shape 분기 (meta-0002 §6-A)

기존 skill-builder.md에 분기 로직을 추가한다. 입력에 `shape=diagnostic|collaborator` 플래그를 받고, 각 shape에 맞춰 다른 산출물 세트를 만든다.

- **장점**:
  - agent 파일 한 개 유지. 디렉토리 단순.
  - frontmatter·ADR 작성 등 공통 로직 공유.
- **단점**:
  - skill-builder는 이미 6개 diagnostic skill에서 검증된 자산이다. 손대면 회귀 위험.
  - 두 산출물 형태(1파일 vs 3파일)가 너무 비대칭이라 분기 로직이 비대화된다.
  - 한 agent 안에 두 모드가 섞이면 모드 간 누수 위험 — diagnostic에 collaborator-스러운 procedure가 섞이거나 그 반대.
  - 한 agent의 system prompt가 두 종착점의 SSOT 템플릿을 둘 다 알아야 함 → research/README.md 참조 구조가 복잡해짐.
- **결론**: 기각. 검증된 자산을 손대는 비용이, agent 파일 1개 절약의 이득보다 크다.

### Option B — collaborator-builder agent를 별도 신설 (meta-0002 §6-B)

새 agent `.claude/agents/collaborator-builder.md`를 만든다. skill-builder는 그대로 두고, diagnostic 전용으로 사실상 좁힌다.

- **장점**:
  - skill-builder는 손대지 않는다 — 회귀 위험 zero. 기존 7개(곧 8개) diagnostic skill 자산의 무결성 유지.
  - collaborator-builder는 페르소나·voice·모드 분기·인테이크 프로토콜의 추출에 집중. 단일 책임.
  - 두 agent가 서로 독립이라 한쪽을 반복 개선해도 다른 쪽이 안 흔들림.
  - 두 input(자매 summary 2개) → 3 output 패턴이 자연스럽게 표현됨.
- **단점**:
  - agent 파일 1개 증가.
  - frontmatter/ADR 작성의 일부 로직이 두 agent에 중복.
  - 사용자/오케스트레이터가 shape에 맞춰 어느 agent를 부를지 미리 정해야 함 (이건 meta-0002에서 이미 정한 정책이라 추가 비용 아님).
- **결론**: 본 ADR이 채택. 단, **언제 materialize할지**는 §3에서 추가 결정.

### Option C — collaborator-builder.md 없이, 첫 collaborator는 one-off Agent로 생성

새 agent 파일을 미리 만들지 않고, 첫 collaborator(Ogilvy)는 일회성 Agent 호출(general-purpose 또는 default claude)로 산출물을 만든다. 산출물이 만족스러우면, 그 결과를 역설계해서 collaborator-builder.md를 materialize한다.

- **장점**:
  - **선-추상 회피**. 한 사례도 안 만들어보고 agent 파일부터 박으면 가정이 빗나갔을 때 두 번 작업.
  - 첫 산출물이 어떤 구조여야 하는지는 사실 아직 모른다 — 모드 분기 명세, 인테이크 프로토콜 형태, voice 인용 사용량 등은 만들어봐야 알 수 있다.
  - 한 번 잘 작동하는 산출물이 생기면, 그걸 보고 collaborator-builder.md를 더 정확히 쓸 수 있다.
- **단점**:
  - 첫 산출물의 재현성이 낮음 — agent 파일이 없으니 두 번째 collaborator를 만들 때 동일 패턴이 보장 안 됨.
  - "곧 만들겠다"가 한 번도 안 만들어지는 위험 (TODO 부채).
- **결론**: 본 ADR이 §3에서 시점 결정에 활용.

## Decision

**Option B**를 정책으로 채택한다. 단, materialize 시점은 **Option C 방식의 역설계**.

### 1) 정책 — collaborator-builder는 별도 agent

- diagnostic shape의 종착점: 기존 `.claude/agents/skill-builder.md` (그대로, 변경 없음).
- collaborator shape의 종착점: 신규 `.claude/agents/collaborator-builder.md` (미래에 materialize).
- 두 agent는 서로 독립. 공통 로직은 ADR/research README의 SSOT 템플릿이 흡수.

### 2) skill-builder.md는 손대지 않는다 (이번에는)

skill-builder는 사실상 diagnostic 전용으로 좁아진다. 그러나:
- **문서 갱신은 보류**. skill-builder.md 안의 description에 "diagnostic 전용" 명시를 추가하는 작업은 collaborator-builder가 실제로 만들어진 이후로 미룬다.
- 이유: skill-builder의 description을 미리 좁히면, collaborator-builder가 만들어지지 않은 동안 트리거 공백이 생긴다. 양쪽이 동시에 정합하는 시점에 갱신한다.

### 3) collaborator-builder.md는 첫 collaborator(Ogilvy) 검증 후 materialize

첫 산출물은 collaborator-builder.md 없이 **일회성 작업**으로 만든다:
- Agent 도구(general-purpose 등)에 상세 프롬프트를 넣어, Ogilvy의 자매 summary 2개를 입력으로 다음 3개 파일을 만들게 한다:
  - `.claude/agents/ogilvy.md` — agent system prompt 본체
  - `.claude/skills/ogilvy/SKILL.md` — 얇은 진입점 (200~400자 본문 목표)
  - `ADR/skills/0007-ogilvy.md` — 해체 기록 (shape: collaborator 명시)
- 산출물을 직접 사용해보고 voice 일관성·모드 분기·인테이크가 작동하는지 검증.
- 검증 후 그 산출물의 **공통 구조·작성 절차·self-check**를 역설계해 `.claude/agents/collaborator-builder.md`로 박는다.

이 방식의 위험은 "역설계가 미뤄지면 부채"라는 것. 완화책:
- 본 ADR의 Application log에 "collaborator-builder.md materialize" 항목을 비워두고, 둘째 collaborator를 들이려 할 때 이 칸이 비어 있으면 그때 만든다.
- 두 번째 collaborator가 한참 동안 안 들어오면 첫 산출물(Ogilvy)이 그대로 "사실상의 collaborator-builder 참조 구현"으로 작동한다 — 부채라기보단 lazy materialize.

### 4) ~~디렉토리 재구조(meta-0002 §2)는 이번 ADR에서 분리~~ → 폐기 (Erratum)

meta-0002의 디렉토리 재구조 자체가 Erratum으로 폐기됨 (`.claude/agents/`는 top-level만 디스커버리). 따라서 본 ADR의 "재구조 분리·연기" 결정은 무효 — 재구조 자체가 없다.

신규 산출물 위치: `.claude/agents/<figure>.md` (평면). 기존 3개 pipeline agent는 그대로. figure agent와 pipeline agent의 구별은 *고유명사 vs 역할 기술어* 네이밍 컨벤션이 흡수.

## Consequences

- **Positive**:
  - skill-builder의 회귀 위험 zero — 기존 7개 diagnostic skill 자산 무결.
  - collaborator-builder의 명세가 추측이 아닌 한 사례 검증을 거쳐 결정됨 — 더 정확한 templating 가능.
  - 두 종착점 agent가 독립이라 향후 한쪽 개선이 다른 쪽을 흔들지 않음.
  - 디렉토리 재구조와 새 산출물 생성이 분리되어 한 번에 깨질 표면이 작음.
- **Negative / Trade-offs**:
  - **재현성 일시 부재**. Ogilvy 산출물이 일회성이라, 둘째 collaborator를 들일 때까지 정형 절차가 없다.
  - **부채 트래킹 필요**. "역설계" 항목이 잊히면 collaborator-builder.md가 영원히 안 만들어진다 — Application log에 명시적으로 비워둠.
  - **skill-builder description의 불일치 일시 잔존**. 사실상 diagnostic 전용이지만 문서엔 그렇게 안 적혀 있는 기간이 있음. 첫 collaborator-builder 완성 시 함께 갱신.
  - ~~**`.claude/agents/ogilvy.md`의 위치 비대칭**~~ → Erratum: 평면으로 통일되어 비대칭이 사라짐. 대신 *시각적 동거*가 새 trade-off — figure agent(고유명사)와 pipeline agent(역할 기술어)가 같은 ls 결과에 섞여 표시됨. 네이밍 컨벤션이 의미적으로는 흡수.
- **Open questions**:
  - one-off Agent 호출이 생성하는 산출물의 일관성. 같은 입력에 같은 출력이 안 나오면 역설계 시점에 어느 버전을 정본으로 삼는가.
  - collaborator-builder.md가 결국 materialize될 때, 일회성 산출과 정형 산출 사이의 미세한 voice 차이를 어떻게 reconcile하는가.
  - 둘째 collaborator를 들이는 시점이 늦어지면 이 lazy materialize 전략이 부채로 변하는 시점은 언제인가 (휴리스틱: 둘째 collaborator가 들어오는 순간 무조건 먼저 박는다).

## Migration notes

- 본 ADR은 새로운 파일을 만들지 않는다. 신규 산출물(Ogilvy)이 이 ADR의 가이드에 따라 만들어진다.
- 본 ADR이 Accepted로 가는 시점은 Ogilvy 3개 파일이 만들어지고 직접 사용 검증된 직후.
- meta-0002의 디렉토리 재구조와 README 갱신은 본 ADR의 후속 마이그레이션 커밋에서 일괄 처리.

## Application log

- TBD — 첫 collaborator(Ogilvy) 적용 후 갱신. 특히 다음 다섯 가지를 기록한다:
  1. 일회성 Agent 호출이 만든 3개 파일의 구조적 일관성 — 자매 summary 2개를 잘 통합했는가, 갈라치기했는가.
  2. agent system prompt에 voice 인용이 몇 개 박혔는가, 인격 일관성에 그게 충분했는가.
  3. 진입 SKILL.md가 의도대로 얇게 유지됐는가, 본체로 비대화하진 않았는가.
  4. ADR/skills/0007의 Decomposition이 두 summary를 잘 묶었는가, 어느 한쪽에 치우치지 않았는가.
  5. **collaborator-builder.md materialize**: 둘째 collaborator를 들이려 할 때 이 칸이 비어 있다면 그때 만든다 (비어 있는 채로 두는 게 의도적인 lazy 전략).
