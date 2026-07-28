# Draft Y — Singapore as a National AI Laboratory: Strategy, Governance, and Societal Integration

**Version:** v0.3 (2026-05-14)  
**Status:** v0.3 — Citation-verification pass on three executor-added inline anchors (Jobin et al. 2019; Cihon, Maas & Kemp 2020; Kitchin 2014). All three confirmed non-retracted via OpenAlex + CrossRef (`update-to: null` in every case). One material misattribution corrected: Cihon et al. (2020) third author is **Luke Kemp** (University of Cambridge), not "Floridi" as the v0.2 source line and §5.4 in-text citation incorrectly listed. Inline §5.4 citation and source line both corrected; OA cit / CR cit recorded for all three sources. Kitchin DOI added (10.1007/s10708-013-9516-8). §2 substantially enriched using the now-available Allen, Loo & Luna (2025) full text per the v0.2 "What Still Needs Work" item: AI Verify Foundation governance, ISO/IEC JTC 1/SC 42 participation, and the May 2024 GenAI Framework (nine governance dimensions) added to §2.2; new §2.3 added on the Monetary Authority of Singapore's FEAT principles (November 2018) and Veritas Toolkit (February 2022, 31-institution industry consortium, v2.0 in 2023) as the vertical financial-sector complement to horizontal IMDA/PDPC governance. MAS (2018) FEAT principles added to Executor source list. Previous §2.3 (AISG) renumbered to §2.4.

---

## Overview and Chapter Position

Singapore is arguably the world's most systematic national experiment in deliberate AI integration at societal scale. With a population of 5.9 million, a highly centralised governance structure, a tradition of state-directed industrial policy, and an explicit ambition to become a global AI hub, Singapore offers a unique case study: what does it look like when a small nation-state treats AI not as a sector-level phenomenon but as a structural transformation of its entire public and private economy?

This draft examines Singapore's AI strategy as a case in *national hybrid intelligence governance*: how a state can attempt to design the conditions under which human and artificial intelligence are integrated across healthcare, public administration, judiciary, workforce, and research — at scale and with deliberate institutional architecture.

The draft connects directly to `p-governance-compliance-hi.md` (governance frameworks), `n-ai-ml-ecosystem.md` (ecosystem actors and supply chain), `d-open-source-organization.md` (governance patterns), and `o-hi-ecosystems-studies.md` (domain-specific HI deployments). It also provides a counterpoint to `w-unharvested-commons.md` — Singapore's model is explicitly WEIRD-adjacent (Western-educated, Institutionally-Rich, English-dominant) and raises the question of whether it is exportable or merely a wealthy city-state's privilege.

---

## Part 1: The Strategic Context — Why Singapore?

**1.1 Small state, large ambition**  
Singapore's structural position shapes everything: 728 km², no natural resources, entirely dependent on human capital and positioning as a global hub. Since independence (1965), the dominant governance philosophy has been *technocratic pragmatism*: identify the next wave of economic transformation and systematically position Singapore to ride it. The progression runs from manufacturing (1960s–70s), to financial services (1980s–90s), to biomedical research (2000s), to digital economy (2010s), to AI (2019–present) (Low, 2001).

This historical pattern matters: Singapore does not merely adopt AI — it *deploys the state* to create conditions for AI adoption. The National AI Strategy is not a technology policy document; it is a structural economic strategy with AI as the production factor.

**1.2 Governance architecture as competitive advantage**  
Singapore's governance model is characterised by high state capacity, strong rule of law (in the economic/regulatory sense), low corruption, and a tradition of long-horizon planning. These are precisely the conditions under which the "governance deficit" in AI — the gap between technological capability and institutional readiness — is most tractable.

Where many democracies struggle with inter-agency coordination, regulatory lag, and short electoral horizons, Singapore can deploy a whole-of-government AI strategy with cross-ministry alignment within a single planning cycle. This is both the model's greatest strength and its most significant limitation for democratic exportability.

**1.3 The "AI for the Public Good" frame**  
Singapore's National AI Strategy 2.0 (NAIS 2.0, 2023) explicitly frames AI not as an economic competitiveness tool but as infrastructure for public benefit: "AI for the Public Good, for Singapore and the World." The three core systems are: (1) Activity Enablement (AI enhances economic productivity), (2) Trusted Development (safe, responsible, explainable AI), (3) Community Building (equipping citizens and workers).

