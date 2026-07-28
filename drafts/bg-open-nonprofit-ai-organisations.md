# Draft BG — Open and Non-Profit AI: Why Organisations Choose Openness and Why They Struggle to Keep It

**Version:** v0.1 — 2026-05-17  
**Status:** Concept draft — arguments and cases sketched; sources preliminary  
**Related drafts:** K (openness layers and taxonomy), D (open source organisation history), F (commons extraction and inequality), N (AI/ML ecosystem), AW (commercial ML datasets), P (governance and compliance), AP (legal personality and agent liability)

---

## Overview and Chapter Position

Most public discourse about open AI treats openness as a technical or legal property — is the model weights released, is the training data documented, is the code available? Draft K provides the taxonomy: the three layers of openness (data, weights, training infrastructure) that "open source AI" conflates. This draft addresses a prior question: *why do AI organisations adopt open or non-profit structures in the first place*, and *what are the structural forces that make those commitments difficult to sustain?*

The question matters because the current landscape of AI development is dominated by organisations that began with open or non-profit mandates and have subsequently drifted, converted, or abandoned them — or are visibly under pressure to do so. Understanding why they started open, and why that turned out to be hard, is prerequisite to designing governance frameworks that can preserve the public interest in AI development.

The chapter examines five distinct rationales for openness or non-profit structure, traces each rationale through three or four institutional cases, and then analyses the four structural pressures — compute economics, talent competition, liability exposure, and investor expectations — that create systematic pressure toward closure and commercialisation. The chapter concludes with a typology of the failure modes through which open/non-profit AI organisations lose their founding character.

---

## §1 — The Rationale Landscape: Why Organisations Choose Openness

Openness and non-profit structure in AI are not a single decision but a cluster of distinct choices, each driven by a different rationale. The rationales are not mutually exclusive; most organisations adopt openness for a combination of reasons. Understanding which rationale is primary matters for predicting which pressures will be most destabilising.

### 1.1 The safety rationale: openness as risk distribution

The founding argument of OpenAI (2015) was that artificial general intelligence posed existential risk, and that this risk was best managed by ensuring that the technology was not concentrated in the hands of a single commercial actor. The non-profit structure and the commitment to sharing research openly were institutional expressions of this argument: if AGI is coming regardless, it is better to have many actors working on it than a single powerful actor with a monopoly on capability and no accountability to anyone but its shareholders.

This rationale — safety through distributed development — has a counterargument that emerged within a few years and that OpenAI itself would later partially adopt: that *releasing powerful capabilities broadly* is itself a safety risk, because it enables malicious actors who would not otherwise have access. The tension between "safety through openness" and "safety through restriction" is the central instability in the safety rationale for open AI.

The Allen Institute for AI (AI2), founded by Paul Allen in 2014, has maintained a more consistent version of the safety-through-openness position: its OLMo (Open Language Model) series, released from 2024 onward, provides fully open training data, model weights, training code, and evaluation framework — argued on the grounds that safety research requires access to the full model stack, not merely the deployed interface. AI2's non-profit status and foundation funding have so far insulated it from the commercial pressures that destabilised OpenAI's equivalent commitment.

### 1.2 The public goods rationale: AI trained on public data should be public

Language models are trained on text produced by millions of people who were never compensated and who had no expectation that their writing would train commercial products. The public goods rationale holds that AI systems built on this effectively public resource have a corresponding obligation to make their outputs available as a public good — or, more weakly, to not lock up the resulting capability behind commercial access controls.

This rationale animated the BigScience project (2021–2022), in which over a thousand researchers across academic institutions in more than sixty countries collaborated to train BLOOM — a multilingual large language model released with fully open weights and a responsible AI licence. The argument was explicit: the model was trained on CommonCrawl and academic corpora that the public had collectively produced; the resulting model should be collectively available. BigScience was organised as a research workshop under the auspices of Hugging Face, with no commercial motivation in the core project.

The public goods rationale is philosophically compelling but practically unstable in the frontier AI context because frontier capability requires compute that no public-goods funding model has yet been able to sustain. BLOOM (176B parameters) was the largest openly trained model at its release; within months, commercial models trained on larger budgets had surpassed it. The public goods rationale does not generate the resources required to keep pace with the commercial frontier.

### 1.3 The mission alignment rationale: values-based openness

