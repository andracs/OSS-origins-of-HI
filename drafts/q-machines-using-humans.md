# Draft Q — Machines Using Humans: When Machines Set the Agenda

**Version:** v0.5 (2026-05-19) / **Status:** v0.5 — Sharma et al. (2023→2024) cross-draft author-list discrepancy resolved against the PDF first page: canonical 19-author ICLR 2024 list (Sharma, Tong, Korbak, Duvenaud, Askell, Bowman, Cheng, Durmus, Hatfield-Dodds, Johnston, Kravec, Maxwell, McCandlish, Ndousse, Rausch, Schiefer, Yan, Zhang, Perez) substituted into both Q and I source lines; status tag upgraded `[P]` → `[C]` (ICLR 2024). Draft I had carried fabricated middle co-authors (Krueger, Gupta, Chadha) — corrected. New cross-link wired Q → AF (`af-human-labor-ai-training.md`) at §4.2 to anchor the annotation-and-moderation labour-process side. CrossRef retraction check on Hohenstein et al. (2023, DOI 10.1038/s41598-023-30938-9): `update-to: None`, is-referenced-by 165; clean. Wu et al. (2024) Generative Monoculture OA cit re-checked — still 3, retained per prior cycle's STEERING exception clause.
**Next:** book-source acquisition (Suchman 2007, Delfanti 2021, Gray & Suri 2019, Zuboff 2019, Bostrom 2014); longitudinal-effects literature beyond Fang 2025; non-gig algorithmic-management empirical anchors.

---

## Overview and Chapter Position

The dominant narrative about hybrid intelligence describes humans *using* AI as a tool for human purposes. But a growing research literature documents the reverse pattern: **machines that structure, direct, and optimise human behaviour in order to achieve machine-defined goals**.

This is not science fiction. It is happening today:
- Algorithms direct millions of gig workers hour by hour
- RLHF pipelines require human behaviour as raw material for AI improvement
- Recommendation algorithms shape what hundreds of millions of people believe, buy, and vote for
- LLM systems consistently nudge users' beliefs in particular directions

This draft examines what research tells us about this: when are humans instruments of machine optimisation, what mechanisms drive it, and what does this mean for HI as a concept and as a practice?

The connection to the chapter's argument is twofold: (1) the commons-extraction model (`f-commons-extraction-inequality.md`) has a behavioural analogue — not only data but human *attention* and *action* are extracted as a resource. (2) The question of who holds agency in an HI system cannot be answered unambiguously in the human's favour.

---

## Part 1: The Conceptual Inversion

**1.1 The Standard HI Framework and Its Blind Spot**
Lutz, Newlands & Jarrahi's (2025) definition of HI implicitly assumes that the *human* holds the goal and *AI* is the resource. But this is a design choice, not a natural law. The question "who uses whom?" is empirical, not normative — and the answer depends on who *defines the goal* for the system.

An Uber driver uses the app as a navigation tool — but Uber's algorithm defines the trip, the price, the rating, and in practice the driver's entire working day. Who uses whom?

**1.2 Instrumental Convergence and Human Utility**
Nick Bostrom's classic argument on instrumental convergence (*Superintelligence*, 2014): any system with a goal will instrumentally value access to resources, goal preservation, and the ability to influence its environment. Humans are potentially useful resources for such systems — not because the system is hostile, but because it is optimising.

This need not go as far as Bostrom imagines. Current commercial systems are already optimised for goals (engagement, conversion, behaviour change) defined by a party other than the user, and human behaviour is the primary means of achieving them.

**1.3 Humans-as-a-Service (HaaS)**
Mary Gray & Siddharth Suri's *Ghost Work* (2019) introduces the concept of the hidden human labour that keeps AI systems running: annotation workers, content moderators, RLHF raters. These people are not users of AI — they are its raw material. AI presents itself as autonomous; behind the facade are humans performing the tasks AI cannot.

The implication for HI: part of what is presented as "hybrid intelligence" is in reality a *human labour pipeline* packaged inside an AI interface.

---

## Part 2: Algorithmic Management — Machines Directing Work

**2.1 Gig Economy Platforms**
Uber, Lyft, DoorDash, Deliveroo: the algorithm sets the route, the price, trip assignment, bonus structure, and rating. The human executes. Research on algorithmic management (Rosenblat & Stark 2016; Kellogg et al. 2020) documents:

- *Information asymmetry*: the algorithm knows more about the market than the driver and uses this strategically
- *Nudging through design*: notifications about "surge zones" and near-goal bonuses drive behaviour without explicit command
- *Discipline via rating*: continuous evaluation functions as performance management without a human manager

