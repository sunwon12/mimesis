# ADR — Architecture Decision Records

이 폴더는 `.claude/skills/` 아래 각 스킬을 **왜·어떻게** 설계했는지 남기는 사고의 로그다.

스킬 자체는 "거장을 모방한 결과물"이지만, ADR은 **우리가 거장을 어떻게 해체했는가**의 기록이다.
시간이 지나면 결과물(스킬)보다 이 해체 과정이 더 큰 자산이 된다.

## 파일명 규칙

```
NNNN-<kebab-case-slug>.md
```

- `NNNN` — 4자리 일련번호 (0001부터)
- slug — 스킬명과 일치시키는 것을 권장 (`mckinsey-mece`, `feynman-technique` 등)

## 템플릿

```markdown
# ADR NNNN: <제목>

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

## 원칙

- **스킬보다 ADR이 먼저** — 사고 없이 스킬을 만들면 카피일 뿐이다.
- **Status는 살아있는 값** — 스킬이 바뀌면 ADR도 갱신하거나 Superseded 처리한다.
- **Application log를 비워두지 마라** — 적용 없이 ADR은 미완성이다.
