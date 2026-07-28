# Draft BJ — Thinking Fast and Slow with Agentic AI: Dual-Process Theory and Hybrid Intelligence

**Version:** v0.1 (2026-06-05)
**Status:** Initial draft — concise treatment. Cross-references: Draft BI (cognitive effects, automation bias), Draft AS (technostress, Bainbridge), Draft H (augmentation and co-evolution), Draft AA (psychology of being outperformed).
**Next:** Tri-source verify Anthony et al. (2017) NeurIPS, Binz & Schulz (2023) PNAS, Hagendorff et al. (2023) Nature Computational Science, Rastogi et al. (2020) CHI, Parasuraman & Manzey (2010) Human Factors.

---

## Abstract

Daniel Kahneman's dual-process theory — the distinction between fast, automatic System 1 thinking and slow, deliberate System 2 thinking — has become one of the most productive frameworks in cognitive science. This chapter argues that the theory acquires a new and structurally important dimension in the context of agentic AI: the System 1/System 2 distinction is not merely a property of individual human minds, but a design space for hybrid intelligence architectures. Current AI systems are, at their core, System 1 machines: fast, pattern-matching, associative, and confident. Deliberate System 2 reasoning — causal inference, counterfactual simulation, compositional generalisation — remains structurally difficult for neural language models and is an active frontier of AI research. The most capable agentic systems are those that combine both modes: fast neural pattern recognition coupled with slow deliberative search. In hybrid human-AI systems, the cognitive labour is redistributed: AI typically handles System 1 load while humans are positioned as System 2 supervisors. The chapter argues that this redistribution is asymmetric and potentially self-undermining — because pervasive AI assistance progressively atrophies the System 2 capacities on which meaningful human supervision depends.

---

## §1 — The Dual-Process Framework

Kahneman's *Thinking, Fast and Slow* (2011) synthesised decades of research by Kahneman, Tversky, and others into a two-system model of human cognition. System 1 operates automatically, rapidly, and without deliberate effort: it recognises faces, reads emotional tone, pattern-matches from prior experience, and produces intuitive judgements. System 2 is slow, effortful, and deliberate: it checks arithmetic, evaluates logical arguments, suppresses impulse, and overrides System 1 when the situation demands it. The boundary between the systems is not anatomical but functional — the same brain hardware can operate in either mode depending on task demands, available cognitive resources, and motivation.

The terminology "System 1" and "System 2" was introduced formally by Stanovich and West (2000) and has since become standard across cognitive science, economics, and decision research. Evans (2008) provides the most comprehensive theoretical synthesis of dual-process theories across domains.

The framework's practical power is its account of cognitive error: most systematic human irrationality — the biases and heuristics documented in Kahneman and Tversky's programme — occurs when System 1 generates a plausible answer that System 2 fails to override. This happens predictably under cognitive load, time pressure, distraction, and when the System 1 answer is fluent and confident enough to pre-empt System 2 engagement.

---

## §2 — Current AI Is a System 1 Machine

The dominant architecture of modern AI — the transformer-based large language model — is structurally a System 1 device. It produces outputs rapidly, in parallel, through learned pattern-matching over a vast training distribution. It does not reason by constructing causal models, decomposing problems into sub-goals, and evaluating plans against counterfactual alternatives. It generates the next token by compressing statistical regularities from training — the functional analogue of intuition, not deliberation.

This is not a criticism but a characterisation. System 1 processing is extraordinarily powerful. A large language model can recognise the genre of a text in milliseconds, produce stylistically appropriate prose across dozens of registers, surface relevant precedents from a legal corpus, and synthesise a research summary — all tasks that would require laborious System 2 effort from a human. The AI's System 1 operates at a scale and speed unavailable to biological cognition.

The limitation is equally characteristic of System 1: the model can be wrong with complete confidence, fail to notice the failure, and generate fluent justifications for the error. Draft I documents LLM overconfidence and calibration failure as the structural consequence of this architecture. Binz and Schulz (2023) confirmed empirically that GPT-3 reproduces the classic Kahneman-Tversky biases — conjunction fallacy, base-rate neglect, anchoring — consistent with a System 1 processing profile.

---

## §3 — Toward AI System 2: The Research Frontier