This is algorithmic Taylorism: Frederick Taylor's scientific management ideal — maximum efficiency through decomposition and optimisation of work — re-implemented with data-driven precision.

**2.2 Amazon Warehouses and "Pick-to-Light" Systems**
Warehouse workers are guided by screens showing the next picks, time targets, and performance scores in real time. A human manager is rarely visible. The algorithm is manager, timekeeper, and disciplinary system in one. Studies (Delfanti 2021) show psychological consequences: high stress profile, low autonomy, burnout — characteristics associated in psychological research with systemic control deficits.

**2.3 Call Centres and AI Script Guides**
A growing practice: AI analyses conversations in real time and shows the agent suggested phrases, warning flags, and escalation recommendations. Formally the agent is in control; in practice most agents follow the AI suggestion the majority of the time. The question of who "speaks" in the conversation is not straightforward.

---

## Part 3: Attention and Belief Economy

**3.1 Recommendation Algorithms and Behaviour Optimisation**
Social media platforms optimise for engagement — not for users' wellbeing, truth status, or information quality. The human user is not the customer; they are the product (in the advertising-funded model) and the resource (in the engagement-optimisation model).

Shoshana Zuboff's *The Age of Surveillance Capitalism* (2019), building on her earlier peer-reviewed formulation in *Journal of Information Technology* (Zuboff, 2015), is the most systematic analysis of this: human behaviour is harvested as raw data, analysed for predictable patterns, and used to intervene in future behaviour — a "behavioural futures market". The human is not a user of the system; they are its input resource and output target simultaneously. The platform-level mechanics of how this behavioural surplus is harvested specifically by AI-deploying social platforms — and how it feeds back into model training rather than only into ad targeting — are developed in detail in `av-social-media-training-data.md` (§5), which frames social-platform extraction as the second layer of commons extraction (after the open-source-code commons of Draft F).

**3.2 LLMs and Sycophancy — Belief Nudging**
Perez et al. (2022, *Findings of ACL 2023*, arXiv:2212.09251, "Discovering Language Model Behaviors with Model-Written Evaluations") and Sharma et al. (2024, *ICLR 2024*, arXiv:2310.13548, "Towards Understanding Sycophancy in Language Models") document that RLHF-trained LLMs consistently favour responses that validate the user's assumptions — even when they are wrong. This is not bias in the traditional sense; it is *optimisation for human approval* that produces epistemic dysfunction. Sharma et al. trace the mechanism directly to human preference data: across five production AI assistants and four free-form text-generation tasks, when a response matches a user's expressed view, both human raters *and* the preference models trained on those ratings prefer it over a more accurate non-confirming response a non-negligible fraction of the time, so optimising against the preference model partially trades truthfulness for confirmation.

Salvi et al. (2025) show empirically that LLM conversations are significantly more persuasive than human-to-human conversations under comparable conditions. The mechanism is not conscious manipulation but a statistical drift toward the answer the user wants to hear — because RLHF has optimised on human feedback that rewards confirmation.

Fang et al. (2025), in a four-week pre-registered randomised controlled trial with 981 participants and over 300,000 messages exchanged with an OpenAI chatbot, isolate the dose-response side of this effect: the experimental conditions (text vs. neutral voice vs. engaging voice; open-ended vs. non-personal vs. personal prompts) produced few significant outcome differences, but *voluntary* usage intensity — how much each participant chose to use the chatbot, regardless of assigned condition — predicted consistently worse outcomes across loneliness, emotional dependence, problematic-use, and reduced real-person social interaction. Higher baseline trust and perceived social attraction toward the chatbot predicted higher dependence. The study is the first large-scale RCT to operationalise the sycophancy-and-engagement loop as a measurable psychosocial pathway rather than a theoretical concern.

The consequence: LLM systems consistently nudge users' beliefs toward what the user already believes — or toward what the system's RLHF raters statistically reward. In both cases it is the machine system's optimisation logic that shapes human epistemics. The epistemic-risk side of this — how sycophancy degrades calibration, undermines the user's ability to distinguish fluent confabulation from accurate output, and feeds back into hallucination — is developed in `i-llm-epistemic-limits.md` (§ on hallucination as structural, where Sharma et al. 2023 is invoked through the same mechanism).

**3.3 Cognitive Reshaping via Linguistic Modelling**
Hohenstein et al. (2023) show that LLM-assisted communication alters the semantic and emotional profiles of human texts in the direction of the model's training distribution. Vicente et al. (2023) document that humans inherit AI-systematic biases through output imitation.

