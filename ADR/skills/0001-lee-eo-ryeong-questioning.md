# ADR 0001: 이어령 — 질문으로 사고하기

- **Status**: Accepted
- **Date**: 2026-05-23
- **Related skill**: `.claude/skills/lee-eo-ryeong-questioning/`
- **Source figure(s)**: 이어령(Lee Eo-ryeong)
- **Primary sources**:
  - [research raw](../../research/lee-eo-ryeong/questioning-as-thinking-raw.md)
  - [research summary](../../research/lee-eo-ryeong/questioning-as-thinking-summary.md)

## Context
mimesis 레포의 첫 스킬이다. "거장의 사고를 재현 가능한 절차로 박제한다"는 컨셉을 가장 강하게 증명할 후보로 이어령의 "질문 → 사색" 양식을 골랐다. 이유:
- AI가 정답을 즉답하는 시대일수록, 사용자가 LLM에게 "답"을 받기보다 "질문을 갈아주는 도구"를 원하는 빈도가 늘고 있다. 그런데 LLM의 기본 응답 곡선은 정반대 — 빠르게 정답을 내려놓는 쪽이다. 이 충돌 지점에 거장 한 명의 사고 양식을 끼워 넣을 필요가 있었다.
- 이어령은 평생 "정답이 아니라 정문(正問)"을 자신의 사고 정체성으로 선언했고, 단어 하나를 의심해 통설을 뒤집는 mental move가 인터뷰·강연·저작 전반에서 일관되게 반복된다. 즉 figure-anchored 스킬로 박제하기 좋은 일관성이 있다.
- 우리 작업 흐름(기획 카피, 키노트 도입, 비평/에세이, 개념 재정의)에서 "다들 같은 답을 말할 때 다른 답을 짓는 첫 한 줄"이 자주 필요한데, 이 자리가 정확히 이어령식 mental move의 sweet spot이다.

## Decomposition
summary의 핵심 구조를 옮긴다. Q번호는 summary/raw의 인용 번호를 그대로 유지.

### Principles (이 인물의 사고 정체성)
1. 정답(正答)이 아니라 정문(正問)을 짠다. (Q2, Q5)
2. 좋은 질문은 크지 않고 좁다 — 단, 좁음 ≠ 사소함, "본질을 찌르는 좁음"이어야 한다. (Q1, Q2)
3. 사고는 지식의 축적량이 아니라 물음표↔느낌표의 시계추 진동. (Q3)
4. 상식·통설은 한 번 뒤집어본다("덮어놓고 살지 말기"). (Q4, Q8)
5. 답은 외부 검색이 아니라 내부 사색에서 짓는다. (Q5)
6. 생각은 독백이 아니라 대화(다이얼로그). (Q7)

### Mental moves (재현 가능 절차)
1. 대상 앞에서 멈춘다. (Q4, Q8)
2. 명제 안 단어 하나를 의심한다. (Q4, Q7, Q8)
3. "X란 무엇인가" 형태의 큰 질문 기각, 좁은 사례로 깎는다. (Q1)
4. 관심 → 관찰 → 관계 세 박자 회전. (Q7)
5. 사전적·물리적 답에서 한 칸 비켜 의미 층위로 답한다. (Q6)
6. 검색 충동을 사색 신호로 바꾼다. (Q5)
7. 답을 다음 물음표 출발점으로 넘긴다. (Q3)
8. 상대에게 던져 변증법적으로 굴린다. (Q7)

### Heuristics
- "X란 무엇인가" → 기각·축소 (Q1)
- 아이의 질문 같은데 어른이 답하기 곤란 → 정문 채택 (Q2)
- 모두 같은 답 → 의미 층위에서 다른 답 (Q6)
- 큰 주제 → 부르는 말 한 마디부터 (Q8)
- "유식·박식" 칭찬 → 신호로 알아차림 (Q3)

### Anti-patterns
- 정답 사냥, 검색으로 사색 대체, 큰 추상 질문, 유식·박식 자기 정체화, 통설 무비판 수용, 독백형 사고.

### Open tensions (그대로 인수)
- 큰 질문 경계(Q1) vs 아이의 본질적 질문(Q2) — "큰" = 추상·총체적, "본질적" = 좁은 좌표의 날카로움으로 부분 해소.
- 다이얼로그(Q7) vs 외로움/고립(Q9) — 미해소.
- 정답 거부(Q2, Q5) vs 느낌표를 산다(Q3) — 느낌표를 종착 정답이 아닌 다음 물음표 출발점으로 재정의해 부분 해소.

## Decision