The leading edge of AI architecture research is the explicit construction of System 2-like reasoning in neural systems. Two influential formulations define this frontier.

**Anthony, Tian, and Barber (2017)** titled their NeurIPS paper "Thinking Fast and Slow with Deep Learning and Tree Search" — explicitly invoking Kahneman. Their architecture combines a fast neural network (System 1: pattern recognition, rapid policy evaluation) with a slow Monte Carlo Tree Search (System 2: deliberate lookahead, counterfactual evaluation). The neural network guides the search; the search corrects the network's intuitions. The combination — best known from the AlphaGo/AlphaZero architecture — outperforms either component alone, and does so precisely because the systems are complementary rather than redundant.

**Bengio (2019)** argued in his NeurIPS keynote that contemporary deep learning is "System 1 AI" and that the core research challenge is building "System 2 deep learning" — systems capable of causal reasoning, variable binding, compositional generalisation, and explicit world modelling. The capabilities Bengio identifies as missing are exactly those that Lake et al. (2017) document as present in human infants but absent in neural networks: intuitive physics, goal inference, and hierarchical program-like representation.

Chain-of-thought prompting (Wei et al., 2022) and extended reasoning in frontier models (Anthropic, OpenAI, DeepMind, 2024–2025) represent an intermediate approach: eliciting System 2-like reasoning from a fundamentally System 1 architecture by conditioning the model to produce explicit intermediate steps. Whether this constitutes genuine System 2 reasoning or sophisticated System 1 mimicry of System 2 remains actively debated — Hagendorff et al. (2023) found that RLHF-tuned models show reduced System 1-style cognitive biases compared to base models, consistent with training-induced System 2-like override capacity.

---

## §4 — Redistribution in Hybrid Systems: Who Thinks Fast, Who Thinks Slow?

In hybrid human-AI systems, the System 1/System 2 boundary is not internal to a single mind but distributed across the human-AI coupling. The AI handles System 1 load — rapid pattern recognition, fluent draft production, database retrieval, anomaly flagging — while the human is positioned as the System 2 supervisor: the deliberate, critical evaluator who catches AI errors, applies contextual judgement, and makes consequential decisions.

This redistribution looks like a clean win: AI frees the human from cognitively burdensome routine processing, allowing human System 2 capacity to focus on higher-order tasks. Steyvers and Kumar (2023) describe this as the complementarity challenge — identifying the specific configuration of human and AI cognitive profiles that maximises joint performance. Bansal et al. (2021) confirm empirically that the most accurate AI is not necessarily the best teammate: complementarity requires the AI and human to cover different parts of the cognitive space, not to converge on the same outputs.

The problem is that this redistribution is cognitively unstable. Extensive exposure to AI System 1 outputs progressively undermines the human System 2 capacity on which the design depends.

**Automation complacency as System 1 takeover.** Parasuraman and Manzey (2010) characterise automation complacency as what happens when a human supervisor's System 2 vigilance is suppressed by the fluency and confidence of automated System 1 outputs: the supervisor's own System 1 accepts the automated recommendation without System 2 override. The more reliable the automation, the stronger the System 1 signal to accept it — and the more damaging the failure when the automation errs in a case outside its training distribution.

**Algorithm aversion as System 1 backlash.** Dietvorst, Logg, and Hsee (2015) document the mirror pathology: observing a single AI error triggers a System 1 emotional response (aversion, distrust) that persists even after System 2 analysis would counsel continued use. Human calibration of AI reliability operates primarily through System 1 channels, not deliberate analysis — making it systematically miscalibrated in both directions.

