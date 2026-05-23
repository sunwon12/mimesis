# ADR — Architecture Decision Records

이 폴더는 **두 결의 사고 로그**다.

```
ADR/
├── skills/    # 거장 1명을 어떻게 해체했는가 — figure-anchored 스킬 1개당 한 장
└── meta/      # 레포 전체를 어떻게 가꿀 것인가 — 트리거 아키텍처·네이밍·파이프라인 등 repo-wide 의사결정
```

스킬 자체는 "거장을 모방한 결과물"이지만, ADR은 **우리가 어떻게 해체·구성했는가**의 기록이다.
시간이 지나면 결과물(스킬)보다 이 해체·구성 과정이 더 큰 자산이 된다.

## 두 결의 차이

| | `skills/` | `meta/` |
| --- | --- | --- |
| **다루는 것** | 한 거장의 사고를 한 스킬로 박제 | 레포 전체의 구조·정책·트리거 흐름 |
| **트리거 단위** | 거장 한 명 추가될 때 | 아키텍처 결정이 새로 생길 때 |
| **번호 의미** | 인물 로스터 추가 순서 | 레포 진화의 마일스톤 순서 |
| **예시** | `0001-lee-eo-ryeong-questioning.md` | `0001-master-router.md` |

두 디렉토리는 **각자 0001부터 독립 번호**를 쓴다. 한쪽이 다른 쪽의 노이즈가 되지 않게.

## 파일명 규칙

```
NNNN-<kebab-case-slug>.md
```

- `NNNN` — 4자리 일련번호 (각 디렉토리 안에서 0001부터 독립)
- slug — `skills/`는 스킬명과 일치, `meta/`는 결정 주제 (`master-router`, `naming-figure-anchored` 등)

## 템플릿 — `skills/`

```markdown
# ADR NNNN: <인물> — <스킬 주제>

- **Status**: Proposed | Accepted | Deprecated | Superseded by ADR-####
- **Date**: YYYY-MM-DD
- **Related skill**: `.claude/skills/<skill-name>/`
- **Source figure(s)**: <인물>
- **Primary sources**: <원문/책/영상 + 위치>

## Context
이 스킬이 필요해진 배경. 어떤 상황에서 막혔고, 왜 거장 X의 사고가 답이 될 거라 판단했는가.

## Decomposition
거장의 사고를 어떻게 해체했는가. 원문에서 추출한 구조·단계·휴리스틱.
요약이 아니라 **재구성**. 가능하면 원문 인용 + 우리의 재해석을 분리해 적는다.

## Decision
스킬을 어떤 형태로 만들 것인가.
- 트리거: 어떤 키워드/상황에 호출되어야 하는가
- 입력: 무엇을 받아야 하는가
- 출력 계약: 무엇을 반환해야 하는가
- 잘라낸 것: 원본 사고 중 의도적으로 제외한 부분과 그 이유

## Consequences
- **Positive**: 이 스킬을 가짐으로써 무엇이 가능해지는가
- **Negative / Trade-offs**: 잃은 것, 위험, 오용 가능성
- **Open questions**: 아직 확신 없는 지점

## Application log
실제로 써본 기록. 잘 작동한 케이스 / 빗나간 케이스 / 이후 개정 사항.
```

## 템플릿 — `meta/`

```markdown
# ADR NNNN: <결정 주제>

- **Status**: Proposed | Accepted | Deprecated | Superseded by ADR-####
- **Date**: YYYY-MM-DD
- **Scope**: <어떤 디렉토리·파일·정책에 영향을 주는가>
- **Affected skills / files**: <구체 경로 목록>

## Context
어떤 레포 차원의 문제·마찰·확장 압력이 이 결정을 요구했는가.
거장 한 명의 해체가 아니라 "레포 전체가 어떤 모양이어야 하는가"의 질문이어야 한다.

## Options considered
1. <옵션 1> — 장단점
2. <옵션 2> — 장단점
3. <옵션 3> — 장단점

## Decision
어떤 옵션을 골랐는가. 트리거·디렉토리·파일명·정책의 **구체적 형태**.

## Consequences
- **Positive**: 레포 진화 측면에서 무엇이 가능해지는가
- **Negative / Trade-offs**: 이 결정이 다른 결정을 어떻게 제약하는가
- **Open questions**: 이후 재고할 지점

## Migration notes (있다면)
기존 자산을 옮겨야 한다면 그 절차와 영향 범위.

## Application log
이 결정이 실제 작업 흐름에 어떻게 작동했는지, 이후 어떤 사례가 이 결정을 강화·약화했는지.
```

## 원칙

- **스킬보다 ADR이 먼저** — 사고 없이 스킬을 만들면 카피일 뿐이다.
- **Status는 살아있는 값** — 스킬·아키텍처가 바뀌면 ADR도 갱신하거나 Superseded 처리한다.
- **Application log를 비워두지 마라** — 적용 없이 ADR은 미완성이다.
- **`skills/`와 `meta/`는 섞이지 않는다** — 한 ADR이 두 결에 걸치면 그건 두 ADR로 쪼개야 한다는 신호다.
