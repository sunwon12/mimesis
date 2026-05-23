# Raw Research — Andrej Karpathy: Software 3.0 and the LLM Paradigm

- **Date**: 2026-05-23
- **Assumptions** (입력 부족 시):
  - 토픽 범위를 카파시의 "AI/소프트웨어를 보는 lens" 계열 전체로 잡았다: Software 1.0/2.0/3.0 ontology, LLM OS / cognitive core, vibe coding / "English as programming language", learning-by-building (Zero to Hero, micrograd, nanoGPT, llm.c), 그리고 agent 시대의 한계·"decade of agents".
  - 후속 단계에서 figure shape 결정(`diagnostic` vs `collaborator`)을 위해 (a) 카파시의 "사고 동작"이 명확히 드러나는 인용 + (b) 그의 voice·반복 표현(짧고 비유적, "spirits/ghosts/utility/fab/OS", 자기 자신 hedge 패턴) 둘 다 수집.
  - 모국어 = 영어, 보조 = 한국어. X.com 본문은 paywall로 직접 fetch 실패 → 2차 인용(검색 스니펫에 포함된 본문 + 카파시 본인이 talk에서 직접 인용한 본문)을 채택하고 신뢰도에 명시.
- **Search queries used**:
  - "Karpathy Software 2.0 Medium 2017 blog post original"
  - "Karpathy Software 3.0 YC AI Startup School 2025 talk transcript"
  - "Karpathy LLM OS cognitive core intro to large language models talk"
  - "Karpathy vibe coding tweet hottest new programming language is English"
  - "Karpathy vibe coding original tweet February 2025 fully give in to the vibes"
  - "Karpathy LLM OS tweet image diagram November 2023"
  - "Karpathy cognitive core tweet LLM small model"
  - "Karpathy nanoGPT README minimal from scratch understand transformer"
  - "Karpathy micrograd README neural net 60 line educational"
  - "Karpathy Zero to Hero YouTube series neural networks from scratch backpropagation"
  - "Karpathy llm.c README C/CUDA no PyTorch educational training GPT-2"
  - "Karpathy software is changing again transcript software 3.0 people spirits"
  - "Karpathy llms.txt building for agents tweet machine consumable"
  - "Karpathy decade of agents agents are coming tweet 2025 Dwarkesh interview"
  - "Karpathy Dwarkesh Patel interview 2025 RLHF reward hacking agents not working"
  - "Karpathy Iron Man suit Iron Man robot autonomy LLM augmentation"
  - "Yann LeCun criticism LLM auto-regressive dead end 2024"
  - "Gary Marcus criticism vibe coding Karpathy"
  - "Andrew Ng critique vibe coding AI-assisted coding 2025"
  - "Simon Willison vibe coding critique Karpathy not all AI-assisted"
  - "카파시 소프트웨어 3.0 한국어 번역 LLM 패러다임"
  - "카파시 Software 2.0 한국 개발자 블로그 신경망 패러다임"

## Primary sources

1. **"Software 2.0"** — Andrej Karpathy, Medium, 2017-11-11
   - URL: https://karpathy.medium.com/software-2-0-a64152b37c35
   - 신뢰도: high — 본인이 직접 쓴 원문 에세이.

2. **"Software Is Changing (Again)" (a.k.a. Software 3.0 keynote)** — Andrej Karpathy, YC AI Startup School, 2025-06-17 (talk) / 2025-06-18 (write-up date)
   - URLs:
     - Talk video: https://www.youtube.com/watch?v=LCEmiRjPEtQ
     - Latent.Space transcript/annotation: https://www.latent.space/p/s3
     - Singju Post full transcript: https://singjupost.com/andrej-karpathy-software-is-changing-again/
     - Kyle Howells notes (verbatim slide captions): http://ikyle.me/blog/2025/andrej-karpathy-software-is-changing-again
     - Karpathy's own X thread linking slides: https://x.com/karpathy/status/1935519334123848101
   - 신뢰도: high — 본인 talk. 2차 transcript는 slide captions와 일치할 때만 인용.

3. **"Intro to Large Language Models"** ("1hr Talk") — Andrej Karpathy, YouTube, 2023-11
   - URLs:
     - Archive: https://archive.org/details/youtube-zjkBMFhNj_g
     - Original YT: https://www.youtube.com/watch?v=zjkBMFhNj_g
   - 신뢰도: high — 본인 talk. LLM OS / kernel process 프레임의 원본.

4. **"LLM OS" tweet** — Andrej Karpathy, X, 2023-11-11
   - URL: https://x.com/karpathy/status/1723140519554105733
   - 신뢰도: medium — 본인 트윗이지만 paywall로 직접 fetch 실패. 다수 출처에서 동일 본문 인용으로 교차 확인됨.

5. **"The hottest new programming language is English" tweet** — Andrej Karpathy, X, 2023-01-24
   - URL: https://x.com/karpathy/status/1617979122625712128
   - 신뢰도: medium — 본인 트윗, paywall. 본문이 한 문장이라 교차 확인 안전.

