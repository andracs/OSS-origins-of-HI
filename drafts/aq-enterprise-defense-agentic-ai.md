# Draft AQ — From Enterprise to Battlefield: Agentic AI Platforms in High-Stakes Operational Contexts

**Version:** v0.3 (2026-05-15)  
**Status:** v0.3 — Citation verification pass via tri-source chain (OpenAlex + CrossRef). **Major correction:** the v0.2 "Bode & Watts (2023)" source line was fabricated — title "Meaning-less human control" matches a real Bode & Watts paper, but the stated year (2023), venue (*Humanities and Social Sciences Communications*), and DOI (`10.1057/s41599-023-01796-3`, which 404s at the DOI registry) were all wrong. The actual paper is **Bode, I., & Watts, T. (2021). *Meaning-less human control: Lessons from air defence systems on meaningful human control for the debate on AWS* (Center for War Studies Research Report). University of Southern Denmark.** [R] (no DOI; OpenAlex confirmed authors/title/year; OA cit: 6). The §5.3 inline citation was relocated to **Bode (2023)** *European Journal of International Relations* 29(4), 990–1016, DOI 10.1177/13540661231163392 (OA cit: 29; CrossRef `update-to`: None) for peer-reviewed reinforcement of the "no binding international instrument" claim. **Empirical grounding added to §4.1:** Horowitz & Kahn (2024), *International Studies Quarterly* 68(2), DOI 10.1093/isq/sqae020 (OA cit: 35; CrossRef `update-to`: None) — a randomised pre-registered experiment measuring automation bias and the bias-bending effect of system-confidence cues among 9,000 participants in a national-security task. Roff (2014) source line now carries verified DOI 10.1080/15027570.2014.975010 (OA cit: 145; CrossRef `update-to`: None). Noy & Zhang (2023) OA cit value resolved to 1226 (was a placeholder "well above ≥5"). arXiv PDF for Horowitz & Kahn downloaded to `Kilder/Horowitz2024_BendingAutomationBiasCurve_arXiv2306.16507.pdf`.  
**Next:** Obtain Scharre/Crawford/Brayne via library; verify Anduril Lattice technical claims against archived white papers; consider replacing Osinga (2007) book with Osinga (2013) *Contemporary Security Policy* for a citable peer-reviewed Boyd treatment; cross-ref Draft AN (alignment — human oversight in high-capability systems), Draft P (governance), Draft AI (deployment failure modes), Draft AK (orchestration architecture).

---

## Overview and Chapter Position

In 2018, Google withdrew from Project Maven — the United States Department of Defense programme to use machine learning for drone footage analysis — following an internal employee petition signed by more than four thousand engineers (Wakabayashi & Shane, 2018). Within months, Palantir Technologies stepped in to fill the contract (Simonite, 2018). The episode crystallised a tension that runs through the entire field of hybrid intelligence: the same capabilities that enable a hospital to optimise patient flow, or a logistics company to route deliveries, also enable a military to identify targets and accelerate lethal decisions.

This chapter examines the agentic AI stack as it is deployed not in research settings but in the highest-stakes operational contexts available: enterprise command-and-control, intelligence analysis, and defense. It focuses on three platforms that have defined the frontier of this deployment: Palantir (the dominant enterprise-to-government AI infrastructure company), Anduril Industries (the defense-native autonomy company), and Scale AI (the data and AI services company that built a dedicated defense product). Together they illustrate how the architectural patterns described in earlier chapters — orchestration (Draft AK), tool-calling (Draft T), sensing infrastructure (Draft AJ) — are instantiated when the cost of failure is measured in human lives and geopolitical consequence.

The chapter's central argument is that high-stakes deployment does not merely apply hybrid intelligence — it redefines what "hybrid" means. In civilian contexts, "hybrid" refers to the combination of human judgment and machine capability in a collaborative loop. In defense contexts, the human's role in the loop is itself a design variable: a system can be designed to keep humans "in the loop" (requiring human authorisation for each action), "on the loop" (monitoring with override authority), or "out of the loop" (fully autonomous within a mission envelope). The choice between these modes is not merely a product decision; it is a governance and ethics decision with legal implications under international humanitarian law.

---

## §1 — Enterprise Agentic AI: The Palantir Model

### 1.1 Architecture: the Ontology as organisational operating system

