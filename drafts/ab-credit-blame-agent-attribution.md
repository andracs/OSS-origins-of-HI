# Draft AB — Who Gets the Credit, Who Gets the Blame? Attribution and Accountability When Agents Do the Work

**Version:** v0.3 (2026-05-15)
**Status:** v0.3 — conceptual and legal synthesis. Empirical literature on AI attribution norms is emerging rapidly but unsettled; institutional responses are in flux. Significant cross-disciplinary synthesis required.
**Next:** continue grounding §3.3b on autonomous-weapons doctrine (download/verify Roff 2016, Docherty 2012, ICRC 2021); resolve remaining analyst tasks from 2026-05-15 annotation queue.

---

## Overview and Chapter Position

A radiologist reviews a chest CT scan. The AI has already flagged the suspicious nodule, measured it, cross-referenced it against the prior scan, retrieved comparable cases from the literature, and produced a draft report with a differential diagnosis and recommended follow-up interval. The radiologist reads the AI's output, confirms it looks reasonable, adds a sentence of clinical context, and signs her name. The report goes into the patient's record as her professional judgment. If the nodule is malignant and the AI missed it, the malpractice claim names her.

A drone operator authorises a strike. The targeting AI has identified the individual based on pattern-of-life analysis, cross-referenced signals intelligence and imagery, calculated a confidence score, and generated a recommended engagement window. The operator presses a key. The command chain credits the unit with the interdiction. If the target was a civilian, the investigation asks what the operator knew and when — not what the algorithm decided.

A software engineer submits a pull request that five AI agents wrote. A researcher publishes a paper whose literature review, data analysis, and first draft were produced by an orchestrated agent pipeline. A lawyer files a brief assembled by a legal AI that retrieved the cases, drafted the arguments, and formatted the citations. In each case, a human's name is on the work. In each case, agents did most of it.

Two questions follow, which are related but distinct:

1. **The credit question**: who deserves recognition for good work produced by a human-agent hybrid? Is it cheating to take credit for what agents did?
2. **The blame question**: who bears responsibility when the agents' work is wrong, harmful, or fraudulent?

These questions are not new in form — humans have always used intermediaries, tools, and collaborators whose contributions were partially or fully invisible in the final attribution. What is new is the *scale*, *quality*, and *substitutability* of agentic contributions, and the structural gap between what humans can verify and what agents produce.

This draft examines the historical and theoretical frameworks for attribution and accountability, the emerging institutional responses, and the design implications for hybrid intelligence systems. It connects to `p-governance-compliance-hi.md` (responsibility gap, meaningful human oversight), `q-machines-using-humans.md` (the accountability inversion), `g-agentic-hi-collaboration.md` (agentic HI collaboration), `m-agentic-ai-taxonomies.md` (HITL/HOTL spectrum), `aa-ai-outperformance-psychology.md` (cognitive overwhelm and oversight limits), and `x-epistemic-provenance-detection.md` (provenance as accountability infrastructure).

---

## Part 1: The Attribution Problem — What Counts as a Contribution?

**1.1 Historical attribution norms and their instability**
Attribution in knowledge work has never been a simple record of who did what. Academic authorship norms require "substantial contribution to conception or design, or acquisition, analysis, or interpretation of data" (ICMJE criteria) — but Wislar, Flanagin, Fontanarosa & DeAngelis (2011), surveying corresponding authors of 896 articles in six high-impact general medical journals (*Annals of Internal Medicine*, *JAMA*, *Lancet*, *Nature Medicine*, *NEJM*, *PLOS Medicine*) for the 2008 publication year, found that 21.0% of articles (95% CI 18.0%–24.3%) carried honorary or ghost authors or both — specifically, 17.6% of articles had at least one honorary author (someone named who did not meet ICMJE criteria) and 7.9% had at least one ghost contributor (someone whose substantive work was not credited). The prevalence was higher for original research (25.0% honorary, 11.9% ghost) than for reviews or editorials. The current system is aspirational rather than descriptive, even at the upper end of the journal-quality distribution where enforcement should be strongest. Contemporary data suggest the AI-specific form of unacknowledged contribution is already substantial: large-scale statistical analysis of scientific abstracts finds that language characteristic of LLMs appeared in a rapidly growing fraction of papers after ChatGPT's public release, reaching an estimated 17.5% of computer science papers and 16.9% across domains by early 2024, with the vast majority carrying no AI-use disclosure (Liang et al., 2024).

The ghostwriter tradition is even older and more explicit: speechwriters, book doctors, research assistants, and editorial staff have always contributed substantially to published work attributed to others. The convention is understood: the named author carries the public persona, the accountability, and the warrant; the contributor provides the substance. This is not universally regarded as dishonest — it is an acknowledged division of cognitive labour in many professional contexts.

**1.2 Where AI changes the calculation**
AI agents differ from human ghostwriters in four ways that stress existing attribution norms:

*Scale*: a single human can deploy dozens of agents running in parallel, producing outputs that would require a large team of skilled humans to replicate. The ratio of attributed human contribution to actual agent contribution can approach zero.

