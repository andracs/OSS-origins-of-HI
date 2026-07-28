# Draft AF — The Invisible Workforce: Human Labor in AI Training

**Version:** v0.14 (2026-05-19)
**Status:** Citation integrity + STEERING focus-1 cross-link cycle. (1) Scott et al. (2023) source-line repaired: prior entry attributed coauthors "Haimson, O. L., Steigman, M. A., & Dugas, M." (none of whom are on the paper) and cited DOI `10.1145/3544548.3581434` (which resolves to an unrelated CHI 2023 paper about computational machine knitting). Authoritative author list per CrossRef on the correct DOI `10.1145/3544548.3581512`: Scott, C. F., Marcu, G., Anderson, R. E., Newman, M. W., & Schoenebeck, S. OA cit refreshed to 79. (2) Two remaining "S2 rate-limited" placeholders resolved against OpenAlex: Gillespie (2018) book *Custodians of the Internet* OA cit 509 (W2994507840); Fairwork Foundation (2023) confirmed as institutional `[R]` with no CrossRef DOI / no direct OpenAlex record. (3) CrossRef retraction checks (≥1 per cycle satisfied): Scott (2023, correct DOI) `update-to: None`; Steiger (2021) `update-to: None`, CrossRef ref-by refreshed to 149; Henrich, Heine & Norenzayan (2010) `update-to: None`. (4) AF↔W cross-link strengthened in §5.2 with new paragraph naming Henrich et al. (2010) and the structural argument that the alignment-stage demographic narrowing reinforces — rather than corrects — the pretraining-stage WEIRD bias documented in Draft W.
**Next:** Library acquisition of Gray & Suri (2019) and Roberts (2019); locate open-access version of Posada (2022) and Irani & Silberman (2013); cross-link to Draft AD (evil encoded in models) connecting the §5.2 demographic-narrowing argument to AD's bias-encoding taxonomy.

---

## Research Question

AI systems are routinely described as products of data, compute, and algorithmic innovation. But every major AI system deployed today was also shaped by hundreds of thousands — possibly millions — of human workers who labeled images, ranked model outputs, reviewed harmful content, and contributed code or text to the commons that became training corpora. **Who are these workers, what do they do, what are the conditions under which they do it, and what does their existence tell us about what hybrid intelligence actually is?**

---

## Part 1 — The Annotation Economy: Scale, Platforms, and Wages

### 1.1 What data annotation is

Every supervised machine learning system depends on labeled data: images tagged with object categories, text classified by sentiment, audio transcribed into words, bounding boxes drawn around faces. The process of producing these labels at scale is data annotation, and it constitutes one of the largest informal labor markets in the world. Estimates of the total annotation workforce are uncertain — the sector is deliberately opaque — but industry analysts and academic researchers have documented a workforce numbering in the millions globally (Gray & Suri, 2019; Tubaro et al., 2020).

The annotation pipeline typically works as follows. A technology company or AI lab needs labeled training data. It contracts with a data labeling platform — Scale AI, Surge AI, Appen, Lionbridge, iMerit, or through a microwork marketplace like Amazon Mechanical Turk (MTurk) — which in turn recruits and manages a distributed workforce of contractors. Workers receive tasks (Human Intelligence Tasks, or HITs, in MTurk terminology) through a web interface, complete them, submit answers, and receive micropayments. There is no employment relationship: workers are independent contractors, with no benefits, no minimum wage protections in most jurisdictions, and no guaranteed workflow.

### 1.2 The platforms

The annotation labor market is stratified. At the top, companies like Scale AI and Surge AI advertise curated, vetted workforces for high-stakes annotation tasks (e.g., for autonomous vehicle sensor fusion, military contracts, foundation model alignment). These platforms have explicit quality-control pipelines and pay somewhat higher rates. In the middle tier, Appen and Lionbridge employ large distributed workforces — Appen has reported contractor counts in the hundreds of thousands (Appen Limited, 2021) — for general-purpose annotation, translation, and relevance evaluation. At the lower end, MTurk and similar microwork platforms (Clickworker, Microworkers, UHRS/Microsoft) offer near-frictionless access to annotation labor at commodity rates.

Wages vary dramatically. Studies of MTurk workers consistently find median effective hourly earnings well below the US federal minimum wage: Hara et al. (2018) found a median wage of \$2.00 per hour in a large-scale audit of MTurk tasks, with only 4% of workers earning above \$7.25/hour. Workers in the Global South — where a majority of annotation labor is now located — earn rates that are low even by local standards when task complexity is accounted for (Gray & Suri, 2019; Perrigo, 2023).

### 1.3 Geographic distribution

The annotation workforce has followed the logic of global labor arbitrage. MTurk originally drew heavily on US workers, but the platform has progressively shifted toward India, which now accounts for a large plurality of its workforce (Difallah et al., 2018). Scale AI and Surge AI have explicitly recruited in Kenya, Uganda, and the Philippines (Fairwork Foundation, 2023). The TIME magazine investigation (Perrigo, 2023) documented that Kenyan workers contracted via Sama — a subcontractor to OpenAI — earned between \$1.32 and \$2.00 per hour to review and classify toxic content from ChatGPT's training pipeline.

The geographic distribution is not incidental. It reflects a deliberate cost minimization strategy in which annotation labor is sourced from jurisdictions with lower labor costs, weaker collective bargaining rights, and limited awareness of the ultimate use of the work. Workers in Kenya labeling data for a US AI company are several institutional steps removed from any accountability mechanism that company might face.

### 1.4 Scale of the workforce

Precise workforce counts are not publicly available. Platform companies do not disclose contractor numbers systematically. The best available estimates:

- Appen reported approximately 1 million registered contractors globally as of 2021 (Appen Annual Report 2021)
- MTurk is estimated to have 500,000–1,000,000 registered workers at any time, with an active core of approximately 100,000 (Gray & Suri, 2019); an empirical capture-recapture measurement found approximately 250,000 unique workers active over a three-month period, with only ~2,000–5,000 workers active on the platform at any given moment (Difallah et al., 2018)
- The data labeling market overall (inclusive of all platforms) was valued at approximately USD 1.7 billion in 2023, projected to reach USD 17.1 billion by 2030 (Grand View Research, 2023 — industry analyst estimate; no peer-reviewed equivalent exists for this projection. The order-of-magnitude growth trajectory is consistent with platform workforce expansion documented in peer-reviewed and institutional literature, including Gray & Suri, 2019 and ILO, 2021)
- Academic estimates of the total global annotation workforce range from several hundred thousand to low millions, depending on definitional scope; the Fairwork Foundation's annual Cloudwork Ratings assess working conditions and workforce scale across major platforms and document continued growth in the distributed annotation workforce (Fairwork Foundation, 2023)

