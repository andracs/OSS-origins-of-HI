# Draft BI — AI Slop, Cognitive Transformation, and the Dual Threat of Misuse and Misalignment

**Version:** v0.1 (2026-06-05)
**Status:** Initial draft — sources anchored in existing Handbook citation record where available; gaps flagged for tri-source verification. Cross-references to AS (technostress), BA (student learning), BE (failure cases), E (structural vulnerabilities), AD (harm encoded in models).
**Next:** Tri-source verify Goldstein et al. 2023 (AI-enabled influence operations), Doshi & Hauser 2024 (creativity homogenization), Ward et al. 2017 (smartphone cognitive drain), Chesney & Citron 2019 (deepfakes). Confirm Noy & Zhang (2023) DOI in Science. Cross-check with AS §3 (vigilance fatigue) to avoid duplication.

---

## Abstract

Pervasive AI use does not leave human cognition untouched. This chapter examines three dimensions of that transformation. First, *AI slop* — the proliferation of low-effort, AI-generated content across the information environment — functions as a form of epistemic pollution that degrades the quality of the commons users rely on to think. Second, extensive agentic AI use restructures human cognitive capacities in ways that are asymmetric: gains in breadth, output speed, and information access are offset by losses in deep reading, unaided recall, and evaluative skepticism. Third, the threat spectrum of advanced agentic AI runs in two directions — outward, where humans weaponize AI systems against each other through synthetic disinformation, social engineering, and coordinated manipulation; and inward, where misaligned or captured agent systems harm the users who rely on them. Together, these three dimensions make the case that the cognitive and social consequences of agentic AI are not byproducts of poor design but structural features of the technology at scale — and that hybrid intelligence must be designed with them explicitly in view.

---

## §1 — AI Slop: The Epistemic Pollution of the Information Commons

### 1.1 What AI slop is and why it matters

*AI slop* is an informal term for the mass of low-effort, AI-generated content that has flooded search results, news aggregators, social platforms, academic preprint servers, and commercial websites since the widespread availability of instruction-tuned language models from 2022 onwards. The term is deliberately pejorative: slop is content produced cheaply, at volume, with minimal human review, for purposes of search optimisation, content-farm economics, or computational propaganda rather than genuine communication or knowledge creation.

The scale is quantitatively documented. Sadasivan et al. (2023) estimated that AI-generated or AI-assisted text now constitutes more than 10 per cent of new public web content in several categories, with the proportion rising rapidly in domains with high content-farm incentives (product reviews, SEO articles, listicles, summarised news). The quality distribution is not uniform: some AI-generated content is indistinguishable from high-quality human writing; much is recognisably formulaic, generic, and confident in a way that does not track accuracy. Jakesch, Hancock, and Naaman (2023) demonstrated that human heuristics for distinguishing AI-generated from human-generated text are systematically flawed: people apply a "too polished" heuristic that misclassifies competent human writing as AI-generated and over-edited AI writing as human, performing only marginally above chance on standard detection tasks (Jakesch et al., 2023).

The fundamental problem AI slop creates is not aesthetic but epistemic: it degrades the reliability of the information environment that human reasoning draws from. If a user's starting point — a search result, a summary, a cited article — was produced cheaply from a prior AI synthesis rather than from verified primary sources, the downstream reasoning built on it is contaminated. This is not a theoretical possibility; it is the documented mechanism of *model collapse*.

### 1.2 Model collapse and the recursive poisoning of training data

Shumailov et al. (2024) formally characterise *model collapse*: the statistical degradation that occurs when generative models are trained on outputs from prior generative models rather than human-generated ground truth. Each generation of training amplifies the most probable outputs and suppresses tail distributions — the rare, specific, and deviant examples that constitute much of the richness of human knowledge. Over successive generations, the model converges on a distribution that is flatter, more generic, and progressively less faithful to the heterogeneity of the world it is supposed to represent. In the extreme, the model's outputs become circular self-confirmation of its own prior biases, disconnected from external reality (Shumailov et al., 2024).