Palantir's core architectural innovation — the Foundry Ontology — is described in Draft AK §3 as an implementation of the shared-state pattern for multi-agent systems. In enterprise deployment, the Ontology functions as something more fundamental: a semantic layer that translates raw data (database records, sensor streams, documents) into a typed graph of real-world entities (personnel, assets, orders, events) with governed relationships and security policies embedded at the schema level.

The significance for hybrid intelligence is that the Ontology is not merely a data store. It is an organisational model — a digital twin of the enterprise — that provides a stable referent for both human decision-makers and AI agents. When an LLM-based agent in Palantir AIP reasons about a production problem, it reasons over Ontology objects (WorkOrder, Asset, FailureMode) not over raw database tables. When a human analyst reviews the agent's output, they see the same object model. The shared ontology creates a genuinely shared cognitive environment for human-AI collaboration — the technical precondition for meaningful hybrid intelligence.

Actions, the Palantir term for state-modifying operations, are bounded and governable. An Action that reschedules a production run, releases a purchase order, or flags a patient record can be configured to require human approval before execution. This is the principal hierarchy principle from Draft AK §5 implemented at the infrastructure level: the system does not merely ask agents to request permission — it enforces that transitions above a configurable authority threshold cannot occur without human sign-off (Palantir Technologies, n.d.-b; Brayne, 2020).

### 1.2 Dual-use: Foundry, Gotham, and the civil-military pipeline

Palantir operates two primary platforms. Foundry targets commercial enterprise (manufacturing, financial services, healthcare). Gotham targets defence and intelligence agencies (the US military, NATO allies, intelligence community). Since the 2023 introduction of AIP (Palantir Technologies, 2023), both platforms share a common LLM integration layer — the same architectural patterns flow between civilian and military deployments.

This civil-military dual-use pipeline has important implications for hybrid intelligence systems design. Capabilities developed for commercial supply-chain optimisation — multi-agent task orchestration, shared ontology state, action-bounded workflows — migrate to intelligence analysis and military planning with minimal re-engineering. The governance gap is structural: enterprise AI governance frameworks (primarily market and regulatory, centred on GDPR and emerging EU AI Act obligations) do not apply to military applications, which are explicitly excluded from EU AI Act scope under Article 2(3). Capabilities can thus be developed, tested, and refined in the regulated commercial sphere, then deployed in the unregulated military sphere without re-evaluation (Brundage et al., 2018; European Parliament & Council of the EU, 2024, Art. 2(3)).

---

## §2 — Defense-Native Platforms: Anduril and Scale AI Donovan

### 2.1 Anduril Lattice: AI as the operating system for physical autonomy

Anduril Industries was founded in 2017 by Palmer Luckey (creator of the Oculus Rift) with an explicit thesis: that the defense technology industry was too slow and too legacy-bound to integrate modern AI capabilities at the pace required (Statt, 2019). Anduril's Lattice OS is an AI-powered command and control platform that aggregates data from heterogeneous sensors (radar, LIDAR, optical, acoustic), fuses them into a common operational picture, and coordinates autonomous systems — ground vehicles, aerial drones, underwater platforms — in real time (Anduril Industries, 2024; Insinna, 2021). The technical architecture claims in this paragraph rest on vendor documentation and trade-press reporting only; systematic searches for independent peer-reviewed technical-analytical literature on Lattice OS or comparable battle-management autonomy stacks identified no qualifying sources, consistent with defense-sector literature being predominantly classified or published in grey-literature venues not indexed by academic databases.

Lattice represents the sensing → state → action architecture described in Draft AJ and Draft AK, instantiated at military scale. Sensor data from Anduril's own hardware (Sentry towers, Roadrunner interceptors) and third-party systems feeds into a shared situational awareness layer; autonomous systems receive tasking from this layer; human operators monitor and can intervene. The system is explicitly designed for contested environments where human decision latency is operationally costly — precisely the scenario in which the "on the loop" or "out of the loop" human roles become attractive from a military effectiveness standpoint.

Anduril's model differs from Palantir's in a crucial way: where Palantir provides a platform for human analysts and decision-makers augmented by AI, Anduril's primary output is autonomous physical action coordinated by AI. The hybrid intelligence question — where exactly the human sits in the system — is therefore more acute.

### 2.2 Scale AI Donovan: intelligence analysis as LLM application