These figures almost certainly undercount the actual workforce because they exclude: workers who perform annotation as part of formal employment (e.g., regional offices of AI companies in the Philippines); volunteers whose contributions to open datasets are not compensated; and workers on unregistered regional platforms operating outside major anglophone markets.

---

## Part 2 — RLHF and Preference Data Workers

### 2.1 What RLHF is and why it needs human labor

Reinforcement Learning from Human Feedback (RLHF) is the technique that transformed large language models from statistical text predictors into assistants capable of following instructions, maintaining conversation, and avoiding overtly harmful outputs (Ouyang et al., 2022 [iCit: 2204]; Bai et al., 2022 [iCit: 479]). The technique works as follows: a base model generates candidate responses to prompts; human contractors rank those responses from best to worst; a reward model is trained on those rankings; and the language model is fine-tuned via reinforcement learning to produce outputs the reward model scores highly.

RLHF is computationally demanding, but the bottleneck is human judgment. The quality of the ranking data — how well contractors understand the task, how consistently they apply criteria, how their values and training influence their assessments — directly determines the values the resulting model encodes. There is no substitute for human judgment in this process; RLAIF (using AI feedback to replace human feedback) has demonstrated scaling potential — Lee et al. (2023) showed that AI feedback can match or approach human feedback quality on several benchmarks — but it introduces new dependencies on the quality of the AI feedback provider and remains an active research direction with unresolved limitations (Lee et al., 2023; Casper et al., 2023 [iCit: 44 inf. cit.]).

### 2.2 Who does the ranking

RLHF contractors are a more specialized subset of the annotation workforce. They are typically required to have proficiency in the language(s) being evaluated, some ability to assess factual accuracy, and capacity to evaluate subtle qualities of helpfulness, tone, and safety. In practice, this means:

- For English-language models: workers recruited in the US, UK, and India with college-level education
- For multilingual coverage: contractors in a wider range of countries, often through Appen or directly via regional subcontractors
- For safety-critical evaluation (explicit content, self-harm, violent extremism): specialized safety teams, often in the Global South — the case documented most thoroughly by Perrigo (2023)

OpenAI, Anthropic, and other frontier labs have not published systematic information about the size, composition, or working conditions of their RLHF contractor workforces (Bommasani et al., 2023). The Bai et al. (2022) Anthropic paper describes a contractor pool but provides no demographic or wage information. Academic critique of this opacity is growing: Casper et al. (2023) identify the lack of systematic documentation of annotator demographics and working conditions as a fundamental limitation of RLHF methodology.

### 2.3 The Kenyan workers case

The single most documented case of RLHF labor conditions is the TIME investigation by Perrigo (2023). The investigation found that:

- OpenAI contracted with Sama, a Kenyan outsourcing company that markets itself as an "ethical AI" provider
- Workers were assigned to review text including graphic descriptions of violence, sexual abuse of children, and bestiality, drawn from the dark web and other unfiltered sources
- Pay was between \$1.32 and \$2.00 per hour
- Workers reported acute psychological distress; some described the work as "torture"
- Sama terminated the OpenAI contract early, citing its own welfare policies; Sama employees subsequently attempted to organize and were dismissed

The Kenyan case has become emblematic of the structural exploitation in RLHF pipelines, but it is not unique. Similar conditions have been reported in content moderation work in the Philippines (Roberts, 2019) and in Latin American data-annotation pipelines. The Miceli and Posada (2022) ethnographic study of three Venezuelan crowdsourcing platforms and a Business Process Outsourcing (BPO) firm in Argentina — the largest peer-reviewed empirical study of Latin American AI annotation labor to date — documents workers entering platforms during Venezuela's economic collapse to perform image labelling, content evaluation, and dataset cleaning at piece rates that, by the authors' calculation, fall below local subsistence thresholds when task-rejection rates are factored in [J] [OA cit: 95].

### 2.4 The psychological cost of RLHF annotation

RLHF workers reviewing harmful outputs are exposed to material that, in any other professional context, would trigger mandatory psychological support: explicit sexual content involving minors, detailed descriptions of torture, graphic violence. No peer-reviewed study has yet documented the psychological effects of RLHF annotation work specifically — the most direct empirical evidence remains the investigative reporting by Perrigo (2023) documenting acute psychological distress among the Kenyan RLHF contractors described in §2.3 (workers who described the experience as "torture"). Content moderation research — closely parallel in exposure profile — documents PTSD symptoms, anxiety disorders, moral injury, and sleep disturbance in workers performing this function (Spence et al., 2023 [OA cit: 40]). The Dahlgren Lindström et al. (2024) sociotechnical critique of RLHF notes that worker welfare considerations are structurally absent from most published RLHF methodology papers, despite being a direct consequence of the technique.

The Casper et al. (2023) open problems paper enumerates "limited number of AI safety researchers working on these problems" as a bottleneck — but does not note that there are thousands of workers living inside those problems while ranking outputs.

---

## Part 3 — Content Moderation as AI Training Labor

### 3.1 The moderation-training pipeline

Content moderation is the process by which harmful content is identified and removed from online platforms. It is also, increasingly, an AI training pipeline. Moderators who review and classify content — is this hate speech? does this image violate community guidelines? — are producing labeled data. That data is used to train classifiers that automate future moderation decisions. The moderator who reviews 500 posts a day is, simultaneously, a platform trust-and-safety worker and an AI trainer.

This dual function is rarely acknowledged by platforms or in the moderation literature. Roberts (2019), in the foundational sociological study of commercial content moderation, describes moderation as "the shadow of social media" — hidden, poorly paid, psychologically costly work that makes platform products possible. Roberts's analysis predates the widespread use of moderation data as explicit AI training input, but her structural analysis applies directly: the work is invisible by design, because visibility would create accountability.