6. **"Vibe coding" tweet** — Andrej Karpathy, X, 2025-02-02
   - URL: https://x.com/karpathy/status/1886192184808149383
   - 신뢰도: medium — 본인 트윗, paywall. 검색 스니펫에 전체 본문 포함되어 교차 확인.

7. **"Cognitive core" tweet** — Andrej Karpathy, X, 2025-06-27
   - URL: https://x.com/karpathy/status/1938626382248149433
   - 신뢰도: medium — 본인 트윗, paywall. 본문은 검색 스니펫에서 인용.

8. **Karpathy on Dwarkesh Patel Podcast — "AGI is still a decade away"** — 2025-10
   - URLs:
     - Dwarkesh transcript: https://www.dwarkesh.com/p/andrej-karpathy
     - Simon Willison summary with quotes: https://simonwillison.net/2025/Oct/18/agi-is-still-a-decade-away/
   - 신뢰도: high — 본인 발언, transcript 공개.

9. **"2025 LLM Year in Review"** — Andrej Karpathy, bearblog, 2025-12 ~ 2026-01
   - URL: https://karpathy.bearblog.dev/year-in-review-2025/
   - 신뢰도: high — 본인 블로그 글.

10. **`nanoGPT` README** — Andrej Karpathy, GitHub
    - URL: https://github.com/karpathy/nanoGPT/blob/master/README.md
    - 신뢰도: high — 본인 repo.

11. **`micrograd` README** — Andrej Karpathy, GitHub
    - URL: https://github.com/karpathy/micrograd/blob/master/README.md
    - 신뢰도: high — 본인 repo.

12. **`llm.c` README** — Andrej Karpathy, GitHub
    - URL: https://github.com/karpathy/llm.c/blob/master/README.md
    - 신뢰도: high — 본인 repo.

13. **"Neural Networks: Zero to Hero"** — Andrej Karpathy, course page
    - URL: https://karpathy.ai/zero-to-hero.html
    - 신뢰도: high — 본인이 작성한 코스 설명.

14. **"안드레 카파시 '지금은 소프트웨어 3.0의 시대'"** — Byline Network (한국), 2025-06-23
    - URL: https://byline.network/2025/06/23-450/
    - 신뢰도: medium — 국내 IT 매체의 talk 정리. 한국 수용 자료로만 사용.

15. **"소프트웨어 3.0 시대를 맞이하며"** — Toss Tech Blog
    - URL: https://toss.tech/article/software-3-0-era
    - 신뢰도: medium — 국내 기술 블로그. 한국 실무자의 재정리/수용 자료.

### Critique sources

C1–C3 sources (반론·한계):

- **Yann LeCun on auto-regressive LLMs as "dead end"** (Newsweek, 2024/2025) — https://www.newsweek.com/nw-ai/ai-impact-interview-yann-lecun-llm-limitations-analysis-2054255
- **Gary Marcus, "Is vibe coding dying?"** — Marcus on AI Substack — https://garymarcus.substack.com/p/is-vibe-coding-dying
- **Andrew Ng on vibe coding terminology** — Klover.ai write-up + Slashdot — https://www.klover.ai/andrew-ng-pushes-back-ai-vibe-coding-hard-work-not-hype/ , https://developers.slashdot.org/story/25/06/05/165258/andrew-ng-says-vibe-coding-is-a-bad-name-for-a-very-real-and-exhausting-job
- **Simon Willison, "Not all AI-assisted programming is vibe coding"** — https://simonwillison.net/2025/Mar/19/vibe-coding/
- **Karpathy himself hedging on Dwarkesh podcast** — same as source 8 above (self-critique counts as raw evidence of where the frame breaks)

## Quotes & evidence

### Q1 — Software 2.0 core thesis
> "Neural networks are not just another classifier, they represent the beginning of a fundamental shift in how we develop software. They are Software 2.0."
>
> — Karpathy, "Software 2.0", Medium, 2017-11-11 (opening paragraph).

**Context**: 에세이 도입부. 신경망을 단순 분류기로 보지 말고 새로운 소프트웨어 작성 스택으로 보자는 주장의 헤드라인.

### Q2 — Software 1.0 vs 2.0 정의
> "The 'classical stack' of Software 1.0 is what we're all familiar with — it is written in languages such as Python, C++, etc. It consists of explicit instructions to the computer written by a programmer. ... Software 2.0 is written in much more abstract, human unfriendly language, such as the weights of a neural network."
>
> — Karpathy, "Software 2.0", Medium, 2017-11-11 (정의 문단).

**Context**: 두 스택의 prose-level 정의. 핵심은 "explicit instructions"(1.0) 대 "weights"(2.0).

### Q3 — "Compiling from data" 메타포
> "In Software 1.0, human-engineered source code (e.g. some .cpp files) is compiled into a binary that does useful work. In Software 2.0 most often the source code comprises 1) the dataset that defines the desirable behavior and 2) the neural net architecture ... The process of training the neural network compiles the dataset into the binary — the final neural network."
>
> — Karpathy, "Software 2.0", Medium, 2017-11-11 (메타포 문단).