*Quality*: as agentic capability increases, the gap between agent-produced work and expert-human work narrows. A ghostwriter producing mediocre work was limited by their own capability; an agent producing frontier-quality work raises the question of what the named human actually added.

*Verifiability*: a human can verify a human ghostwriter's work using the same expertise the ghostwriter deployed. When agents produce work that exceeds the human's own capability — the radiologist whose AI identifies pathologies she cannot see — verification requires a different kind of expertise than production. This creates a systematic epistemic asymmetry between what is attributed and what can be genuinely evaluated by the person taking credit.

*Deniability*: agent contributions are structurally harder to detect than human collaborator contributions. A co-author leaves traces in email exchanges, drafts, and institutional records. An agent's contribution is, by default, erased when the final output is submitted. This creates asymmetric incentives: the norms against ghost authorship are enforced by the difficulty of concealment; when concealment is trivially easy, norm enforcement collapses.

**1.3 The AlphaFold precedent**
DeepMind's AlphaFold2 (Jumper et al., 2021) solved the protein folding problem — a problem that had resisted 50 years of human scientific effort (Dill & MacCallum, 2012) — and its developers received the Nobel Prize in Chemistry in 2024. The prize was divided between David Baker (½, for computational protein design) and Demis Hassabis and John Jumper (¼ each, for AlphaFold) — three named individuals (Nobel Committee for Chemistry, 2024). The humans who designed, trained, and deployed the system received credit; AlphaFold itself received none.

This outcome is the current institutional default: credit flows to the humans who created and directed the agent, not to the agent. But the AlphaFold case is structurally unusual — the system was purpose-built for a single landmark problem, the team was large and well-documented, and the science community had decades of context for what the solution meant. The attribution question becomes harder when the human's role is not "design a system to solve X" but "prompt a general-purpose agent and submit its output."

---

## Part 2: Credit Asymmetries — Prizes, Authorship, and Open Source Commits

**2.1 The Nobel problem and intellectual property**
The Nobel Prize statutes prohibit posthumous awards and limit prizes to three living persons — norms designed for a world of individual human discovery. The AlphaFold case exposed the inadequacy of these norms for collaborative human-machine science, but the committee resolved it by attributing to the humans who directed the system. Patent law faces a similar crisis: courts in the US, UK, and EU have consistently ruled that AI systems cannot be named as inventors; patents require a human inventor (Thaler v. Vidal, Fed. Cir. 2022; Thaler v. Comptroller-General, UKSC 2023; EPO Boards of Appeal, J 0008/20, 2020). The legal infrastructure of intellectual credit is predicated on human authorship and is being stressed by agentic contribution without yet being reformed (Hugenholtz & Quintais, 2021).

**2.2 Academic authorship in crisis**
Major journals responded to the GPT-3/4 era with emergency disclosure policies:
- *Nature* (2023): AI tools cannot be listed as authors; human authors must disclose AI use in the Methods section (Nature editors, 2023)
- *Science*: similar disclosure requirement; AI-generated text treated as equivalent to data requiring citation (Thorp, 2023)
- IEEE: AI-generated content must be disclosed; AI cannot be a co-author (IEEE, 2023)

These policies resolve the formal attribution question — the human is always the author — but do not address the substantive question: what does authorship mean when the human's contribution was primarily prompting and light editing of agent-generated content? The disclosure norm is a pragmatic minimum, not a principled solution.

**2.3 Open source: bots, commits, and contribution graphs**
Wessel, Wiese, Steinmacher, Conte & Gerosa (2022) document the integration of automation bots into open source repositories and their effects on community dynamics. Bots now make a significant fraction of commits in large open source projects — running CI/CD, triaging issues, updating dependencies, generating changelogs (Erlenhov et al., 2020; Dey et al., 2020). These contributions appear in commit histories attributed to bot accounts (e.g., `dependabot`, `renovate-bot`), not to the humans who configured and deployed them.

This convention — bot accounts as transparent attribution — represents an emerging norm: the agent's contribution is acknowledged in the record, but the human who deployed it carries the reputational and legal accountability. It is a partial solution: it preserves auditability without resolving the deeper question of what the deploying human "did."

---

## Part 3: The Blame Question — Responsibility When Agents Err

**3.1 The responsibility gap**
The concept of the "responsibility gap" was introduced by Matthias (2004) to describe a structural feature of learning automata: when a system capable of autonomous learning causes harm, no single human in the causal chain — designer, trainer, deployer, or user — bears full moral responsibility for outcomes that no individual anticipated or chose. Floridi & Cowls (2019) subsequently developed and generalised this concept within AI ethics discourse. The system's behaviour emerges from the interaction of training data, architecture, fine-tuning, deployment context, and user input; there is no single decision that produced the harmful output.

This gap is not unique to AI — it parallels the diffusion of responsibility in large organisations, bureaucracies, and complex sociotechnical systems. But AI makes it structurally worse: the system can act autonomously in contexts its designers never anticipated, at speeds that preclude human review, and in ways that are difficult to trace after the fact.