### 3.2 The scale and geography of moderation labor

Content moderation is, like annotation, a globally distributed labor force concentrated in lower-income countries. Roberts (2019) documents operations in the Philippines as a primary site of platform moderation for anglophone content. Facebook (Meta) has been reported to employ thousands of content moderators in Nairobi, working through Sama and subsequently Accenture — a situation that generated litigation when moderators, led by Daniel Motaung, organised and were dismissed (Fairwork Foundation, 2023; Foxglove Foundation, 2023). TikTok's moderation operations have been documented in Malaysia and elsewhere in Southeast Asia (Chan & Potkin, 2023; Fairwork Foundation, 2023).

The Roberts (2014) dissertation work — later published in article form as Roberts (2016), *Commercial Content Moderation: Digital Laborers' Dirty Work* (peer-reviewed; OA cit: 160), and developed into the 2019 Yale UP book — found that US-based moderation work was also significant, but that the work was systematically obscured: moderators were not described as content reviewers in public communications, operated under strict NDAs, and were structurally isolated from the product teams whose decisions created the content they reviewed. Roberts (2016) is the highest-impact peer-reviewed article anchor for the §3 invisibility analysis; the 2019 book extends the analysis with additional fieldwork in the Philippines.

### 3.3 Psychological trauma and moral injury

The documented psychological consequences of content moderation work include (Steiger et al., 2021; Spence et al., 2023; Scott et al., 2023):

- Post-traumatic stress disorder (PTSD), documented in quantitative surveys and qualitative studies of professional moderators — Steiger et al. (2021) found significant PTSD symptom prevalence in a quantitative survey of content moderators across major platforms [C] [OA cit: 157], while Spence et al. (2023) found PTSD-consistent symptom profiles including intrusive thoughts and hypervigilance in their qualitative sample
- Moral injury — the specific distress arising from performing work that violates one's ethical commitments — common in workers forced to make rapid classification decisions about ambiguous harmful content (Litz et al., 2009)
- Desensitization, which moderators report both as a coping mechanism and as a source of distress ("I used to be horrified by this; now I'm not, and that horrifies me")
- Burnout and high turnover, which platforms manage by cycling workers rapidly rather than investing in worker welfare

Spence et al. (2023) [OA cit: 40] conducted a qualitative study of content moderators' psychological experiences and found widespread reports of intrusive thoughts, hypervigilance, and difficulty separating work exposure from personal life — symptoms consistent with secondary traumatic stress disorder. The Scott et al. (2023) paper "Trauma-Informed Social Media" [OA cit: 79] argues for structural redesign of moderation workflows to reduce exposure, but notes that platform incentives do not support such investment.

### 3.4 The invisibility mechanism

Content moderation labor is invisible by design. Non-disclosure agreements prevent moderators from speaking about their work. Job titles are euphemistic ("content reviewer," "trust and safety analyst," "community operations specialist"). Moderation is performed by subcontractors rather than direct employees, insulating platforms from legal liability and labor obligations (Gillespie, 2018; Newton, 2019). When a platform spokesperson describes AI-powered moderation, the human workers behind the training data that makes that AI function are absent from the description.

This invisibility serves a commercial purpose: it allows platforms to project a clean, automated image while quietly maintaining large human workforces performing the classification labor the automation depends on. It also protects the platforms from the political consequences of disclosing that their AI moderation tools were trained on data produced under conditions that many observers would regard as harmful.

---

## Part 4 — Invisible Labor in the Open Source Commons

### 4.1 The volunteer whose work becomes training data

The annotation economy operates through explicit contracts — workers are recruited, assigned tasks, and paid. But a parallel and vastly larger form of AI training labor is entirely voluntary, uncompensated, and often performed without awareness that the work is being used for AI training at all. This is the labor of open source contributors, Wikipedia editors, Stack Overflow answerers, and the millions of people whose creative and intellectual production constitutes the internet's textual commons.

As documented in Draft F (commons extraction and political economy) and Draft W (unharvested commons), the training corpora for all major language models are built predominantly from this volunteer labor. Common Crawl, which underlies most large training datasets, is a scrape of publicly accessible text produced by humans. The Pile (EleutherAI), C4 (Google), and RefinedWeb (Falcon) are processed versions of the same underlying commons. The code in GitHub Copilot's training data was written by millions of developers who published it under open source licenses that neither contemplated nor explicitly authorized this specific use.

### 4.2 The ghost work framing applied to open source

Gray and Suri (2019) coined the term "ghost work" to describe the on-demand, API-mediated labor that supports AI systems — microwork that is structurally invisible because it occurs behind automated interfaces. Their analysis focused on the annotation and moderation workforce, but the ghost work framing applies with equal precision to open source contributors whose work is systematically extracted without acknowledgment.

The open source contributor is a ghost worker in a specific sense: their labor is present in the model's capabilities (a model trained on GitHub code can write code because millions of people wrote code that became training data), but absent from any accounting of the value chain. The contributor does not appear in the model card, the system prompt, the press release, or the revenue sharing arrangement. They are, in Gray and Suri's terms, "on-demand" labor that has been permanently consumed rather than periodically invoked.

This connects directly to the analysis in Draft A (commons accumulation history): the open source timeline is also a labor history. Every commit to a public repository is an act of intellectual work that has, since approximately 2021, become training data for AI systems generating hundreds of billions of dollars in market capitalization.

### 4.3 Consent, attribution, and the license question

The legal status of using open source code as AI training data is contested. The GitHub Copilot class action (Doe v. GitHub, No. 4:22-cv-06823-JST, N.D. Cal., filed Nov. 3, 2022) argues that training on copyleft code without reproducing accompanying license notices violates open source licenses. The counter-argument is that training constitutes "fair use" (US) or a technically permitted form of information extraction. This legal dispute has not been resolved as of this writing.

But the ethical question is distinct from the legal one. Even if training on publicly available text is legally permissible, the question of whether it is ethically consistent with the social contract of open source contribution remains. Open source contributors published their code expecting it to be used, learned from, and built upon — within a community of practice that reciprocates. The use of that code as private training data for closed commercial systems represents a form of commons enclosure that the original contributors did not contemplate and cannot reverse. This connects to Draft F's analysis of the extractive relationship between platform capitalism and the digital commons.