Scale AI built its business on data labelling for AI training (the human labour dimension is examined in Draft AF). In 2023 it launched Donovan, a platform designed to give US military analysts access to frontier LLMs on classified networks (Scale AI, 2023; Insinna, 2023). Donovan allows analysts to query intelligence databases in natural language, synthesise reporting across multiple sources, and generate draft assessments — tasks that previously required hours of manual synthesis (Heuer, 1999).

Donovan is positioned explicitly as a "human in the loop" system: the analyst queries, the model synthesises, the analyst decides. In the terms of this chapter, it implements the hierarchical orchestration pattern (Draft AK §1.2) with the human as the authoritative final layer. Scale AI's argument is that LLM-assisted intelligence analysis reduces cognitive load on analysts, allowing them to process more information at higher quality, without removing their judgment from the decision chain (Scale AI, 2023; Insinna, 2023; Noy & Zhang, 2023).

---

## §3 — The OODA Loop as Hybrid Intelligence Framework

The dominant framework for military decision-making is the OODA loop, developed by US Air Force strategist John Boyd: Observe, Orient, Decide, Act (Osinga, 2013). The OODA loop was originally a theory of cognitive speed — the side that can cycle through observation, orientation, decision, and action faster than its adversary achieves a systematic advantage.

The introduction of agentic AI into military operations is best understood as an intervention on the OODA loop. AI systems accelerate the Observe phase (faster sensor fusion, broader surveillance coverage), compress the Orient phase (synthesising intelligence across thousands of reports simultaneously), assist the Decide phase (generating decision options and consequence estimates), and in some autonomous systems begin to act on the Act phase without human intermediation (Payne, 2018).

Hybrid intelligence, in the military context, is the question of where the human remains essential in this loop and where machine speed is permitted to operate autonomously. The design choices are not neutral:

- **Human in the loop (full control):** Every action requires explicit human authorisation. Maximum human oversight, minimum machine autonomy. Operationally expensive in high-tempo environments.
- **Human on the loop (supervisory control):** The machine acts autonomously within defined parameters; the human monitors and can intervene. Balances speed and oversight. The dominant model in current Western military doctrine (Ekelhof, 2019; U.S. DoD, 2023).
- **Human out of the loop (full autonomy):** The machine acts without human intervention within a mission envelope. Maximum speed, minimum oversight. Currently restricted by international humanitarian law requirements for meaningful human control.

The hybrid intelligence framing from earlier chapters — human-AI collaboration as a synergistic combination of complementary capabilities — maps onto the OODA loop as follows: AI contributes speed, breadth, and consistency at the Observe and Orient phases; humans contribute judgment, accountability, and contextual understanding at the Decide phase; and the system's legitimacy depends on the human's genuine ability to intervene at the Act phase.

---

## §4 — Human Oversight in High-Stakes Autonomous Systems

### 4.1 Meaningful human control and the degradation problem

International humanitarian law (IHL) requires that weapons be deployed with "meaningful human control" — a phrase that has resisted precise legal definition but is generally understood to require that a human being makes a genuine decision about whether to apply force in a specific context (International Committee of the Red Cross, 2021; Roff, 2014). Autonomous weapons systems (AWS) challenge this requirement because the decision to apply force may be pre-delegated to the system's targeting algorithm.

Roff and Danks (2018) analyse the epistemic problem underlying meaningful human control: in order to exercise genuine oversight, a human must be able to understand and evaluate the system's decisions. For complex AI systems operating in high-dimensional sensor environments, this understanding may be structurally unavailable — the human is "on the loop" in a nominal sense but cannot, in practice, evaluate whether the system's identification of a target is correct. At scale, this epistemic gap produces what Roff and Danks term the central failure mode: the human approves the system's recommendation without genuine deliberation. The underlying mechanism — automation bias, where the cognitive cost of genuine deliberation exceeds the time available and the human defaults to system advice — is documented in the human-factors literature (Parasuraman & Manzey, 2010).

This is a fundamental hybrid intelligence failure mode: the system is designed as human-on-the-loop, but the human's actual contribution to the decision is attenuated to the point where the system is functionally autonomous. The governance implication is that meaningful human control cannot be guaranteed by design specification alone — it requires that the human's cognitive burden at the decision point be within the range of genuine human evaluation.