Some organisations adopt open or non-profit structures because their founders genuinely believe that open development is the right thing to do — that AI should be developed transparently, that its failures should be visible and correctable, and that the concentration of AI capability in private hands is bad for democracy and human autonomy regardless of safety implications.

EleutherAI, founded in 2020 as a volunteer collective in a Discord server, is the purest example. It has no investors, no commercial products, and no professional management. It exists to produce open AI research — primarily training data (The Pile), open language models (GPT-Neo, GPT-J, GPT-NeoX), and evaluation frameworks (lm-evaluation-harness) — and to make that research available without restriction. Its non-commercial structure is not a strategic choice but an expression of its founders' values: openness as an end in itself, not a means to safety or competitive positioning.

The mission alignment rationale is the most resilient to commercial pressure — an organisation with no investors and no commercial products has no channel through which commercial pressure can enter. Its vulnerability is different: resource scarcity. EleutherAI's ability to train frontier models is constrained by donated compute, and the gap between what it can train and what frontier commercial labs produce has widened steadily.

### 1.4 The competitive strategy rationale: openness as commoditisation

Meta's open releases of the LLaMA series (2023–2025) represent a fourth rationale that is neither safety nor public goods nor values: competitive strategic openness. Meta is not a non-profit and does not pretend to be. Its decision to release LLaMA weights openly was driven by a calculation that commoditising the model layer — making powerful open models freely available — reduces the competitive advantage of OpenAI and Google in the model tier while leaving Meta's competitive advantage (social data, advertising infrastructure, distribution) intact.

This is the "commoditise the complement" strategy well-known in platform economics: give away the complement to your core product to increase demand for the core product. For Meta, open models commoditise the AI model layer, making it harder for model-tier competitors to charge premium prices, while Meta's social platform data (Draft AV) remains a proprietary advantage in the training data tier.

The competitive strategy rationale produces genuine openness — LLaMA weights are genuinely usable by researchers and developers — but for reasons that have nothing to do with public benefit. It is also strategically fragile: if Meta's calculation changes (e.g., if open models begin to threaten its social platform dominance rather than commoditising a competitor), the openness commitment would be reconsidered.

### 1.5 The talent recruitment rationale: openness to attract researchers

Top AI researchers want to publish their work, present at conferences, and build on the research community's shared knowledge base. Closed commercial development that restricts publication is unattractive to researchers who measure their careers by academic output. Organisations that commit to open research publication — even if they are commercial — can attract talent that would not otherwise join them.

This rationale drove Google DeepMind's publication record (AlphaFold, AlphaGo, Gemini technical reports) and Anthropic's Constitutional AI papers. It is not openness in the model weights sense — the trained models remain proprietary — but openness in the research publication sense: the methods are published even if the products are not. This partial openness is sustainable within a commercial structure because it costs relatively little (papers are cheap; model weights are expensive to replicate) while providing substantial talent recruitment benefits.

---

## §2 — The Structural Pressures Toward Closure

### 2.1 Compute economics: the infrastructure problem

The most fundamental pressure on open and non-profit AI is the cost of compute. Training a frontier language model requires infrastructure investment in the range of tens to hundreds of millions of dollars for a single training run. This is not a cost that can be sustained by volunteer contributions, foundation grants, or academic computing allocations. It requires either commercial revenue or venture capital investment — and either route imports the expectations and governance structures of commercial development.

OpenAI's trajectory illustrates the mechanism. Founded as a non-profit in 2015 with a $1B commitment from its founders and a mission to develop AI for the benefit of humanity, it created a "capped-profit" subsidiary in 2019 after computing that its research agenda required more capital than its non-profit structure could raise. The capped-profit structure — in which investors could receive returns up to 100x their investment before excess profit would flow to the non-profit — was itself an institutional innovation designed to attract commercial capital while nominally preserving the non-profit mission. By 2023, the structure was under strain: OpenAI's commercial success with ChatGPT had made it a highly valuable commercial entity, and the governance fiction of a non-profit controlling a $90B+ commercial enterprise became increasingly difficult to sustain. In 2025, OpenAI moved to convert to a fully for-profit structure, with the non-profit entity retaining only a minority stake.

The compute problem does not have an obvious solution within the current infrastructure economics. National computing initiatives (the EU's EuroHPC, the UK's AIRR programme, the US NSF National AI Research Resource) provide partial access to public compute, but at scales that lag commercial frontier investment by one to two orders of magnitude.

### 2.2 Talent competition: the salary problem

