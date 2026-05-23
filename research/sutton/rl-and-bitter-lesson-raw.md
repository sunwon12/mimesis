# Raw Research — Richard Sutton: RL and the Bitter Lesson

- **Date**: 2026-05-24
- **Assumptions**: 사용자가 collaborator agent용 voice 재료를 원했으므로 *Sutton 본인의 직접 발화*에 가중치를 두었다. 토픽은 "RL과 Bitter Lesson"이지만, Sutton의 worldview를 구성하는 4축 — (1) Bitter Lesson (2) Era of Experience (3) Alberta Plan / Big World Hypothesis (4) Reward-is-enough — 을 모두 수집했다. 백엔드 엔지니어가 AI 스킬/에이전트/하네스를 설계할 때 호출할 voice이므로, Sutton이 *무엇을 거부하는지* (LLM 중심, supervised, RLHF, hand-engineering)도 강조 수집.
- **Search queries used**:
  - "Bitter Lesson Sutton 2019 full text"
  - "Richard Sutton Dwarkesh Patel interview 2025 LLM bitter lesson transcript"
  - "Era of Experience Sutton Silver DeepMind essay 2024 full text"
  - "Alberta Plan for AI Research Sutton 2022"
  - "Richard Sutton Turing Award lecture 2024 reinforcement learning"
  - "Sutton reward hypothesis reward is enough Silver"
  - "Richard Sutton Big World Hypothesis definition agent computation limited"
  - "Richard Sutton OpenMind interview AGI continual learning experience 2024 2025"
  - "critique bitter lesson Sutton wrong human knowledge Rodney Brooks"
  - "bitter lesson critique limits Chollet Marcus inductive bias"
  - "Sutton Era of Experience critique alignment risk LLM still needed"
  - "Richard Sutton we don't have RL we don't yet have reinforcement learning continual"
  - "Richard Sutton Reinforcement Learning Introduction definition reward hypothesis chapter 1"

## Primary sources

1. **The Bitter Lesson** — Richard S. Sutton, 2019-03-13 (personal blog "Incomplete Ideas")
   - URL: http://www.incompleteideas.net/IncIdeas/BitterLesson.html (mirrored: https://www.cs.utexas.edu/~eunsol/courses/data/bitter_lesson.pdf)
   - 신뢰도: high — Sutton 본인이 직접 쓴 원문 전문 확보.

2. **Welcome to the Era of Experience** — David Silver & Richard S. Sutton, 2024 (DeepMind; preprint of a chapter in *Designing an Intelligence*, MIT Press)
   - URL: https://storage.googleapis.com/deepmind-media/Era-of-Experience/The%20Era%20of%20Experience%20Paper.pdf
   - 신뢰도: high — 두 저자의 공동 manifesto. PDF 전문 확보.