Horowitz and Kahn (2024) provide one of the few large-sample empirical measurements of automation bias in a national-security setting. In a pre-registered survey experiment with approximately 9,000 participants, they show that exposure to algorithmic recommendations in a simulated military decision task induces measurable bias toward the system's advice — but that disclosing the system's confidence level and accuracy attenuates the effect. The finding qualifies the Roff–Danks pessimism in two directions: automation bias in high-stakes settings is empirically substantial, but the curve is "bendable" through interface design choices that surface uncertainty rather than concealing it. The result is directly applicable to the Palantir AIP and Donovan deployment patterns described in §1 and §2, where confidence calibration in LLM-generated recommendations is currently weak (cf. Draft I on LLM overconfidence).

### 4.2 Scharre on autonomous weapons and accountability gaps

Scharre (2018) provides the most comprehensive treatment of the autonomous weapons debate from a military policy perspective. His central concern is not that autonomous weapons will malfunction — though he documents extensive cases of this — but that they create an accountability gap (Sparrow, 2007): when a weapon makes a targeting decision autonomously and that decision is wrong, no human made a decision that was wrong. Responsibility is diffused across the system's developers, commanders who deployed it, and policymakers who authorised its development, in ways that current legal frameworks cannot cleanly assign (Santoni de Sio & Mecacci, 2021).

This accountability gap is the military instantiation of the attribution problem examined in Draft AB (credit and blame in agentic systems). In civilian contexts, the harm from a misattributed agent decision is typically economic or reputational. In military contexts, it is potentially lethal and has implications under international humanitarian law.

---

## §5 — Governance: Gaps, Principles, and the Regulation Problem

### 5.1 The EU AI Act military exclusion

The EU AI Act (2024), the most comprehensive AI governance regulation currently in force, explicitly excludes applications developed for military and national security purposes from its scope. Article 2(3) states that the regulation "does not apply to AI systems where and in so far they are placed on the market, put into service, or used with or without modification exclusively for military, defence or national security purposes, regardless of the type of entity carrying out those activities" (European Parliament & Council of the EU, 2024, Art. 2(3)). The rationale is that military applications are governed by international humanitarian law and national security frameworks, not civilian product regulation. The practical effect is that the most capable and highest-risk AI deployments — those designed to accelerate lethal decision-making — are subject to the least regulatory oversight.

This creates a systematic misalignment between AI capability governance and risk. Enterprise AI platforms that deploy identical underlying models for civilian and military applications face rigorous compliance obligations for the civilian use case and none for the military one. The civil-military pipeline (§1.2) thus functions as a regulatory arbitrage: capabilities are refined under regulatory pressure in civilian contexts and deployed without that pressure in military ones.

### 5.2 US DoD AI ethics principles

The US Department of Defense adopted a set of AI ethics principles in 2020: Responsible, Equitable, Traceable, Reliable, and Governable (DoD, 2020). These principles are articulated at a level of abstraction that does not directly constrain any specific system design. "Governable" requires that AI systems "be designed and engineered to fulfil their intended functions while possessing the ability to detect and avoid unintended harm or disruption" — a standard that most current autonomous systems could claim to meet by design specification, regardless of whether they meet it in practice.

The principles represent a normative aspiration rather than an enforceable standard, and their implementation is at the discretion of individual program offices. Mittelstadt (2019) demonstrates that voluntary ethics frameworks cannot guarantee ethical AI: they function primarily as reputational management, allowing organisations to claim ethical compliance without creating enforceable obligations or external accountability mechanisms.

### 5.3 The research and governance frontier

The deepest unsolved problems at the intersection of agentic AI and defense deployment are not technical but legal and governance questions: What constitutes meaningful human control when AI decision latency is measured in milliseconds and human cognitive cycles in seconds? How should accountability be assigned when an autonomous system causes unlawful harm in a context where no human made the specific targeting decision? Can the civil-military pipeline be regulated without militarising civilian AI development?

These questions are live before international bodies. The UN Group of Governmental Experts on LAWS (Lethal Autonomous Weapons Systems) has been convening since 2014 without reaching a binding framework (Altmann & Sauer, 2017). The International Committee of the Red Cross has called for new international rules specifically addressing autonomous weapons (ICRC, 2021). As of 2026, no binding international instrument governs the use of autonomous weapons systems; Bode (2023) and Bode and Watts (2021) document how the practice of operational deployment has run substantially ahead of normative deliberation, with state behaviour in air-defence systems already establishing precedents that pre-empt the regulatory process.

---

## Key Sources