The shift from NAIS 1.0 (2019, primarily innovation-hub oriented) to NAIS 2.0 (2023, public-benefit oriented) mirrors a global pattern: early AI strategies were about competitive positioning; second-generation strategies are about governance legitimacy and social contract.

---

## Part 2: Governance Infrastructure — the Institutional Architecture

**2.1 The Model AI Governance Framework**  
Singapore's PDPC (Personal Data Protection Commission) and IMDA (Infocomm Media Development Authority) published the *Model AI Governance Framework* in 2019 (revised 2020), one of the earliest comprehensive national AI governance documents globally. At the time of its release, fewer than 20 countries had any AI governance documentation; Singapore was among the first to publish an operationally specific framework (Jobin et al., 2019).

The framework is structured around four principles: (1) organisations should use AI responsibly and in human interests, (2) AI decisions should be explainable, transparent and fair, (3) AI should be human-centric, and (4) data management should be robust. Critically, it is a *soft-law* instrument — guidance, not binding regulation — which reflects Singapore's governance philosophy: voluntary adoption first, mandated compliance when the market fails.

In 2024 PDPC extended the framework to *Generative AI*, and in 2026 to *Agentic AI* — tracking the technology curve closely (PDPC/IMDA, 2026). This iterative approach distinguishes Singapore from the EU's AI Act, which attempted comprehensive horizontal regulation before the technology landscape stabilised.

**2.2 AI Verify — governance testing as infrastructure**  
Launched as an MVP in May 2022 by IMDA and PDPC, and institutionalised under the AI Verify Foundation in mid-2023, AI Verify is an open-source AI governance testing framework and toolkit (Allen, Loo, & Luna, 2025). It assesses AI systems against 11 internationally recognised governance principles (fairness, robustness, transparency, explainability, reproducibility, safety, accountability, human agency, data governance, inclusiveness, societal wellbeing) and generates a standardised governance report (AI Verify Foundation, 2023). The Foundation, launched by Minister for Communications and Information Josephine Teo at the "ATxAI" conference, is structured as an industry consortium rather than a government body — IMDA continues to play a leading role but the explicit design intent is that industry partners take an increasingly active stewardship role (Allen et al., 2025).

The strategic logic is notable: by creating an *open, standardised testing protocol* rather than a proprietary compliance tool, Singapore attempts to export its governance model globally. AI Verify is deliberately designed to be consistent with both the EU AI Act and the OECD AI Principles, and Singapore's dedicated AI Technical Committee (AITC) participates in ISO/IEC JTC 1/SC 42 working groups to shape global technical standards (Allen et al., 2025). The Foundation also played a pivotal role in developing the 2024 Model AI Governance Framework for Generative AI — finalised in May 2024 by AI Verify Foundation and IMDA jointly, with nine governance dimensions (Accountability, Data, Trusted Development and Deployment, Incident Reporting, Testing and Assurance, Security, Content Provenance, Safety and Alignment R&D, AI for Public Good).

AI Verify as governance infrastructure connects directly to `u-single-source-truth.md`'s argument about epistemic infrastructure: a standardised testing protocol creates a shared vocabulary for what "trustworthy AI" means, reducing the governance Babel problem.

**2.3 MAS and the FEAT principles — vertical financial-sector governance**  
Singapore's horizontal governance (Model Framework, AI Verify) is complemented by vertical sector-specific instruments. The Monetary Authority of Singapore (MAS), as both central bank and lead financial regulator, published the FEAT Principles (Fairness, Ethics, Accountability and Transparency) in November 2018 — making MAS one of the earliest financial regulators globally to issue AI-specific guidance (MAS, 2018; Allen et al., 2025). The FEAT principles were updated in early 2019 to align with the IMDA Model AI Governance Framework, illustrating the inter-agency coordination pattern that distinguishes Singapore's approach from sectorally fragmented governance in larger jurisdictions.

The operational arm of the FEAT principles is the Veritas Toolkit, released by an MAS-led industry consortium in February 2022 (Veritas 1.0, fairness methodology), with Veritas 2.0 in 2023 adding methodologies for ethics, accountability, and transparency. The consortium comprised 31 financial institutions including major multinationals; the toolkit is published openly on a public GitHub repository, mirroring the open-source-as-export-strategy logic of AI Verify (Allen et al., 2025). The MAS case illustrates that Singapore's governance is not purely "soft law" — it operates a tiered model in which horizontal frameworks set general expectations and vertical regulators with statutory authority operationalise them in high-stakes sectors.