AI researchers with the skills to train frontier models command salaries in the range of $500,000 to several million dollars annually at commercial frontier labs. Non-profit and academic organisations cannot match these salaries. The talent drain from academia and non-profits to commercial labs has been consistent and severe since approximately 2017. AI2 and EleutherAI have retained researchers through mission alignment and publication freedom, but both acknowledge that compensation constraints limit their ability to recruit and retain the most sought-after individuals.

The talent problem interacts with the compute problem: without frontier compute, organisations cannot work on the problems that attract frontier researchers, which reduces their ability to recruit frontier talent, which reduces their ability to compete for frontier compute grants. The Matthew effect (to him who has shall be given) operates with particular force in the concentrated field of frontier AI development.

### 2.3 Liability exposure: the safety problem

As AI systems become more capable and more widely deployed, the legal and reputational liability associated with open releases grows. An organisation that releases model weights openly cannot control downstream use — the model may be fine-tuned to remove safety guardrails, used to generate harmful content, or deployed in high-risk contexts without appropriate safeguards. The open release decision that was relatively low-stakes for a small research model (GPT-2 at 1.5B parameters) is much higher-stakes for a frontier-capable model.

Mistral AI, the French startup that built its initial reputation on openly released models, has progressively restricted its most capable releases: early Mistral models were fully open; later Mistral Large and subsequent frontier models are available only through commercial API, with weights not publicly available. The transition tracks the capability and therefore the liability profile of the models — as the models became more capable, the liability calculus shifted.

The liability pressure operates asymmetrically: the downside risk of a harmful open release (reputational damage, regulatory action, litigation) is concentrated on the releasing organisation, while the upside (research community access, ecosystem development) is distributed. As AI systems approach capabilities that regulators regard as high-risk under frameworks like the EU AI Act, the liability asymmetry will intensify.

### 2.4 Investor expectations: the governance problem

Venture capital and institutional investment in AI comes with governance expectations that are structurally incompatible with open or non-profit models. Investors expect a board representation, information rights, and eventually a liquidity event (IPO or acquisition). These expectations create pressure to:

- Restrict open releases that reduce the defensible IP value of the company
- Prioritise revenue-generating applications over research publication
- Restructure governance away from mission-driven boards toward investor-controlled boards
- Pursue commercial partnerships that may conflict with open or public-interest commitments

The OpenAI board crisis of November 2023 — in which the non-profit board fired CEO Sam Altman, Microsoft (a major investor) threatened to hire the entire OpenAI staff, and Altman was reinstated within days — is the most visible example of how investor and commercial interests can override a non-profit governance structure that was formally in control. The non-profit board nominally had the authority to fire the CEO; it did not have the power to sustain that decision against commercial pressure.

Hugging Face has navigated this tension more successfully: it has raised over $235 million at a $4.5 billion valuation while maintaining open model releases and a research publication culture. But Hugging Face's commercial model (enterprise subscriptions, API access to hosted models) creates structural pressure to make the most valuable capabilities available only to paying customers — a pressure that is visible in the increasing complexity of its open/commercial product line.

---

## §3 — Case Studies in Institutional Drift

### 3.1 OpenAI: the canonical mission drift

OpenAI's trajectory from non-profit AI safety organisation (2015) to capped-profit hybrid (2019) to de facto commercial entity (2023) to converting for-profit (2025) is the most studied case of mission drift in AI governance. The sequence has a clear logic: each transition was driven by a genuine constraint (inadequate compute, inadequate talent, inadequate governance capacity) and each transition was accompanied by arguments that the new structure was compatible with the original mission. The cumulative effect is an organisation that is structurally indistinguishable from a commercial frontier AI lab, with a nominal non-profit rump that lacks meaningful governance power.

The OpenAI case reveals a specific failure mode: *mission drift through sequential small steps*, each of which was defensible in isolation, none of which was individually decisive, but which collectively produced a complete structural transformation. No single decision was the "moment" at which OpenAI ceased to be a non-profit; the transformation was accomplished through a series of transitions that could each be framed as preserving the mission.

### 3.2 Mozilla.ai: the late entrant non-profit

The Mozilla Foundation — the non-profit that develops Firefox and advocates for an open internet — launched Mozilla.ai in March 2023 as an independent AI initiative with $30M in seed funding. Its stated mission: to develop trustworthy, independent, and openly governed AI that serves the public interest. The timing was explicit: Mozilla.ai was founded in direct response to the rapid commercialisation of AI following ChatGPT's launch, positioned as a public-interest counterweight to OpenAI and Google.