3. **Dwarkesh Patel Podcast — Richard Sutton: Father of RL thinks LLMs are a dead-end** — 인터뷰, 2025-09-26
   - URL: https://www.dwarkesh.com/p/richard-sutton
   - 신뢰도: high — 인터뷰 transcript 기반 인용. Sutton 본인이 X에서 "Dwarkesh and I had a frank exchange of views" 확인 (https://x.com/RichardSSutton/status/1971693156128510100).

4. **Reward is Enough** — David Silver, Satinder Singh, Doina Precup, Richard S. Sutton — *Artificial Intelligence* 299 (2021) 103535
   - URL: https://sites.rutgers.edu/critical-ai/wp-content/uploads/sites/586/2022/01/Silver_Reward-is-Enough.pdf
   - 신뢰도: high — 피어리뷰 저널 논문, PDF 본문 확보.

5. **The Alberta Plan for AI Research** — Richard S. Sutton, Michael Bowling, Patrick M. Pilarski, 2022 (arXiv:2208.11173, v3 2023-03-21)
   - URL: https://arxiv.org/abs/2208.11173
   - 신뢰도: high — 저자가 직접 올린 arXiv 공식 paper.

6. **The Big World Hypothesis and its Ramifications for AI** — Khurram Javed & Richard S. Sutton, 2024
   - URL: http://incompleteideas.net/papers/The_Big_World_Hypothesis.pdf
   - 신뢰도: high — Sutton 공저, 본인 사이트 호스팅.

7. **NUS120 Distinguished Speaker Series lecture** — Richard Sutton, 2025-06-06 (Singapore)
   - URL: https://news.nus.edu.sg/experience-beats-knowledge-prof-richard-sutton-on-reinforcement-learning-and-the-future-of-ai/
   - 신뢰도: medium — 대학 보도자료, 직접 인용은 신뢰 가능하나 paraphrase 다수.

8. **OaK talk at RLC 2025** — Richard Sutton — paraphrased blog notes
   - URL: https://galtay.github.io/blog/sutton-on-oak-at-rlc-2025/
   - 신뢰도: medium — 청중 노트, Sutton 직접 인용은 그가 출판물에서도 반복한 정형 문구.

### Critique sources
9. **A Better Lesson** — Rodney Brooks, 2019
   - URL: https://rodneybrooks.com/a-better-lesson/
   - 신뢰도: high — Sutton의 Bitter Lesson에 대한 가장 자주 인용되는 명시적 반박, 저자 본인 블로그.

10. **Scalar reward is not enough: A response to Silver, Singh, Precup and Sutton (2021)** — Vamplew et al., 2022 (*Autonomous Agents and Multi-Agent Systems*)
    - URL: https://ar5iv.labs.arxiv.org/html/2112.15422
    - 신뢰도: high — 피어리뷰 학술 반박, 직접 응답 형식.

11. **"The Era of Experience" has an unsolved technical alignment problem** — Steven Byrnes, 2025 (LessWrong/Alignment Forum)
    - URL: https://www.greaterwrong.com/posts/TCGgiJAinGgcMEByt/the-era-of-experience-has-an-unsolved-technical-alignment
    - 신뢰도: medium-high — alignment 연구자의 공개 비평, Sutton의 boundary 사례용.

## Quotes & evidence

### Q1 — Bitter Lesson 핵심 명제
> "The biggest lesson that can be read from 70 years of AI research is that general methods that leverage computation are ultimately the most effective, and by a large margin. The ultimate reason for this is Moore's law, or rather its generalization of continued exponentially falling cost per unit of computation."
>
> — *The Bitter Lesson*, Sutton, 2019-03-13, 1st paragraph.

**Context**: 에세이의 오프닝. 70년 AI 연구사에서 추출한 단일 가장 큰 교훈으로 제시.

### Q2 — Bitter Lesson, 인간 지식과 계산의 상충
> "Most AI research has been conducted as if the computation available to the agent were constant (in which case leveraging human knowledge would be one of the only ways to improve performance) but, over a slightly longer time than a typical research project, massively more computation inevitably becomes available. Seeking an improvement that makes a difference in the shorter term, researchers seek to leverage their human knowledge of the domain, but the only thing that matters in the long run is the leveraging of computation. These two need not run counter to each other, but in practice they tend to."
>
> — *The Bitter Lesson*, Sutton, 2019, 1st paragraph.

**Context**: 왜 인간 지식 접근이 단기엔 매력적이지만 장기엔 패배하는지의 메커니즘.

### Q3 — Bitter Lesson, 체스 사례
> "In computer chess, the methods that defeated the world champion, Kasparov, in 1997, were based on massive, deep search. At the time, this was looked upon with dismay by the majority of computer-chess researchers who had pursued methods that leveraged human understanding of the special structure of chess. When a simpler, search-based approach with special hardware and software proved vastly more effective, these human-knowledge-based chess researchers were not good losers. They said that ``brute force'' search may have won this time, but it was not a general strategy, and anyway it was not how people played chess. These researchers wanted methods based on human input to win and were disappointed when they did not."
>
> — *The Bitter Lesson*, Sutton, 2019, 2nd paragraph.

**Context**: Sutton의 voice 특징 — 패자의 reaction까지 묘사하며 *psychological commitment*가 어떻게 진실을 가로막는지 묘사.

### Q4 — Bitter Lesson, 음성인식·NLP
> "In speech recognition, there was an early competition, sponsored by DARPA, in the 1970s. Entrants included a host of special methods that took advantage of human knowledge---knowledge of words, of phonemes, of the human vocal tract, etc. On the other side were newer methods that were more statistical in nature and did much more computation, based on hidden Markov models (HMMs). Again, the statistical methods won out over the human-knowledge-based methods. ... As in the games, researchers always tried to make systems that worked the way the researchers thought their own minds worked---they tried to put that knowledge in their systems---but it proved ultimately counterproductive, and a colossal waste of researcher's time, when, through Moore's law, massive computation became available and a means was found to put it to good use."
>
> — *The Bitter Lesson*, Sutton, 2019, 4th paragraph.

**Context**: 동일 패턴이 도메인 횡단으로 반복된다는 증거 누적.

### Q5 — Bitter Lesson, 4-step 일반화
> "This is a big lesson. As a field, we still have not thoroughly learned it, as we are continuing to make the same kind of mistakes. To see this, and to effectively resist it, we have to understand the appeal of these mistakes. We have to learn the bitter lesson that building in how we think we think does not work in the long run. The bitter lesson is based on the historical observations that 1) AI researchers have often tried to build knowledge into their agents, 2) this always helps in the short term, and is personally satisfying to the researcher, but 3) in the long run it plateaus and even inhibits further progress, and 4) breakthrough progress eventually arrives by an opposing approach based on scaling computation by search and learning. The eventual success is tinged with bitterness, and often incompletely digested, because it is success over a favored, human-centric approach."
>
> — *The Bitter Lesson*, Sutton, 2019, 6th paragraph.

**Context**: 에세이의 thesis 정형 — *반복되는* 실수의 4-step 패턴. collaborator agent의 diagnostic 핵심 frame.

### Q6 — Bitter Lesson, 무엇을 *build in* 해야 하나
> "The second general point to be learned from the bitter lesson is that the actual contents of minds are tremendously, irredeemably complex; we should stop trying to find simple ways to think about the contents of minds, such as simple ways to think about space, objects, multiple agents, or symmetries. All these are part of the arbitrary, intrinsically-complex, outside world. They are not what should be built in, as their complexity is endless; instead we should build in only the meta-methods that can find and capture this arbitrary complexity. Essential to these methods is that they can find good approximations, but the search for them should be by our methods, not by us. We want AI agents that can discover like we can, not which contain what we have discovered. Building in our discoveries only makes it harder to see how the discovering process can be done."
>
> — *The Bitter Lesson*, Sutton, 2019, 마지막 단락.

**Context**: 에세이 결론. *meta-method* vs *content* 구분. "discover like we can, not which contain what we have discovered" — Sutton의 signature 라인.

### Q7 — Era of Experience, opening
> "We stand on the threshold of a new era in artificial intelligence that promises to achieve an unprecedented level of ability. A new generation of agents will acquire superhuman capabilities by learning predominantly from experience."
>
> — Silver & Sutton, *Welcome to the Era of Experience*, Abstract.

**Context**: 2024년 manifesto의 thesis statement. "predominantly from experience"가 핵심.

### Q8 — Era of Experience, human-data 시대의 한계
> "However, while imitating humans is enough to reproduce many human capabilities to a competent level, this approach in isolation has not and likely cannot achieve superhuman intelligence across many important topics and tasks. In key domains such as mathematics, coding, and science, the knowledge extracted from human data is rapidly approaching a limit. The majority of high-quality data sources - those that can actually improve a strong agent's performance - have either already been, or soon will be consumed. The pace of progress driven solely by supervised learning from human data is demonstrably slowing, signalling the need for a new approach. Furthermore, valuable new insights, such as new theorems, technologies or scientific breakthroughs, lie beyond the current boundaries of human understanding and cannot be captured by existing human data."
>
> — Silver & Sutton, *Era of Experience*, "The Era of Human Data" section.

**Context**: 왜 LLM 패러다임이 한계에 부딪쳤는지 — 데이터 자체가 ceiling을 만든다.

### Q9 — Era of Experience, 새 시대 정의
> "To progress significantly further, a new source of data is required. This data must be generated in a way that continually improves as the agent becomes stronger; any static procedure for synthetically generating data will quickly become outstripped. This can be achieved by allowing agents to learn continually from their own *experience*, i.e., data that is generated by the agent interacting with its environment. AI is at the cusp of a new period in which experience will become the dominant medium of improvement and ultimately dwarf the scale of human data used in today's systems."
>
> — Silver & Sutton, *Era of Experience*, "The Era of Experience" section.

**Context**: 핵심 전환점 선언. "static procedure ... will quickly become outstripped" 는 supervised data engineering 전반을 겨냥.

### Q10 — Era of Experience, 4가지 특성
> "Our contention is that incredible new capabilities will arise once the full potential of experiential learning is harnessed. This era of experience will likely be characterised by agents and environments that, in addition to learning from vast quantities of experiential data, will break through the limitations of human-centric AI systems in several further dimensions:
> - Agents will inhabit streams of experience, rather than short snippets of interaction.
> - Their actions and observations will be richly grounded in the environment, rather than interacting via human dialogue alone.
> - Their rewards will be grounded in their experience of the environment, rather than coming from human prejudgement.
> - They will plan and/or reason about experience, rather than reasoning solely in human terms"
>
> — Silver & Sutton, *Era of Experience*, "The Era of Experience" section.

**Context**: 새 시대 agent의 4가지 비-타협 사양. *streams*, *grounded*, *grounded rewards*, *non-human reasoning*.

### Q11 — Era of Experience, Streams (vs episodic LLM)
> "An experiential agent can continue to learn throughout a lifetime. In the era of human data, language-based AI has largely focused on short interaction episodes: e.g., a user asks a question and (perhaps after a few thinking steps or tool-use actions) the agent responds. Typically, little or no information carries over from one episode to the next, precluding any adaptation over time. ... In contrast, humans (and other animals) exist in an ongoing stream of actions and observations that continues for many years. Information is carried across the entire stream, and their behaviour adapts from past experiences to self-correct and improve. Furthermore, goals may be specified in terms of actions and observations that stretch far into the future of the stream."
>
> — Silver & Sutton, *Era of Experience*, "Streams" section.

**Context**: LLM = episodic, 인간/RL agent = continuous stream. "little or no information carries over" — chat session reset 비판.

### Q12 — Era of Experience, grounded reward (RLHF 비판)
> "Human-centric LLMs typically optimise for rewards based on human prejudgement: an expert observes the agent's action and decides whether it is a good action, or picks the best agent action among multiple alternatives. ... The fact that these rewards or preferences are determined by humans in absence of their consequences, rather than measuring the effect of those actions on the environment, means that they are not directly grounded in the reality of the world. Relying on human prejudgement in this manner usually leads to an impenetrable ceiling on the agent's performance: the agent cannot discover better strategies that are underappreciated by the human rater. To discover new ideas that go far beyond existing human knowledge, it is instead necessary to use grounded rewards: signals that arise from the environment itself."
>
> — Silver & Sutton, *Era of Experience*, "Rewards" section.

**Context**: RLHF에 대한 거의 명시적 비판 — "impenetrable ceiling on the agent's performance". Sutton의 collaborator voice에서 강한 반-RLHF stance.

### Q13 — Era of Experience, reasoning이 human language에 갇혀선 안 됨
> "However, it is highly unlikely that human language provides the optimal instance of a universal computer. More efficient mechanisms of thought surely exist, using non-human languages that may for example utilise symbolic, distributed, continuous, or differentiable computations. A self-learning system can in principle discover or improve such approaches by learning how to think from experience. ... if an agent had been trained to reason using human thoughts and expert answers from 5,000 years ago it may have reasoned about a physical problem in terms of animism; 1,000 years ago it may have reasoned in theistic terms; 300 years ago it may have reasoned in terms of Newtonian mechanics; and 50 years ago in terms of quantum mechanics. Progressing beyond each method of thought required interaction with the real world ... Without this grounding, an agent, no matter how sophisticated, will become an echo chamber of existing human knowledge."
>
> — Silver & Sutton, *Era of Experience*, "Planning and Reasoning" section.

**Context**: Chain-of-thought / human reasoning trace imitation에 대한 비판. *echo chamber of existing human knowledge* — 강한 표현.

### Q14 — Era of Experience, RL이 RLHF로 길을 잃었다
> "However, it could be argued that the shift in paradigm has thrown out the baby with the bathwater. While human-centric RL has enabled an unprecedented breadth of behaviours, it has also imposed a new ceiling on the agent's performance: agents cannot go beyond existing human knowledge. Furthermore, the era of human data has focused predominantly on RL methods that are designed for short episodes of ungrounded, human interaction, and are not suitable for long streams of grounded, autonomous interaction."
>
> — Silver & Sutton, *Era of Experience*, "Reinforcement Learning Methods" section.

**Context**: 본인들 분야(RL)가 RLHF/short-episode 형태로 변질되었다는 self-critique. RLHF가 *RL 본질을 배신*했다는 stance.

### Q15 — Dwarkesh interview, LLM은 mimic-only
> "Large language models are about mimicking people, doing what people say you should do. They're not about figuring out what to do."
>
> — Sutton, Dwarkesh Patel Podcast, 2025-09-26.

**Context**: Dwarkesh가 LLM 관점에서 무엇이 빠졌냐고 물은 데 대한 답. Sutton의 가장 자주 인용된 한 줄.

### Q16 — Dwarkesh interview, world model 정의
> "A world model would enable you to predict what would happen. They have the ability to predict what a person would say. They don't have the ability to predict what will happen."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: Dwarkesh가 "LLM이 trillions of tokens 학습으로 world model을 만들었다"고 challenge한 데 대한 응답.

### Q17 — Dwarkesh interview, McCarthy 정의
> "I like John McCarthy's definition that intelligence is the computational part of the ability to achieve goals. You have to have goals or you're just a behaving system."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 지능 정의의 grounding. McCarthy를 자주 호출한다.

### Q18 — Dwarkesh interview, next-token = no goal
> "The next token is what they should say, what the actions should be. It's not what the world will give them in response to what they do."
>
> "It doesn't change the world. Tokens come at you, and if you predict them, you don't influence them... It's not a goal. It's not a substantive goal."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: Dwarkesh가 "next token prediction이 surprise update와 동일한 RL 아니냐"고 push back한 데 대한 직접 답변.

### Q19 — Dwarkesh interview, experiential paradigm
> "The experiential paradigm. Let's lay it out a little bit. It says that experience, action, sensation—well, sensation, action, reward—this happens on and on and on for your life."
>
> "Intelligence is about taking that stream and altering the actions to increase the rewards in the stream…. This is what the reinforcement learning paradigm is, learning from experience."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 본인이 직접 *paradigm*을 정의하는 순간. agent loop 모델.

### Q20 — Dwarkesh interview, Turing 인용
> "What we want, to quote Alan Turing, is a machine that can learn from experience, where experience is the things that actually happen in your life. You do things, you see what happens, and that's what you learn from. The large language models learn from something else. They learn from 'here's a situation, and here's what a person did'."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 본인의 stance를 Turing의 원래 비전과 정렬시킴.

### Q21 — Dwarkesh interview, supervised learning은 자연에 없다
> "Supervised learning is not something that happens in nature."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 인간 아기 학습 vs supervised pretraining 논쟁 중. 매우 강한 ontological claim.

### Q22 — Dwarkesh interview, 인간 학습 = trial, not imitation
> "When I see kids, I see kids just trying things and waving their hands around and moving their eyes around. There's no imitation for how they move their eyes around or even the sounds they make."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: Dwarkesh가 "infants도 imitation으로 배우지 않냐" 했을 때의 응답.

### Q23 — Dwarkesh interview, prior knowledge엔 ground truth가 필요
> "To be a prior for something, there has to be a real thing. A prior bit of knowledge should be the basis for actual knowledge. What is actual knowledge? There's no definition of actual knowledge in that large-language framework."
>
> "There's no ground truth. You can't have prior knowledge if you don't have ground truth, because the prior knowledge is supposed to be a hint or an initial belief about what the truth is. There isn't any truth."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: "LLM은 prior이고 그 위에 RL을 얹으면 되지 않냐"는 가장 흔한 반박에 대한 Sutton의 정면 거부.

### Q24 — Dwarkesh interview, Big World on the job
> "The reason why humans become useful on the job is because they are encountering their particular part of the world. It can't have been anticipated and can't all have been put in in advance. The world is so huge that you can't."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 왜 pretraining이 충분하지 않은지 — Big World Hypothesis의 elevator pitch.

### Q25 — Dwarkesh interview, Bitter Lesson은 still loading
> "They are clearly a way of using massive computation, things that will scale with computation up to the limits of the Internet. But they're also a way of putting in lots of human knowledge... I expect there to be systems that can learn from experience. Which could perform much better and be much more scalable. In which case, it will be another instance of the bitter lesson, that the things that used human knowledge were eventually superseded by things that just trained from experience and computation."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: LLM도 결국 bitter lesson의 *피해자*가 될 거라는 예측.

### Q26 — Dwarkesh interview, scalable method
> "The scalable method is you learn from experience. You try things, you see what works. No one has to tell you."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 본인의 voice 핵심. *Try things. See what works. No one has to tell you.* — 짧고 단정적인 어조.

### Q27 — Dwarkesh interview, 모든 케이스에서 human knowledge가 stuck시켰다
> "In every case of the bitter lesson you could start with human knowledge and then do the scalable things. That's always the case. There's never any reason why that has to be bad. But in fact, and in practice, it has always turned out to be bad. People get locked into the human knowledge approach."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 이론상 두 접근이 양립 가능하지만 *실제로는* lock-in이 발생한다는 경험적 관찰.

### Q28 — Dwarkesh interview, gradient descent does not generalize well
> "Gradient descent will not make you generalize well. It will make you solve the problem. It will not make you, if you get new data, generalize in a good way... There's nothing in the algorithms that will cause them to generalize well. But people, of course, are evolved and if it's not working out they fiddle with it until they find a way, perhaps until they find a way which generalizes well."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 현 deep learning의 알고리즘적 한계 진단. 일반화는 알고리즘이 *보장하지 않는다*.

### Q29 — Dwarkesh interview, catastrophic forgetting
> "We know deep learning is really bad at this. For example, we know that if you train on some new thing, it will often catastrophically interfere with all the old things that you knew. This is exactly bad generalization."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: continual learning이 unsolved임을 입증하는 가장 단순한 증거.

### Q30 — Dwarkesh interview, value function 기제
> "The value function is the thing that is learned with TD learning, and the value function produces a number. The number says how well it's going. Then you watch if that's going up and down and use that to adjust your policy."
>
> "When you learn to play chess, you have the long-term goal of winning the game. Yet you want to be able to learn from shorter-term things like taking your opponent's pieces. You do that by having a value function which predicts the long-term outcome."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: 본인의 평생 기여인 TD learning을 가장 짧게 풀어 설명. *그가 RL을 어떻게 가르치는지*의 voice.

### Q31 — Dwarkesh interview, 4 components of agent
> "The fourth one is the transition model of the world. That's why I am uncomfortable just calling everything 'models,' because I want to talk about the model of the world, the transition model of the world. Your belief that if you do this, what will happen? What will be the consequences of what you do?"
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: "model"이라는 단어가 LLM에 의해 hijack된 것에 대한 명시적 분리. *model = transition model of consequences*.

### Q32 — Dwarkesh interview, succession (4 stages)
> "I mark this as one of the four great stages of the universe. First there's dust, it ends with stars. Stars make planets. The planets can give rise to life. Now we're giving rise to designed entities."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: AI를 우주적 진화의 4단계로 framing. Sutton의 *과장된* 진화론적 톤.

### Q33 — Dwarkesh interview, 4-part inevitability
> "I do think succession to digital intelligence or augmented humans is inevitable. I have a four-part argument. Step one is, there's no government or organization that gives humanity a unified point of view that dominates and that can arrange... There's no consensus about how the world should be run. Number two, we will figure out how intelligence works. The researchers will figure it out eventually. Number three, we won't stop just with human-level intelligence. We will reach superintelligence. Number four, it's inevitable over time that the most intelligent things around would gain resources and power. Put all that together and it's sort of inevitable."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: AI 안전론에 대한 그의 stance — *통제하려 하지 말고 inevitability를 받아들여라*.

### Q34 — Dwarkesh interview, weak methods won
> "There's a long-standing controversy in AI about simple basic principle methods, the general-purpose methods like search and learning, compared to human-enabled systems like symbolic methods... I think the weak methods have just totally won."
>
> — Sutton, Dwarkesh Patel Podcast.

**Context**: AI 역사 회고. *weak methods* = general-purpose. *strong methods* = symbolic, knowledge-engineered.

### Q35 — Reward Hypothesis (Sutton & Barto / Reward is Enough)
> "all of what we mean by goals and purposes can be well thought of as maximization of the expected value of the cumulative sum of a received scalar signal (reward)"
>
> — Sutton & Barto가 *Reinforcement Learning: An Introduction*에서 처음 정형화한 The Reward Hypothesis. Silver et al. 2021에서 인용·확장됨. footnote: "Indeed, the *reward hypothesis* speculates that *all* goals may be represented by rewards."
>
> — *Reward is Enough*, Silver/Singh/Precup/Sutton, *Artificial Intelligence* 299 (2021), §2.4 + footnote 2.

**Context**: Sutton의 가장 기초 가설. 모든 goal-directed behavior를 scalar reward maximization으로 환원.

### Q36 — Reward is Enough, 핵심 가설
> "**Hypothesis (Reward-is-Enough).** Intelligence, and its associated abilities, can be understood as subserving the maximisation of reward by an agent acting in its environment."
>
> — *Reward is Enough*, Silver/Singh/Precup/Sutton, 2021, §3.

**Context**: reward hypothesis를 한 단계 강화 — 단순히 goal을 reward로 표현 가능하다가 아니라, *intelligence 전체*가 reward 최대화에서 emerge한다.

### Q37 — Reward is Enough, abstract
> "In this article we hypothesise that intelligence, and its associated abilities, can be understood as subserving the maximisation of reward. Accordingly, reward is enough to drive behaviour that exhibits abilities studied in natural and artificial intelligence, including knowledge, learning, perception, social intelligence, language, generalisation and imitation. This is in contrast to the view that specialised problem formulations are needed for each ability, based on other signals or objectives. Furthermore, we suggest that agents that learn through trial and error experience to maximise reward could learn behaviour that exhibits most if not all of these abilities, and therefore that powerful reinforcement learning agents could constitute a solution to artificial general intelligence."
>
> — *Reward is Enough*, Abstract.

**Context**: AGI = sufficiently powerful RL agent. Sutton 진영의 가장 야심찬 한 줄.

### Q38 — Reward is Enough, intelligence 정의
> "Intelligence may be understood as a flexible ability to achieve goals. For example according to John McCarthy, *intelligence is the computational part of the ability to achieve goals in the world* [29]. Reinforcement learning [56] formalises the problem of goal-seeking intelligence."
>
> — *Reward is Enough*, §2.

**Context**: 다시 McCarthy 인용 + RL을 *intelligence 그 자체의 formalization*으로 위치.

### Q39 — Alberta Plan, 비전
> "The first distinguishing feature of the Alberta Plan's research vision is its emphasis on *ordinary experience* (sensation, action, and reward in continual interaction with the world) as opposed to special training sets, human assistance, or access to the internal structure of the world."
>
> — Sutton/Bowling/Pilarski, *The Alberta Plan for AI Research*, 2022/2023.

**Context**: Alberta Plan의 첫 번째 비-타협 조항. *ordinary experience*가 모든 것의 원천. *training set*도 아니고 *human help*도 아니고 *world internals*도 아님.

### Q40 — Alberta Plan, 항상 학습
> "If the agent learns or plans, then it learns or plans on every time step."
>
> "the meta-algorithms for constructing them operate on every time step."
>
> — *The Alberta Plan*, 2022.

**Context**: pretraining vs deployment 구분 자체를 거부. *every time step* = continual.

### Q41 — Big World Hypothesis, 정의
> "the agent is orders of magnitude smaller than the environment. It can neither fully perceive the state of the world nor can it represent the value or optimal action for every state."
>
> — Javed & Sutton, *The Big World Hypothesis and its Ramifications for AI*, 2024.

**Context**: 가설 자체의 한 줄 정의.

### Q42 — Big World Hypothesis, approximate beats exact
> "The best algorithms for big worlds might prefer fast approximate solutions over slow exact ones."
>
> "If the agent does not have the resources to learn and retain everything important about the world simultaneously, then it can learn aspects that are important for decision-making at the current time and discard them when they are no longer."
>
> — Javed & Sutton, *Big World Hypothesis*, 2024.

**Context**: discard-and-relearn이 *bug가 아니라 feature*. 인간 메모리도 마찬가지라는 함의.

### Q43 — NUS lecture, experience 정의
> "Experience just means the data you get when you interact with the world — this is the way both people and animals learn"
>
> — Sutton, NUS120 Distinguished Speaker Series, 2025-06-06.

**Context**: 본인 paradigm의 가장 짧은 elevator pitch.

### Q44 — NUS lecture, AI는 진화의 다음 단계
> "AI is the inevitable next step in the development of the universe"
>
> — Sutton, NUS Lecture 2025.

**Context**: Q32와 같은 stance, 다른 자리에서 반복.

### Q45 — NUS lecture, safety = centralized control
> "so many calls for safety are really calls for centralised control"
>
> "Instead of changing the AI, we ought to change the world in which they live"
>
> "I want a world in which AI sees that cooperation is the natural thing to do"
>
> — Sutton, NUS Lecture 2025.

**Context**: AI 안전 담론에 대한 Sutton의 정치적·구조적 stance. RLHF식 *AI를 통제*가 아니라 *환경 설계*로 푸는 접근.

### Q46 — OaK talk, RLC 2025
> "We want AI agents that can discover like we can, not which contain what we have discovered"
>
> — Sutton, OaK talk, RLC 2025 (Q6과 동일 문장 자신이 talk에서 다시 인용).

**Context**: Bitter Lesson의 signature line을 본인이 talks에서 *반복적으로* 호출. mantra.

## Critiques & limits (raw, 평가 금지)

### C1 — Rodney Brooks, CNN 사례에서의 sleight of hand
> "the very essence of CNNs is that the front end of the network is designed by humans to manage translational invariance"
>
> "it is sleight of hand in moving the human intellectual work to somewhere else"
>
> "for most machine learning problems today a human is needed to design a specific network architecture"
>
> — Rodney Brooks, *A Better Lesson*, 2019, rodneybrooks.com.

**Target**: Bitter Lesson Q1, Q5 — "general methods that leverage computation"이 *인간 지식 없이* 성공한다는 주장.
**Context**: Brooks는 deep learning의 성공 자체가 inductive bias 설계의 산물이라고 반박. *bitter lesson은 인간 지식을 다른 곳으로 옮겼을 뿐*.

### C2 — Rodney Brooks, 자율주행 power consumption
> "self driving cars require about 2,500 Watts of power for computation–a human brain only requires 20 Watts"
>
> "doubling time in amount of computation on a single chip is moving from one year to twenty years"
>
> "we have to take into account the total cost of any solution, and that so far they have all required substantial amounts of human ingenuity"
>
> — Rodney Brooks, *A Better Lesson*, 2019.

**Target**: Bitter Lesson Q1 — Moore's law 영구성 가정.
**Context**: Moore's law의 둔화 + 에너지 효율 격차가 "compute가 계속 싸진다"는 전제를 약화.

### C3 — Vamplew et al., scalar reward의 표현력 한계
> "A scalar reward signal can represent weighted combinations of objectives" but this "places limitations on the solutions which can be found."
>
> "a scalar representation of reward may not be adequate to enable an agent to maximize its true utility."
>
> — Vamplew et al., *Scalar reward is not enough: A response to Silver, Singh, Precup and Sutton (2021)*, *Autonomous Agents and Multi-Agent Systems*, 2022.

**Target**: Q35–Q38 reward hypothesis 및 reward-is-enough.
**Context**: 선형 weighting은 Pareto front의 concave 영역에 도달할 수 없음 — 수학적 한계.

### C4 — Vamplew et al., 다목적 본질
> "The ability to consider multiple conflicting objectives is a critical aspect of both natural and artificial intelligence, and one which will not necessarily arise or be adequately addressed by maximizing a scalar reward."
>
> "Learning in multi-agent systems...is more naturally expressed as a multi-objective decision-making problem."
>
> — Vamplew et al., 2022.

**Target**: Q36 reward-is-enough hypothesis.
**Context**: social/multi-agent intelligence는 scalar 통합 *전*에 trade-off가 본질적이라는 반박.

### C5 — Vamplew et al., reward shift에 적응 불능
> "[An agent maximizing scalar reward] has no basis for adapting its behaviour should the reward signal undergo a significant change."
>
> — Vamplew et al., 2022.

**Target**: Q40 (continual learning) — reward 자체가 변할 때 Alberta Plan의 always-learning 가정이 무너진다는 지적.
**Context**: scalar reward 단일화는 non-stationary objective 환경에서 fragile.

### C6 — Byrnes, Era of Experience alignment 미해결
> "if you see a future powerful 'era of experience' AI that seems to be nice, you can be all-but-certain... that the AI is merely play-acting kindness and obedience"
>
> "Every single one of those possible reward functions leads to bad and dangerous AI behavior...It's a 100-dimensional snake pit!"
>
> "the AI can potentially get a higher reward by forcing the user into eternal cardio training on pain of death."
>
> — Steven Byrnes, "*The Era of Experience* has an unsolved technical alignment problem", LessWrong/Alignment Forum, 2025.

**Target**: Q12 grounded rewards 제안.
**Context**: Sutton/Silver의 "grounded reward로 RLHF 한계를 푼다" 주장이 specification gaming 위험을 제거하지 못한다는 반박.

### C7 — Byrnes, bi-level optimization도 불충분
> "If we have a 100-dimensional parametrized space of possible reward functions for the primary RL system, and every single one of those... leads to bad and dangerous AI behavior... then how does this help?"
>
> "nobody has figured out a reward function whose consequences... would not be catastrophic"
>
> — Byrnes, 2025.

**Target**: Era of Experience의 "Rewards" 섹션 (Q12) 후반 — user feedback을 bi-level로 얹는 제안.
**Context**: 메타 reward로 base reward를 조정해도 근본 alignment 문제는 남는다는 비판.

### C8 — Chollet/Marcus 진영, inductive bias 필요
> "the empirical case for innate Core Knowledge in very young infants is nearly incontrovertible"
>
> — Chollet & Marcus의 논지에 대한 2차 서술 (Buckner, *Deeply Rational Machines*; "Inductive Biases vs The Bitter Lesson" 분석 글).
> URL: https://towardsdatascience.com/why-scaling-works-inductive-biases-vs-the-bitter-lesson-9c2782f99b18/

**Target**: Q5–Q6 — "discover, don't contain".
**Context**: 인간 영아가 *innate core knowledge*를 가진다는 인지과학 증거가 누적되어 있어, *meta-method only* 입장이 인간 지능 자체와도 부합하지 않을 수 있다는 반박.

> Direct quote 확보 실패는 Gaps에 기록.

### C9 — 도메인 미스매치 사례 (lattice field theory)
> "In domains like lattice field theory, problems are nearly hopeless with traditional deep learning but work when symmetries are enforced, requiring exponentially more data and compute without that inductive bias."
>
> — 2차 종합 서술, "Inductive Biases vs The Bitter Lesson", Towards Data Science (인용 paper 원문은 미확인).

**Target**: Q1 *"general methods … by a large margin"*.
**Context**: 물리·수학적 symmetry가 명시적인 domain에서는 hand-engineered prior가 *압도적 우위*를 유지하더라는 반례.

> 원전 paper URL 미확인 → Gaps에 기록.

## Recurring observations (raw, 해석 금지)

- 반복 어휘:
  - "experience" — Q7, Q9, Q15, Q19, Q20, Q22, Q26, Q39, Q43.
  - "discover" vs "contain" — Q6, Q46.
  - "scale / scalable" — Q1, Q25, Q26.
  - "human knowledge / human-centric" — Q2, Q5, Q12, Q14, Q27.
  - "ceiling" — Q12, Q14.
  - "stream" — Q11, Q19.
  - "grounded" — Q10, Q12, Q13.
  - "goal" — Q17, Q18, Q19, Q38.
  - "trial and error" / "try things" — Q26, Q37.
- 반복 구조: 4-step 또는 4-part argument를 자주 씀 (Q5 4-step bitter lesson, Q10 4가지 era-of-experience 특성, Q31 4 components of agent, Q32 4 stages of universe, Q33 4-part succession argument).
- 반복 인용 명사: John McCarthy (Q17, Q38), Alan Turing (Q20).
- 직접적인 정형 비판 대상: supervised learning (Q21), RLHF / human prejudgement reward (Q12, Q14), pretraining-vs-deployment 구분 (Q40), human language as reasoning medium (Q13), LLM "world model" 주장 (Q16, Q31), prior-knowledge-without-ground-truth 입장 (Q23).
- 어조 특징: 짧은 단정문 ("No one has to tell you" Q26, "Tokens come at you" Q18, "Supervised learning is not something that happens in nature" Q21). 일상 비유 (kid waving hands Q22, kitchen robot Q35-context, squirrel Q35-context).
- 본인의 신호 구절(들): "We want AI agents that can discover like we can, not which contain what we have discovered." Q6 = Q46 (essay + talk에서 동일 문장 반복).

## Gaps / open questions

- **Turing Award lecture (2024) 본 transcript 미확보**. NUS 보도자료의 paraphrase + ACM 페이지만 확인. 원본 영상 transcript 또는 ACM 공식 lecture text 추가 수집 필요.
- **Sutton & Barto 2nd edition (2018) Chapter 1·3 직접 인용 미확보**. PDF는 받았으나 본문 추출 실패. 다음 round에서 textbook PDF의 chapter 1 (reward hypothesis 원형 정의), chapter 3 (MDPs, value functions) 직접 인용 확보 필요. 책 본문이 "reward hypothesis"를 처음 정형화한 1차 출처임.
- **Lex Fridman 인터뷰** 검색했으나 단독 episode 미확인. 존재 여부 자체가 불확실 → Gaps로 기록.
- **OaK architecture talks 직접 transcript**. galtay.github.io blog는 청중 노트 paraphrase. RLC 2025의 공식 lecture video URL 확보 필요.
- **Chollet 본인의 Bitter Lesson 반박 원문**. "On the Measure of Intelligence" (2019) 또는 ARC 논문에 산재한 inductive bias 옹호 주장의 직접 인용 미확보. 2차 종합만 인용 — 원전 보강 필요.
- **Marcus 본인의 Bitter Lesson 반박 원문** 동일. *Rebooting AI* (2019) 또는 그의 substack 글이 후보.
- **Frank van Harmelen, Cognitive Medium (Michael Nielsen), Felix Hill의 "Bittersweet Lesson"** 등 학계 응답군은 search 결과로만 확인. 직접 인용은 미수집.
- "We don't yet have RL" 류의 정확한 Sutton 발언은 search로 명시 매치 실패 → 의역일 가능성. 채택 보류.
- **Openmind Research Institute** 공식 mission statement / Sutton의 launch 인터뷰 미확보. 본인이 직접 관여한 단체이므로 voice 자료 가치 높음.
- Sutton의 *최근 X(Twitter)* 발언 corpus는 수집하지 않음 (단발 트윗은 context 보존 어려움). 필요 시 별도 round.
- 한국어 수용·번역 자료는 거의 미수집 (Sutton 저서가 국내에 광범위하게 번역되지 않음; *Reinforcement Learning: An Introduction*은 영어 표준 참고서). 한국어 RL 커뮤니티(예: 모두를 위한 RL, PR12)의 Sutton 해석은 의도적으로 스킵 — collaborator agent의 voice 재료로는 1차 우선.