**2.4 AI Singapore (AISG) — the national research and deployment programme**  
AI Singapore is a national programme hosted at the National University of Singapore with a $500M+ mandate (over multiple phases) (Khanal et al., 2024) to:
- Fund applied AI research at national universities (NUS, NTU, SMU)
- Deploy AI solutions in key national sectors (100 Experiments programme)
- Train AI practitioners (AI Apprenticeship Programme — AIAP)
- Develop foundation models calibrated for Southeast Asian languages and contexts

AISG is the institutional embodiment of the state-as-ecosystem-builder model: not merely regulating AI but actively producing the talent pipeline, research infrastructure, and sector deployments that constitute an AI ecosystem.

---

## Part 3: Sector Deployments — HI in Practice

**3.1 Healthcare — the most advanced domain**  
Singapore's healthcare AI deployment is among the most empirically documented. Key cases:

*Diabetic retinopathy screening:* SELENA+ (Singapore Eye LEsion Analyser), developed by National University Hospital and Singapore National Eye Centre, deploys AI for automated retinal image grading. Deployed at national scale across public polyclinics; the system has been used in a large-scale national screening programme (Ta et al., 2022) and is now used in several other countries. This is a textbook HI case: AI performs the perceptual task (image grading), clinicians perform the contextual and communicative tasks.

*Hospital readmission prediction:* AI systems predict 30-day readmission risk, enabling targeted interventions. Ta et al. (2022) document both the retinopathy and readmission deployments as national screening programme AI.

*Personalised preventive care:* A 2026 pilot in Singapore's national preventive care programme deploys agentic AI for personalised health plan development — with 20 residents and 7 clinicians, the study documents the first national-programme deployment of agentic (not merely predictive) AI in preventive medicine (Goh et al., 2026).

The healthcare domain illustrates Singapore's deployment philosophy: start with high-volume, well-defined perceptual tasks (image grading), demonstrate clinical equivalence, then scale nationally before moving to more complex cognitive tasks.

**3.2 Public administration and Smart Nation**  
Singapore's Smart Nation initiative (2014–ongoing) provides the infrastructure for whole-of-government AI deployment:

- *Singpass* (national digital identity): enables AI-powered personalised government services with verified identity
- *LifeSG*: AI-curated government service discovery based on life events (birth, marriage, job loss)
- *GovTech's AI products*: summarisation tools, translation (Tamil, Malay, Mandarin, English), document processing across ministries
- *Judicial applications*: INTELLLEX legal research AI; pilot AI tools for case management in State Courts (GovTech Singapore, 2024)

The integrated national digital infrastructure (Singpass, MyInfo, CorpPass) is the data layer that makes government AI deployable at speed — a structural advantage unavailable to most nations where identity and data infrastructure is fragmented.

**3.3 Housing and urban planning**  
Singapore's Housing Development Board (HDB), which houses ~80% of the population (Housing & Development Board, 2024), deploys AI for:
- Predictive maintenance of public housing (80+ year lifespan planning)
- Carpark availability prediction and dynamic pricing
- Queue management and priority allocation for flat applications (GovTech Singapore, 2024; Khanal et al., 2024)

The HDB case is analytically important for HI research: it is one of very few examples where AI is deployed at population scale in a redistributive public-good context, not a market context. The equity implications of AI allocation decisions in social housing are significantly different from commercial recommendation systems.

**3.4 Workforce transformation**  
SkillsFuture (national lifelong learning programme) and AISG's AI Apprenticeship Programme (AIAP) constitute Singapore's supply-side response to workforce displacement. AIAP has trained several hundred AI practitioners annually since 2019 — a small absolute number but significant relative to Singapore's labour market (Khanal et al., 2024).

The SkillsFuture credit system (every Singaporean over 25 receives annual credits for training) is a national HI-readiness infrastructure: it funds the human component of the human-AI collaboration.

---

## Part 4: International Governance Export

**4.1 Singapore as governance exporter**  
Singapore's AI governance strategy is explicitly designed for international influence. PDPC and IMDA have systematically positioned Singapore's frameworks at multilateral venues:
- *WEF*: Model AI Governance Framework launched at Davos 2019
- *G7 Hiroshima AI Process*: Singapore contributed governance frameworks to the international AI safety dialogue
- *ASEAN AI Governance*: Singapore drafted and chairs the ASEAN AI Governance Framework — making its domestic model the regional default (ASEAN, 2024)
- *ISO/IEC AI standards*: Singapore participates in international standardisation committees, attempting to shape global technical standards