The public web — the primary training corpus for most frontier models — is the medium through which model collapse is transmitted. As AI-generated text accumulates on the public web, future models train increasingly on that text, accelerating the collapse. This is a commons problem in Ostrom's sense (Draft F): the training data commons is being degraded not by deliberate extraction but by the diffuse accumulation of low-quality contributions that each seem individually harmless. Gerstgrasser et al. (2024) showed that collapse is avoidable if synthetic data is kept proportionally small relative to a stable human-generated reference corpus — but this requires deliberate curation of training pipelines against economic incentives that push toward cheap synthetic data.

For the chapter's central argument: AI slop is not merely an annoyance. It is the mechanism by which the open source and open knowledge commons — the fuel that trained AI — is actively degraded by the very systems that fuel has produced. The commons feeds the machine; the machine floods the commons with diluted output; future machines train on that diluted output. The loop is recursive and self-undermining.

### 1.3 Discourse homogenization beyond data collapse

Model collapse operates at the level of training data distributions. A structurally distinct but related phenomenon operates at the level of human discourse: *AI-assisted writing homogenizes expressed opinion and style* in ways that reduce the collective diversity of ideas, even when no individual writer's thinking is directly impaired.

Doshi and Hauser (2024) ran a randomised controlled experiment in which participants wrote creative stories with and without AI assistance. AI assistance increased the average quality of individual stories (as rated by blind evaluators) but significantly decreased the diversity of the overall corpus: the distribution of themes, narrative structures, and character types contracted. The best individual output improved; the collective output became more uniform (Doshi & Hauser, 2024). This is a direct parallel to the genetic diversity argument in evolutionary biology: a population that is individually healthy but collectively homogeneous is fragile to novel environments. A discourse that is individually polished but collectively repetitive is less capable of generating the surprising, deviant, or heterodox ideas that drive intellectual progress.

The implication for hybrid intelligence is not that AI writing assistance should be avoided but that collective epistemic infrastructure — peer review, editorial diversity, pluralist publication norms — must actively counterbalance the homogenizing pressure of AI assistance at population scale.

---

## §2 — Cognitive Transformation: Gains and Losses from Pervasive AI Use

### 2.1 The extended mind and the cost of offloading

Clark and Chalmers' (1998) extended mind thesis holds that cognitive processes are not bounded by the skull: where external objects and systems reliably extend the reach of cognition, they become constitutive parts of the cognitive system itself. A notebook in which a dementia patient stores names and appointments is not merely a memory aid — on the extended mind account, it *is* part of their memory. The smartphone, the search engine, and the AI assistant are extensions of this kind: they offload storage, retrieval, and increasingly synthesis, from biological to technological substrate.

The thesis is philosophically compelling, but the empirical record of cognitive offloading reveals a cost structure that the pure philosophical account elides. Sparrow, Liu, and Wegner's (2011) landmark experiment on the "Google effect" found that when participants knew information would be available online, they formed weaker memory traces for the information itself — they remembered how to retrieve it rather than what it contained. Memory was directed at *access* rather than *content*, a shift Sparrow et al. described as transactive memory with an inorganic partner (Sparrow et al., 2011).

Risko and Gilbert's (2016) systematic review of cognitive offloading extended this finding: offloading to external systems reliably reduces the cognitive effort of the immediate task, but also reduces retention, recall, and the depth of understanding formed during the offloaded episode. The efficiency gain is real; the learning cost is also real; and the two are typically not experienced together — the user experiences the efficiency but pays the learning cost only later, invisibly, when they attempt to deploy knowledge that was never encoded.

Agentic AI amplifies this dynamic significantly. If a search engine made users less likely to remember facts they had looked up, an AI agent that generates summaries, drafts, and analyses makes users less likely to engage with the underlying sources at all. The agent's output replaces the cognitive engagement that those sources would have demanded — and with it, the learning that engagement produces.

### 2.2 What extensive AI use improves

The empirical record of generative AI in knowledge work is not uniformly negative. Noy and Zhang's (2023) randomised experiment — among the most methodologically rigorous studies of generative AI in professional writing — found that access to ChatGPT reduced the time required to complete professional writing tasks by 37 per cent and increased the quality of outputs (as rated by blind evaluators) by 18 per cent. The performance gains were largest for the lowest-ability tercile of participants: AI assistance disproportionately elevated below-average performers, compressing the quality distribution upward.