### 4.4 The missing acknowledgment

AI labs have begun acknowledging, under pressure, the human labor in their annotation pipelines (Bommasani et al., 2023) — partly through the discourse around RLHF transparency, partly through investigative journalism like Perrigo (2023). The open source commons labor is almost entirely unacknowledged. Model cards for frontier models typically list training datasets but not the human beings who created them. The concept of provenance as applied in Draft X (epistemic provenance and detection) has not been extended to the labor dimension: we lack any standard for attributing training data to the human beings who produced it.

---

## Part 5 — Hybrid Intelligence Implications: The Human-in-the-Loop Nobody Talks About

### 5.1 Annotation as a form of hybrid intelligence

The standard framing of hybrid intelligence (HI) focuses on the collaboration between a trained AI system and a human user: the model suggests, the human accepts or modifies, the system learns from outcomes. But this framing erases an earlier and more fundamental HI interaction: the one between the human annotator and the model during training.

Every RLHF ranking represents a human judgment being encoded into model weights. Every image label is a human perceptual decision being converted into training signal. The annotator is not a passive data source — they are an active intelligent agent whose judgments, biases, cultural assumptions, and working conditions shape the model's behavior. The model that users interact with is, in a precise sense, a crystallization of millions of human judgments made by workers in Kenya, the Philippines, India, and Venezuela about what constitutes a "better" or "worse" AI response.

This means that annotation labor is a form of hybrid intelligence — specifically, the kind described by Tubaro et al. (2020) as "embedded human intelligence": human cognitive work that is absorbed into an automated system and reproduced at scale. The trainers, verifiers, and imitators in Tubaro et al.'s typology are the human component of a hybrid system that presents itself as purely automated.

### 5.2 The values question

If annotation workers shape model values through their rankings, then the values encoded in frontier AI models reflect the working conditions, incentives, and demographic characteristics of those workers. Workers paid \$2/hour to complete tasks as quickly as possible have different incentive structures than carefully supervised domain experts. Workers from Kenya applying standards they were trained on by a US company are encoding a specific cultural perspective on what counts as harmful, helpful, or appropriate.

The geographic concentration of RLHF labour also has an inverse implication mapped in Draft W (`w-unharvested-commons.md`): the populations *most* underrepresented in pretraining corpora — Henrich, Heine & Norenzayan's (2010) non-WEIRD demographics, oral-tradition speakers, low-resource-language communities — are also largely outside the recruitment funnels that supply preference annotators. The Kenyan and Filipino workforces described in §1.3 and §2.3 are a partial exception, but their inclusion is structured by anglophone language proficiency and by training instructions written in the dominant ontology of US-headquartered AI labs (Miceli & Posada, 2022). The result is that two independent extraction layers — pretraining text and preference rankings — converge on the same demographic narrowing, so the WEIRD bias documented in Draft W is not corrected at the alignment stage but reinforced by it. This is the structural feature that the Dahlgren Lindström et al. (2024) and Casper et al. (2023) critiques identify without naming: the alignment pipeline inherits, rather than offsetting, the upstream representational asymmetries that Draft W enumerates.

Casper et al. (2023) note that RLHF introduces "hidden assumptions" about whose values are being optimized and whose preferences count. Dahlgren Lindström et al. (2024) argue that the sociotechnical limitations of RLHF — including the structural invisibility of annotator demographics and working conditions — are not incidental bugs but features of a system designed to produce a clean narrative of "human-aligned AI" while obscuring the messiness of how that alignment is actually produced.

### 5.3 The labor question in HI design

If annotation is a form of HI, then HI design must address labor conditions, not just interface design. A hybrid intelligence system that extracts value from low-wage contractors in the Global South while delivering that value to high-wage knowledge workers in the Global North is a particular kind of HI — one that amplifies existing inequalities rather than counteracting them (Couldry & Mejias, 2019; Crawford, 2021).

The HI research community has focused heavily on the human side of human-AI collaboration in the deployment phase: how do doctors use AI diagnostic tools? how do programmers interact with Copilot? This focus systematically ignores the human labor in the training phase that makes those deployment-phase interactions possible. A complete account of hybrid intelligence would trace the full value chain: from the annotator ranking outputs in Nairobi, through the model trained on those rankings, to the knowledge worker benefiting from the model's capabilities in San Francisco.

### 5.4 Automation as labor displacement in a labor-dependent system

There is a structural tension at the heart of the AI labor economy: the systems being trained to automate knowledge work are themselves dependent on human labor to function. As AI capabilities improve, some annotation tasks are automated (AI can now pre-label images for human verification rather than requiring humans to label from scratch). But new annotation tasks are continuously created: more capable models require more nuanced preference data; safety capabilities require evaluation of increasingly sophisticated adversarial inputs; multilingual and multimodal extension requires new annotation categories.

Gray and Suri (2019) document what they call the paradox of automation's last mile: the more tasks are automated, the more new tasks arise that require human judgment to train the next generation of automation. The annotation economy is not a transitional stage on the way to fully automated AI; it is a permanent structural feature of the AI development pipeline, one that grows alongside AI capabilities rather than being displaced by them.

---

## Part 6 — Open Questions

### Empirical gaps

1. **Workforce size**: No reliable global count of annotation workers exists. The 2–3 million estimate cited in industry analyses (ILO, 2021; Kässi & Lehdonvirta, 2018) is extrapolated from platform self-reporting, which systematically undercounts casual and informal workers.

2. **Longitudinal wage data**: Are annotation wages rising, falling, or stable relative to local cost of living? No systematic longitudinal study has been published.

3. **Psychological intervention efficacy**: Which interventions (blurring tools, rotation, psychological support) actually reduce harm to content moderators? The literature is thin and mostly non-experimental.

4. **Annotator influence on model values**: To what extent do systematic demographic biases in annotation workforces show up as measurable biases in model outputs? The causal chain from annotator demographics to model behavior has not been rigorously established.

5. **Open source contributor awareness**: Do open source contributors know their code is used as training data? If informed, would they opt out? No large-scale survey exists.

### Conceptual questions

