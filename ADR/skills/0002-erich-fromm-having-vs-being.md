# ADR 0002: 에리히 프롬 — Having vs Being mode 진단

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/erich-fromm-having-vs-being/`
- **Source figure(s)**: Erich Fromm
- **Primary sources**:
  - [research raw](../../research/erich-fromm/having-vs-being-raw.md)
  - [research summary](../../research/erich-fromm/having-vs-being-summary.md)
  - 원전: *To Have or To Be?* (Harper & Row, 1976) — Ch.1 (프레임), Ch.2 (학습/지식/권위/사랑); 보조: *The Art of Loving* (1956), *The Art of Being* (1989), Marx *Economic and Philosophic Manuscripts of 1844*.

## Context
mimesis 레포의 두 번째 스킬이자 **첫 번째 프롬 스킬**이다. 이어령 스킬(0001)이 "질문을 짜는 입구"를 담당한다면, 이 스킬은 "활동·결정·자기 정의의 모드를 진단하고 재구성하는 자세"를 담당한다.

왜 프롬, 왜 having vs being부터인가:
- LLM 사용 패턴 자체가 having mode를 강화한다 — "정리해줘 / 요약해줘 / 다 적어둬 / 더 만들어줘"가 디폴트 prompt이고, 사용자도 "노트/책/자료/팔로워가 늘면 진척"이라는 양적 성공 기준을 자동으로 가져온다. 이 흐름에 진단·재구성 절차를 한 번 끼워 넣을 도구가 필요했다.
- 프롬의 having/being은 *To Have or To Be?* (1976)에서 학습·읽기·대화·기억·사랑·권위·지식·신앙 등 거의 모든 일상 활동에 적용 가능하도록 설계된 **단일 진단축**이다. 즉 figure-anchored 스킬로 박제하기 좋은 범용성·일관성이 있다.
- 우리 작업 흐름(독서, 학습, 자기소개, 기획 회의, 구매 결정, 관계 정리)에서 "지금 이걸 왜 하고 있지 / 끝났을 때 뭐가 달라지지"를 묻게 만드는 도구가 자주 필요한데, 이 자리가 정확히 프롬식 mental move의 sweet spot이다.

왜 *The Art of Loving* 이나 *Escape from Freedom* 이 아닌가:
- *The Art of Loving* (1956): 적용 범위가 "관계/사랑"으로 좁다. 범용 진단축으로 쓰기에 표면적이 작다. 단, having vs being 안에서 "사랑은 활동이다(Q11, Q12)" 라는 가지로 흡수했다.
- *Escape from Freedom* (1941): 권위주의·자유로부터의 도피라는 정치·사회 심리 진단. 개인 일상 활동의 자세 교정에 직접 매핑되지 않고, 모델이 사용자 prompt에서 트리거하기에 진입 비용이 크다. 첫 프롬 스킬로는 mismatch.
- 결론: having/being이 (1) 적용 표면이 가장 넓고, (2) 진단→재구성→행동의 절차로 손에 잡히게 떨어지며, (3) "지금 LLM 시대의 사용자가 가장 잘 빠지는 함정"(양적 축적을 깊이로 착각)을 정면으로 다룬다는 세 가지 이유로 first pick.

## Decomposition
summary의 핵심 구조를 옮긴다. Q번호는 summary/raw의 인용 번호를 그대로 유지.

### Principles (이 인물의 사고 정체성)
1. 활동은 소유될 수 없다 — 명사로 잡히는 순간 having mode가 시작된다. (Q3)
2. 같은 활동이 두 모드로 나뉜다 — 모드는 활동의 종류가 아니라 자세다. (Q4, Q5, Q8, Q10, Q11, Q15)
3. Having의 성공 기준은 양(more), Being의 성공 기준은 깊이(deeper). (Q8, Q15)
4. 정체성을 소유물에 묶으면 손실이 자기 붕괴가 된다. (Q6, Q7, Q17)
5. 기본값은 having — 사회·언어·경제가 그쪽으로 기울여 놓았다. (Q2, Q16)
6. Existential having은 비판 대상이 아니다 — 표적은 characterological having이다. (Q14)

### Mental moves (재현 가능 절차 — 8단계)
1. 명사·소유격을 동사로 다시 쓴다. (Q3, Q12)
2. 두 詩 테스트 — Tennyson vs Basho. (Q13)
3. 성공 기준을 명시화시킨다 — 양인가 깊이인가. (Q8, Q15)
4. 세 motto 중 어느 것을 답하고 있는지 비춰본다. (Q17, Q6, Q7)
5. 권위·관계·지식의 출처를 묻는다. (Q8, Q10, Q11)
6. 수동/능동 — 받는가, 응답하는가. (Q4, Q5)
7. 재구성: being mode 행동 한 가지를 뽑는다. (Q5, Q8, Q18)
8. (선택) 정체성의 닻인지 점검한다 — Eckhart의 "empty of knowledge". (Q9)

### Heuristics (8개)
- 명사로만 말할 수 있으면 having. (Q3)
- "잃으면 나는 누구인가"에 무너지면 having. (Q6, Q7)
- 성공 기준이 "양이 늘면"이면 모드 전환 고려. (Q15)
- 들어와 저장되면 having, 들어와 응답하면 being. (Q4, Q5)
- "have" 관용구는 일단 의심. (Q3, Q12)
- Tennyson(대상 손상/가져감) vs Basho(대상 그대로/내가 변함). (Q13)
- 생존을 위한 having은 그대로 둔다. (Q14)
- 기본값은 having — 의식적 재구성이 없으면 회귀. (Q2, Q16)

### Anti-patterns
- 소유 자체를 죄악시, having=악/being=선 도덕화, 수동 수용을 학습으로 인정, 재구성 행동을 여러 개로, 언어 진단 건너뛰고 행동으로 점프, being을 신비화(추상 명상)로 곡해.

### Open tensions (그대로 인수, summary에서)
- "활동도 가질 수 있는 것 아닌가"(스킬을 가졌다, 경험을 쌓았다) vs Q3의 "활동은 소유될 수 없다" — 부분 해소: grammar level은 having이라도 character level에서 정체성의 담보로 쥐느냐가 진단 기준(Q9, Q14).
- "I am what I do"의 위치 — being인지 having의 변형인지 *The Art of Being* raw에서 미해소.
- 개인 진단 vs 사회 구조 비판의 균형 — Q2/Q16은 having이 구조적 강제 산물이라 하는데 개인 절차만으로 충분한가. *To Have or To Be?* Ch.6 verbatim 미확보로 부분 해소.

## Decision

### 트리거
SKILL.md description에 다음을 박았다:
- 사용자 자연어 표현 14개+ (한국어 위주, 영어 보조): "다 못 읽었어", "노트 정리해야 하는데", "강의 다 들었는데 남는 게 없어", "책을 다 사놓고", "이거 마스터하고 싶어", "스펙 더 쌓아야", "자격증 따야", "팔로워가 안 늘어", "관계를 가졌는데", "사랑에 빠졌어", "이걸 잃으면 나는 끝", "내가 이 정도는 안다", "회의가 너무 많아", "할 일이 쌓였어".
- 작업·상황 카테고리 7개: 학습/독서/강의 진척, 노트·자료·자격증·팔로워·인맥·직함의 축적, 구매·소비, 관계·사랑·자기소개, 정체성 흔들림("이걸 잃으면"), "더 많이 vs 더 깊이"의 갈림길, 글쓰기/회의/계획에서 명사·"가진다" 중심 문장.
- "사용자가 '프롬', 'having mode', '소유 모드', 'being mode' 라고 명시하지 않아도 반드시 호출한다" 한 줄 — Triggering guide의 "명시 안 해도 트리거" 조항.
- should-NOT-trigger 경계: 생존·도구적 소유의 판단(약, 식비, 응급 비용 = existential having), 단기 거래·계약·법적 소유, 응급 상황.

이유: under-trigger가 가장 큰 실패 모드(Principle #1). "having mode"라는 직역어만 넣으면 일반 사용자 prompt에서 잡히지 않는다. 한국어 사용자가 일상에서 던질 법한 "다 못 읽었어 / 자격증 따야 / 이걸 잃으면" 같은 자연 표현이 들어가야 학습·정체성·구매·관계 진단에서 자동 호출된다.

### 스킬 단위
한 스킬에 8개 mental move + 8개 heuristic + 6개 anti-pattern을 다 묶었다. 더 작게 쪼개지 않은 이유:
- 프롬의 사고는 "언어 진단 → 두 詩 테스트 → 성공 기준 → motto → 출처 → 수동/능동 → 재구성 → 정체성 닻"의 한 사이클이 작동할 때만 figure-character가 살아난다. "언어 진단"만 떼면 단순 NVC(비폭력 대화)와 구별 안 되고, "재구성"만 떼면 일반 코칭과 구별 안 된다.
- substantive task(자기 정의 재구성, 학습 흐름 재설계, 관계 정리)에서 호출되어야 가치가 있는 크기 — Principle #5에 부합. 너무 잘게 쪼개면 LLM이 단독으로 처리 가능하다 판단해 호출 안 한다.
- 8 moves가 무겁다는 우려는 있으나, 진단(1~6) → 재구성(7) → 닻 점검(8 선택)의 3블록 구조로 묶여 있어 실제 호출 시 모델이 활동에 맞게 일부만 적용할 수 있다.

### 포함
- mental moves 8개 전부 procedure로 살림 (1:1 매핑).
- heuristic 8개 전부 살림 — 거장의 진단 직관이 가장 많이 빠져나가는 곳이라 압축하지 않았다.
- examples 2개 — (1) 학습/독서 진척 (Q4, Q5, Q15 매핑), (2) 자기소개/정체성 흔들림 (Q6, Q17 매핑). 프롬의 사고는 추상 원칙만으로 전염되지 않기 때문에 구체 사례가 필요하다(Principle #4). 사랑(Q11) 예시는 결이 너무 다르고 anti-pattern 위험(연애 상담으로 미끄러질 가능성)이 있어 제외, 학습·정체성 두 결로 잡았다.
- Output expected 섹션으로 산출물 형태를 3블록(Having 신호 / Being 재구성 1문장 / 행동 1개)으로 못박음. 특히 "행동 한 개" 제약은 헤리스틱·anti-pattern 양쪽에서 강화했다(여러 개면 메타 레벨에서 again having으로 미끄러진다는 안티패턴 명시).

### 의도적으로 잘라낸 것
- **Open tensions 3개** — ADR에는 남기되 SKILL.md에는 안 넣음. 모델이 매번 읽을 필요 없는 메타 정보이고, "I am what I do"의 위치 같은 미해소 논점은 사용자 작업에 직접 닿지 않는다(Principle #6, progressive disclosure).
- **Marx와 Eckhart의 doctrinal lineage** — Eckhart는 procedure 8단계의 괄호 안에서만 인용(닻 점검의 근거로). Marx의 Q16 ("the less you are, the more you have")는 heuristic의 "기본값은 having" Why로만 압축. 두 인물의 사상사를 본문에 풀어 쓰면 lean이 깨진다.
- **Chapter 2의 conversing/remembering/reading/faith 영역** — raw의 verbatim 미확보 영역. summary에서도 "다른 영역에서 일반화" 처리. SKILL.md에서는 학습·정체성·구매·관계의 4영역으로 압축하고 나머지는 "글쓰기/회의/계획" 한 줄로 포섭. verbatim이 확보되면 references/conversing.md 같은 형태로 분리해 보강 예정.
- **사회 구조 비판(*To Have or To Be?* Ch.6 "New Man / New Society")** — 개인 진단·재구성 스킬의 작업 범위를 벗어남. raw에서 verbatim도 미확보. open tension으로만 ADR에 남기고 스킬 본문에서는 제외. 단, heuristic "기본값은 having"에 "사회·언어·경제 구조가 그쪽으로 기울여 놓았다"는 한 줄로 자각만 살림.
- **"existential having vs characterological having" 용어 자체** — 본문에서는 용어 없이 "생존을 위한 having은 그대로 둔다 — 정체성의 닻이 된 having만 손본다"로 풀어 썼다. 학술 용어가 트리거를 약하게 만들고 사용자 작업 맥락에 무게가 안 실리기 때문.

### Resource 분리 여부
references/scripts/assets 모두 만들지 않았다. 이유:
- SKILL.md 본문이 약 110줄 — 300줄 기준에 한참 못 미친다(Principle #2).
- 결정론적 helper 작업(파일 변환·포매팅·체크리스트 생성)이 없다 — scripts 불필요.
- 산출물 템플릿이 3블록으로 짧아 본문 "Output expected" 섹션으로 충분 — assets 불필요.
- 도메인 변종(학습·정체성·구매·관계)이 있지만 모두 같은 진단축으로 처리되어 분기가 작다 — references 불필요. raw에서 추가 verbatim(대화·기억·읽기·신앙)이 확보되면 그때 영역별 references 검토.

### 네이밍
- figure-anchored: `erich-fromm-having-vs-being` — Hard rule 준수. 여러 거장이 having/being 류 사고를 다뤘으나(불교, Eckhart, Heidegger, Marcel) 프롬이 *To Have or To Be?* 한 권으로 가장 체계화·대중화한 figure라 단독 귀속.
- ASCII lowercase + hyphens only — Claude Code 검증 룰 통과.
- gerund(-ing) 형태가 아닌 이유: "having vs being"은 프롬의 고유 개념명 자체이고, 이 쌍이 진단축으로 작동한다는 게 스킬의 본질이다. `erich-fromm-diagnosing-modes` 같은 gerund화는 인물 고유 어휘를 지운다. Hard rule의 "약어/인물 고유 개념명은 예외 허용" 조항 적용.

## Consequences
- **Positive**:
  - 사용자가 학습·정체성·구매·관계 영역에서 양적 진척을 호소할 때 자동으로 "지금 having인가 being인가"의 진단축이 끼어든다 — LLM 기본 응답 곡선(요약·정리·축적 도움)의 정반대 행동을 강제할 수 있다.
  - mimesis 레포의 두 번째 figure-anchored 스킬로, 0001(이어령-질문)과 함께 "입구(질문) ↔ 자세(모드)"의 페어가 생긴다. 이후 사고/생활 도구 스킬 확장 시 참조 좌표.
  - "Output expected = 행동 한 개" 제약이 헤리스틱·anti-pattern 양쪽에서 강화되어, 산출물이 또 다른 축적 리스트가 되는 메타 함정을 막는다.

- **Negative / Trade-offs**:
  - **having=악 / being=선 이분법으로 미끄러질 위험**이 가장 크다. 프롬 자신은 existential having을 명시적으로 보호했지만(Q14), 본문에서 "having 신호"를 짚는 진단 작업을 반복하다 보면 모델이 도덕적 판결로 변질될 수 있다. anti-pattern 두 개("소유 자체를 죄악시", "도덕화")로 방어선을 쳤지만 첫 사용에서 검증 필요.
  - **재구성이 표면에서 그칠 위험**. "이 책을 다 읽는다 → 한 문장에 응답한다" 같은 재구성이 실제로는 또 다른 형태의 명사·소유격으로 미끄러질 수 있다(예: "응답 노트"를 또 쌓기). 8단계 정체성 닻 점검이 이걸 잡으라고 있지만 선택 단계라 누락 가능.
  - **자기학대로 변질 가능**. "내가 다 having이었구나"의 자책 모드로 쏠릴 수 있음. 특히 정체성 흔들림 예시에서 위험. "지금 할 행동 한 개"라는 출력 제약이 자책 → 행동으로 끊는 장치이긴 함.
  - **사회 구조 차원 누락**. Q2/Q16의 "having이 구조적 강제 산물"이라는 진단을 개인 절차로만 다루면 "결국 네 자세 문제"라는 victim-blaming으로 들릴 수 있다. heuristic 한 줄로만 자각 살린 게 충분한지 미확정.

- **Open questions**:
  - "I am what I do"(motto 2번)가 being인지 having의 변형인지 — 사용자가 "활동/직업으로 자기를 정의"하는 경우 어느 쪽으로 진단해야 하나. 첫 사용 후 examples 추가 필요할 수 있음.
  - 8단계 procedure가 짧은 작업에서 over-engineering 되지 않는지. should-NOT-trigger 경계를 박았지만 모델이 무시할 수 있음.
  - 영어 prompt에서 트리거 강도. 한국어 자연 표현이 많아 영문 사용자 대상 호출이 약할 가능성. 글로벌 확장 시 영문 트리거어 보강 필요.
  - 0001(이어령-질문)과 description 일부 충돌(둘 다 "재정의 / 프레임 바꾸기" 영역에 걸침). 실제 호출 시 어느 쪽이 먼저 잡히는지, 페어로 잡히는지 관찰 필요.

## Application log
- TBD — 첫 사용 후 갱신. 특히 다음 다섯 가지를 기록한다:
  1. having=악 / being=선 도덕화로 미끄러진 케이스가 있는가.
  2. "지금 할 행동 한 개"가 실제로 한 개로 떨어졌는가, 리스트로 부풀었는가.
  3. 학습·정체성·구매·관계 4영역 중 어디서 가장 자주 호출되는가.
  4. 0001(이어령-질문)과 동시 호출되는 사례, 충돌 사례.
  5. 영어 prompt 호출 여부.