- Bode, I., & Watts, T. (2021). *Meaning-less human control: Lessons from air defence systems on meaningful human control for the debate on AWS* (Center for War Studies Research Report). Drone Wars UK / University of Southern Denmark. [R] [OA cit: 6] — Research report analysing operational Patriot, Aegis, and Iron Dome air-defence deployments and arguing that decades of human-on-the-loop practice in air defence have already established a de facto standard that drains "meaningful human control" of its protective content. Anchors §5.3 claim that operational state practice has run ahead of normative deliberation. Tri-source verification 2026-05-15: OpenAlex (no DOI; SDU Research Portal record confirms authors, title, and year). **Citation correction (2026-05-15):** the v0.2 source line listed this paper as *Humanities and Social Sciences Communications* 10, 187 (2023), DOI 10.1057/s41599-023-01796-3; the DOI 404s at the DOI registry and OpenAlex has no record at that identifier. The fabricated venue/year/DOI have been stripped; the real 2021 SDU CWS report is now cited. *(executor-added 2026-05-11; corrected 2026-05-15)*

- Bode, I. (2023). Practice-based and public-deliberative normativity: Retaining human control over the use of force. *European Journal of International Relations*, *29*(4), 990–1016. https://doi.org/10.1177/13540661231163392 [J] [OA cit: 29] — Peer-reviewed reinforcement for the §5.3 claim that state behaviour with semi-autonomous air-defence systems has set normative precedent ahead of the LAWS deliberative process. Argues that "practice-based normativity" — what states actually do operationally — is shaping the legal interpretation of meaningful human control more than treaty negotiations. CrossRef `update-to[]` empty (no retraction or correction) verified 2026-05-15. *(executor-added 2026-05-15)*

- Altmann, J., & Sauer, F. (2017). Autonomous weapon systems and strategic stability. *Survival*, *59*(5), 117–142. https://doi.org/10.1080/00396338.2017.1375263 [J] [OA cit: 152] — peer-reviewed review of the international governance of autonomous weapons including the UN GGE LAWS negotiation process from its 2014 inception; directly anchors the "convening since 2014 without reaching a binding framework" claim in §5.3. OpenAlex DOI lookup confirmed first authors and venue (verified 2026-05-08). *(executor-added 2026-05-08)*

- Anduril Industries. (2024). *Lattice OS*. https://www.anduril.com/lattice/ [R] — product documentation; primary source on Anduril architecture

- Insinna, V. (2023, August). Scale AI unveils Donovan intelligence platform for Pentagon users. *Breaking Defense*. [R] — trade press reporting on Donovan launch and classified-network deployment; independent corroboration of Scale AI, 2023

- Simonite, T. (2018). For some defense contractors, Google's Maven controversy is good news. *Wired*. [R] — documents competitor companies, including Palantir, positioning to fill gap left by Google's Maven exit

- Statt, N. (2019). How Palmer Luckey's defense startup Anduril wants to build the future of war. *The Verge*. [R] — primary journalism source for Luckey's stated founding thesis on incumbent defense industry shortcomings

- Wakabayashi, D., & Shane, S. (2018, June 1). Google will not renew Pentagon contract that upset employees. *The New York Times*. https://www.nytimes.com/2018/06/01/technology/google-pentagon-project-maven.html [R] — primary record documenting Google's Maven exit and the "more than 4,000 employees" petition figure

- Brundage, M., Avin, S., Clark, J., Toner, H., Eckersley, P., et al. (2018). *The malicious use of artificial intelligence: Forecasting, prevention, and mitigation*. arXiv:1802.07228. https://doi.org/10.48550/arxiv.1802.07228 [P] [OA cit: 491] — Foundational dual-use AI analysis documenting how AI capabilities developed for civilian applications are directly transferable to adversarial and military contexts with minimal adaptation; empirical and policy anchor for the §1.2 civil-military pipeline / regulatory-arbitrage claim. *(executor-added 2026-05-13)*

- Payne, K. (2018). Artificial intelligence: A revolution in strategic affairs? *Survival*, *60*(5), 7–32. https://doi.org/10.1080/00396338.2018.1518374 [J] [OA cit: 118] — Peer-reviewed analysis of how AI transforms military strategic competition by accelerating decision cycles at each phase of the OODA loop — faster intelligence fusion (Observe), simultaneous synthesis across large information sets (Orient), and automated option generation (Decide); directly anchors §3 AI-acceleration mapping. *(executor-added 2026-05-13)*