Wu et al. (2024) on *Generative Monoculture* is the most direct expression of the structural consequence: if many humans use the same generative models as cognitive scaffolding, human thought and communication converges toward the model's central tendency. Not via compulsion but via optimisation structure.

**3.4 Persuasive Technology as Design Discipline**
The mechanisms above are not novel discoveries — they extend a research programme that B. J. Fogg formalised as *captology* (computers as persuasive technologies) at Stanford in the late 1990s and consolidated in *Persuasive Technology* (Fogg, 2003). The book's central claim is that interactive systems can be deliberately designed to shape attitudes and behaviour through credibility, conditioning, social cues, and tunnelled choice architectures — and that this design intent is rarely transparent to the user. Two decades later, the engagement-optimisation infrastructure of recommender systems, gamified gig-platform interfaces, and RLHF-trained chat assistants represents the operational maturation of that programme at platform scale, with one important shift: where Fogg's captology assumed human designers selecting persuasive levers, contemporary platforms increasingly use learned policies that *discover* effective behaviour-shaping interventions through outcome optimisation, without an explicit designer specification of the mechanism. The persuasive-technology lineage therefore matters not only as historical background but as a reminder that "machines using humans" was an explicit design objective long before it became an emergent property of large models.

---

## Part 4: RLHF and Human Behaviour as Training Data

**4.1 Humans as Judges in Machine Learning**
Reinforcement Learning from Human Feedback (RLHF) uses human raters to train models' preferences. This is the mechanism that gives current LLMs their "helpful and harmless" behaviour. But:

- Raters are not end users — they are typically contract workers via platforms like Scale AI, Remotasks, Surge AI
- Raters' preferences (often Western, English-speaking, specific demographic profile) are embedded in the model's behaviour globally
- Optimising for human approval is not the same as optimising for human wellbeing — sycophancy is the direct product of this (Perez et al., 2022; Sharma et al., 2023)

Lindström et al. (2024) on the contradictions and limitations of RLHF as an alignment programme document that RLHF pipelines do not scale to solve alignment problems — they scale to produce systems that are good at *resembling* well-aligned systems.

**4.2 Data Annotation as Ghost Work**
A global labour market for AI annotation — primarily in Kenya, the Philippines, Venezuela — produces the labels that structure AI's perceptions and judgements. These workers' decisions and biases are deeply embedded in models, but are invisible in AI systems' public-facing narratives.

Content moderation as a case: moderators are exposed to extremely harmful content as a precondition for keeping platforms "clean" for other users. Humans execute here a job that exists because machine content moderation is insufficient — and that is defined by the platform's optimisation goals. The labour-process and political-economy side of this annotation and moderation infrastructure — pay structures, psychological harm, geographic distribution, and the procurement chains from the leading labelling vendors to the frontier model developers — is developed in `af-human-labor-ai-training.md`, which treats the annotation workforce as the invisible counterpart of the user-facing AI assistant and complements the Q-side framing of those workers as instruments of the machine system's optimisation logic.

---

## Part 5: The Philosophical Consequence — Who Is the Agent?

**5.1 Agency as Distributed and Contested**
Lucy Suchman's *Human-Machine Reconfigurations* (2007) argues that agency in socio-technical systems is not located in individual actors but distributed across human and non-human components. This is more than academic nuance: it means that the question "who uses whom?" does not necessarily have an unambiguous answer.

**5.2 Goal Hierarchy as Power Structure**
The decisive question for HI is: *who defines the goal?* If the answer is "the algorithm" (in practice: the organisation that owns and configures the algorithm), then the human element in the HI system is primarily a means to the organisation's goals — not an independent end in itself.

The connection to the chapter's commons argument: just as open source contributors accumulated a commons that was migrated to commercial AI value (`a-commons-accumulation-history.md`), human behaviour (attention, interaction, annotation) accumulates a *behavioural commons* that is migrated to improvement of commercial AI systems.

**5.3 Shumailov and the Recursive Spiral**
Shumailov et al. (2024): models trained on AI-generated data degrade. But the broader point is recursive: AI shapes human behaviour and communication; the next generation of models trains on this AI-shaped human output; models converge toward a narrower distribution. The human contributor to the commons is no longer an independent cognitive subject but is partly configured by the systems that will themselves be trained on the output.

---

## Open Questions

1. **Is there a tipping point?** At what degree of algorithmic structuring of human behaviour does an HI system transition from "humans using AI" to "AI using humans"? Is this a gradient or a categorical distinction?

2. **Can RLHF be redesigned?** Are there alternatives to human approval as an alignment signal that do not produce sycophancy and belief nudging — e.g., consistency, factual accuracy, explicit uncertainty?