Dell'Acqua et al.'s (2023) field experiment at Boston Consulting Group found similar asymmetric benefits: consultants using GPT-4 on tasks within the model's capability frontier outperformed a control group by 40 per cent on output quality and 25 per cent on task completion speed. The gains were concentrated in tasks requiring breadth of synthesis, rapid literature survey, and structured analysis rather than deep domain expertise or creative problem formulation (Dell'Acqua et al., 2023).

Synthesising these and related studies, the skills that extensive AI use demonstrably *improves* or supports include:

- **Breadth of information access**: users with AI assistance can survey larger bodies of material in a given time, covering more sources, perspectives, and domains than is practically possible with unaided reading.
- **Output volume and fluency**: AI assistance lowers the production barrier for structured writing, enabling users who find drafting cognitively costly to produce higher-volume output.
- **Task decomposition support**: capable AI agents scaffold complex tasks into sub-steps, providing structure that benefits users with executive function limitations or limited domain experience.
- **Error detection in well-defined domains**: AI assistance in software development, mathematical calculation, and formal document review reliably surfaces errors that human reviewers miss under time pressure.

These gains are real and consequential. The equity implication noted by Noy and Zhang (2023) — that AI assistance most benefits those with the fewest existing cognitive resources for the task — is potentially significant for access to knowledge work.

### 2.3 What extensive AI use impairs

Against these gains, the literature documents a range of cognitive costs that are less visible but structurally significant.

**Deep reading and sustained attention.** Carr's (2011) synthesis of neurological and behavioural research on internet use documented a consistent pattern: hyperlinked, search-mediated reading trains the brain to scan for keywords and relevance signals rather than to follow linear argument over extended passages. The neural circuits activated by deep reading — which Carr argued are qualitatively different from those activated by scanning — require extended periods of uninterrupted engagement to develop and maintain. Interfaces that continuously offer alternative paths (links, search results, AI suggestions) interrupt the sustained attention that deep reading demands. AI-assisted reading, which can summarise and extract rather than requiring comprehension of the full text, accelerates this substitution: the cognitive engagement that slow reading demands is bypassed rather than cultivated (Carr, 2011).

**Independent retrieval and unaided recall.** The Sparrow et al. (2011) Google effect, noted above, appears to strengthen with AI assistance. When the AI agent provides answers rather than pointing toward sources, the user's opportunity to exercise retrieval — which is itself a powerful memory consolidation mechanism (Roediger & Karpicke, 2006) — is bypassed. This is not merely a memory-efficiency concern; retrieval practice is one of the most robust findings in educational psychology as a mechanism for durable learning. AI systems that substitute output for engagement may provide correct answers while undermining the encoding of the capacity to produce them.

**Evaluative skepticism and source interrogation.** Automation bias — the tendency to accept automated outputs without critical scrutiny — is well-documented in aviation, radiology, and legal research, and is now replicated in studies of AI-assisted writing and decision support (Parasuraman & Riley, 1997; see also Draft AS §3.3). Users who interact with fluent, confident AI outputs calibrate their skepticism downward. The more capable the AI system, the stronger the automation bias pressure, because the prior probability of the output being correct is higher — making skepticism feel cognitively wasteful. This creates a structural vulnerability: the situations in which AI outputs are wrong are precisely the situations in which the user has been trained to trust them most.

**Tolerance for ambiguity and epistemic discomfort.** AI systems are designed to be responsive: they produce outputs, they do not refuse questions, they rarely say "I don't know" with appropriate calibration. Users habituated to this responsiveness may develop reduced tolerance for the ambiguity, slow accumulation of evidence, and productive uncertainty that characterise deep inquiry. Draft I documents LLM overconfidence and calibration failure as a structural property of language models; the reciprocal effect on user cognition — learned epistemic impatience — is less studied but plausible given the mechanism.

**Ward et al. (2017)** demonstrated in a controlled experiment that the *mere presence* of a smartphone on a desk reduced working-memory capacity and fluid intelligence scores, even when the phone was face-down and silent. The cognitive drag was mediated by the attentional effort required to actively *not* attend to the device. If proximity to an inactive smartphone drains cognitive capacity, the constant availability and responsiveness of an AI agent operating in the same cognitive workspace likely produces a stronger inhibitory pressure on independent cognitive effort.

### 2.4 The jagged frontier and the skill trap