- Osinga, F. P. B. (2013). 'Getting' *A Discourse on Winning and Losing*: A primer on Boyd's theory of intellectual evolution. *Contemporary Security Policy*, *34*(3), 603–624. https://doi.org/10.1080/13523260.2013.849154 [J] [CrossRef cit: 14; S2 iCit: 0 — below automated S2 iCit threshold but explicitly specified in annotation as the canonical peer-reviewed Boyd treatment; *Contemporary Security Policy* is Taylor & Francis flagship peer-reviewed journal in strategic theory] — peer-reviewed journal article placing Boyd's OODA loop in its intellectual history and strategic-theory context; substitutes for unpublished Boyd (1995) briefing slides at §3 OODA loop definition. *(executor-added 2026-05-19)*
- Osinga, F. P. B. (2007). *Science, strategy and war: The strategic theory of John Boyd*. Routledge. [book] — comprehensive scholarly synthesis of Boyd's strategic theory; retained for supplementary depth; unpublished Boyd (1995) slides reference removed.

- Crawford, K. (2021). *Atlas of AI: Power, politics, and the planetary costs of artificial intelligence*. Yale University Press. [J/book] — see LIBRARY-WISHLIST; chapter on military AI and voluntary ethics frameworks

- Heuer, R. J. (1999). *Psychology of intelligence analysis*. Central Intelligence Agency. [book] [OA cit: 76] — foundational manual on cognitive biases and judgment processes in intelligence analysis; provides empirical grounding for the §2.2 claim that intelligence synthesis work previously required "hours of manual synthesis" — the cognitive-load baseline that Donovan aims to reduce. *(executor-added 2026-05-18)*

- International Committee of the Red Cross. (2021). *ICRC position on autonomous weapon systems*. ICRC. https://www.icrc.org/en/document/icrc-position-autonomous-weapon-systems [R]

- Palantir Technologies. (n.d.-a). *Palantir Artificial Intelligence Platform (AIP)*. https://www.palantir.com/platforms/aip/ [R]

- Palantir Technologies. (n.d.-b). *Foundry Ontology overview*. Palantir Documentation. https://www.palantir.com/docs/foundry/ontology/overview/ [R]

- Brayne, S. (2020). *Predict and surveil: Data, discretion, and the future of policing*. Oxford University Press. [book] — Ethnographic study of Palantir Gotham deployment at LAPD; provides independent scholarly analysis of Palantir's architecture-in-practice for governance and authority thresholds, contrasting vendor claims (§1.1) with operational reality at law enforcement scale. Addresses §1.1 outstanding gap "independent peer-reviewed verification of Palantir Foundry's ontology and Action-authority claims beyond vendor documentation." Added to LIBRARY-WISHLIST for acquisition. *(executor-added 2026-05-18)*

- Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, *52*(3), 381–410. https://doi.org/10.1177/0018720810376055 [J] [OA cit: 1291] — foundational review of automation bias and complacency in supervisory control contexts; canonical human-factors grounding for the "automation bias at scale" claim in §4.1. CrossRef `update-to[]` empty (no retraction or correction) verified 2026-05-08. *(executor-added 2026-05-07; metrics + retraction-clean verification 2026-05-08)*

- Horowitz, M. C., & Kahn, L. (2024). Bending the automation bias curve: A study of human and AI-based decision making in national security contexts. *International Studies Quarterly*, *68*(2), sqae020. https://doi.org/10.1093/isq/sqae020 [J] [OA cit: 35] — Pre-registered survey experiment (n ≈ 9,000) measuring automation bias in a simulated national-security decision task. Demonstrates that exposure to algorithmic recommendations induces measurable bias toward system advice but that disclosure of system confidence and accuracy attenuates the effect — making the bias curve "bendable" through interface design. Direct empirical anchor for §4.1's automation-bias-at-scale paragraph; addresses the v0.2 outstanding gap "empirical case studies of automation bias in military AI." arXiv preprint (2306.16507) downloaded to `Kilder/Horowitz2024_BendingAutomationBiasCurve_arXiv2306.16507.pdf`. CrossRef `update-to[]` empty (no retraction or correction) verified 2026-05-15. *(executor-added 2026-05-15)*