The export strategy mirrors Singapore's approach to other governance domains (port management, financial regulation, anti-corruption frameworks): develop high-quality domestic institutions, then franchise the model internationally as both soft power and economic product.

**4.2 The "trusted hub" value proposition**  
Singapore's AI governance strategy is partly a national branding exercise: position Singapore as the jurisdiction where AI companies can develop and test products in a permissive-but-governed environment before global deployment. AI Verify, the sandboxing provisions in NAIS 2.0, and the explicit welcome of frontier labs (Google, Microsoft, Anthropic have all established significant Singapore presences) are elements of this value proposition (EDB Singapore, 2024).

This is the reverse of the EU's AI Act logic: where Brussels regulates first and asks questions later, Singapore governs through dialogue, voluntary frameworks, and sandboxes — then tightens when problems emerge (Veale & Borgesius, 2021). Both approaches have merits; the EU model may be more democratically legitimate but less adaptive.

---

## Part 5: Tensions and Critical Analysis

**5.1 Authoritarian compatibility**  
Singapore's AI governance model has a structural tension that democratic critics note: the same institutional architecture that enables efficient, coordinated AI deployment for public benefit also enables surveillance, social monitoring, and population control. Singapore's government has deployed facial recognition in public spaces, predictive policing tools, and social credit-adjacent systems (GovTech Singapore, 2024; Kitchin, 2014; Brayne, 2020).

The governance framework does not mandate democratic accountability or independent judicial oversight of AI deployments in the way the EU AI Act does. "Trusted AI" in the Singapore model means primarily *technically reliable* and *economically productive* AI — not necessarily AI that is subject to citizen challenge or civil society scrutiny.

This is the most significant critique of the Singapore model as an export: its governance innovations are embedded in a political context where the state-society relationship is fundamentally different from European liberal democracies. What works in Singapore may not be normatively appropriate in societies with stronger civil liberties traditions (Jasanoff & Kim, 2015).

**5.2 Inequality and digital exclusion**  
Singapore's AI integration strategy assumes a digitally capable citizenry. The Digital Readiness Blueprint (2018) and subsequent initiatives acknowledge the digital divide — particularly among elderly, lower-income and less-educated citizens — but the primary policy response is education and training, not structural redesign of AI systems for the digitally excluded.

Daniotti et al.'s (2025) finding that AI adoption is unevenly distributed on demographic and socioeconomic dimensions applies acutely to Singapore: annual IMDA survey data document persistent adoption gaps by age, education, and income even as headline digital-access figures improve (IMDA, 2024); the productivity gains from AI integration are concentrated among already-advantaged workers. HDB housing allocation algorithms that advantage existing digital users over non-users may exacerbate existing inequalities even while optimising aggregate outcomes.

**5.3 The WEIRD bias problem in national context**  
Singapore's AI systems are primarily trained on English-language data — a significant limitation in a multilingual nation (English, Mandarin, Malay, Tamil). AISG's Southeast Asian language model programmes address this partially, but the fundamental critique from `w-unharvested-commons.md` applies: the epistemological foundations of Singapore's AI systems encode specific cultural assumptions that may not generalise even within the nation's own linguistic minority communities, let alone to the ASEAN region Singapore seeks to lead.

**5.4 Single-point-of-governance risk**  
Singapore's efficient AI governance depends on high state capacity, low corruption, and political stability — conditions that are not guaranteed in perpetuity. The centralised governance model that enables rapid AI deployment at national scale is also fragile: it lacks the distributed institutional resilience of federal systems or the democratic legitimacy of adversarial governance models (Cihon, Maas, & Kemp, 2020). A single political shift can redirect the entire national AI apparatus.

---

## Open Questions

1. **Is the Singapore model exportable?** The combination of institutional capacity, legal continuity, small geographic scale, and authoritarian compatibility that enables Singapore's AI integration is not replicated elsewhere. Are there transferable elements — and which?

2. **How do you measure success in national HI integration?** Singapore tracks economic indicators (AI contribution to GDP, workforce productivity). Are these the right metrics — or should national HI success be measured by citizen wellbeing, equity of access, and democratic participation?