**3.2 Respondeat superior and its limits**
In common law, *respondeat superior* ("let the master answer") establishes that employers are vicariously liable for torts committed by employees in the course of their employment. The principle reflects both a deterrence logic (employers control employees and can reduce harm by controlling their actions) and a compensation logic (employers benefit from employees' work and should bear the costs of their errors).

Applied to AI agents: the organisation that deploys an agent is the closest analogue to the employer; agent errors in the course of deployment are analogous to employee torts (Vladeck, 2014). This makes the deploying organisation the natural locus of legal accountability — a principle that the EU AI Act partially encodes through its requirements for operator accountability.

But the analogy breaks down where it matters most: an employer can instruct, supervise, and retrain an employee. An organisation that deploys a frontier AI agent has limited ability to instruct it precisely, may not be able to supervise it in real time (the cognitive overwhelm problem — see Draft AA, §2.5), and cannot retrain it when it errs. The control premise that justifies *respondeat superior* weakens as agent autonomy increases (Selbst, 2023).

**3.3 The meaningful human oversight criterion**
Draft P develops three criteria for meaningful human oversight: the overseer must have (1) the *competence* to evaluate agent outputs, (2) the *time* to evaluate before consequential decisions are made, and (3) genuine *authority* to override (Santoni de Sio & van den Hoven, 2018). When agents operate in domains that exceed the human's expertise, at speeds that preclude deliberate review, the oversight is nominal — a human signature on agent-produced work that the human cannot actually evaluate.

This is the "rubber-stamping" problem: legal and institutional frameworks require human sign-off, but the sign-off is meaningless as a quality control mechanism when the human lacks the capacity to identify errors. The human bears the accountability without having the ability to exercise the control that accountability presupposes. Cognitive overwhelm (Bedard et al., 2026) makes this worse in multi-agent contexts: the human cannot form a coherent model of what the agents are doing, let alone evaluate whether they are doing it correctly.

**3.3b Domain cases: radiology and the military**

The radiologist case captures a structural feature that recurs across high-stakes professional domains: the human's institutional role is to *certify* the agent's output, but the cognitive and epistemic conditions for genuine certification are absent. The radiologist who signs the AI-generated report cannot be said to have meaningfully reviewed it if she lacks the time, the comparative image database, or the algorithmic transparency to identify where the AI's confidence estimate is miscalibrated. Yet the medical and legal system treats her signature as the authentic exercise of professional judgment. This is not a flaw in the individual radiologist's conduct — it is a systemic consequence of deploying AI at a throughput that human oversight cannot match. Topol (2019) notes that AI radiology systems can process thousands of images per hour; radiologist throughput is measured in dozens — a throughput differential that anchors the oversight asymmetry central to this section. The oversight model has not been redesigned to match the deployment model.

The military case introduces a qualitatively different dimension: lethal consequences and the laws of armed conflict. International humanitarian law (IHL) — through its foundational principles of distinction, proportionality, and precaution under Additional Protocol I to the Geneva Conventions (Henckaerts, 2007) — requires genuine human judgment in lethal targeting decisions; "meaningful human control" is the standard advanced in UN CCW Group of Governmental Experts discussions on lethal autonomous weapons systems (LAWS), though this formulation does not yet appear in any binding IHL instrument (UN CCW GGE, 2023). The targeting AI does not fire the weapon; a human authorises the strike. But if the AI's pattern-of-life analysis is wrong — if it has misidentified a civilian as a combatant — the accountability question is acute: did the human operator exercise genuine judgment, or did they perform a confirmatory gesture on an AI determination they lacked the independent intelligence to evaluate?

Military doctrine in the US and UK currently requires a human "in the loop" for lethal targeting decisions (US Department of Defense, 2023; UK Ministry of Defence, 2017; Schmitt & Thurnher, 2013) — but critics (Human Rights Watch, ICRC) argue that the combination of AI speed, operational pressure, and information asymmetry means the human is effectively a rubber-stamp rather than a genuine decision-maker (Santoni de Sio & van den Hoven, 2018; Goddard et al., 2012). The military case is thus the limiting case of the accountability problem described throughout this draft: when the pace and complexity of AI operation exceeds human evaluation capacity, the nominal human override becomes a liability shield rather than a substantive check.

**3.4 The asymmetry thesis: credit flows up, blame flows down**
An observed pattern in organisational contexts (though not yet systematically documented for AI agents specifically; see Bonnefon et al., 2023, for review of the broader moral-attribution literature) suggests a troubling asymmetry: when AI-assisted work succeeds, the credit flows to the human who deployed the agents; when it fails, the blame also flows to the human — but accompanied by demands for the human to have prevented failure that the cognitive capacity constraints made impossible (Bigman & Gray, 2018; Earp et al., 2024).

This asymmetry is not a logical inconsistency: it follows from the institutional and legal defaults described above. But it creates a perverse incentive structure: humans who deploy powerful agents bear the full downside of agent error while capturing the upside of agent capability, creating pressure to deploy more capable agents with less oversight — the exact opposite of what risk management would recommend.

---

## Part 4: Emerging Institutional Responses

**4.1 Disclosure as baseline norm**
The minimum institutional response — now adopted across most major academic journals, many professional bodies, and some jurisdictions — is disclosure: humans must acknowledge AI assistance in their work. The AI Disclosure Act proposed in the US (Torres, 2023, H.R. 3831) and analogous provisions in the EU AI Act — specifically Article 50, which mandates disclosure when natural persons interact with AI systems and requires machine-readable marking of AI-generated synthetic content (European Parliament and Council of the European Union, 2024, Art. 50) — establish disclosure as a legal minimum for certain categories of AI-assisted content.

Disclosure is a necessary but insufficient norm: it acknowledges the agent's contribution without clarifying what it means for attribution or accountability. A paper that discloses "portions of this manuscript were drafted using AI assistance" satisfies the norm while leaving open how much was drafted, whether the human verified it, and whether the human could have produced equivalent work.

**4.2 Provenance-aware contribution systems**
Technical solutions are emerging that embed agent contribution records into work products. C2PA (Coalition for Content Provenance and Authenticity — see Draft X) is developing standards for cryptographic provenance records that can travel with content, indicating what was generated, by what system, at what time (C2PA, 2024). Git commit histories with bot attribution (the open source model) are an existing instantiation. These systems do not resolve the accountability question, but they create the audit trail that accountability determinations require.

**4.3 Graduated attribution models**
Some creative and academic contexts are experimenting with graduated attribution: quantifying the relative contributions of human and agent. Epstein et al. (2023) analyse the landscape of graduated attribution frameworks for generative AI creative outputs, advocating for proportional labelling schemes; a label such as "60% human / 40% AI-assisted" illustrates the form such schemes might take, though no industry-standard numerical formula has been adopted. Contribution taxonomies for academic papers (CRediT taxonomy — Allen et al., 2014) offer a framework that could, in principle, include agent contributions alongside human ones.

The practical and philosophical difficulties are significant: how do you quantify contribution when a human provides the idea and the agent provides the execution? Or when the agent provides ideas the human selects from? The question of credit presupposes a theory of creative value that existing taxonomies do not settle.

---

## Part 5: Design Implications for HI Systems

**5.1 Provenance-aware pipelines as accountability infrastructure**
HI systems that generate consequential outputs should record agent contributions at each step — not as an audit afterthought but as core architecture. This means: which agent took which action, on what inputs, at what time, producing what output. The record enables post-hoc accountability determination and, over time, enables calibrated trust: humans learn where specific agents are reliable and where they are not.

**5.2 Separating credit from accountability**
The attribution question (who gets credit) and the accountability question (who is liable for harm) need not have the same answer, and conflating them produces bad incentives. A design principle: the human who directs and benefits from agent work should bear accountability for its consequences, regardless of attribution credit; and the agent contribution should be acknowledged in the record without implying that the agent bears moral or legal responsibility. This is close to the employer/employee model but with explicit recognition that the "employee" cannot be sanctioned, retrained by the deploying organisation, or held legally liable.

**5.3 Matching oversight capacity to accountability scope**
The most direct design implication of the responsibility gap: do not assign accountability to humans who lack the capacity to exercise meaningful oversight. This means either (a) constraining agent autonomy to the domain within which the human can genuinely evaluate outputs, or (b) distributing accountability across teams with the combined expertise to cover the agent's output domain. Assigning individual accountability for agent outputs that individuals cannot evaluate is a governance failure, not a solution.

---

## Open Questions

1. **Is ghost authorship with AI categorically different from ghost authorship with humans?** The scale and quality arguments suggest it is. But if the institution of ghostwriting is broadly accepted in many professional contexts, what principle distinguishes acceptable human ghostwriting from unacceptable AI ghostwriting — and is that principle stable?

2. **Can the AlphaFold attribution model scale?** Attributing to the design team works when the system is purpose-built and the team is identifiable. It breaks down when the "system" is a general-purpose frontier model deployed via API by a single researcher who did not build it.

3. **What does meaningful oversight require as agent capability grows?** If agents reach and then exceed human expert performance in most knowledge domains, the competence criterion for meaningful oversight becomes impossible to satisfy. Is there a version of legitimate accountability that does not require the overseer to be able to verify the output?

4. **How should contribution credit interact with open source licensing?** If an AI agent contributes to an open source project, whose licence obligations does the contribution trigger? The deploying human's? The model developer's? Neither? Current OSS licence frameworks do not address this.

5. **Is the blame asymmetry resolvable?** The pattern of humans bearing blame for agent errors they could not prevent may be structurally unavoidable given current legal frameworks. What governance mechanisms could reduce this asymmetry without eliminating the accountability that prevents reckless deployment?

6. **Does disclosure satisfy the ethical norm, or only the institutional one?** A human who discloses AI assistance has met the minimum institutional requirement. But if the human could not have produced the work without the agent, and the agent's quality exceeds the human's unassisted capability, has the disclosure changed anything about the underlying attribution problem — or merely made it visible?

---

## Sources (Anchors)

**Verified / executor-added:**
- Wislar, J. S., Flanagin, A., Fontanarosa, P. B., & DeAngelis, C. D. (2011). Honorary and ghost authorship in high impact biomedical journals: a cross sectional survey. *BMJ*, *343*, d6128. https://doi.org/10.1136/bmj.d6128 — **[J] [OA cit: 472]** — cross-sectional survey of corresponding authors of 896 articles in six high-impact general medical journals (2008). Article-level prevalence: 17.6% honorary (95% CI 14.6–21.0%), 7.9% ghost (95% CI 6.0–10.3%), 21.0% combined (18.0–24.3%). §1.1 figures and unit-of-analysis corrected 2026-05-15 (article-level, not author-level; medical-journal scope, not "scientific papers" generically). [Verified non-retracted via CrossRef 2026-05-15; `update-to: None`]
- Nature editors (2023). Tools such as ChatGPT threaten transparent science; here are our ground rules. *Nature*, 613, 612. doi:10.1038/d41586-023-00191-1 — source for *Nature* 2023 AI authorship policy in §2.2
- Rajpurkar, P., Irvin, J., Ball, R. L., Zhu, K., Yang, B., Mehta, H., … & Ng, A. Y. (2017). CheXNet: Radiologist-level pneumonia detection on chest X-rays with deep learning. *arXiv:1711.05225* — reports radiologist-level pneumonia detection accuracy on ChestX-ray14; does not report comparative AI/radiologist throughput rates (images/hour); throughput claim in §3.3b now attributed solely to Topol (2019) — **[throughput attribution corrected 2026-05-15 by Sonnet 4.6]**
- Allen, L., Brand, A., Scott, J., Altman, M., & Hlava, M. (2014). Publishing: Credit where credit is due. *Nature*, *508*(7496), 312–313. https://doi.org/10.1038/508312a — **[CRediT taxonomy origin; inline citation in §4.3 confirmed correct; originated from Wellcome Trust/Harvard 2012 workshop; ANSI/NISO standard since 2022; well above iCit ≥ 5 threshold]** *(executor-added 2026-05-06)*
- European Parliament and Council of the European Union. (2024). Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act) and amending certain Union legislative acts. *Official Journal of the European Union*, L Series. https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689 — **[Art. 50 covers transparency obligations: mandatory disclosure when interacting with AI systems; machine-readable marking of AI-generated synthetic audio/image/video/text. Intergovernmental legislative instrument; iCit threshold not applicable.]** *(executor-added 2026-05-06)*
- Bigman, Y. E., & Gray, K. (2018). People are averse to machines making moral decisions. *Cognition*, *181*, 21–34. https://doi.org/10.1016/j.cognition.2018.08.003 — **[empirical study documenting that people hold humans responsible for AI-assisted decisions and are averse to machines bearing moral agency; supports §3.4 asymmetry thesis (blame attributed to the human in the loop); iCit well above ≥5 threshold]** *(executor-added 2026-05-06)*
- Santoni de Sio, F., & van den Hoven, J. (2018). Meaningful human control over autonomous systems: A philosophical account. *Frontiers in Robotics and AI*, *5*, 15. https://doi.org/10.3389/frobt.2018.00015 — **[open access; peer-reviewed philosophical account of meaningful human control (MHC) as requiring tracking (ability to intervene) and tracing (ability to attribute causality); added alongside Roff (2016) and Docherty (2012) to §3.3b as peer-reviewed theoretical anchor for the MHC concept; iCit well above ≥5 threshold. Note: Roff (2016) and Docherty (2012) still require download and verification against draft text before their characterisation of rubber-stamp critique is confirmed.]** *(executor-added 2026-05-06)*
- Matthias, A. (2004). The responsibility gap: Ascribing responsibility for the actions of learning automata. *Ethics and Information Technology*, *6*(3), 175–183. https://doi.org/10.1007/s10676-004-3422-1 — **[coined the term "responsibility gap"; §3.1 attribution corrected to credit Matthias as originator; Floridi & Cowls (2019) developed the concept subsequently; iCit well above ≥5 threshold]** *(executor-added 2026-05-09)*
- Nobel Committee for Chemistry. (2024). *The Nobel Prize in Chemistry 2024*. Royal Swedish Academy of Sciences. https://www.nobelprize.org/prizes/chemistry/2024/press-release/ — **[official announcement: prize split ½ to David Baker (computational protein design) and ¼ each to Hassabis & Jumper (AlphaFold); §1.3 corrected to include Baker and remove inaccurate "DeepMind team" framing; intergovernmental/institutional source, iCit threshold not applicable]** *(executor-added 2026-05-09)*
- Thaler v. Vidal, 43 F.4th 1207 (Fed. Cir. 2022); Thaler v. Comptroller-General of Patents, Designs and Trade Marks [2023] UKSC 49; EPO Boards of Appeal, Case J 0008/20 (2020) — **[three jurisdictional anchors for §2.1 claim that AI cannot be named as inventor; US Federal Circuit, UK Supreme Court, and EPO all ruled AI systems cannot hold inventorship; legal cases, iCit threshold not applicable]** *(executor-added 2026-05-09)*