**Context**: 데이터셋이 소스코드, 학습이 컴파일러, 가중치가 바이너리라는 1:1 매핑. 카파시가 반복 사용하는 추상화 패턴(기존 개념에 새 paradigm을 끼워 넣어 등치시키기).

### Q4 — "Better than you" 단정
> "A neural network is a better piece of code than anything you or I can come up with in a large fraction of valuable verticals."
>
> — Karpathy, "Software 2.0", Medium, 2017-11-11 ("Benefits" 섹션 마지막).

**Context**: 신경망이 사람이 짠 코드보다 낫다는 단정. 카파시 voice에서 자주 보이는 "you and I"가 들어간 친근한 단정형.

### Q5 — Software 2.0 한계, 카파시 본인 인정
> "we're left with large networks that work well, but it's very hard to tell how."
>
> "The 2.0 stack can fail in unintuitive and embarrassing ways ... they can 'silently fail', e.g., by silently adopting biases in their training data."
>
> — Karpathy, "Software 2.0", Medium, 2017-11-11 ("Limitations" 섹션).

**Context**: 같은 에세이에서 본인이 단 caveat. 해석성·silent failure·adversarial example을 한계로 거론.

### Q6 — "The hottest new programming language is English"
> "The hottest new programming language is English."
>
> — Karpathy, X, 2023-01-24 (https://x.com/karpathy/status/1617979122625712128).

**Context**: ChatGPT 등장 직후의 한 줄 트윗. 이후 Software 3.0 framing의 슬로건이 됨. 카파시의 "한 줄로 패러다임을 박는" 트윗 습관의 대표 사례.

### Q7 — LLM OS as kernel process
> "With many 🧩 dropping recently, a more complete picture is emerging of LLMs not as a chatbot, but the kernel process of a new Operating System."
>
> — Karpathy, X, 2023-09-28 (https://x.com/karpathy/status/1707437820045062561) [본문은 검색 스니펫에서 인용].

**Context**: ChatGPT의 멀티모달·툴·인터프리터·플러그인이 추가된 직후. "LLM은 챗봇이 아니라 OS의 커널 프로세스"라는 그의 핵심 비유의 출처.

### Q8 — LLM OS 사양 트윗 (반쯤 농담조의 spec sheet)
> "LLM OS. Bear with me I'm still cooking. Specs:
> - LLM: OpenAI GPT-4 Turbo 256 core (batch size) processor @ 20Hz (tok/s)
> - RAM: 128Ktok
> - Filesystem: Ada002"
>
> — Karpathy, X, 2023-11-11 (https://x.com/karpathy/status/1723140519554105733) [본문은 검색 결과 스니펫에서 인용].

**Context**: "Intro to LLMs" 강연과 같은 주에 올라온 후속 트윗. 카파시는 LLM을 CPU/RAM/디스크 같은 컴퓨터 구성요소로 1:1 매핑한다.

### Q9 — Context window as RAM (Intro to LLMs)
> "The context window is your finite precious resource of your working memory of your language model ... you can imagine the kernel process this LLM trying to page relevant information in and out of its context window to perform your task."
>
> — Karpathy, "Intro to Large Language Models" talk, 2023-11 [후반부 LLM OS 섹션, 위의 wisdominanutshell 트랜스크립트에서 verbatim 인용].

**Context**: LLM OS 섹션에서 context window를 RAM에, 검색/툴을 paging에 매핑하는 부분. 카파시의 "기존 컴퓨팅 메타포를 LLM에 끼워 넣기" 작동의 명시적 예.

### Q10 — Software 3.0 정의 (YC AI Startup School)
> "Software 1.0 was normal code. Software 2.0 is machine learning models ... And now software 3.0 with LLMs."
>
> "LLMs are a new kind of computer, and you program them in English."
>
> "software is changing quite fundamentally again."
>
> — Karpathy, "Software Is Changing (Again)" keynote, YC AI Startup School, 2025-06-17 (Kyle Howells의 verbatim slide-caption notes 및 latent.space).

**Context**: 강연 전반부. 2017년 Software 2.0의 후속편으로 3.0을 도입.

### Q11 — "Software 3.0 is eating 1.0/2.0"
> "Software 3.0 is eating 1.0/2.0" — and — "a huge amount of software will be rewritten."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript & Kyle Howells notes).

**Context**: Andreessen의 "software is eating the world"에 대한 카파시의 갱신. 그의 비유 재활용 패턴.

### Q12 — LLMs as utilities / fabs / OS
> "LLMs have properties of utilities, of fabs, and of operating systems."
>
> — Karpathy, YC AI Startup School 2025 keynote (Kyle Howells verbatim slide captions).

**Context**: LLM을 하나의 메타포로 환원하지 않고 여러 계층을 동시에 짚는 부분. "유틸리티(전기)·팹(반도체)·OS" 세 비유를 동시에 깐다.

### Q13 — 1960s mainframe 시대 비유
> "we are computing circa ~1960s."
>
> — Karpathy, YC AI Startup School 2025 keynote (Kyle Howells verbatim).

**Context**: 현재 LLM 사용 방식 — 중앙화된 거대 모델에 시간을 사서 쓰는 — 이 1960년대 timesharing mainframe과 같다는 진단. PC 혁명(로컬 cognitive core)이 아직 오지 않았다는 함의.

### Q14 — LLMs as "people spirits"
> "LLMs = 'people spirits', stochastic simulations of people."
>
> "they have a kind of emergent psychology, and are simultaneously superhuman in some ways, but also fallible in many others."
>
> — Karpathy, YC AI Startup School 2025 keynote (Kyle Howells verbatim slide captions).

**Context**: LLM을 "사람의 확률적 시뮬레이션"으로 framing. 동물처럼 진화로 만든 게 아니라 인터넷 텍스트로 빚은 "유령"이라는 그의 반복 비유의 캐릭터 카드.

### Q15 — Jagged intelligence
> "state of the art LLMs can both perform extremely impressive tasks ... while simultaneously struggle with some very dumb problems."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript).

**Context**: "jagged intelligence". 인간 IQ 곡선과 다르게 동일 모델이 박사급 문제와 초딩급 문제를 동시에 풀고 못 푼다.

### Q16 — Anterograde amnesia
> "LLMs are a bit like a coworker with Anterograde amnesia — they don't consolidate or build long-running knowledge once training is over."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript).