**The atrophy problem.** Rastogi et al. (2020) demonstrate directly that AI-assisted decision-making shifts human cognitive processing toward System 1 heuristics: people anchor on the AI recommendation, rely on the AI's apparent confidence as a fluency cue, and reduce the depth of independent information search. The human's System 2 is not engaged more selectively — it is engaged less often and less deeply. This is the mechanism underlying the jagged-frontier skill trap (Dell'Acqua et al., 2023, Draft BI §2.4): the human has been trained by AI assistance to operate in a System 1 mode toward AI-produced outputs, precisely in the domain where System 2 scrutiny is most necessary.

---

## §5 — Design Implications

The dual-process framework makes the design challenge precise. A hybrid intelligence system that positions AI as System 1 and the human as System 2 is only sustainable if the human's System 2 capacity is actively maintained — not passively assumed. Four design principles follow:

**Preserve System 2 engagement.** Interfaces that present AI outputs as provisional rather than authoritative — requiring the human to actively evaluate rather than passively accept — slow the atrophy of deliberative capacity. Explainability mechanisms that surface the AI's reasoning chain give the human something to engage System 2 with. The friction is the feature.

**Design for appropriate reliance, not maximum trust.** Lee and See (2004) established that the goal of automation design is *appropriate* reliance — calibrated to actual AI reliability — not maximal trust. In dual-process terms: the design should trigger System 2 engagement at the boundary of AI competence, and allow System 1 acceptance only within it. This requires dynamic UI elements that signal confidence and scope, not static "the AI says X" presentations.

**Acknowledge that AI chain-of-thought is not human System 2.** Extended reasoning in frontier models produces reasoning traces that *look* like System 2 deliberation. Users who read these traces may infer deeper reliability than is warranted — mistaking fluent pseudo-deliberation for genuine causal inference. The epistemological status of chain-of-thought reasoning in LLMs is an open research question; it should not be treated as resolved in deployed systems.

**Institutions as collective System 2.** Where individual System 2 capacity is unreliable — under time pressure, cognitive load, or atrophy from automation — institutional structures can substitute. Peer review, mandatory second opinions, adversarial red-teaming, and audit requirements are System 2 processes externalised into social architecture. Hybrid intelligence design should consider what institutional System 2 infrastructure is required to govern AI-assisted decisions at scale.

---

## Key Sources

- Anthony, T., Tian, Z., & Barber, D. (2017). Thinking fast and slow with deep learning and tree search. *NeurIPS 2017*.
- Bansal, G., et al. (2021). Is the most accurate AI the best teammate? Far-sighted virtual agents for human-AI teams. *AAAI 2021*.
- Bengio, Y. (2019). From System 1 deep learning to System 2 deep learning. *NeurIPS 2019 keynote*.
- Binz, M., & Schulz, E. (2023). Using cognitive psychology to understand GPT-3. *PNAS*, 120(6), e2218523120.
- Dell'Acqua, F., et al. (2023). Navigating the jagged technological frontier. Harvard Business School Working Paper 24-013. [→ Draft BI §2.4]
- Dietvorst, B. J., Logg, J. M., & Hsee, C. K. (2015). Algorithm aversion: People erroneously avoid algorithms after seeing them err. *Journal of Experimental Psychology: General*, 144(1), 114–126.
- Evans, J. St. B. T. (2008). Dual-processing accounts of reasoning, judgment, and social cognition. *Annual Review of Psychology*, 59, 255–278.
- Goyal, A., & Bengio, Y. (2022). Inductive biases for deep learning of higher-level cognition. *Proceedings of the Royal Society A*, 478(2266).
- Hagendorff, T., et al. (2023). Human-like intuitive behavior and reasoning biases emerged in large language models but disappeared in ChatGPT. *Nature Computational Science*, 3, 833–838.
- Kahneman, D. (2011). *Thinking, Fast and Slow*. Farrar, Straus and Giroux.
- Lake, B. M., Ullman, T. D., Tenenbaum, J. B., & Gershman, S. J. (2017). Building machines that learn and think like people. *Behavioral and Brain Sciences*, 40, e253.
- Lee, J. D., & See, K. A. (2004). Trust in automation: Designing for appropriate reliance. *Human Factors*, 46(1), 50–80.
- Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, 52(3), 381–410.
- Rastogi, C., et al. (2020). Deciding fast and slow: The role of cognitive biases in AI-assisted decision making. *Proceedings of ACM CHI 2020*.
- Stanovich, K. E., & West, R. F. (2000). Individual differences in reasoning: Implications for the rationality debate. *Behavioral and Brain Sciences*, 23(5), 645–665.
- Steyvers, M., & Kumar, A. (2023). Three challenges for AI-assisted decision-making. *Perspectives on Psychological Science*, 18(6), 1384–1392.
- Wei, J., et al. (2022). Chain-of-thought prompting elicits reasoning in large language models. *NeurIPS 2022*.