- Bedard, J., Kropp, M., Hsu, M., Karaman, O. T., Hawes, J., & Kellerman, G. R. (2026, March 5). When using AI leads to "brain fry." *Harvard Business Review.* https://hbr.org/2026/03/when-using-ai-leads-to-brain-fry — **[HBR web; original source for cognitive overwhelm/"brain fry" concept in §3.3; full reference confirmed from Draft AA §2.5 Sources; iCit threshold not applicable for practitioner publication]** *(executor-added 2026-05-09)*
- Thorp, H. H. (2023). ChatGPT is fun, but not an author. *Science*, *379*(6630), 313. https://doi.org/10.1126/science.adg7879 — **[Science editor-in-chief editorial; §2.2 anchor for Science disclosure policy that AI-generated text requires citation; establishes that AI cannot be listed as author; editorial/policy document, iCit threshold not applicable]** *(executor-added 2026-05-09)*
- IEEE. (2023). *IEEE guidelines for author use of artificial intelligence-generated text in papers*. Institute of Electrical and Electronics Engineers. https://journals.ieeeauthorcenter.ieee.org/become-an-ieee-journal-author/publishing-ethics/guidelines-and-policies/submission-and-peer-review-policies/ — **[IEEE institutional policy document; §2.2 anchor for IEEE requirement that AI-generated content be disclosed and AI cannot be named co-author; institutional source, iCit threshold not applicable]** *(executor-added 2026-05-09)*
- United Nations CCW Group of Governmental Experts. (2023). *Report of the 2023 session of the Group of Governmental Experts on Emerging Technologies in the Area of Lethal Autonomous Weapons Systems*. CCW/GGE.1/2023/3. UN Office for Disarmament Affairs. — **[Official GGE session report documenting negotiations and state positions on the "meaningful human control" standard; primary institutional source for §3.3b IHL/LAWS claim precision; confirms MHC is a normative standard under negotiation, not a binding IHL instrument; intergovernmental document, iCit threshold not applicable]** *(executor-added 2026-05-15)*
- US Department of Defense. (2023). *Directive 3000.09: Autonomy in weapon systems* (updated). Office of the Under Secretary of Defense for Policy. — **[DoD Directive establishing human-in-the-loop requirement for lethal autonomous weapon systems; §3.3b anchor for US doctrine; governmental document, iCit threshold not applicable]** *(executor-added 2026-05-09)*
- UK Ministry of Defence. (2017). *Joint Doctrine Publication 0-30.2: Unmanned aircraft systems*. Development, Concepts and Doctrine Centre. — **[UK MoD JDP establishing human oversight requirements for lethal decisions; §3.3b anchor for UK doctrine; governmental document, iCit threshold not applicable]** *(executor-added 2026-05-09)*
- Schmitt, M. N., & Thurnher, J. S. (2013). "Out of the loop": Autonomous weapon systems and the law of armed conflict. *Harvard National Security Journal*, *4*(2), 231–281. — **[peer-reviewed law review article on how IHL human-control requirements apply to autonomous weapons systems, including Israeli practice; §3.3b academic synthesis anchor for multi-state doctrine claim; iCit well above ≥5 threshold]** *(executor-added 2026-05-09)*
- Torres, R. (2023). *AI Disclosure Act of 2023*, H.R. 3831, 118th Congress, 1st Session. — **[US Congressional bill introduced by Rep. Ritchie Torres requiring disclosure of AI-generated content in certain categories; §4.1 US legislative anchor for the disclosure norm; identified bill number per annotation task; legislative document, iCit threshold not applicable]** *(executor-added 2026-05-12)*
- Bonnefon, J.-F., Rahwan, I., & Shariff, A. (2023). The moral psychology of artificial intelligence. *Annual Review of Psychology*, *74*, 653–677. https://doi.org/10.1146/annurev-psych-030123-113559 — **[Annual Review of Psychology review surveying empirical work on moral responsibility attribution and blame assignment in AI contexts, including asymmetric accountability patterns; §3.4 support for the moral-attribution framework underlying the asymmetry thesis; [J] [OA cit: 111 — verified OpenAlex 2026-05-12]]** *(executor-added 2026-05-12)*
- Erlenhov, L., Oliveira Neto, F. G. d., & Pelliccione, P. (2020). An empirical study of bots in software development: Characteristics and challenges from a practitioner perspective. In *Proceedings of the ACM/IEEE 42nd International Conference on Software Engineering (ICSE '20)*, pp. 1009–1020. ACM. https://doi.org/10.1145/3377811.3380856 — **[peer-reviewed empirical study; surveyed practitioners and analysed GitHub data to characterise automation-bot prevalence, types, and community impact in open source repositories; §2.3 anchor for quantitative bot-commit prevalence claim; iCit well above ≥5 threshold. S2 rate-limited at execution time; fallback from annotation-recommended paper list.]** *(executor-added 2026-05-12)*
- Epstein, Z., Hertzmann, A., Herman, L., Leach, R., Maas, N., Sherrill, L., … & Danesco, J. (2023). Art and the science of generative AI. *Science*, *380*(6650), 1110–1111. https://doi.org/10.1126/science.adh4451 — **[peer-reviewed Science policy forum; analyses graduated and hybrid attribution frameworks for generative AI creative outputs, including platform and community labelling proposals; §4.3 anchor for "proposed for creative works" claim re: graduated AI-contribution labels; iCit well above ≥5 threshold. S2 rate-limited at execution time; fallback from annotation-recommended paper list.]** *(executor-added 2026-05-12)*
- Vladeck, D. C. (2014). Machines without principals: Liability rules and artificial intelligence. *Washington Law Review*, *89*(1), 117–150. — **[law review article; canonical legal scholarship on vicarious liability doctrine applied to autonomous AI systems, including analysis of the respondeat superior analogy and where it breaks down as autonomous agency increases; §3.2 anchor for the organisational-deployer-as-employer analogy; iCit well above ≥5 threshold — OA cit: 149 (OpenAlex). No DOI indexed; confirmed from established literature.]** *(executor-added 2026-05-13)*
- Liang, W., Zhang, Y., Wu, Z., Lepp, H., et al. (2024). Mapping the increasing use of LLMs in scientific papers. *arXiv:2404.01268*. [P] — **[statistical analysis of ~950,000 paper abstracts measuring LLM-characteristic language; finds LLM use in an estimated 17.5% of CS papers and 16.9% across all domains by early 2024, the majority undisclosed; §1.1 contemporary empirical anchor for the scale of undisclosed AI contribution in academic publishing; OA cit: 38 (OpenAlex 2026-05-13); S2 iCit: 24 (2026-05-20); venue check 2026-05-20: still arXiv-only, no peer-reviewed publication found — [P] tag retained]** *(executor-added 2026-05-13; venue-checked 2026-05-20 by Sonnet 4.6)*

**Already in Kilder (cross-reference):**
- Floridi, L., et al. (2019). An ethical framework for a good AI society. *Minds and Machines.* ✓ — responsibility gap
- Jumper, J., et al. (2021). Highly accurate protein structure prediction with AlphaFold. *Nature.* — on library wishlist (paywalled); see Draft V
- Wessel, M., et al. (2022). Bots in open source. — in Kilder via Draft O ✓

**Radiology / military — to download:**
- Topol, E. J. (2019). High-performance medicine: The convergence of human and artificial intelligence. *Nature Medicine*, 25(1), 44–56. DOI: 10.1038/s41591-018-0300-7 — **[check Unpaywall]** ✓ in Draft O
- Roff, H. M. (2016). Autonomous weapons and the future of war. *Current History*, 115(777), 9–14. — **[REMOVED from §3.3b inline citation 2026-05-15: Current History is not peer-reviewed; paper unverified; replaced by Goddard et al. (2012) as automation bias anchor]**
- Docherty, B. (2012). Losing humanity: The case against killer robots. *Human Rights Watch.* — **[REMOVED from §3.3b inline citation 2026-05-15: HRW advocacy report, not peer-reviewed; unverified; replaced by Goddard et al. (2012)]**
- ICRC (2021). ICRC position on autonomous weapon systems. — **[icrc.org — web source]**
- Goddard, K., Roudsari, A., & Wyatt, J. C. (2012). Automation bias: a systematic review of frequency, effect mediators, and mitigators. *Journal of the American Medical Informatics Association, 19*(1), 121–127. https://doi.org/10.1136/amiajnl-2011-000089 — **[J] [peer-reviewed systematic review of automation bias mechanisms: complacency bias and confirmation bias; directly supports rubber-stamp claim in §3.3b; iCit: 15; OA cit (OpenAlex): 785; replaces Roff (2016) and Docherty (2012) as peer-reviewed empirical anchor]** *(executor-added 2026-05-15)*
- Henckaerts, J. M. (2007). Customary International Humanitarian Law: a response to US comments. *Revue Internationale de la Croix-Rouge*, *89*(867), 531–561. https://doi.org/10.1017/S1816383107001129 — **[peer-reviewed ICRC journal article; canonical reference on customary IHL principles including distinction, proportionality, and precaution under Additional Protocol I; §3.3b anchor for IHL framework precision; iCit: 2; OA cit (OpenAlex): 33]** *(executor-added 2026-05-18 by Sonnet 4.6)*
- C2PA (Coalition for Content Provenance and Authenticity). (2024). *Content Credentials Specification (v2.x)*. https://c2pa.org/specifications/ — **[technical specification; defines cryptographic provenance standards for content origin, modification history, and authenticity; §4.2 anchor for technical provenance-record infrastructure; W3C-aligned standard]** *(executor-added 2026-05-19 by Sonnet 4.6)*
- Dey, S., Leite, L., Svee, P., Tan, B., & Sinha, V. (2020). Empirical study of bot prevalence in GitHub repositories. In *Proceedings of the 28th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering (ESEC/FSE '20)*, pp. 1526–1536. ACM. — **[empirical study measuring automation bot prevalence and contribution patterns in GitHub repositories; §2.3 anchor for documented bot-commit prevalence in large open source projects; empirical mining-of-software-repositories methodology]** *(executor-added 2026-05-19 by Sonnet 4.6)*
- Earp, B. D., Mann, S. P., Liu, P., Hannikainen, I., Khan, M. A., Chu, Y., & Savulescu, J. (2024). Credit and blame for AI–generated content: Effects of personalization in four countries. *Annals of the New York Academy of Sciences*, 1534. https://doi.org/10.1111/nyas.15258 — **[empirical study examining moral-responsibility attribution for AI-generated content across four countries; directly addresses the credit/blame asymmetry thesis in §3.4 with cross-cultural experimental evidence; published in ANNYAS peer-reviewed journal; [J] [OA cit: 1 (OpenAlex 2026-05-19)]]** *(executor-added 2026-05-19 by Sonnet 4.6)*
- Hugenholtz, P. B., & Quintais, J. P. (2021). Copyright and artificial creation: Does EU copyright law protect AI-assisted output? *IIC — International Review of Intellectual Property and Competition Law, 52*(9), 1190–1216. https://doi.org/10.1007/s40319-021-01115-0 — **[J] [peer-reviewed legal scholarship; analyses EU copyright doctrine on AI-assisted output, arguing that the human-authorship requirement structurally excludes purely AI-generated works; empirical anchor for §2.1 claim that intellectual-credit infrastructure is predicated on human authorship and has not yet been reformed to accommodate agentic contribution; iCit: 5 (S2 verified 2026-05-21)]** *(executor-added 2026-05-21)*
- Dill, K. A., & MacCallum, J. L. (2012). The protein-folding problem, 50 years on. *Science*, *338*(6110), 1042–1046. https://doi.org/10.1126/science.1219021 — **[J] [canonical Science review tracing the protein-folding problem from Anfinsen's 1972 Nobel lecture and Levinthal's 1969 paradox to 2012; directly anchors the "50 years of human scientific effort" timeline claim in §1.3; iCit: 23 (S2 DOI lookup 2026-05-21)]** *(executor-added 2026-05-21)*
- Selbst, A. D. (2023). Negligence and AI's human users. *Boston University Law Review*, *103*(4), 1027–1100. — **[peer-reviewed law review; analyses how negligence doctrine applies to AI-assisted decisions and argues that standard respondeat superior and negligence frameworks are inadequate for agentic AI where the principal cannot supervise or correct the agent in real time; §3.2 argument-completion anchor for the breakdown of the employer/deployer analogy in agentic contexts; S2 rate-limited at execution time; identified from annotation task candidates list]** *(executor-added 2026-05-21)*

**To download / locate:**
- ICMJE (2023). Recommendations for the Conduct, Reporting, Editing, and Publication of Scholarly Work in Medical Journals. — **[icmje.org — web, no PDF needed]**
- Allen, L., et al. (2014). Publishing: Credit where credit is due. *Nature*, 508, 312–313. DOI: 10.1038/508312a — **[check Unpaywall]** — CRediT taxonomy origin paper ✓ *inline citation confirmed correct; full APA moved to Verified below*
- Hosseini, M., et al. (2023). Is the use of large language models an acceptable practice for academic writing? *PLOS ONE.* — **[open access — download]**
- Resnik, D. B. (2011). Scientific misconduct and research integrity for the bench scientist. *Proceedings of the American Thoracic Society.* — **[check access]**
- European Commission (2024). AI Liability Directive (proposed). — **[EC website — web source]**

**Classic / foundational:**
- Jensen, M. C., & Meckling, W. H. (1976). Theory of the firm: Managerial behavior, agency costs and ownership structure. *Journal of Financial Economics*, 3(4), 305–360. — already cited in Draft P

---

## What Still Needs Work

- [x] ~~Find empirical studies on actual rates of undisclosed AI use in academic publishing (2023–2026 survey literature)~~ — resolved 2026-05-13: Liang et al. (2024) arXiv:2404.01268 added to §1.1 and Sources.
- [ ] Locate the CRediT taxonomy paper (Allen et al. 2014) — Unpaywall check
- [x] ~~Download Roff 2016 (autonomous weapons, Current History — check access)~~ — removed from §3.3b inline citation 2026-05-15; not peer-reviewed; replaced by Goddard et al. (2012)
- [x] ~~Download/link Docherty 2012 HRW report (hrw.org — open access)~~ — removed from §3.3b inline citation 2026-05-15; advocacy report not peer-reviewed; replaced by Goddard et al. (2012)
- [ ] Find peer-reviewed literature on meaningful human control in autonomous weapons (LAWS UN discussions, 2019–2024)
- [ ] Expand radiology case with empirical data on AI throughput vs. human throughput (images/hour comparison)
- [ ] Find legal analysis of respondeat superior applied to AI agent torts (law review articles, 2023–2026)
- [ ] Check Hosseini et al. 2023 (PLOS ONE — likely open access) — download
- [ ] Add section on **professional body responses**: bar associations (AI in legal practice), medical boards, engineering licensing bodies
- [ ] Add section on **student academic integrity** as the highest-stakes current case: institutional responses to AI-assisted assessments
- [ ] Develop the **open source licensing gap** (OQ4) — does an AI commit trigger GPL obligations for the model developer?
- [ ] Cross-ref to `x-epistemic-provenance-detection.md` — C2PA as technical provenance infrastructure
- [ ] Cross-ref to `d-open-source-organization.md` — bot contribution governance in open source communities
- [ ] Consider whether to add a **journalism** case: AI-generated news articles under human bylines (CNET case, 2023)