1. If annotation is a form of hybrid intelligence, does this require reconceptualizing the "H" in HI? Standard HI frameworks (Dellermann et al., 2019; Lutz et al., 2025) assume the human is a beneficiary or co-author of HI outcomes. The annotation worker is a human whose intelligence is absorbed into the system but who may receive no benefit from the resulting capabilities.

2. Is there a meaningful distinction between a "training-phase human" (annotator) and a "deployment-phase human" (user) in an RLHF system? The ranking decisions of training workers shape the model's behavior toward all future users — a form of indirect and unacknowledged HI at scale.

3. Does the ghost work framing from Gray and Suri (2019) need updating for the generative AI era? Ghost work in 2019 described on-demand microwork maintaining discrete automated pipelines. In 2025, annotation workers are shaping the values of systems that interact with billions of people. The scale and consequence are qualitatively different.

### What Still Needs Work

- [ ] Acquire Gray & Suri (2019) *Ghost Work* — foundational; must be in LIBRARY-WISHLIST.md (book)
- [ ] Acquire Roberts (2019) *Behind the Screen* — foundational; must be in LIBRARY-WISHLIST.md (book)
- [x] Tubaro et al. (2020) *Big Data & Society* confirmed open access — journal is gold OA; freely available at DOI *(executor-confirmed 2026-05-07)*
- [x] Replace unverifiable Hao (2023) Venezuela citation with peer-reviewed anchor — *Miceli & Posada (2022) PACM HCI 6(CSCW2) acquired and integrated into §2.3 (2026-05-13)*
- [x] Correct Dahlgren Lindström et al. (2024) attribution — *prior fabricated author list and year corrected via OpenAlex W-id (2026-05-13)*
- [ ] Find Posada (2022) ICS paper on open access — Semantic Scholar shows paywall
- [ ] Find Irani & Silberman (2013) CHI paper — ACM DL, may have open access version
- [x] Download Spence et al. (2023) psychological impacts paper — *acquired 2026-05-08 from corrected DOI 10.5817/cp2023-4-8; PDF in `Kilder/Spence2023_PsychologicalImpactsContentModeration_Cyberpsychology.pdf`*
- [x] Correct Scott et al. (2023) author list and DOI — *prior fabricated coauthors and wrong DOI corrected via CrossRef 2026-05-19; correct DOI `10.1145/3544548.3581512`; full author list Scott, Marcu, Anderson, Newman, Schoenebeck*
- [x] Resolve Gillespie (2018) and Fairwork Foundation (2023) S2-rate-limited placeholders — *Gillespie OpenAlex W2994507840 OA cit 509; Fairwork confirmed `[R]` institutional, no CrossRef DOI*
- [ ] Add empirical wage data table (MTurk median, Scale AI rate cards, Appen rates, Kenyan TIME figures)
- [ ] Verify workforce size estimates against ILO data and recent academic surveys
- [ ] Connect to Draft AD (evil encoded in models) — the harm in models is in part a consequence of harmful annotation working conditions

---

## References

Bommasani, R., Klyman, K., Longpre, S., Kapoor, S., Maslej, N., Cottier, B., Zhang, D., & Liang, P. (2023). The Foundation Model Transparency Index (arXiv:2310.12941). Stanford Center for Research on Foundation Models. https://arxiv.org/abs/2310.12941 — Evaluates 10 major foundation model providers across 100 transparency criteria; finds systematically low disclosure rates for training data provenance, annotator demographics, and labour conditions — directly substantiates the opacity claim in §2.2. [P] [OA cit: 41]

Appen Limited. (2021). *Annual Report 2021*. Appen Limited. https://ir.appen.com/en/asx-reports-and-presentations/ — Corporate disclosure; primary source for Appen contractor workforce scale figures cited in §1.2 and §1.4. [R]

Couldry, N., & Mejias, U. A. (2019). Data colonialism: Rethinking big data's relation to the contemporary subject. *Television & New Media*, *20*(4), 313–328. https://doi.org/10.1177/1527476418796632 — Theoretical framework for the Global South extraction / Global North accumulation dynamic in data economies; canonical anchor for the argument that AI labor arrangements amplify existing global inequalities rather than distributing AI's benefits equitably. [J] [OA cit: 1387] [Verified non-retracted via CrossRef 2026-05-18, `update-to: None`]

Crawford, K. (2021). *Atlas of AI: Power, Politics, and the Planetary Costs of Artificial Intelligence*. Yale University Press. — Empirical survey of AI's global resource and labor extraction chains, from lithium mining to annotation workforces; canonical anchor for the structural argument that AI systems externalize environmental and human costs onto Global South communities while delivering capabilities to Global North users. [B] [OA cit: 580]

Bai, Y., Jones, A., Ndousse, K., Askell, A., Chen, A., DasSarma, N., … Kaplan, J. (2022). *Training a helpful and harmless assistant with reinforcement learning from human feedback* (arXiv:2204.05862). arXiv. https://arxiv.org/abs/2204.05862 — PDF: `Bai2022_RLHF_HelpfulHarmless_arXiv2204.05862.pdf` [P] [iCit: 479] [OA cit: 361]

Bender, E. M., Gebru, T., McMillan-Major, A., & Shmitchell, S. (2021). On the dangers of stochastic parrots: Can language models be too big? *Proceedings of FAccT 2021*, 610–623. https://doi.org/10.1145/3442188.3445922 — PDF: `Bender2021_StochasticParrots_FAccT2021.pdf` [C] [OA cit: 5160]

Casper, S., Davies, X., Shi, C., Gilbert, T. K., Scheurer, J., Rando, J., … Hadfield-Menell, D. (2023). Open problems and fundamental limitations of reinforcement learning from human feedback. *Transactions on Machine Learning Research*. https://arxiv.org/abs/2307.15217 — PDF: `Casper2023_OpenProblemsRLHF_arXiv2307.15217.pdf` [J] [iCit: 44] [OA cit: 89]

Dellermann, D., Ebel, P., Söllner, M., & Leimeister, J. M. (2019). Hybrid intelligence. *Business & Information Systems Engineering, 61*(5), 637–643. https://doi.org/10.1007/s12599-019-00595-2 — Seminal definition of hybrid intelligence as superior complementary achievement; canonical reference for HI frameworks invoked in §6. [J] [OA cit: 539] [Cross-referenced in Draft O]