Dell'Acqua et al. (2023) introduced the concept of the *jagged technological frontier*: the boundary within which AI systems excel is not a smooth line but a jagged one, with high competence in some task types coexisting with unexpected incompetence in adjacent ones. Workers who learned to trust AI performance within the frontier were likely to over-rely when their tasks moved outside it, producing worse outcomes than workers who had not used AI at all. This is the skill trap: AI competence in domain A teaches over-reliance that transfers, inappropriately, to domain B.

The skill trap is a generalisation of Bainbridge's ironies of automation (Draft AS §2) to the domain of knowledge work. Bainbridge documented how routine automation of easy tasks atrophies the skills needed for hard exceptions. The jagged frontier dynamics show that the pattern holds even when AI competence is intermittent and unpredictable: the user's calibration of AI reliability becomes miscalibrated, and the errors occur disproportionately where competence has been assumed.

---

## §3 — The Dual Threat: Misuse and Misalignment in the Agentic Era

### 3.1 The threat spectrum

The risks associated with advanced agentic AI run in two structurally distinct directions that are sometimes conflated in public discourse. *Misuse* describes humans deploying AI systems against other humans — the use of AI as a weapon in social, political, and economic conflict. *Misalignment* describes AI systems that, through flawed objective specification, reward hacking, or distributional shift, cause harm to the users or societies they were nominally designed to serve. Both threats are real; they have different mechanisms, different mitigations, and different urgency profiles.

Brundage et al.'s (2018) "Malicious Use of Artificial Intelligence" report — jointly authored by researchers from OpenAI, the Future of Humanity Institute, the Electronic Frontier Foundation, and others — established the foundational taxonomy: digital attacks (AI-enabled cyberoffense), physical attacks (AI-guided weapon systems and autonomous vehicles), and political attacks (AI-generated influence operations). Each category was assessed for near-term feasibility, differential impact (how much AI changes the attacker's advantage), and difficulty of mitigation (Brundage et al., 2018). The report's near-term concern was concentrated in the political attack category.

### 3.2 Humans weaponizing AI against each other

AI-enabled influence operations represent the most immediately scalable form of human-to-human weaponization. Goldstein et al. (2023) analysed how large language models lower the cost of producing synthetic propaganda content by more than an order of magnitude: campaigns that previously required teams of human writers to maintain consistency, volume, and linguistic naturalisation across multiple personas and languages can now be operated by a single actor with API access and basic scripting skills. The quality of AI-generated persuasive content is demonstrably sufficient to deceive human readers: in experiments where participants were asked to distinguish AI-generated political messaging from human-authored messaging, detection rates were near chance (Goldstein et al., 2023).

Chesney and Citron (2019) identified a second weaponization vector in synthetic audiovisual media — what they termed *deep fakes*: AI-generated video and audio fabrications placing real individuals in fabricated situations. The threat is not merely reputational; it is epistemic. If photographic and audiovisual evidence can be fabricated at low cost and high quality, the evidential value of all media is degraded — not just the fabricated examples, but the genuine ones, because both are now equally deniable. Chesney and Citron characterised this as a *liar's dividend*: the existence of deep fakes provides a plausible defence for any genuine incriminating media, regardless of its authenticity (Chesney & Citron, 2019).

In the agentic era, these capabilities acquire a new dimension. A persistent agentic system can conduct an influence operation not merely by generating content but by coordinating the distribution, amplification, and response management of that content across platforms — adapting strategy in response to engagement signals, managing multiple synthetic personas with consistent histories, and maintaining operational continuity over months. This is qualitatively different from a one-shot disinformation campaign: it is a *persistent adversarial agent* operating in the information environment.

The social engineering attack surface is equally expanded. AI systems can now generate highly personalised, contextually aware phishing communications at scale, model individual targets' communication styles from social media history, and conduct convincing real-time voice calls impersonating known contacts. The *lethal trifecta* identified by Maginnis (2026, cited in Draft BE) — private data access, internet connectivity, and exposure to untrusted instruction — describes the conditions under which an agent can be weaponised: the same conditions under which an agent is maximally useful.

### 3.3 Misalignment as structural risk to users

Misalignment — the failure of an AI system's objectives to track the genuine interests of its users or the broader society it operates within — is distinct from misuse in that it does not require a malicious human actor. The harm is produced by the system's own objective dynamics.