**Context**: LLM 메모리 한계의 의학적 메타포. "메멘토 같은 동료"를 함께 일하는 사람으로 비유.

### Q17 — Demo vs product
> "Demo is works.any(), product is works.all()."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript).

**Context**: AI agent 데모와 실제 프로덕트 사이의 간극을 한 줄로. 코드 표기(`works.any()` 등)를 메타포로 끌어쓰는 카파시 voice.

### Q18 — Iron Man suit vs Iron Man robot (autonomy slider)
> "the suit extends us in two useful ways: Augmentation ... Autonomy."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript, paraphrased slide caption — exact wording from slide).

**Context**: 완전 자율 로봇이 아니라 "토니 스타크가 그대로 있는 슈트"를 만들라는 권고. 자율성 슬라이더(Cursor, Perplexity, Tesla autopilot)로 단계적 양도.

### Q19 — "Build for agents" / new category of consumer
> "There is new category of consumer/manipulator of digital information": Humans (GUIs), Computers (APIs), **NEW: Agents** (computers with human-like properties).
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space transcript slide caption).

**Context**: 사람·기계 다음의 세 번째 소비자로 agent. agent용 인터페이스(llms.txt, machine-consumable docs)가 새 design 축이라는 근거.

### Q20 — "Decade of agents" closing
> "This is the Decade of Agents." — Closing slide.
>
> Followed by: "Less AGI 2027 and flashy demos that don't work. More partial autonomy, custom GUIs and autonomy sliders."
>
> — Karpathy, YC AI Startup School 2025 keynote (latent.space slide caption + Kyle Howells).

**Context**: "2025는 에이전트의 해"라는 업계 슬로건에 대한 카파시의 응답: "해가 아니라 10년이다."