Gillespie, T. (2018). *Custodians of the Internet: Platforms, content moderation, and the hidden decisions that shape social media*. Yale University Press. — Analyses the structural mechanisms by which platforms obscure moderation labor: NDA clauses, euphemistic job titles, and the use of subcontractors to insulate platforms from legal and labour obligations; canonical academic reference for §3.4 invisibility argument. [B] [OA cit: 509] — *OpenAlex W2994507840 (Tarleton Gillespie author A5018245743); Yale UP monograph carries no CrossRef DOI, so retraction status cannot be checked via the DOI route — book retractions, where they occur, are issued by the publisher rather than via CrossRef.*

Gray, M. L., & Suri, S. (2019). *Ghost work: How to stop Silicon Valley from building a new global underclass*. Eamon Dolan/Houghton Mifflin Harcourt. — Book: see LIBRARY-WISHLIST.md

Chan, R., & Potkin, F. (2023, March 31). TikTok's trust and safety teams face burnout amid high content moderation demands.
 *Reuters*. https://www.reuters.com/technology/tiktok-trust-safety-teams-face-burnout-amid-high-content-moderation-demands-2023-03-31/ — Investigative reporting on TikTok moderation operations in Malaysia and Southeast Asia

Difallah, D., Filatova, E., & Ipeirotis, P. (2018). Demographics and dynamics of Mechanical Turk workers. In *Proceedings of the Eleventh ACM International Conference on Web Search and Data Mining* (WSDM '18) (pp. 135–143). ACM. https://doi.org/10.1145/3159652.3159661 — Empirical capture-recapture measurement of MTurk worker population: ~250k unique workers active over a three-month window, with ~2k–5k workers active at any given moment; canonical quantitative anchor for MTurk workforce scale. [C] [OA cit: 510]

Doe, J., et al. v. GitHub, Inc., Microsoft Corp., & OpenAI, Inc., No. 4:22-cv-06823-JST (N.D. Cal. filed Nov. 3, 2022). Class action challenging use of open-source copyleft code in GitHub Copilot's training data without reproducing accompanying license notices; plaintiffs later amended to Matthew Butterick et al. as lead plaintiff. [R]

Fairwork Foundation. (2023). *Fairwork Cloudwork Ratings 2023: Labour Standards in the Platform Economy*. Oxford Internet Institute, University of Oxford. https://fair.work/en/fw/publications/fairwork-cloudwork-ratings-2023/ — Annual third-party assessment of working conditions and workforce scale across major cloudwork and annotation platforms; cited in §1.4, §1.3, and §3.2. [R] — *Institutional report, no CrossRef DOI; OpenAlex title search returns no direct record for the 2023 Cloudwork Ratings (institutional reports are unevenly indexed). iCit / OA cit not applicable; admissibility rests on the `[R]` policy-source tier of the STEERING source-quality standard rather than on citation impact.*

Foxglove Foundation. (2023). *Daniel Motaung and others v. Meta Platforms Inc. and others: Kenyan content moderators take legal action*. Foxglove Legal. https://foxglove.org.uk/case/kenya-content-moderators-vs-meta/ — Legal case documentation; primary source for Meta/Accenture Nairobi content moderation workforce and labour conditions

Hara, K., Adams, A., Milland, K., Savage, S., Callison-Burch, C., & Bigham, J. P. (2018). A data-driven analysis of workers' earnings on Amazon Mechanical Turk. In *Proceedings of the 2018 CHI Conference on Human Factors in Computing Systems* (Article 449). ACM. https://doi.org/10.1145/3173574.3174023 — arXiv:1711.00646; OA green via Singapore Management University repository (https://ink.library.smu.edu.sg/sis_research/4209). [C] [OA cit: 483] — canonical CHI 2018 crowdwork wages study; CrossRef retraction status verified clean 2026-05-08.

Henrich, J., Heine, S. J., & Norenzayan, A. (2010). The weirdest people in the world? *Behavioral and Brain Sciences*, *33*(2–3), 61–83. https://doi.org/10.1017/S0140525X0999152X — Foundational diagnosis of the WEIRD (Western, Educated, Industrialised, Rich, Democratic) sampling bias in behavioural science; invoked in §5.2 to anchor the argument that RLHF recruitment funnels reproduce the demographic narrowing already documented at pretraining stage in Draft W. Also the canonical reference for Draft W's WEIRD argument, so the cross-link is anchored by a shared source. [J] [OA cit: 11,809] [CrossRef ref-by: 9,197] [Verified non-retracted via CrossRef 2026-05-19, `update-to: None`] *(added 2026-05-19 cycle to support the AF↔W cross-link mandated by STEERING focus-override)*

ILO. (2021). *World Employment and Social Outlook 2021: The role of digital labour platforms in transforming the world of work*. International Labour Organization. https://doi.org/10.54394/FHEM2152 — Institutional labour market documentation; documents the scale of digital labour platforms and estimates of the global platform workforce; anchor for the workforce-size figure in §6 Empirical gap 1. [R]

Kässi, O., & Lehdonvirta, V. (2018). Online labour index: Measuring the online gig economy for policy and research. *Technological Forecasting and Social Change*, 137, 241–248. https://doi.org/10.1016/j.techfore.2018.07.056 — Constructs the Oxford Internet Institute Online Labour Index, tracking occupational and geographic trends in online gig labour markets across platforms; provides independently constructed quantitative estimates of online labour platform workforce scale that partially anchor the 2–3 million figure in §6; [J] [OA cit: well above ≥5; confirmed from established digital labour economics literature; S2 rate-limited at execution time]. *(executor-added 2026-05-20)*

Kulikov, I., Whitehouse, C., Wu, T., Saha, S., Helenowski, E., Yuan, W., Golovneva, O., Lanchantin, J., Bachrach, Y., Foerster, J., Li, X., Fang, H., Sukhbaatar, S., & Weston, J. (2026). Autodata: An automatic data scientist to create high-quality data. Meta AI RAM Blog. https://facebookresearch.github.io/RAM/blogs/autodata/ — Web source; no PDF [R] — arXiv preprint announced "coming soon"; iCit pending. Relevance: agentic pipeline that automates the iterative dataset construction work previously performed by human annotation workers and data scientists; raises the question of whether the human labor this draft examines is being displaced by agents rather than simply offshored.

Lee, H., Phatale, S., Mansoor, H., Mésnard, T., Ferret, J., Lu, K., Bishop, C., Hall, E., Cărbune, V., Rastogi, A., & Prakash, S. (2023). RLAIF vs. RLHF: Scaling reinforcement learning from human feedback with AI feedback (arXiv:2309.00267). arXiv. https://doi.org/10.48550/arxiv.2309.00267 — Google Research paper demonstrating that AI feedback (RLAIF) can match or approach human feedback (RLHF) quality on summarization and dialogue benchmarks, while scaling more efficiently; primary empirical anchor for RLAIF as a live research direction in §2.1. [P] [OA cit: 67]

Dahlgren Lindström, A., Methnani, L., Krause, L., Ericson, P., Martínez de Rituerto de Troya, Í., Coelho Mollo, D., & Dobbe, R. (2024). AI alignment through reinforcement learning from human feedback? Contradictions and limitations (arXiv:2406.18346). arXiv. https://arxiv.org/abs/2406.18346 — PDF: `Lindstrom2025_RLHFSociotechnicalLimits_arXiv2406.18346.pdf` [P] [OA cit: 2] — *Author list and year corrected 2026-05-13 via OpenAlex verification. The prior reference entry ("Lindstrom, S., Razak, F., Jobin, A., & Vayena, E., 2025") was an attribution error: OpenAlex W-id for arXiv:2406.18346 returns first author Adam Dahlgren Lindström with six coauthors as listed above, publication year 2024. Inline citations in §2.4 and §5.2 updated to match. No published journal venue at time of check; remains preprint.*

Lutz, C., Newlands, G., & Jarrahi, M. H. (2025). Hybrid intelligence. In W. Xu (Ed.), *Handbook of Human-Centered Artificial Intelligence*. Springer. https://doi.org/10.1007/978-981-97-8440-0_87-1 — Defines hybrid intelligence as "the mutual augmentation of human and AI capabilities through continuous interaction, where both learn and adapt over time"; canonical contemporary HI framework invoked in §6. [PDF saved: Kilder/Lutz, Newlands, Jarrahi 2025 - Hybrid Intelligence.pdf] [C]

Miceli, M., & Posada, J. (2021). Wisdom for the crowd: Discoursive power in annotation instructions for computer vision. *Workshop on Data-Centric AI (DCAI), NeurIPS 2021*. — PDF: not on arXiv; [to find]

Miceli, M., & Posada, J. (2022). The data-production dispositif. *Proceedings of the ACM on Human-Computer Interaction, 6*(CSCW2), Article 460, 1–37. https://doi.org/10.1145/3555561 — PDF: `Kilder/MiceliPosada2022_DataProductionDispositif_arXiv2205.11963.pdf` (arXiv-preprint version of the PACM HCI paper). Ethnographic study of three Venezuelan crowdsourcing platforms and a Buenos Aires BPO firm; the largest peer-reviewed empirical anchor for Latin American AI annotation labour. Provides §2.3 with a scholarly source for the Venezuela claim that replaces the prior unverifiable journalistic reference. [J] [OA cit: 95] — *Added 2026-05-13. CrossRef retraction status: clean (`update-to: None`). Gold OA via ACM.*

Newton, C. (2019, February 25). The Trauma Floor: The secret lives of Facebook moderators in America. *The Verge*. https://www.theverge.com/2019/2/25/18229714/cognizant-facebook-content-moderator-interviews-trauma-working-conditions-arizona — Investigative report documenting Facebook content moderators employed by Cognizant subcontractor under NDA, with euphemistic job titles and structural isolation from Facebook's direct employment; canonical journalistic source for §3.4 subcontractor-insulation and NDA-suppression claims. [R]

Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C. L., Mishkin, P., Zhang, C., Agarwal, S., Slama, K., Ray, A., Schulman, J., Hilton, J., Kelton, F., Miller, L. E., Simens, M., Askell, A., Welinder, P., Christiano, P., Leike, J., & Lowe, R. (2022). Training language models to follow instructions with human feedback. *Advances in Neural Information Processing Systems (NeurIPS 2022)*. arXiv:2203.02155. https://doi.org/10.52202/068431-2011 — Introduces InstructGPT; foundational demonstration that RLHF transforms base LLMs into instruction-following assistants; the canonical primary-source citation for RLHF as an assistant-training technique (Ouyang et al. established RLHF at scale; Bai et al. 2022 is the Anthropic extension to helpful/harmless objectives). [C — NeurIPS 2022] [iCit: 2204 (S2 confirmed 2026-05-18)] *(executor-added 2026-05-18)*

Perrigo, B. (2023, January 18). Exclusive: OpenAI used Kenyan workers on less than \$2 per hour to make ChatGPT less toxic. *TIME*. https://time.com/6247678/openai-chatgpt-kenya-workers/ — Web source; no PDF

Posada, J. (2022). Embedded reproduction in platform data work. *Information, Communication & Society*, 25(6), 816–834. https://doi.org/10.1080/1369118X.2022.2036030 — Paywalled: see LIBRARY-WISHLIST.md

Roberts, S. T. (2014). *Behind the screen: The hidden digital labor of commercial content moderation* [Doctoral dissertation, University of Illinois at Urbana-Champaign]. IDEALS Repository. http://hdl.handle.net/2142/50401 — Foundational doctoral fieldwork; article-form publication is Roberts (2016) below; trade-press elaboration is Roberts (2019). [R] — *Source line corrected 2026-05-18: prior entry attributed this work to* First Monday *19(10), but the First Monday Vol. 19 Issue 10 (October 2014) table of contents contains no Roberts entry — the 2014 work is the UIUC dissertation, not a First Monday article; the 2018 First Monday paper by Roberts is a separate work ("Digital detritus", DOI 10.5210/fm.v23i3.8283).*

Roberts, S. T. (2016). Commercial content moderation: Digital laborers' dirty work. In S. U. Noble & B. M. Tynes (Eds.), *The intersectional internet: Race, sex, class and culture online* (pp. 147–160). Peter Lang. — Peer-reviewed article-form publication of the §3.2 invisibility analysis; primary published anchor for the structural-obscurity argument in §3.4. [C] [OA cit: 160] — *Added 2026-05-18 via OpenAlex search; replaces the misattributed Roberts (2014) First Monday reference as the peer-reviewed anchor in §3.2.*

Roberts, S. T. (2019). *Behind the screen: Content moderation in the shadows of social media*. Yale University Press. https://doi.org/10.12987/9780300245318 — Book: see LIBRARY-WISHLIST.md. [B] [OA cit: 281] — Ethnographic extension of the 2014 dissertation and 2016 article with additional Philippines fieldwork.

Scott, C. F., Marcu, G., Anderson, R. E., Newman, M. W., & Schoenebeck, S. (2023). Trauma-informed social media: Towards solutions for reducing and healing online harm. In *Proceedings of the 2023 CHI Conference on Human Factors in Computing Systems* (CHI '23). Association for Computing Machinery. https://doi.org/10.1145/3544548.3581512 — Theory-building CHI 2023 paper that adapts the six trauma-informed-care principles from clinical health practice to social-media moderation workflow design; canonical reference for the §3.3 argument that structural redesign — not individual coping — is the necessary route to reducing moderator harm. [C] [OA cit: 79] [Verified non-retracted via CrossRef 2026-05-19, `update-to: None`] — *Author list, DOI, and OA cit corrected 2026-05-19: prior entry attributed coauthors "Haimson, O. L., Steigman, M. A., & Dugas, M." (none of whom are on the paper) and cited DOI `10.1145/3544548.3581434` (which resolves to an unrelated CHI 2023 paper titled "Physically Situated Tools for Exploring a Grain Space in Computational Machine Knitting"). Authoritative authorship per CrossRef DOI lookup on the correct identifier `10.1145/3544548.3581512`.*

Steiger, M., Bharucha, T. J., Venkatagiri, S., Riedl, M., & Lease, M. (2021). The psychological well-being of content moderators: The emotional labor of commercial moderation and avenues for improving support. In *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems* (CHI '21), Article 341. ACM. https://doi.org/10.1145/3411764.3445092 — Canonical quantitative survey of content moderator psychological health across major platforms; documents PTSD symptom prevalence, emotional labor burden, and intervention strategies; referenced by virtually all subsequent empirical work on moderator well-being. [C] [OA cit: 157] [CrossRef ref-by: 149] [Verified non-retracted via CrossRef 2026-05-19, `update-to: None`]

Spence, R., Bifulco, A., Bradbury, P., Martellozzo, E., & DeMarco, J. (2023). The psychological impacts of content moderation on content moderators: A qualitative study. *Cyberpsychology: Journal of Psychosocial Research on Cyberspace*, 17(4), Article 8. https://doi.org/10.5817/cp2023-4-8 — PDF: `Kilder/Spence2023_PsychologicalImpactsContentModeration_Cyberpsychology.pdf`. [J] [OA cit: 40] — DOI corrected 2026-05-08; the previously cited DOI (10.5817/CP2023-2-1) resolves to a different paper (Quintana-Orts et al., on cybervictimization). Third author corrected from "J. Bradbury" to "P. Bradbury" (Paula). Diamond OA via Cyberpsychology (Masaryk University). CrossRef retraction status verified clean.

Tubaro, P., Casilli, A. A., & Coville, M. (2020). The trainer, the verifier, the imitator: Three ways in which human platform workers support artificial intelligence. *Big Data & Society*, 7(1). https://doi.org/10.1177/2053951720919776 — **Open access** (gold; SAGE, Creative Commons; *Big Data & Society* is a fully gold OA journal). [J] [OA cit: 234] — DOI corrected 2026-05-08 (the previously cited 10.1177/2053951720938463 returns 404 on both OpenAlex and CrossRef; the correct identifier is 720919776). Introduces the trainer/verifier/imitator typology of AI platform labor used in §5.1. CrossRef retraction status verified clean. *(executor-confirmed OA 2026-05-07; DOI fix 2026-05-08; OA citation count refreshed 2026-05-13)*

Litz, B. T., Stein, N., Delaney, E., Lebowitz, L., Nash, W. P., Silva, C., & Maguen, S. (2009). Moral injury and moral repair in war veterans: A preliminary model and intervention strategy. *Clinical Psychology Review*, 29(8), 695–706. https://doi.org/10.1016/j.cpr.2009.07.003. — Foundational paper introducing the moral injury construct; defines moral injury as the specific psychological distress arising from performing, witnessing, or failing to prevent actions that violate one's deeply held moral beliefs; canonical clinical anchor for §3.3 moral injury claim in content moderation labor context. [iCit: 270] [J — Clinical Psychology Review] *(executor-added 2026-05-19)*

---

## Cross-references

- **Draft A** (commons accumulation history) — every open source commit is also annotation labor history; the GitHub timeline is a labor timeline
- **Draft F** (commons extraction inequality) — annotation labor as another dimension of the extractive relationship; the value chain from worker to shareholder
- **Draft W** (unharvested commons) — the flip side: what annotation labor *cannot* capture (oral knowledge, indigenous epistemologies) remains outside the training pipeline. The §5.2 paragraph (new 2026-05-19) anchors the AF↔W connection more substantively: the WEIRD-sampling argument that W applies to pretraining corpora extends, through shared recruitment funnels (anglophone proficiency, US-style training instructions), to the RLHF preference-data layer documented here — so alignment does not correct the upstream representational asymmetry but reproduces it
- **Draft AB** (credit/blame, agent attribution) — who is responsible for harm caused by a model whose values were shaped by poorly paid contractors under duress?
- **Draft AD** (evil encoded in models) — harmful biases in model outputs are in part a product of the conditions under which alignment data was produced
- **Draft AV** (social media training data) — the upstream extraction (users' behavioural surplus) and the post-extraction labour chain (this draft) form two structurally analogous and operationally complementary asymmetries in the same value system; AV §3 references AF as the post-extraction labour chain and AV §5 OQ4 raises the open question of whether social platforms are the unacknowledged alignment infrastructure for frontier AI — a question whose answer depends on the RLHF preference-data labour described here in §2