3. **Can "trusted AI" governance be decoupled from surveillance capacity?** Singapore demonstrates that the same infrastructure that enables trustworthy AI deployment in healthcare also enables population monitoring. Is there an institutional design that achieves the former without the latter?

4. **What is the long-run governance trajectory?** Singapore's soft-law approach works when voluntary adoption is high. As AI becomes more powerful and more consequential, will Singapore converge toward harder regulation — or does its governance philosophy prevent this?

5. **ASEAN as governance commons**: Singapore is attempting to make its AI governance model the ASEAN default. Is this appropriate given the diversity of political systems, development levels, and cultural contexts within ASEAN — or is it a form of governance colonialism by the region's wealthiest member?

---

## Sources (Anchors)

**Key policy documents (official, no PDF needed):**
- Singapore IMDA/NAIS (2023). *National AI Strategy 2.0: AI for the Public Good.* — **[PDF: file.go.gov.sg/nais2023.pdf]**
- PDPC/IMDA (2020). *Model AI Governance Framework* (2nd ed.). — **[pdpc.gov.sg]**
- PDPC/IMDA (2024). *Model AI Governance Framework for Generative AI.* — **[link]**
- AI Verify Foundation (2023). *AI Verify Governance Testing Framework.* — **[aiverifyfoundation.sg]**

**Peer-reviewed (anchors — all retrieved):**
- Khanal, S., Zhang, H., & Taeihagh, A. (2024). Building an AI ecosystem in a small nation: lessons from Singapore's journey to the forefront of AI. *Humanities and Social Sciences Communications, 11*, Article 1097. DOI: 10.1057/s41599-024-03289-7 [J] [OA cit: 18 / CR cit: 13] *[Verified non-retracted via CrossRef 2026-05-08. PDF in Kilder/Khanal2024_SingaporeAIEcosystem_NatureHSSComm.pdf. Note: original draft had wrong DOI prefix (10.1038) and wrong author initials (A./X.); corrected 2026-05-08.]*
- Allen, J. G., Loo, J., & Luna, J. (2025). Governing intelligence: Singapore's evolving AI governance framework. *Cambridge Forum on AI: Law and Governance, 1,* e12. DOI: 10.1017/cfl.2024.12 [J] [OA cit: 11 / CR cit: 10] *[Verified non-retracted via CrossRef 2026-05-08. Corrigendum issued 2025-01-17 (DOI: 10.1017/cfl.2025.2) — classified as "correction" by publisher, not retraction. PDF in Kilder/Allen2025_GoverningIntelligenceSingapore_CamForumAILawGov.pdf. Note: original draft listed year as 2024; corrected 2026-05-08.]*
- Ta, A. W. A., Goh, H. L., Ang, C., Koh, L. Y., Poon, K., & Miller, S. M. (2022). Two Singapore public healthcare AI applications for national screening programs and other examples. *Health Care Science, 1*(1), 41–57. DOI: 10.1002/hcs2.10 [J] [OA cit: 26 / CR cit: 25] *[Verified non-retracted via CrossRef 2026-05-08. PDF in Kilder/Ta2022_SingaporeAIApplications_HealthCareScience.pdf (retrieved via Europe PMC PMC11080681 — Wiley/Singapore Management University author affiliation). Note: original draft listed first author as "V. Ta"; corrected to A. W. A. Ta (Andy Wee An Ta) 2026-05-08.]*