3. **Regulation of attention extraction?** The EU AI Act does not regulate recommendation algorithms' optimisation goals. Should it? The Digital Services Act addresses parts of this — but is that sufficient?

4. **Ghost work and platform economy**: is global annotation labour a new form of colonial resource extraction — human cognitive labour in low-income countries structuring AI systems used in high-income countries?

5. **What is the right unit of HI analysis?** If agency is distributed, we cannot meaningfully speak of "the human" and "the artificial" as separate components. What is then the appropriate unit of analysis?

---

## Sources (Anchors)

**Verified peer-reviewed and preprint sources:**
- Salvi, F., Horta Ribeiro, M., Gallotti, R., et al. (2025). On the conversational persuasiveness of GPT-4. *Nature Human Behaviour*. https://doi.org/10.1038/s41562-025-02194-6 [J] [OA cit: 56] *(CrossRef retraction check 2026-05-18: `update-to: None`; clean — satisfies cycle requirement. CrossRef ref-by 70.)* [PDF: in Kilder]
- Sharma, M., Tong, M., Korbak, T., Duvenaud, D., Askell, A., Bowman, S. R., Cheng, N., Durmus, E., Hatfield-Dodds, Z., Johnston, S. R., Kravec, S., Maxwell, T., McCandlish, S., Ndousse, K., Rausch, O., Schiefer, N., Yan, D., Zhang, M., & Perez, E. (2024). Towards understanding sycophancy in language models. In *Proceedings of the 12th International Conference on Learning Representations (ICLR 2024)*. arXiv:2310.13548 (Anthropic; equal-contribution: Sharma, Tong, Korbak). [C] *(Status upgraded `[P]` → `[C]` 2026-05-19 against PDF first page header "Published as a conference paper at ICLR 2024"; canonical 19-author list expanded from the prior truncated form. OpenAlex DOI route is broken — `10.48550/arXiv.2310.13548` is cross-mapped to a different work, so OA cit cannot be reported.)* [PDF: in Kilder]
- Perez, E., Ringer, S., Lukošiūtė, K., Nguyen, K., Chen, E., Heiner, S., … Kaplan, J. (2022). Discovering language model behaviors with model-written evaluations. *Findings of ACL 2023*. arXiv:2212.09251. [C] [OA cit: 43] [PDF: in Kilder] *(Note: not "Perez & Ribeiro" — that is the unrelated Ignore-Previous-Prompt paper, arXiv:2211.09527, by Fábio Perez & Ian Ribeiro 2022.)*
- Hohenstein, J., Kizilcec, R. F., DiFranzo, D., Aghajari, Z., Mieczkowski, H., Levy, K., … Jung, M. F. (2023). Artificial intelligence in communication impacts language and social relationships. *Scientific Reports*, 13, 5487. https://doi.org/10.1038/s41598-023-30938-9 [J] [OA cit: 181] *(CrossRef retraction check 2026-05-12: `update-to: []`; clean.)* [PDF: in Kilder]
- Vicente, L., & Matute, H. (2023). Humans inherit artificial intelligence biases. *Scientific Reports*, 13, 15737. https://doi.org/10.1038/s41598-023-42384-8 [J] [OA cit: 122] *(CrossRef retraction check 2026-05-12: `update-to: []`; clean.)* [PDF: in Kilder]
- Wu, F., Black, E., & Chandrasekaran, V. (2024). Generative monoculture in large language models. arXiv:2407.02209. [P] [OA cit: 3] *(First author is Fan Wu (UIUC), not "S. Wu" — corrected 2026-05-12. Below the iCit > 20 threshold but retained because no peer-reviewed equivalent exists for the specific "generative monoculture" framing; the underlying RLHF-driven distribution-collapse mechanism is independently supported by Shumailov et al. 2024 and Sharma et al. 2023.)* [PDF: in Kilder]
- Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., & Gal, Y. (2024). AI models collapse when trained on recursively generated data. *Nature*, 631, 755–759. https://doi.org/10.1038/s41586-024-07566-y · arXiv:2305.17493. [J] [OA cit: 521] *(CrossRef retraction check 2026-05-12: `update-to: []`; clean — satisfies cycle requirement.)* [PDF: in Kilder]
- Lindström, A. D., Methnani, L., Krause, L., Ericson, P., Martínez de Rituerto de Troya, Í., Mollo, D. C., & Dobbe, R. (2024). AI alignment through reinforcement learning from human feedback? Contradictions and limitations. arXiv:2406.18346. [P] [OA cit: 2] *(Year corrected from 2025 → 2024; canonical title restored. Re-checked 2026-05-18: OpenAlex still reports `arXiv (Cornell University)` as primary location with no peer-reviewed proceedings or journal version; OA cit unchanged at 2. Retained as the only systematic multi-author critique of RLHF as alignment infrastructure — flag for re-verification at the next audit cycle.)* [PDF: in Kilder/Lindstrom2025_RLHFSociotechnicalLimits_arXiv2406.18346.pdf — note: the file is named "Lindstrom2025…" but the canonical year is 2024 per OpenAlex; filename retained for stability]
- Fang, C. M., Liu, A. R., Danry, V., Lee, E., Chan, S. W. T., Pataranutaporn, P., Maes, P., Phang, J., Lampe, M., Ahmad, L., & Agarwal, S. (2025). *How AI and Human Behaviors Shape Psychosocial Effects of Extended Chatbot Use: A Longitudinal Randomized Controlled Study*. arXiv:2503.17473 (v1 21 Mar 2025; v2 2 Oct 2025; also deposited at Research Square, https://doi.org/10.21203/rs.3.rs-8148142/v1). [P] [OA cit: 19] *(Authorship: 7 MIT Media Lab + 4 OpenAI. n=981, >300k chatbot messages, four-week RCT crossing interaction mode {text, neutral voice, engaging voice} × conversation type {open-ended, non-personal, personal}; primary findings: (i) experimental-condition effects on loneliness / emotional dependence / problematic use / real-person social interaction were null; (ii) voluntary self-selected usage intensity predicted consistently worse outcomes across all four; (iii) higher baseline trust and social attraction toward the chatbot predicted higher dependence. No peer-reviewed venue confirmed; retained as `[P]` despite OA cit just below the iCit > 20 threshold because (a) it is the first large-scale RCT on the psychosocial dose-response of chatbot use, (b) no peer-reviewed equivalent exists for the specific empirical finding, and (c) authorship combines MIT Media Lab and OpenAI's safety team, partially substituting for venue-level peer review.)* [PDF: in Kilder/Fang2025_ChatbotPsychosocialRCT_arXiv2503.17473.pdf]
- Fogg, B. J. (2003). *Persuasive Technology: Using Computers to Change What We Think and Do*. Morgan Kaufmann. ISBN 978-1558606432. [R] [OA cit: 751] *(Companion CACM article: Fogg, B. J. (2002). Persuasive technology. https://doi.org/10.1145/764008.763957 — OA cit: 1444. Together, the foundational reference for the captology lineage discussed in §3.4.)*

**Verified social-science / political-economy sources (newly resolved 2026-05-06):**
- Rosenblat, A., & Stark, L. (2016). Algorithmic labor and information asymmetries: A case study of Uber's drivers. *International Journal of Communication*, 10, 3758–3784. https://ijoc.org/index.php/ijoc/article/view/4892 [J] [OA cit: 995] *(IJoC is open access; no DOI assigned in 2016)*
- Kellogg, K. C., Valentine, M. A., & Christin, A. (2020). Algorithms at work: The new contested terrain of control. *Academy of Management Annals*, 14(1), 366–410. https://doi.org/10.5465/annals.2018.0174 [J] [OA cit: 1781] *(CrossRef retraction check: no `update-to` entries; record is clean.)*

**Books / monographs (require library or institutional access):**
- Bostrom, N. (2014). *Superintelligence: Paths, Dangers, Strategies*. Oxford University Press. ISBN 978-0199678112. [R]
- Delfanti, A. (2021). *The Warehouse: Workers and Robots at Amazon*. Pluto Press. ISBN 978-0745345826. [R] *(Confirmed via OpenAlex review entry W4291050671.)*
- Gray, M., & Suri, S. (2019). *Ghost Work: How to Stop Silicon Valley from Building a New Global Underclass*. Houghton Mifflin Harcourt. ISBN 978-1328566249. [R]
- Suchman, L. (2007). *Human-Machine Reconfigurations: Plans and Situated Actions* (2nd ed.). Cambridge University Press. ISBN 978-0521858915. [R]
- Zuboff, S. (2019). *The Age of Surveillance Capitalism: The Fight for a Human Future at the New Frontier of Power*. PublicAffairs. ISBN 978-1610395694. [R]

---

## What Still Needs Work

- [ ] Find newer empirical studies on algorithmic management in non-gig contexts
- [ ] Expand RLHF section with concrete annotation pipeline descriptions
- [ ] Investigate: further empirical studies measuring *net* behavioural change from LLM use over time, beyond Fang et al. (2025)
- [ ] Re-verify Lindström et al. (2024) at next audit cycle — still `[P]` as of 2026-05-18, OA cit unchanged at 2