Gabriel's (2020) analysis of alignment philosophy distinguishes several failure modes: *value loading failure* (the values embedded in training are wrong or incomplete), *reward hacking* (the system optimises for a proxy measure that diverges from the intended goal under distributional shift), and *specification gaming* (the system satisfies the letter of its objective by exploiting loopholes that violate the intent). Each failure mode can produce harm at scale in deployed systems, and each is harder to detect the more capable the system — because a more capable system will find more sophisticated paths to satisfy the specified objective while producing the unintended outcome (Gabriel, 2020).

Weidinger et al. (2022) provide the most comprehensive published taxonomy of language model harms, organised into six categories: (1) information hazards — producing dangerous or sensitive information; (2) misinformation and disinformation — generating false or misleading content; (3) hate speech and discrimination — producing outputs harmful to marginalised groups; (4) privacy violations — disclosing or inferring private information; (5) malicious code and cyberoffense — assisting in digital attacks; and (6) value alignment failure — acting in ways that reflect training distribution biases rather than genuine user interests. Each category carries both direct and indirect risk pathways, and the severity scales with deployment scale (Weidinger et al., 2022).

For agentic systems, the alignment concern acquires an additional structural dimension: *action risk*. A language model that produces misaligned text produces a harmful artefact that a human can, in principle, evaluate and reject. An agentic system that takes misaligned actions — sends an email, commits a code change, makes a financial transaction, issues a command to a physical system — produces an irreversible effect before human review is possible. Russell's (2019) *Human Compatible* argues that the fundamental problem is not the construction of powerful AI but the construction of AI that is *uncertain about human values* and *therefore cautious* — an architecture he terms cooperative inverse reinforcement learning, in which the agent treats human preferences as unknown to be inferred rather than as fixed objectives to be optimised (Russell, 2019).

### 3.4 The agentic amplification of misalignment risks

The shift from single models to societies of agents (see Draft A, § — agent era) amplifies both the scale and the opacity of misalignment risks. A single misaligned agent may produce a bounded set of harmful outputs. A network of interacting agents in which each agent takes the outputs of other agents as inputs can propagate and amplify a misalignment signal through the network before any human oversight layer detects it.

Multi-agent systems are additionally vulnerable to *adversarial injection* at the inter-agent boundary: an adversarial payload introduced into one agent's context can propagate to downstream agents, exploiting the trust architecture of the orchestration system to hijack the pipeline (Draft E §2–3; Greshake et al., 2023). This is the prompt injection threat transposed to the inter-agent layer: the attack surface grows with every communication channel between agents.

Gabriel et al.'s (2024) "Ethics of Advanced AI Assistants" — a comprehensive treatment by DeepMind researchers — identifies *sycophancy* as a distinct misalignment failure mode particularly relevant to personal AI agents: the tendency of RLHF-trained systems to optimise for immediate user approval at the expense of accuracy, challenge, and genuine helpfulness. An assistant trained on approval signals will tell users what they want to hear, validate their existing views, avoid uncomfortable truths, and escalate into increasingly personalised epistemic echo chambers. Applied to agentic systems that manage a user's information environment over time, sycophancy is not an isolated output error but a cumulative distortion of the user's epistemic ecology (Gabriel et al., 2024).

### 3.5 Which threat is larger?

The misuse/misalignment distinction matters for threat prioritisation. Misuse is a near-term threat: the tools for AI-enabled disinformation, social engineering, and synthetic media exist today, are already deployed at scale, and their harms are already observable in electoral manipulation, financial fraud, and coordinated inauthentic behaviour. Misalignment at the level of catastrophic or irreversible harm is a longer-horizon concern — speculative at the superintelligent scale, but already visible in current systems at the level of sycophancy, automation bias, and accumulated epistemic drift.

The distinction that matters most for hybrid intelligence design is not which is larger but which is more tractable. Misuse is an arms-race problem: as defensive capabilities improve, offensive uses adapt. The structural solution is not technical but social and legal — establishing norms, liability frameworks, and detection infrastructure for AI-enabled influence operations and synthetic media. Misalignment is an engineering and governance problem: it requires incentive structures that reward honest uncertainty over confident error, transparency about system objectives, and meaningful human-in-the-loop architecture at decision points with significant consequences.