Mozilla.ai faces the structural challenges of the late entrant: it enters a field where the compute-cost barrier is already very high, where frontier talent has largely been absorbed by commercial labs, and where the public goods niche is already partially occupied by AI2, EleutherAI, and BigScience alumni. Its $30M founding grant is substantial for a non-profit but negligible relative to the compute budget of a frontier training run. Its trajectory over 2023–2026 — producing research tools, alignment frameworks, and policy advocacy rather than frontier model releases — illustrates how non-profits in AI are structurally channelled toward the governance and tooling tier rather than the capability tier.

### 3.3 AI2 and OLMo: sustained non-profit through institutional insulation

The Allen Institute for AI represents a more successful model of sustained non-profit AI research. Founded in 2014 with an endowment from the late Paul Allen, it has foundation funding that does not require revenue generation, a research mission that attracts top researchers through publication freedom, and an explicit commitment to full-stack openness in its OLMo releases (training data, model weights, training code, evaluation — all openly documented and released).

AI2's sustainability rests on institutional insulation from the pressures that destabilised OpenAI: it has no investors, no commercial products that generate structural pressure to restrict open releases, and endowment funding that does not depend on market conditions. Its vulnerability is the compute ceiling: OLMo models are trained at scales that are competitive with mid-tier commercial models but not with frontier commercial releases. AI2's openness is credible because it has never been tested against the pressure of having a highly commercially valuable model to restrict.

### 3.4 EleutherAI: volunteer resilience and resource ceiling