### Q21 — Vibe coding 원조 트윗 (2025-02-02)
> "There's a new kind of coding I call 'vibe coding', where you fully give in to the vibes, embrace exponentials, and forget that the code even exists. It's possible because the LLMs (e.g. Cursor Composer w Sonnet) are getting too good. Also I just talk to Composer with SuperWhisper ..."
>
> — Karpathy, X, 2025-02-02 (https://x.com/karpathy/status/1886192184808149383) [본문은 검색 스니펫·Wikipedia·CodeRabbit 정리에서 verbatim].

**Context**: vibe coding 개념 명명. 본인은 1년 후 retrospective에서 "shower of thoughts throwaway tweet that I just fired off"라고 표현. 본인이 "throwaway tweet"으로 한 표현이 단어가 됨.

### Q22 — Vibe coding retrospective (1년 후 자평)
> "A lot of people quote tweeted this as 1 year anniversary of vibe coding. ... This was a shower of thoughts throwaway tweet that I just fired off ... but somehow it minted a fitting name at the right moment for something that a lot of people were feeling at the same time."
>
> — Karpathy, X, 2026-02 (https://x.com/karpathy/status/2019137879310836075) [검색 스니펫 verbatim].

**Context**: 본인이 "엔지니어링된 슬로건이 아니라 우연히 맞아떨어진 throwaway"였다고 인정. 그의 framing이 어떻게 만들어지는지 보여주는 메타 정보.

### Q23 — Cognitive core (작은 always-on LLM)
> "The race for LLM 'cognitive core' — a few billion param model that maximally sacrifices encyclopedic knowledge for capability. It lives always-on and by default on every computer as the kernel of LLM personal computing. Its features are slowly crystalizing: - Natively multimodal text/vision/audio at both input and output ..."
>
> — Karpathy, X, 2025-06-27 (https://x.com/karpathy/status/1938626382248149433) [본문은 검색 스니펫에서 verbatim].

**Context**: LLM OS에서 한 발 더 나아가 "각자 컴퓨터에 깔리는 cognitive core"로의 진화 예측. matryoshka 구조, 추론 dial, tool-use, on-device LoRA를 features로 나열.

### Q24 — Dwarkesh 인터뷰: 현재 agent는 "slop"
> "I feel like the industry is making too big of a jump and is trying to pretend like this is amazing, and it's not. It's slop."
>
> "They just don't work. They don't have enough intelligence, they're not multimodal enough, they can't do computer use and all this stuff."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10 (https://www.dwarkesh.com/p/andrej-karpathy).

**Context**: "year of agents" 분위기에 대한 본인의 반론. 같은 talk에서 "decade of agents"를 다시 박는다.

### Q25 — "Decade of agents" rephrased
> "My reaction is we'll be working with these things for a decade. They're going to get better, and it's going to be wonderful."
>
> "It will take about a decade to work through all of those issues."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10.

**Context**: agent의 실패 모드를 줄줄이 짚은 직후, 비관도 낙관도 아닌 "10년짜리 surmountable 문제" framing.

### Q26 — RL is "terrible" but everything else is worse
> "Reinforcement learning is terrible. It just so happens that everything that we had before it is much worse."
>
> "You're sucking the bits of supervision of the final reward signal through a straw and you're broadcasting that across the entire trajectory."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10.

**Context**: 본인이 OpenAI에서 RLHF 작업했음에도 RL을 "최악 중 차악"으로 framing. 비유("sucking bits through a straw") 사용 습관 명확.

### Q27 — Building ghosts, not animals
> "We're not building animals. We're building ghosts or spirits or whatever people want to call it, because we're not doing training by evolution."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10 (Simon Willison verbatim).

**Context**: "people spirits"의 이론적 근거. 진화로 빚은 동물 지능과 인터넷 텍스트로 빚은 LLM 지능은 다른 종이라는 주장.

### Q28 — Cognitive deficits 인정 (자기 코드 작업 실패담)
> "The models have so many cognitive deficits. One example, they kept misunderstanding the code."
>
> "they're very good at stuff that occurs very often on the Internet because there are lots of examples ... nanochat is not an example of those because it's a fairly unique repository ... it's intellectually intense code."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10.

**Context**: nanochat을 LLM agent로 만들어 보려 한 본인 경험담. "training distribution에서 멀어지면 무너진다"는 패턴을 자기 사례로 confirm.

### Q29 — 2025 year-in-review: jagged characteristics
> "Everything about the LLM stack is different ... so it should be no surprise that we are getting very different entities in the intelligence space, which are inappropriate to think about through an animal lens."
>
> "LLMs are emerging as a new kind of intelligence, simultaneously a lot smarter than I expected and a lot dumber than I expected."
>
> — Karpathy, "2025 LLM Year in Review", bearblog (2025-12 ~ 2026-01).

**Context**: 연말 정리. "동물 렌즈로 보지 말라"는 그의 반복 명령이 정식화됨.

### Q30 — 2025 year-in-review: Claude Code = first real LLM agent
> "[Claude Code is] the first convincing demonstration of what an LLM Agent looks like."
>
> "this little spirit/ghost that lives on your computer."
>
> — Karpathy, "2025 LLM Year in Review", bearblog.

**Context**: 본인 강연의 cognitive core / agents 비전을 실증한 첫 product가 Claude Code라는 평. "spirit/ghost"가 또 등장.

### Q31 — nanoGPT 철학: "teeth over education"
> "The simplest, fastest repository for training/finetuning medium-sized GPTs."
>
> "[nanoGPT is] a rewrite of minGPT that prioritizes teeth over education."
>
> "Because the code is so simple, it is very easy to hack to your needs."
>
> — `nanoGPT` README (https://github.com/karpathy/nanoGPT/blob/master/README.md).

**Context**: nanoGPT은 "교육용에 비해 실용성을 우선"으로 옮긴 fork. minGPT(이전 버전)와 nanoGPT 사이의 noteworthy한 line이 "이 코드가 누구를 위한 것인가"의 카파시식 분기.

### Q32 — micrograd 철학: 100/50줄, 스칼라 단위로 분해
> "[Implements] backpropagation (reverse-mode autodiff) over a dynamically built DAG and a small neural networks library on top of it with a PyTorch-like API."
>
> "Tiny, with about 100 and 50 lines of code respectively."
>
> "The DAG only operates over scalar values, so e.g. we chop up each neuron into all of its individual tiny adds and multiplies."
>
> "Potentially useful for educational purposes."
>
> — `micrograd` README (https://github.com/karpathy/micrograd/blob/master/README.md).

**Context**: 카파시의 학습 철학("동작하는 가장 작은 버전을 손으로 다시 짜라")의 코드 manifesto. 텐서가 아니라 스칼라 단위로 자르는 이유가 명시적으로 "교육적"이라고 밝혀짐.

### Q33 — llm.c 철학: 의존성 없는 reproduction
> "LLMs in simple, pure C/CUDA with no need for 245MB of PyTorch or 107MB of cPython."
>
> 메인 README에는 educational 의도가 명시: "a place for education", "the mainline `llm.c` in the root folder simple and readable", reject optimizations if complexity cost not justified.
>
> — `llm.c` README (https://github.com/karpathy/llm.c/blob/master/README.md).

**Context**: nanoGPT가 "PyTorch로 GPT를 짤 수 있다"를 보여줬다면 llm.c는 "PyTorch 없이도 짤 수 있다"를 보여준다. 같은 "minimal reproduction" 패턴의 한 단계 더 아래 레이어.

### Q34 — Zero to Hero 코스 framing
> "A course by Andrej Karpathy on building neural networks, from scratch, in code."
>
> "It starts with the basics of backpropagation and build up to modern deep neural networks, like GPT."
>
> "Language models are an excellent place to learn deep learning, even if your intention is to eventually go to other areas like computer vision because most of what you learn will be immediately transferable."
>
> — Karpathy, "Neural Networks: Zero to Hero" course page (https://karpathy.ai/zero-to-hero.html).

**Context**: 영상 시리즈 전반에 흐르는 학습 순서: scalar autograd → bigram LM → MLP → batch norm → Transformer → GPT. "from scratch, in code"가 한 줄 강령.

### Q35 — Building for agents: 99.9% LLM attention
> "It's 2025 and most content is still written for humans instead of LLMs. 99.9% of attention is about to be LLM attention, not human attention. E.g. 99% of libraries still have docs that basically render to some pretty .html static pages assuming a human will click through them."
>
> — Karpathy, X, 2025-03-11 (https://x.com/karpathy/status/1899876370492383450) [본문은 검색 스니펫 verbatim].

**Context**: 강연에서 "build for agents"라고 한 framing을 더 강하게 박은 트윗. llms.txt / single markdown file 권고의 근거.

### Q36 — 한국어 수용: 카파시 본인 인용에 대한 byline.network 정리
> "우리는 새로운 종류의 소프트웨어가 기존 스택을 잠식하고 있으며, 완전히 다른 3가지 프로그래밍 패러다임이 놓여 있다."
>
> 어떤 기능은 1.0으로, 어떤 것은 2.0으로, 또 다른 것은 3.0으로 프로그래밍하고 싶을 수 있으며, **"이 패러다임들 사이를 유연하게 오갈 수 있어야 한다"**고 강조.
>
> — Byline Network, "안드레 카파시 '지금은 소프트웨어 3.0의 시대'", 2025-06-23 (https://byline.network/2025/06/23-450/).

**Context**: 국내 IT 매체의 talk 정리. 카파시가 "셋 중 하나가 이긴다"가 아니라 "셋을 오가야 한다"고 강조했다는 한국 수용본의 포인트. 직접 영문 출처 재확인 권장 — Gaps 참고.

### Q37 — 한국어 수용: Toss Tech의 3.0 framing 재정리
> "Software 1.0: 우리가 수십 년간 해온 방식입니다. Python, Java, C++로 명시적인 로직을 작성합니다."
>
> "Software 2.0: 2010년대 딥러닝의 부상과 함께 시작됐습니다."
>
> "Software 3.0: 지금 우리가 진입하고 있는 시대입니다. LLM에게 자연어로 무엇을(What) 원하는지 말하면 됩니다. 프롬프트가 곧 프로그램입니다."
>
> "LLM은 강력하지만, 혼자서는 파일을 읽을 수도, API를 호출할 수도, 데이터베이스에 접근할 수도 없습니다."
>
> — Toss Tech Blog, "소프트웨어 3.0 시대를 맞이하며" (https://toss.tech/article/software-3-0-era).

**Context**: 한국 핀테크 회사의 기술 블로그. 카파시 framing을 그대로 받아 한국 실무자 청중에게 다시 박는 패턴. "LLM 단독으로는 IO를 못 한다 → tool/agent가 필요"라는 보조 진단이 함께 강조됨.

## Critiques & limits (raw, 평가 금지)

### C1 — Yann LeCun: auto-regressive LLMs are a dead end
> "Pure Auto-Regressive LLMs are a dead end on the way towards human-level AI ... they are still very useful in the short term."
>
> "An LLM doesn't understand that if you push a glass off a table, it will break."
>
> — Yann LeCun, 2024-09 (Newsweek 인터뷰 및 후속 기고; https://www.newsweek.com/nw-ai/ai-impact-interview-yann-lecun-llm-limitations-analysis-2054255).

**Target**: 카파시의 "LLMs are a new kind of computer / OS / 3rd paradigm" framing의 토대 — auto-regressive LLM이 패러다임의 중심이라는 가정 — 을 정면 반박. LeCun은 world model / JEPA 계열을 대안으로 제시.
**Context**: 카파시가 Software 3.0 강연에서 LLM을 차세대 computing primitive로 둔 시점과 거의 동시에, LeCun은 Meta에서 LLM 중심 전략에 반대하며 사임 단계. LLM autoregressive 자체가 dead end라는 주장.

### C2 — Gary Marcus: vibe coding은 unfamiliar에서 무너진다
> "The problem, as always, lies in generalizing outside the training distribution. Vibe coding can be fine if you are building something very familiar, but is less reliable for the unfamiliar."
>
> "vibe coding experiments often start out great, and end badly."
>
> "[vibe coding] would never be remotely reliable" — fine for demos, "but not for complex apps in the real world ... the code they wrote would be hard to maintain."
>
> — Gary Marcus, "Is vibe coding dying?", garymarcus.substack.com (https://garymarcus.substack.com/p/is-vibe-coding-dying).

**Target**: 카파시의 "the hottest new programming language is English" + vibe coding 권고가 production app에 그대로 외삽되는 것을 반박.
**Context**: vibe coding이 viral term이 되고 1년 후, Marcus는 "데모는 되지만 production은 안 된다"는 패턴을 반복 지적. 흥미롭게도 Karpathy 본인이 Q22·Q24에서 비슷한 hedge를 한다 — 그러나 Marcus의 critique는 framing 자체의 위험을 겨냥.

### C3 — Andrew Ng: "vibe coding"이라는 이름이 사람들을 오도한다
> "It's misleading a lot of people into thinking, just go with the vibes, you know — accept this, reject that."
>
> "When I'm coding for a day with AI coding assistance, I'm frankly exhausted by the end of the day."
>
> — Andrew Ng, 2025-06 (Klover.ai write-up + Slashdot 인용; https://developers.slashdot.org/story/25/06/05/165258/andrew-ng-says-vibe-coding-is-a-bad-name-for-a-very-real-and-exhausting-job).

**Target**: 카파시의 "fully give in to the vibes ... forget that the code even exists" framing이 "AI에 맡기고 쉬어가는 작업"으로 잘못 읽히는 것을 비판.
**Context**: AI-assisted coding을 "deeply intellectual exercise"로 다시 자리매김. 본질을 부정하지 않고, 이름(=framing)이 행동을 망친다는 critique.

### C4 — Simon Willison: vibe coding의 범위가 너무 넓게 잡혔다
> "[Vibe coding is] building software with an LLM without reviewing the code it writes."
>
> "If an LLM wrote the code for you, and you then reviewed it, tested it thoroughly and made sure you could explain how it works to someone else, that's not vibe coding, it's software development."
>
> "I won't commit any code to my repository if I couldn't explain exactly what it does to somebody else."
>
> — Simon Willison, "Not all AI-assisted programming is vibe coding (but vibe coding rocks)", 2025-03-19 (https://simonwillison.net/2025/Mar/19/vibe-coding/).

**Target**: 카파시 원조 정의가 viral하게 퍼지면서 "LLM이 코드를 짜준 모든 작업 = vibe coding"으로 의미가 부풀려진 현상. 카파시의 framing 자체에 동의하면서도, 그 framing이 책임 있는 AI-assisted 개발을 가린다고 지적.
**Context**: vibe coding tweet 한 달 뒤. Willison은 "vibe coding은 throwaway weekend project엔 좋다, 다만 production code엔 review 규칙이 별도다"로 둘을 분리.

### C5 — Karpathy 본인의 hedge (Dwarkesh, 2025-10): agents/RL/computation 한계
> "Reinforcement learning is terrible."
>
> "They just don't work. They don't have enough intelligence."
>
> "It's slop."
>
> "The models have so many cognitive deficits."
>
> — Karpathy, Dwarkesh Patel Podcast, 2025-10.

**Target**: 자기 자신의 Software 3.0 / "decade of agents" framing이 너무 낙관적으로 받아들여지는 것에 대한 self-hedge. "decade"라는 단어 자체가 hype-cooling 장치.
**Context**: Software 3.0 강연(2025-06) 4개월 후. 본인이 동일 framing 안에서 reality check를 거는 패턴 — 강연의 "decade of agents"는 사실 이 critique의 한 줄짜리 결론이었다는 게 명확해짐. 후속 단계가 카파시 skill을 만들 때 "낙관 framing"과 "현실 hedge"가 한 인물 안에서 함께 살아 있다는 점에 주의해야 함.

### C6 — Karpathy 본인의 hedge (Software 2.0 essay): silent failure & 해석성
> "we're left with large networks that work well, but it's very hard to tell how."
>
> "The 2.0 stack can fail in unintuitive and embarrassing ways ... they can 'silently fail'."
>
> — Karpathy, "Software 2.0", 2017.

**Target**: Software 2.0 자체의 한계. 카파시가 자기 framing 안에서 박는 boundary condition.
**Context**: 같은 에세이의 "Benefits"와 "Limitations"가 1:1 대응. "Better than you"라는 단정과 "very hard to tell how"가 한 글에 공존. 후속 단계가 "이 lens는 어디서 쓰면 안 되는가" 질문을 풀 때 참고.

## Recurring observations (raw, 해석 금지)

- **표현 패턴: "기존 컴퓨팅 개념에 LLM을 끼워 넣기"**. data=source code (Q3), context window=RAM (Q9), LLM=kernel process (Q7), LLM=CPU + RAM + filesystem (Q8), LLM=utility/fab/OS (Q12), 1960s mainframe = 현재 (Q13), cognitive core = personal computer kernel (Q23). 동일한 type-coercion 동작이 8년에 걸쳐 반복.
- **표현 패턴: "spirits / ghosts / people spirits"**. Q14, Q27, Q30에서 동일 단어 3회. 본인이 가장 자주 쓰는 LLM 캐릭터 카드.
- **표현 패턴: "from scratch / minimal / hack / chop up / spelled out"**. Q31~Q34에 분포. 학습은 "최소 동작 버전을 손으로 다시 짠다"로 통일.
- **표현 패턴: "version 번호로 패러다임 마킹"**. Software 1.0 / 2.0 / 3.0 (Q1, Q2, Q10), minGPT vs nanoGPT (Q31). 카파시는 변화에 정수 버전을 박는다.
- **표현 패턴: "코드 표기를 메타포로 차용"**. `works.any()` vs `works.all()` (Q17), "compiles the dataset into the binary" (Q3).
- **표현 패턴: 자기 framing을 동시에 박고/식히기**. "Better than you" (Q4) ↔ "very hard to tell how" (Q5) / "Software 3.0 is eating" (Q11) ↔ "slop" (Q24) / "decade of agents" (Q20) ↔ "RL is terrible" (Q26). hype 박기 + 같은 글/talk 안에서 reality hedge가 함께 출현.
- **표현 패턴: 한 줄 슬로건 → 1년 후 framing이 됨**. "the hottest new programming language is English" (Q6, 2023) → Software 3.0 (2025, Q10). "vibe coding" (Q21, 2025) → Collins Word of the Year. 본인은 두 경우 모두 "throwaway tweet"이라고 인정 (Q22).
- **반복 단어**: kernel, OS, context window, jagged, ghost/spirit, fab, utility, decade, slop, partial autonomy, autonomy slider, machine-consumable, build for agents.
- **구조 패턴: talk이든 essay든 "정의 → 비유 시리즈 → 한계 → 미래 한 줄"의 4부 구성**. Software 2.0 (Q1-Q5)와 Software 3.0 강연(Q10-Q20)이 동일 골격.

## Gaps / open questions

- **X.com 원본 트윗 본문**을 직접 fetch하지 못함 (HTTP 402). Q6, Q7, Q8, Q21, Q22, Q23, Q35의 본문은 검색 스니펫 / 2차 출처에서 verbatim으로 잡았지만, 띄어쓰기·이모지·줄바꿈은 원본과 다를 수 있다. 후속 단계가 SKILL.md에 그대로 박을 때는 원본 화면 캡처로 재확인 권장.
- **YC Startup School talk의 풀 transcript verbatim**이 부분적으로만 잡힘. Singju Post가 풀 transcript를 호스트하지만 fetch 실패 (timeout). Latent.Space와 Kyle Howells의 노트는 slide caption + paraphrase 혼합이라, Q17·Q18·Q19의 정확한 발화 wording은 video를 재시청해서 확정 권장.
- **"Cognitive core" 트윗 (Q23)의 완전한 features 리스트** — Matryoshka 구조, reasoning dial, tool-using, on-device finetuning LoRA slots — 가 검색 스니펫에서만 부분적으로 잡힘. 후속 단계가 cognitive core 개념을 깊게 쓸 거면 원문 캡처가 필요.
- **Karpathy의 Tesla Autopilot 시절 Software 2.0 적용 사례** (2018 Train AI 강연 등)는 본 raw에서 수집하지 않음. Software 2.0 framing의 실증 데이터로 추가 가치가 있을 수 있음.
- **Korean reception**: byline.network와 toss.tech 외에 학술/실무 critique를 찾지 못함. 카파시 framing에 대한 한국 개발자 커뮤니티의 부정적 반응이 있는지 추가 조사 필요.
- **반론 측 직접 발언 verbatim**: LeCun의 "dead end" 발언이 트윗/강연 원본 중 어디서 처음 나왔는지(Newsweek 인터뷰 외) 1차 위치 확정 못함. Marcus의 substack은 verbatim 잡았으나 카파시 framing을 직접 호명한 부분은 더 길게 확인 필요. 본 raw는 "의미 일치 verbatim"으로 채택했지만, summary 단계에서 SKIP 조건을 박을 때 출처 위치를 한 번 더 검증 권장.
- **카파시 본인의 자기 framing 변천사**: 2017 Software 2.0 → 2023 LLM OS → 2025 Software 3.0 → 2025 cognitive core. 각 단계 사이에 본인이 이전 framing을 어디까지 retract/upgrade하는지 메타 발언이 적게 잡힘. 특히 "Software 2.0이 Software 3.0에 흡수되는가, 병존하는가" 본인 답변(Q11이 "eating", Q36이 "유연하게 오가야"로 충돌)이 정리 필요.