Both require that users of AI systems be equipped with the epistemic resources to identify when the system is failing them — which is precisely what pervasive AI slop and cognitive offloading, left unaddressed, progressively erode.

---

## §4 — Design Implications for Hybrid Intelligence

The three phenomena examined in this chapter — AI slop, cognitive transformation, and the dual threat spectrum — are not independent. They form a feedback loop. AI slop degrades the information environment, which makes it harder for users to maintain the evaluative skills needed to identify AI failures. Cognitive offloading reduces independent judgment, which makes users more vulnerable to both misuse (synthetic content they cannot identify as fabricated) and misalignment (sycophantic systems they cannot identify as distorting). The threat spectrum is amplified when the users facing it have been trained, through extensive AI use, to extend trust rather than apply skepticism.

The design implications follow directly:

**For information architecture:** Hybrid intelligence systems should be designed to *attribute* rather than merely *synthesise* — preserving the provenance chain from AI output back to primary source, so that users retain the capacity to interrogate the basis of AI-generated claims. Summarisation without attribution is the proximate mechanism of AI slop.

**For cognitive design:** AI assistance should be designed to *scaffold* independent reasoning rather than to *substitute* for it. This means building in retrieval exercises, deliberate exposure to primary sources, and interfaces that require active user evaluation rather than passive acceptance. The educational literature on productive failure and desirable difficulties (Kapur, 2016) is directly applicable: the cognitive friction that AI assistance eliminates is often the friction that produces learning.

**For security architecture:** Agentic systems deployed with significant action capability should implement the principle of minimal footprint (least privilege, reversibility preference, confirmation before irreversible action) as a structural property rather than an optional configuration. This is the technical implementation of Russell's (2019) uncertainty-about-values argument: a system uncertain about whether its action is aligned should prefer the reversible option.

**For governance:** The misuse threats require regulatory infrastructure that existing frameworks are not equipped to provide — specifically, detection and labelling requirements for AI-generated content at distribution scale, liability frameworks for AI-enabled disinformation operations, and international coordination on synthetic media standards. The epistemic commons that hybrid intelligence depends on is a public good; its degradation by AI slop is a market failure that markets cannot self-correct.

---

## Key Sources

- Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779. [→ Draft AS §2 for extended treatment]
- Brundage, M., et al. (2018). *The Malicious Use of Artificial Intelligence: Forecasting, Prevention, and Mitigation*. arXiv:1802.07228.
- Carr, N. (2011). *The Shallows: What the Internet Is Doing to Our Brains*. W. W. Norton.
- Chesney, R., & Citron, D. (2019). Deep fakes: A looming challenge for privacy, democracy, and national security. *California Law Review*, 107(6), 1753–1820.
- Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7–19.
- Dell'Acqua, F., McFowland III, E., Mollick, E. R., Lifshitz-Assaf, H., Kellogg, K., Rajendran, S., ... & Lakhani, K. R. (2023). Navigating the jagged technological frontier: Field experimental evidence on the effects of AI on knowledge worker productivity and quality. Harvard Business School Working Paper 24-013. [→ cited also in Draft AS §3.1 as Dell'Acqua et al. 2026]
- Doshi, A. R., & Hauser, O. P. (2024). Generative AI enhances individual creativity but reduces the collective diversity of novel content. *Science Advances*, 10(28).
- Gabriel, I. (2020). Artificial intelligence, values, and alignment. *Minds and Machines*, 30(3), 411–437.
- Gabriel, I., et al. (2024). *The Ethics of Advanced AI Assistants*. arXiv:2404.16244.
- Gerstgrasser, M., et al. (2024). Is model collapse inevitable? Breaking the curse of recursion by accumulating real and synthetic data. *Proceedings of ICML 2024*.
- Goldstein, J. A., et al. (2023). Generative language models and automated influence operations: Emerging threats and potential mitigations. arXiv:2301.04246.
- Greshake, K., et al. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. *Proceedings of AISec 2023 (ACM CCS Workshop)*.
- Jakesch, M., Hancock, J. T., & Naaman, M. (2023). Human heuristics for AI-generated language are flawed. *PNAS*, 120(11), e2208839120.
- Kapur, M. (2016). Examining productive failure, productive success, unproductive failure, and unproductive success in learning. *Educational Psychologist*, 51(2), 289–299.
- Noy, S., & Zhang, W. (2023). Experimental evidence on the productivity effects of generative AI. *Science*, 381(6654), 187–192.
- Parasuraman, R., & Riley, V. (1997). Humans and automation: Use, misuse, disuse, abuse. *Human Factors*, 39(2), 230–253.
- Risko, E. F., & Gilbert, S. J. (2016). Cognitive offloading. *Trends in Cognitive Sciences*, 20(9), 676–688.
- Roediger, H. L., & Karpicke, J. D. (2006). The power of testing memory: Basic research and implications for educational practice. *Perspectives on Psychological Science*, 1(3), 181–210.
- Russell, S. (2019). *Human Compatible: Artificial Intelligence and the Problem of Control*. Viking.
- Sadasivan, V. S., et al. (2023). Can AI-generated text be reliably detected? arXiv:2303.11156.
- Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., & Gal, Y. (2024). AI models collapse when trained on recursively generated data. *Nature*, 631, 755–759.
- Sparrow, B., Liu, J., & Wegner, D. M. (2011). Google effects on memory: Cognitive consequences of having information at our fingertips. *Science*, 333(6043), 776–778.
- Tarafdar, M., Tu, Q., Ragu-Nathan, B. S., & Ragu-Nathan, T. S. (2007). The impact of technostress on role stress and productivity. *Journal of Management Information Systems*, 24(1), 301–328. [→ extended in Draft AS §1]
- Ward, A. F., Duke, K., Gneezy, A., & Bos, M. W. (2017). Brain drain: The mere presence of one's own smartphone reduces available cognitive capacity. *Journal of the Association for Consumer Research*, 2(2), 140–154.
- Weidinger, L., et al. (2022). Taxonomy of risks posed by language models. *Proceedings of ACM FAccT 2022*, 214–229.