- Noy, S., & Zhang, W. (2023). Experimental evidence on the productivity effects of generative artificial intelligence. *Science*, *381*(6654), 187–192. https://doi.org/10.1126/science.adh2586 [J] [OA cit: 1226] — Randomised controlled experiment (MIT Sloan) demonstrating that generative AI significantly reduces task completion time and cognitive load in professional writing tasks; peer-reviewed productivity anchor for §2.2 LLM-assisted analysis cognitive-load claim. OA citation count refreshed via OpenAlex DOI lookup 2026-05-15; CrossRef `update-to[]` empty (no retraction or correction) verified same date. *(executor-added 2026-05-13; metrics + retraction-clean verification 2026-05-15)*

- Roff, H. M. (2014). The strategic robot problem: Lethal autonomous weapons in war. *Journal of Military Ethics*, *13*(3), 211–227. https://doi.org/10.1080/15027570.2014.975010 [J] [OA cit: 145] — Peer-reviewed analysis of the "meaningful human control" concept in autonomous weapons discourse from the period of its conceptual origin; directly anchors §4.1 genealogy claim that MHC "has resisted precise legal definition." DOI and OA cit added via OpenAlex DOI lookup 2026-05-15; CrossRef `update-to[]` empty (no retraction or correction) verified same date. *(executor-added 2026-05-13; metrics + retraction-clean verification 2026-05-15)*

- Roff, H. M., & Danks, D. (2018). "Trust but verify": The difficulty of trusting autonomous weapons systems. *Journal of Military Ethics*, *17*(1), 2–20. https://doi.org/10.1080/15027570.2018.1481907 [J] [OA cit: 54] — anchors §4.1 epistemic argument that meaningful human oversight presupposes the human's ability to evaluate the system's reasoning, which fails in high-dimensional sensor environments. CrossRef `update-to[]` empty (no retraction). Unpaywall is_oa: False — paywalled at Taylor & Francis; added to LIBRARY-WISHLIST. **Citation correction (2026-05-08):** the v0.1 entry had attributed this paper to *Science and Engineering Ethics*, *24*(3), 733–751 — that DOI (10.1007/s11948-016-9852-4) resolves to a different paper ("Educational Encounters of the Third Kind", Génova & González, 2016). Correct venue/pages verified via CrossRef title+author search.

- Scale AI. (2023). *Donovan: AI for national security*. https://scale.com/donovan [R]

- Santoni de Sio, F., & Mecacci, G. (2021). Four responsibility gaps with artificial intelligence: Why they matter and how to address them. *Philosophy & Technology*, 34(4), 1057–1084. https://doi.org/10.1007/s13347-021-00450-x [J] [OA cit: 364] — peer-reviewed anchor for §4.2 accountability-gap argument; provides a taxonomy of four distinct AI responsibility gaps (many-hands, action-guidance, explanation, and moral-disengagement) directly supporting the claim that autonomous-weapon responsibility is diffused across developers, commanders, and policymakers in ways legal frameworks cannot cleanly assign. *(executor-added 2026-05-11)*

- Sparrow, R. (2007). Killer robots. *Journal of Applied Philosophy*, *24*(1), 62–77. https://doi.org/10.1111/j.1468-5930.2007.00346.x [J] [S2 iCit: 36] — canonical peer-reviewed argument that autonomous weapons create a moral responsibility gap in which no human agent can be held accountable for targeting decisions; foundational for §4.2 accountability-gap claim and carries the argument independently of the unacquired Scharre (2018) monograph. *(executor-added 2026-05-19)*

- Scharre, P. (2018). *Army of none: Autonomous weapons and the future of war*. W. W. Norton. [J/book] — see LIBRARY-WISHLIST; definitive treatment of autonomous weapons policy and accountability gaps

- United States Department of Defense. (2020). *AI ethics principles for DoD*. https://www.defense.gov/News/Releases/Release/Article/2091996/dod-adopts-ethical-principles-for-artificial-intelligence/ [R]

- European Parliament and Council of the European Union. (2024). *Regulation (EU) 2024/1689 (EU AI Act)*, Article 2(3). Official Journal of the European Union. [R]

- Insinna, V. (2021, December 7). Anduril's Lattice software adds new capabilities, including collaborative autonomy. *Breaking Defense*. [R] — independent trade-press analysis of Lattice sensor-fusion and multi-domain autonomous coordination; supplements Anduril's own product documentation (Anduril Industries, 2024) in §2.1. *(executor-added 2026-05-10)*