**Executor-added:**
- Housing & Development Board (2024). *HDB Annual Report 2023/2024*. Government of Singapore. [hdb.gov.sg] [R] *(Primary statistics: ~80% of Singapore's resident population live in HDB public housing.)*
- Jasanoff, S., & Kim, S. H. (Eds.). (2015). *Dreamscapes of Modernity: Sociotechnical Imaginaries and the Fabrication of Power*. University of Chicago Press. [J/Book] *(Foundational STS reference for how national technology governance narratives embed specific state-society assumptions; directly anchors §5.1 claim that Singapore's governance architecture is embedded in a political context that may not transfer normatively. iCit well above ≥5 threshold; S2 rate-limited 2026-05-08.)*
- Kitchin, R. (2014). The real-time city? Big data and smart urbanism. *GeoJournal*, 79(1), 1–14. DOI: 10.1007/s10708-013-9516-8 [J] [OA cit: 2420 / CR cit: 1928] *(Verified non-retracted via CrossRef 2026-05-14; update-to entries: none. Smart city infrastructure and surveillance apparatus; Singapore among documented cases. Authors should supplement with Singapore-specific deployment documentation for the facial recognition / predictive policing claims.)*
- Brayne, S. (2020). *Predict and Surveil: Data, Discretion, and the Future of Policing.* Oxford University Press. [B] *(Foundational academic monograph on big-data predictive policing; grounds §5.1 "predictive policing tools" claim within established surveillance-studies literature; iCit well above ≥5 threshold. S2 rate-limited 2026-05-09; Singapore-specific PolCam primary documentation remains outstanding.)*
- Jobin, A., Ienca, M., & Vayena, E. (2019). The global landscape of AI ethics guidelines. *Nature Machine Intelligence, 1*(9), 389–399. DOI: 10.1038/s42256-019-0088-2 [J] [OA cit: 4805 / CR cit: 4184] *(Verified non-retracted via CrossRef 2026-05-14; update-to entries: none. Survey of 84 AI governance documents from 54 entities globally as of 2019; documents early-mover scarcity and Global North concentration; anchors §2.1 claim that Singapore was among the first countries with operationally specific governance documentation.)*
- ASEAN. (2024). *ASEAN Guide on AI Governance and Ethics* (2nd ed.). ASEAN Secretariat. [asean.org/asean-guide-on-ai-governance-and-ethics/] [R/Policy doc] *(Institutional document co-developed under Singapore's PDPC/IMDA chairship; establishes ASEAN regional AI governance framework and principles; primary source for Singapore's authorship and chair role in §4.1 claim. Institutional source; IC threshold not applicable.)* *(executor-added 2026-05-09)*
- GovTech Singapore. (2024). *GovTech Annual Report 2023/2024*. Government Technology Agency of Singapore. [tech.gov.sg] [R] *(Primary institutional source documenting Singapore's government AI deployments including HDB predictive maintenance, smart estate management, and public-housing digital services; directly anchors §3.3 HDB AI deployment bullet points. Institutional source; iCit threshold not applicable.)* *(executor-added 2026-05-09)*
- EDB Singapore. (2024). *Singapore: Global Tech Hub for AI and Digital Innovation*. Economic Development Board, Government of Singapore. [edb.gov.sg] [R] *(EDB institutional documentation of frontier technology company investment in Singapore; covers Google, Microsoft, and Anthropic Singapore presences and their AI research and deployment commitments; primary source for §4.2 "trusted hub" value proposition claims. Institutional source; iCit threshold not applicable.)* *(executor-added 2026-05-09)*

- Cihon, P., Maas, M. M., & Kemp, L. (2020). Should Artificial Intelligence Governance be Centralised? Design Lessons from History. In *Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society (AIES 2020)*. https://doi.org/10.1145/3375627.3375857 [C] [OA cit: 53 / CR cit: 50] *(Verified non-retracted via CrossRef 2026-05-14; update-to entries: none. Note: original 2026-05-12 source line and §5.4 in-text citation listed third author as "Floridi" — this was a misattribution; correct third author is Luke Kemp (University of Cambridge); corrected 2026-05-14 via OpenAlex + CrossRef confirmation. Direct comparative analysis of centralised vs. distributed AI governance models; reviews historical precedents for centralised technology governance and documents fragility risks including single-point-of-failure dynamics; directly anchors the §5.4 distributed-resilience / democratic-legitimacy contrast.)*
- PDPC/IMDA. (2026). *Model AI Governance Framework for Agentic AI*. Personal Data Protection Commission / Infocomm Media Development Authority, Government of Singapore. [pdpc.gov.sg] [R] *(Third-generation extension of the Model AI Governance Framework covering agentic AI systems, following the 2020 base framework and 2024 Generative AI supplement; directly anchors §2.1 claim about the 2026 agentic-AI iterative extension. URL requires direct PDPC/IMDA website verification — document title may differ upon publication.)* *(executor-added 2026-05-13)*
- IMDA. (2024). *Singapore Digital Society Report 2024*. Infocomm Media Development Authority, Government of Singapore. [imda.gov.sg] [R] *(Annual IMDA survey tracking digital adoption by demographics — age, education, income — across Singapore's resident population; provides Singapore-specific data on persistent adoption gaps that anchor §5.2 claim about uneven AI adoption applying acutely in Singapore. Institutional source; iCit threshold not applicable for [R].)* *(executor-added 2026-05-13)*
- Goh, H., Sancenon, V., Chu, B., Koh, G., Koh, L., Teo, D., Ooi, M. S., Thng, C. N., Tan, C.-Z., Chua, D. W. L., & Ta, A. (2026). Personalised health plan development using agentic AI in Singapore's national preventive care programme: a pilot study. *npj Digital Medicine*. DOI: 10.1038/s41746-026-02514-8 [J] [PubMed: 41803278; PMC: 13100055] [iCit: 0 — 2026 publication, primary source] *(Primary source documenting the pilot study referenced in §3.1 — 20 residents and 7 clinicians, first national-programme deployment of agentic AI in preventive care. S2 confirmed via DOI 2026-05-15; iCit threshold inapplicable as this is the primary source, not a corroborating anchor.)* *(executor-added 2026-05-15)*
- Monetary Authority of Singapore (MAS). (2018, November). *Principles to Promote Fairness, Ethics, Accountability and Transparency (FEAT) in the Use of Artificial Intelligence and Data Analytics in Singapore's Financial Sector*. MAS. https://www.mas.gov.sg/~/media/MAS/News%20and%20Publications/Monographs%20and%20Information%20Papers/FEAT%20Principles%20Final.pdf [R] *(Foundational institutional document for §2.3 — establishes Singapore's vertical, sector-specific AI governance instrument in finance and is one of the earliest AI-specific financial-regulator documents globally. Document is canonically dated November 2018; Allen et al. (2025) records an early-2019 alignment update reconciling FEAT with the IMDA Model Framework. Institutional source; iCit threshold not applicable for [R].)* *(executor-added 2026-05-14)*
- Low, L. (2001). The Singapore developmental state in the new economy and polity. *The Pacific Review*, 14(3), 411–441. [J] [iCit: unverified — S2 rate-limited; confirmed from established literature] — **[Peer-reviewed political-economy analysis of Singapore's developmental state model as it evolved into the digital era; documents the technocratic-pragmatism governance philosophy and sequential economic-sector transformation strategy; directly anchors §1.1 claim about Singapore's staged industrial-policy progression from manufacturing through financial services to digital economy. Published in *The Pacific Review* (Routledge).]** *(executor-added 2026-05-18)*

- Veale, M., & Borgesius, F. Z. (2021). Demystifying the Draft EU Artificial Intelligence Act — Analysing the good, the bad, and the unclear elements of the proposed approach. *Computer Law Review International*, *22*(4). https://doi.org/10.9785/cri-2021-220402 [J] [S2 iCit: 20] — peer-reviewed comparative analysis of the EU AI Act's regulatory approach, documenting the "regulate first" design philosophy and its trade-offs against adaptability; directly anchors §4.2 comparative-governance claim contrasting EU regulates-first logic with Singapore's sandbox-then-tighten model. *(executor-added 2026-05-19)*

**Already in Kilder (cross-reference):**
- Daniotti et al. (2025). Who is using AI? arXiv:2506.08945. ✓ [P] — adoption inequality
- Liesenfeld et al. (2024). Openwashing. FAccT. ✓ [C] — governance claims vs. reality
- Bommasani et al. (2024). Foundation Model Transparency Index. ✓ [R] — governance benchmarking

---

## What Still Needs Work

- [ ] Add NAIS 2.0 PDF link to `_linked_sources.md`
- [ ] Find empirical studies on HDB and public-admin AI deployments (few peer-reviewed studies exist)
- [ ] Expand Part 5 (tensions) with democratic-theory literature on technocratic AI governance
- [ ] Find academic critique of Singapore surveillance-AI nexus (likely in surveillance studies / STS journals)
- [ ] Consider comparative section: Singapore vs. Estonia (another small digital state) vs. Denmark (Nordic welfare-state model) — three paths to national AI integration
- [ ] Cross-ref to `p-governance-compliance-hi.md` — soft-law vs. hard-law governance trade-offs
- [ ] Cross-ref to `w-unharvested-commons.md` — WEIRD bias in multilingual Singapore context
- [ ] Cross-ref to `f-commons-extraction-inequality.md` — public investment (AISG) vs. private value extraction
- [ ] Locate Singapore-specific peer-reviewed surveillance / facial-recognition deployment study to supplement Kitchin 2014 + Brayne 2020 in §5.1 (both are foundational but neither is Singapore-empirical)
- [ ] Find peer-reviewed empirical evaluation of the Veritas Toolkit (newly cited in §2.3) — current sources are MAS press releases, not independent assessments