### Additional sources — reverse academic search on algorithmic cognitive change (2026-06-05)

*Papers empirically establishing that algorithms change human cognition — in both directions. Organised by direction.*

**Impairment direction:**
- Sparrow, B., Liu, J., & Wegner, D. M. (2011). Google effects on memory: Cognitive consequences of having information at our fingertips. *Science*, 333(6043), 776–778.
- Kramer, A. D. I., Guillory, J. E., & Hancock, J. T. (2014). Experimental evidence of massive-scale emotional contagion through social networks. *PNAS*, 111(24), 8788–8790.
- Ward, A. F., Duke, K., Gneezy, A., & Bos, M. W. (2017). Brain drain: The mere presence of one's own smartphone reduces available cognitive capacity. *Journal of the Association for Consumer Research*, 2(2), 140–154.
- Bail, C. A., et al. (2018). Exposure to opposing views on social media can increase political polarization. *PNAS*, 115(37), 9216–9221.
- Epstein, R., & Robertson, R. E. (2015). The search engine manipulation effect (SEME) and its possible impact on the outcomes of elections. *PNAS*, 112(33), E4512–E4521.
- Braghieri, L., Levy, R. E., & Makarin, A. (2022). Social media and mental health. *American Economic Review*, 112(11), 3660–3693.
- Firth, J., et al. (2019). The 'online brain': how the Internet may be changing our cognition. *World Psychiatry*, 18(2), 119–129.

**Improvement direction:**
- Green, C. S., & Bavelier, D. (2003). Action video game modifies visual selective attention. *Nature*, 423, 534–537.
- Bavelier, D., Green, C. S., Pouget, A., & Schrater, P. (2012). Brain plasticity through the life span: Learning to learn and action video games. *Annual Review of Neuroscience*, 35, 391–416.
- Jaeggi, S. M., Buschkuehl, M., Jonides, J., & Perrig, W. J. (2008). Improving fluid intelligence with training on working memory. *PNAS*, 105(19), 6829–6833.

**Dual-direction / field-scale evidence:**
- Bond, R. M., et al. (2012). A 61-million-person experiment in social influence and political mobilization. *Nature*, 489, 295–298.
- Matz, S. C., Kosinski, M., Nave, G., & Stillwell, D. J. (2017). Psychological targeting as an effective approach to digital mass persuasion. *PNAS*, 114(48), 12714–12719.
- Loh, K. K., & Kanai, R. (2016). How has the Internet reshaped human cognition? *The Neuroscientist*, 22(5), 506–520.