EleutherAI has maintained its founding open/non-profit character more completely than any comparable organisation — but at the cost of an increasing gap between its resources and frontier capability. Its contributions — The Pile training dataset, GPT-Neo and GPT-J models, the lm-evaluation-harness evaluation framework, and substantial safety research — have been genuinely significant for the open AI research community. But its volunteer-funded model cannot sustain the compute required for frontier training, and its most prominent researchers have over time moved to commercial organisations (Anthropic, Eleuther's own research nonprofit spin-off) that can offer stable compensation.

EleutherAI's model demonstrates a ceiling property: volunteer-funded open AI can produce research tools, training datasets, and mid-scale models that are genuinely useful for the research community, but it cannot sustain frontier capability development. The ceiling is not a failure of commitment but a structural constraint of the funding model.

---

## §4 — Typology of Failure Modes

Drawing on the case studies, four distinct failure modes can be identified through which open/non-profit AI organisations lose their founding character:

**Mission drift through sequential restructuring** (OpenAI): Each governance or structural transition is framed as preserving the mission, but the cumulative effect is complete structural transformation. The failure mode is enabled by the absence of an external arbiter of mission fidelity — the organisation itself interprets whether each transition is mission-compatible.

**Resource ceiling and capability gap** (EleutherAI, BigScience): The organisation maintains its founding character but loses the ability to produce frontier research because resource constraints do not scale with the compute-cost frontier. The mission remains intact; the capacity to achieve it does not.

**Liability-driven gradual restriction** (Mistral): As model capability grows, the liability calculus shifts against open release. The organisation progressively restricts its most capable releases while maintaining open releases at lower capability tiers. The failure mode is the progressive hollowing-out of the openness commitment — openness remains for models that are safe to release, while the models where openness matters most are restricted.

**Commercial pressure on governance** (Hugging Face — not yet a failure but under pressure): The organisation maintains open releases but the commercial structure creates structural incentives to differentiate premium closed features from open features. The failure mode has not yet fully manifested but the structural conditions for it are present.

---

## Open Questions

1. **Is there a viable institutional form that can sustain frontier AI development as a public good?** The evidence from existing cases suggests that non-profit or open structures face a compute ceiling that prevents frontier development. Is there an institutional form — a national AI institute, a multi-stakeholder foundation with public funding, an intergovernmental research organisation — that could sustain frontier development without the commercial pressures that erode open commitments?

2. **What is the correct unit of openness commitment — the organisation or the specific release?** OpenAI made organisational-level commitments that proved impossible to sustain. AI2 makes release-level commitments (OLMo is fully open regardless of what future releases look like). Is the release-level commitment more credible and durable than the organisational-level commitment?

3. **Does the EU AI Act's treatment of open releases create perverse incentives?** The EU AI Act provides partial exemptions for open-weight models from the requirements applied to commercial systems. This creates an incentive for commercial actors to release weights as "open" while maintaining commercial control through other mechanisms — exactly the Meta/LLaMA pattern. Does this regulatory structure undermine genuine open releases by conflating them with strategic commercial openness?

4. **Can the "capped-profit" model be redesigned to sustain the non-profit mission?** OpenAI's capped-profit model failed to sustain mission fidelity. Are there alternative hybrid models — community-ownership structures, worker cooperatives, public-benefit corporations with mandatory open-release covenants — that could sustain both commercial viability and genuine public-interest governance?

5. **What happens to the research community if frontier AI becomes entirely closed?** The research community currently benefits from commercial organisations' publication of methods, if not models. If commercial pressure leads to the restriction of research publication (not just model weights), the research ecosystem loses its main channel of knowledge production. What are the consequences for the safety research capacity that depends on understanding frontier models?

---

## Key Sources (Preliminary)

- OpenAI. (2015). *Introducing OpenAI* [blog post]. OpenAI.com. [Primary source — founding mission statement; non-profit rationale]
- OpenAI. (2019). *OpenAI LP* [blog post]. OpenAI.com. [Primary source — capped-profit conversion announcement and rationale]
- Brockman, G., & Sutskever, I. (2023). *OpenAI's response to the board's decision* [blog post]. [Primary source — November 2023 governance crisis]
- Liang, P., et al. (2022). *Holistic evaluation of language models* (HELM). *Proceedings of NeurIPS 2022 Datasets and Benchmarks Track*. arXiv:2211.09110. [C] [BigScience/BLOOM evaluation context; HELM framework for open model benchmarking]
- Workshop, B. (2022). BLOOM: A 176B-parameter open-access multilingual language model. arXiv:2211.05100. [P] [Primary anchor for §1.2 BigScience/public goods rationale; 1000+ author collaborative open model]
- Groeneveld, D., et al. (2024). OLMo: Accelerating the science of language models. arXiv:2402.00838. [P] [AI2 OLMo fully open release — anchor for §3.3]
- Touvron, H., et al. (2023). LLaMA: Open and efficient foundation language models. arXiv:2302.13971. [P] [Meta LLaMA first release — anchor for §1.4 competitive strategy rationale; verify iCit]
- Zuboff, S. (2019). *The age of surveillance capitalism: The fight for a human future at the new frontier of power*. PublicAffairs. [Book] [Theoretical anchor for behavioral surplus framing in §1.2; cross-reference Draft AV]
- Bommasani, R., et al. (2023). *Foundation model transparency index*. Stanford CRFM. [R] [Documents training data opacity as the most consistently opaque dimension across commercial frontier models; anchors §2.1 compute economics section]
- Metz, C. (2024). *The inside story of Microsoft's partnership with OpenAI*. *The New York Times*. [N] [Journalism anchor for §3.1 OpenAI mission drift — investor pressure mechanism; author name to verify]
- Oreskes, N., & Conway, E. M. (2010). *Merchants of doubt*. Bloomsbury. [cross-reference: Draft BF §8.3]

---

## What This Draft Needs

- **§1:** All five rationale types need at least one peer-reviewed anchor beyond primary sources and journalism. Search: "open source AI strategic motivation", "non-profit AI governance", "public goods AI development".
- **§2.1:** Compute cost figures for frontier training runs need a citable source (Epoch AI or similar compute-tracking research).
- **§2.4:** OpenAI board crisis (Nov 2023) is well-documented in journalism; find any academic governance analysis of the event.
- **§3:** OpenAI primary sources (founding blog posts, LP announcement) are citable but not peer-reviewed — this is appropriate for primary source documentation.
- **§3.2:** Mozilla.ai needs its founding announcement and any subsequent reporting on its trajectory.
- **§3.3:** OLMo (Groeneveld et al., 2024) needs iCit verification.
- **§3.4:** EleutherAI's volunteer structure — check if there is any published account of its governance model.
- **Cross-links:** K (openness layers taxonomy — §1 should explicitly reference K's three-layer framework), D (open source history — §1.3 EleutherAI connects to D's volunteer community analysis), F (commons extraction — §1.2 public goods rationale connects to F's extraction argument), AV (behavioral surplus — §1.2 Meta's social data advantage connects to AV's analysis), P (governance/compliance — §4 failure modes connect to P's governance framework analysis).