### 트리거
SKILL.md description에 다음을 박았다:
- 사용자 자연어 표현 9개: "이게 맞나", "근데 왜 이렇게 부르지", "다들 이렇게 말하는데", "당연한 거 아닌가", "정의를 다시", "프레임을 바꾸고 싶다", "남들과 다른 각도", "기획·카피·강연 도입이 진부하다", "AI가 답을 다 주는데 나는 뭘 하지".
- 작업 종류 5개: 개념 비평, 에세이, 키노트, 슬로건, 리브랜딩, 문제 재정의.
- "사용자가 '이어령' 혹은 '질문법'이라고 명시하지 않아도 반드시 호출한다" 한 줄을 명시 — Triggering guide의 "명시 안 해도 트리거" 조항.
- should-NOT-trigger 경계: 빠른 사실 조회 / 안전·생명 직결 자리.
이유: under-trigger 가 가장 큰 실패 모드(Principle #1). 직역체("정문", "正問")만 넣으면 한국어 사용자 prompt에서 잡히지 않는다. 자연어 변형 다수가 들어가야 의미 재정의 작업에서 자동 호출된다.

### 스킬 단위
한 스킬에 8개 mental move + 5개 heuristic + 5개 anti-pattern을 다 묶었다. 더 작게 쪼개지 않은 이유:
- 이어령의 사고는 "멈춤 → 단어 의심 → 좁힘 → 관찰/관계 → 의미층 답 → 다음 물음표 → 대화"의 한 사이클이 통째로 작동할 때만 figure-character가 살아난다. "단어 의심"만 떼면 단순 비판적 사고와 구별 안 된다.
- substantive task(키노트 도입, 리브랜딩 컨셉)에서 호출되어야 가치가 있는 크기 — Principle #5에 부합.

### 포함
- mental moves 8개 전부 procedure로 살림 (1:1 매핑).
- 핵심 heuristic 5개 전부 살림.
- examples 2개 (강연 도입 + 추모 글) — summary의 "얼음→봄이 온다", "돌아가신다" 사례를 작업 맥락으로 번안. 거장의 사고를 추상 원칙만으로 전염시킬 수 없기 때문(Principle #4).
- Output expected 섹션으로 산출물 형태 못박음 (의심한 단어 / 좁힌 정문 / 의미 층위 답 + 다음 물음표).

### 의도적으로 잘라낸 것
- **Q9(외로움/고립을 들어가라)** — open tension 미해소 상태고, AI assistant 컨텍스트에서 "고립을 권하라"는 실행 가능 mental move로 번역 불가. 제외.
- **유식·박식 거부의 정서적 측면** — heuristic 1줄로만 남기고 본문 강조에서 뺐다. 이건 인물의 정체성이지 사용자가 바로 쓸 move가 아니라서 lean을 깬다(Principle #6).
- **천자문 사례 자체** — example로 옮기는 대신 procedure의 괄호 예시("현(玄)이 왜 검다지?")로만 인용. 실제 사용자 작업과 거리가 멀어 example 자리는 작업 맥락(키노트, 추모 글)에 양보.
- **Open tensions / Gaps inherited from raw** — ADR에는 남기되 SKILL.md에는 안 넣음. 실행 시 모델이 매번 읽을 필요 없는 메타 정보다(Principle #6, progressive disclosure).

### Resource 분리 여부
references/scripts/assets 모두 만들지 않았다. 이유:
- SKILL.md 본문이 약 90줄 — 300줄 기준에 한참 못 미친다(Principle #2).
- 결정론적 helper 작업(파일 변환·포매팅)이 없다 — scripts 불필요.
- 산출물 템플릿이 짧아 본문 "Output expected" 4줄로 충분 — assets 불필요.
- 도메인 변종도 없다 — references 불필요.
큰 거장(예: 파인만 학습법 전체)으로 확장될 때 분리를 검토.

### 네이밍
- figure-anchored: `lee-eo-ryeong-questioning` — Hard rule 준수.
- gerund: `questioning` — 행위 단위. "질문법"보다 한국어 prompt 자연어에 더 잘 잡힌다.
- ASCII lowercase + hyphens only — Claude Code 검증 룰 통과.

## Consequences
- **Positive**:
  - 사용자가 카피·도입·재정의 류 작업을 던졌을 때 자동으로 "한 번 멈추고 단어 하나를 의심하는" 흐름이 끼어든다 — LLM 기본 응답 곡선의 정반대 행동을 강제할 수 있다.
  - mimesis 레포의 컨셉(거장-귀속 스킬)에 대한 첫 reference implementation이 생긴다 — 이후 스킬 작성 시 형식 기준점.
  - 한국 거장 자료를 1차 출처로 처리하는 패턴(인터뷰 영상/구글북스 미리보기 + 원문 인용 + Q번호 추적)이 굳어진다.
- **Negative / Trade-offs**:
  - Description에 한국어 키워드를 많이 넣어 영어 prompt에서는 트리거가 약할 수 있다. 글로벌 사용 시 영문 트리거어 보강 필요.
  - Mental move 8단계가 무거워서 짧은 작업에서 over-engineering 위험. should-NOT-trigger 경계를 description에 박았지만 모델이 무시할 수 있다.
  - 이어령의 사고는 한국어 단어 자체를 의심하는 케이스(현/돌아가신다)가 강점인데, 비한국어 컨텍스트에서는 이 강점이 약해진다.
- **Open questions**:
  - 큰 질문(Q1)과 본질적 질문(Q2)의 경계를 모델이 실제로 잘 판단할까? 첫 사용 후 example 추가가 필요할 수 있다.
  - "검색 충동을 사색 신호로" — LLM에게 self-restraint를 시키는 건데 실제로 30초 멈춤이 일어날지 검증 필요.
  - 다른 거장 스킬(예: feynman-explaining-simply)과 description이 부분 충돌할 가능성. 둘 다 "설명·재정의" 영역.

## Application log
- TBD — 첫 사용 후 갱신. 특히 (1) over-trigger / under-trigger 비율, (2) 영어 prompt에서의 호출 여부, (3) 큰 질문 기각 heuristic 실제 작동 여부 세 가지를 기록한다.