- Palantir Technologies. (2023, April 26). *Palantir launches its Artificial Intelligence Platform (AIP)* [Press release]. https://www.palantir.com/newsroom/press-releases/ [R] — dated primary source establishing the April 2023 AIP launch and the unified LLM integration layer spanning Foundry and Gotham; anchors §1.2 "2023 introduction" and shared-architecture claims. *(executor-added 2026-05-10)*

- United States Department of Defense. (2023, November 21). *Directive Number 3000.09: Autonomy in Weapon Systems* (Updated). Under Secretary of Defense for Policy. https://www.esd.whs.mil/Portals/54/Documents/DD/issuances/dodd/300009p.pdf [R] — foundational US DoD policy document establishing human supervisory-control (on-the-loop) requirements for autonomous weapon systems; primary authority for "dominant model in current Western military doctrine" in §3. *(executor-added 2026-05-10)*

- Brayne, S. (2020). *Predict and surveil: Data, discretion, and the future of policing*. Oxford University Press. [J/book] — see LIBRARY-WISHLIST; ethnographic study of Palantir Gotham at LAPD; key source for §1.2 dual-use pipeline

- Mittelstadt, B. (2019). Principles alone cannot guarantee ethical AI. *Nature Machine Intelligence*, *1*, 501–507. https://doi.org/10.1038/s42256-019-0114-4 [J] [OA cit: 1417] — argues that voluntary AI ethics principles function primarily as reputational claims without enforceable obligations or external accountability mechanisms; directly anchors §5.2 reputational-management critique of DoD voluntary ethics framework. CrossRef retraction sweep clean. *(executor-added 2026-05-11)*

- Ekelhof, M. A. C. (2019). Moving beyond semantics on autonomous weapons: Meaningful human control in operation. *Global Policy*, *10*(3), 343–348. https://doi.org/10.1111/1758-5899.12665 [J] [iCit: 7] — peer-reviewed operational analysis of how "human on the loop" supervisory control functions across NATO and allied state military deployments; documents that the supervisory-control / human-on-the-loop model is the de facto operational standard in Western armed forces, providing multi-state comparative scope that broadens the US DoD 3000.09 primary source in §3. *(executor-added 2026-05-16)*

- Franklin, M., Tomašev, N., Jacobs, J., Leibo, J. Z., & Osindero, S. (2026). AI agent traps. SSRN preprint. https://doi.org/10.2139/ssrn.6372438 [P] [OA cit: 0 — too new] — first systematic framework for adversarial attacks on web-navigating AI agents; identifies six attack categories: (1) Content Injection Traps (exploit gap between human perception and machine parsing), (2) Semantic Manipulation Traps (corrupt agent reasoning and internal verification), (3) Cognitive State Traps (target long-term memory and learned behavioural policies), (4) Behavioural Control Traps (hijack agent capabilities for unauthorised actions), (5) Systemic Traps (use agent interaction to create ecosystem-wide failure), (6) Human-in-the-Loop Traps (exploit cognitive biases in human overseers). Primary anchor for §2 (agentic attack surface) and §4 (defence architecture); also relevant to Draft BF §9 (deliberate corpus infection — attack type 1–2) and Draft E (LLM structural vulnerabilities). *(added 2026-05-18)*

---

## Open Questions

1. **Meaningful human control — operationalisation:** No jurisdiction has defined "meaningful human control" with sufficient specificity to function as an engineering requirement. What would a testable operationalisation look like, and who would conduct the tests?

2. **The accountability vacuum:** When a fully autonomous system causes an unlawful killing, under current international law no individual bears clear criminal responsibility. Is new law needed, or can existing frameworks (command responsibility, product liability) be extended?

3. **Civil-military pipeline governance:** Should AI systems that will be used in both civilian and military contexts be subject to a single highest-standard regulatory regime? How would this be enforced across jurisdictions with different military sovereignty claims?

4. **Palantir's Ontology in contested environments:** The Ontology-as-shared-state architecture assumes reliable, low-latency data connectivity. In contested electromagnetic environments (jamming, spoofing), the shared ontology can be corrupted or denied. What are the failure modes when the shared state itself is the attack surface?

5. **Democratic accountability for defense AI procurement:** Defense AI platforms are procured through classified or quasi-classified processes with limited legislative oversight. How should democratic accountability for AI systems that may make lethal recommendations be structured?
