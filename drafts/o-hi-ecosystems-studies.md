# Draft O — Hybrid Intelligence Ecosystems: A Synthesis of Empirical Studies

**Version:** v0.3 (2026-05-11)  
**Status:** literature overview and domain synthesis. Sources section: OpenAlex `cited_by_count` added to seven previously-pending preprint entries; Walsh-Wang-Ying (2025) and Bensch et al. (2025) resolved as Springer *Handbook of Human-Centered Artificial Intelligence* book chapters (DOI 10.1007/978-981-97-8440-0_6-1 and _40-1); Walsh author initials corrected (T./B./R. → S./Q./L.); Jeong et al. (2024, arXiv:2410.12010) flagged for re-attribution — actual paper is a cross-LLM fairness audit, not "bias amplification in AI-assisted decisions" as previously cited in §2.6. Topol (2019) retraction-free per CrossRef (`update-to: None`). In-depth per-study analysis still missing.

---

## Overview and Chapter Position

A *hybrid intelligence system* is a single configuration of human and AI. A *hybrid intelligence ecosystem* is something broader: the overall network of actors, systems, norms and institutions within a domain that shape how humans and AI interact and create value together.

This draft gathers empirical and theoretical studies that describe HI ecosystems — not as laboratory experiments but as observed phenomena in real domains. It answers: *which types of HI ecosystems are empirically documented, what characterises them, and what do we know about the conditions for them to function?*

The draft is the chapter's empirical foundation for the claims in `g-agentic-hi-collaboration.md` and `m-agentic-ai-taxonomies.md`, and it provides the concrete cases that illustrate the structural arguments in `n-ai-ml-ecosystem.md` and `f-commons-extraction-inequality.md`.

---

## Part 1: Foundational definitions and frameworks

**1.1 Dellermann et al. (2019) — the seminal HI definition**  
Dellermann's definition is the starting point for most of the recent HI literature:  
> "Hybrid Intelligence is the ability to achieve complex goals by combining human and artificial intelligence, thereby reaching superior results to those each of them could have accomplished separately."

Three core elements: (1) complex goals, (2) complementarity rather than substitution, (3) superiority over either alone. This is a normative definition — it describes not all configurations but those that *work*. Empirically it is an open question when the conditions are met.

**1.2 Lutz, Newlands & Jarrahi (2025) — three-layer framework**  
The most up-to-date and broadly applied theoretical framework for HI as a social phenomenon describes three levels:
- *Micro level*: individual cognitive interaction (decision support, augmentation)
- *Meso level*: organisational structures (division of labour, governance, roles)
- *Macro level*: institutional and societal consequences (norms, regulation, inequality)

The three-layer framework is useful because it explicitly connects individual-level psychology with societal-level consequences — something many technical HI studies omit.

**1.3 Raisch & Krakowski (2021) — Automate, Augment, Abandon**  
Three strategies for what organisations do with human tasks under AI adoption:
- *Automate*: AI replaces humans in the task
- *Augment*: human and AI share the task (HI configuration)
- *Abandon*: the task is dropped because AI makes it irrelevant

Implication: "hybrid intelligence" is not all configurations, but specifically the *augment* strategy. Empirically there is reason to think that neither pure automation nor pure augmentation is universally superior — context decides.

---

## Part 2: Domain-specific studies

### 2.1 Medicine — the best-documented HI domain

**Topol (2019) — High-Performance Medicine**  
Eric Topol's synthesis article in *Nature Medicine* is the most cited work on HI in clinical practice. The core argument: AI can outperform human clinicians in specific perceptual tasks (image diagnostics, ECG analysis, histopathology) but cannot replace clinical judgement, the narrative understanding of the patient, or the relational dimension of care. The optimum is therefore HI: AI handles data pattern recognition, the human handles context, communication and accountability.

Topol's *High-Performance Medicine* concept is an operational definition of HI in a concrete domain and is widely cited as the model for what HI should aim at.

**Empirical evidence for diagnostic HI:**  
- Dermatology: Esteva et al. (2017, *Nature*) showed that a CNN matched 21 board-certified dermatologists on biopsy-proven melanoma classification — but the comparison was AI vs. human, not AI+human; subsequent reader studies (e.g. Tschandl et al. 2020, *Nature Medicine*) found that combined performance depends heavily on how AI predictions are presented to clinicians, with poorly designed interfaces actually degrading expert judgement.
- Radiology: Ardila et al. (2019, *Nature Medicine*) — a deep-learning model trained on the NLST dataset reduced false positives by 11% and false negatives by 5% for lung-cancer screening, with model+radiologist outperforming the radiologist alone in retrospective comparison.
- Psychiatry: Fang et al. (2025, arXiv:2503.17473) — randomised controlled trial of chatbot-based psychosocial support showing measurable clinical effect, but raising the replacement-vs-supplement question that defines the HI/automation boundary.

The pattern across these three sub-domains: AI parity (or near-parity) on the perceptual task, but HI configuration is sensitive to **interface design** and **clinician trust calibration** — exactly the variables Schemmer et al. (2023) identify as the operational core of "appropriate reliance."

**2.2 Software development — the fastest-growing HI domain**

**Becker et al. (2025) — productivity study**  
Documents measurable productivity gains from AI-assisted code development. Key findings: AI assistance markedly reduces the time required to solve well-defined tasks; the effect is largest for mid-tier developers; the relative advantage of top programmers shrinks.

**Wang et al. (2025) — AI Code in the Wild**  
Empirical mapping of how AI-generated code looks in real codebases. Findings: AI code is identifiable via stylistic patterns; quality varies systematically with task type; review processes absorb part of the error rate.

**Wessel et al. (2022) — two complementary studies on GitHub bots**  
GitHub bots (automated software agents) integrated in pull-request workflows constitute an early, well-documented example of HI collaboration in software production.
- *Quality gatekeepers* (Wessel et al., 2022, *Empirical Software Engineering*) uses a regression discontinuity design on 1,194 GitHub projects to show that adopting code-review bots increases monthly merged pull requests, decreases monthly non-merged pull requests, and decreases inter-developer communication.
- *Bots for Pull Requests: The Good, the Bad, and the Promising* (Wessel et al., 2022, ICSE '22) is the qualitative companion piece — it documents how the same bot interactions can become disruptive and noisy, leading to information overload (the basis of the often-quoted "bot fatigue" effect: e.g. one developer reporting "20 notifications per day" from a single bot). Together the two papers establish the productivity gain *and* the cognitive cost — the dual signature of an early HI configuration.

**AutoGen (Wu et al. 2023)**  
The multi-agent framework that enables orchestration of LLM agents in software-development flows. Not an empirical study but a system design that documents how HI collaboration can be structured technically.

**2.3 Scientific research**

Science is potentially the domain with the highest HI synergy: AI can handle literature search, hypothesis generation, data analysis and simulations; humans contribute problem formulation, interpretation and domain expertise.

**AlphaFold (DeepMind, 2021)**  
Protein-structure prediction is the most dramatic example: AI solved a 50-year-old problem, but investigating what the results *mean* biologically continues to require human expertise. A pure HI example: AI solves a well-defined computational problem, biologists interpret the consequences.

**Agentic science (Chu et al. 2026, arXiv:2604.22748)**  
Describes a future of fully autonomous scientific agents — not as HI but as autonomous research. Relevant as contrast: when is scientific AI a tool (HI) and when is it an independent agent?

**2.4 Creative industries**

See `l-creativity-ai.md` for full treatment. Briefly: empirical evidence for creative HI is the weakest documented — most studies are case studies or experiments, not field observations of real creative HI systems.

**2.5 Spaceflight and safety-critical domains**

**Bensch et al. (2025) — Human-in/on-the-Loop in spaceflight**  
A concrete case study of how Human-in-the-Loop and Human-on-the-Loop are designed for safety-critical systems with high latency (communication delay to ISS, Mars). The domain forces explicit governance choices about autonomy level — a natural experiment for HI design.

**2.6 Legal systems and decision-making**

Predictive policing, risk-assessment tools in criminal justice (COMPAS), AI-assisted legal research. This is the HI domain with the most strongly documented failures: the systems reproduce and amplify structural bias (cf. `b-closed-models-risks.md`). Specific empirical anchor pending re-attribution — the previously cited Jeong et al. (2024, arXiv:2410.12010) was a cross-LLM fairness-audit study (*Bias Similarity Measurement*), not about decision-amplification; canonical anchors to substitute are Angwin et al. (2016, ProPublica COMPAS investigation) and Dressel & Farid (2018, *Science Advances*).

---

## Part 3: Cross-cutting findings

**3.1 The complementarity hypothesis — empirical status**  
The theory says: HI > AI alone and HI > human alone. Empirically the picture is nuanced:
- In *perceptual* tasks (image diagnostics, language understanding): AI often at par with or better than humans; HI may give a small additional gain
- In *cognitively complex* tasks (diagnosis with context, creative problem solving): HI consistently better
- In *socio-emotional* tasks (patient care, negotiation, leadership): humans consistently better, AI assistance may interfere

**3.2 Appropriate reliance — the central challenge**  
Schemmer et al. (2023) shows that HI systems function optimally only if the human *calibrates their trust correctly* in the AI component. Over-reliance (the human follows AI blindly) and under-reliance (the human ignores AI) are both failure states. Calibrated trust requires the human to understand the AI's strengths and weaknesses — which is itself a competence requirement.

**3.3 Theory of Mind as precondition**  
Walsh, Wang and Ying (2025) — a chapter in Springer's *Handbook of Human-Centered Artificial Intelligence* — argue that effective human-AI collaboration requires a form of *theory of mind* in both directions: the human must have a model of what the AI can and cannot do; the AI should (ideally) have a model of the user's intention and capacity. Asymmetry here is a frequent cause of HI breakdown.

**3.4 Institutional conditions**  
Effective HI ecosystems are not technical systems alone — they require institutional support structures:
- Clear roles and accountability allocation (who decides when AI is right)
- Error culture that allows correction without blame
- Competence development (Amershi et al.'s 18 principles)
- Governance for edge cases and failure scenarios

**3.5 Adoption and inequality**  
Daniotti et al. (2025) documents that AI adoption is unevenly distributed across demographics, geography and sector. HI gains are not universally accessible — which converges with the argument in `f-commons-extraction-inequality.md`.

---

## Part 4: What we still need to know

**4.1 Longitudinal studies**  
Almost all empirical HI research is cross-sectional or short-term. We do not know whether HI gains hold over time, whether competences atrophy, or whether HI systems are continuously optimised.

**4.2 Systemic effects**  
Studies focus on individual systems. We have very little knowledge of what happens when many HI systems operate in the same domain simultaneously — competition, standardisation pressure, monoculture risks (cf. `j-language-substrate-limits.md`).

**4.3 Failure-mode documentation**  
There is a publication bias toward success stories. Systematic documentation of HI breakdowns — where and why HI gives *worse* results than pure human decision — is underrepresented in the literature.

**4.4 Cross-domain generalisability**  
Can we generalise from medicine to law, from software to creative industries? Lutz et al.'s framework attempts this, but empirically cross-domain comparisons are rare.

---

## Open Questions

1. **Is the complementarity hypothesis falsifiable?** Can we formulate the conditions precisely enough to test them systematically across domains?

2. **When is HI gain real vs. measurement artefact?** Many HI studies use benchmarks designed for AI evaluation, not for HI evaluation. What would an HI-specific benchmark look like?

3. **Is "appropriate reliance" an individual competence problem or a system-design problem?** Schemmer et al. treat it as individual; but organisational structures and UI design can make calibration easier or harder.

4. **HI maturity models**: Is it possible to set up a maturity model for HI ecosystems (analogous to CMMI for software development) that describes what more/less mature HI implementations look like?

---

## Sources (Anchors)

Tags per STEERING.md source-quality standard: `[J]` peer-reviewed journal · `[C]` peer-reviewed conference · `[P]` preprint only · `[R]` technical/institutional report.

**Already in Kilder:**
- Lutz, C., Newlands, G., & Jarrahi, M. H. (2025). *Hybrid Intelligence*. `[J]` (forthcoming book chapter / journal — three-layer micro/meso/macro framework)
- Topol, E. J. (2019). High-performance medicine: the convergence of human and artificial intelligence. *Nature Medicine, 25*, 44–56. https://doi.org/10.1038/s41591-018-0300-7 `[J]` — verified against PDF (review article, three-level framing: clinicians / health systems / patients); CrossRef `update-to: None` (retraction-free, checked 2026-05-11).
- Amershi, S., et al. (2019). Guidelines for Human-AI Interaction. *CHI '19*. `[C]`
- Schemmer, M., Kühl, N., Benz, C., Bartos, A., & Satzger, G. (2023). Appropriate Reliance on AI Advice: Conceptualization and the Effect of Explanations. *IUI '23* (ACM Conference on Intelligent User Interfaces). `[C]` — verified against PDF (introduces Appropriateness of Reliance, AoR, as two-dimensional metric)
- Walsh, S., Wang, Q., & Ying, L. (2025). Theory of Mind in Human-AI Interaction and AI. In *Handbook of Human-Centered Artificial Intelligence*. Springer Nature Singapore. https://doi.org/10.1007/978-981-97-8440-0_6-1 `[Book chapter — Springer reference work; OA cit: 0]` — author initials previously given as T./B./R. corrected to S./Q./L. against OpenAlex W4416214382 + CrossRef record (2026-05-11). CrossRef `update-to: None`.
- Bensch, L., Bensch, O., Nilsson, T., & Paradiso, J. A. (2025). Human-in/on-the-Loop AI: Enabling Human Controllability and Decision-Making in Spaceflight. In *Handbook of Human-Centered Artificial Intelligence*. Springer Nature Singapore. https://doi.org/10.1007/978-981-97-8440-0_40-1 `[Book chapter — Springer reference work; OA cit: 1]` — venue resolved 2026-05-11 (was tagged `[P]/[C]` pending). CrossRef `update-to: None`. Submitted-version OA at RWTH Publications (record 1032478).
- Wang, B., Yu, W., Zhong, Y., Yu, H., Lian, K., & Lu, C. (2025). AI Code in the Wild: Measuring Security Risks and Ecosystem Shifts of AI-Generated Code in Modern Software. arXiv:2512.18567. `[P; OA cit: 0]` — title and first-author identity corrected against OpenAlex (was previously cited as "Wang et al. (2025). AI Code in the Wild").
- Wessel, M., Serebrenik, A., Wiese, I., Steinmacher, I., & Gerosa, M. A. (2022). Quality gatekeepers: investigating the effects of code review bots on pull request activities. *Empirical Software Engineering, 27*(108). `[J]` — verified
- Wessel, M., Abdellatif, A., Wiese, I., Conte, T., Shihab, E., Gerosa, M. A., & Steinmacher, I. (2022). Bots for Pull Requests: The Good, the Bad, and the Promising. *ICSE '22*. `[C]` — verified (qualitative companion to the EMSE paper; ground for the "bot fatigue" claim)
- Daniotti, S., Wachs, J., Feng, X., & Neffke, F. (2025). Who is using AI to code? Global diffusion and impact of generative AI. arXiv:2506.08945. `[P; OA cit: 0]`
- Wu, Q., Bansal, G., Zhang, J., Wu, Y., Li, B., Zhu, E., et al. (2023). AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation. arXiv:2308.08155. `[P; OA cit: 147]` — meets `[P]` retention threshold (OA cit > 100); widely-deployed multi-agent framework.
- Fang, C. M., Liu, A. R., Danry, V., Lee, E., Chan, S. W. T., & Pataranutaporn, P. (2025). How AI and Human Behaviors Shape Psychosocial Effects of Extended Chatbot Use: A Longitudinal Randomized Controlled Study. arXiv:2503.17473. `[P; OA cit: 19]` — full title and authorship resolved via OpenAlex W4414820664 (also deposited at Research Square, DOI 10.21203/rs.3.rs-8148142/v1).
- ~~Jeong et al. (2024). Bias in AI-assisted decisions. arXiv:2410.12010.~~ **Misattribution — pending re-attribution.** The arXiv:2410.12010 paper authored by Jeong, Ma, & Houmansadr is titled *Bias Similarity Measurement: A Black-Box Audit of Fairness Across LLMs* — a cross-model fairness-auditing study, **not** about bias amplification in AI-assisted human decisions. The §2.6 in-text citation has been removed in v0.3 pending identification of the intended source (candidates: Angwin et al. 2016 ProPublica COMPAS investigation; Dressel & Farid 2018 *Science Advances*; Fogliato et al. 2021 *FAccT*). Confirmed via OpenAlex DOI lookup (doi:10.48550/arXiv.2410.12010) + abstract reading on 2026-05-11.
- Chu et al. (2026). Agentic World Modeling. arXiv:2604.22748. `[P]` — too new for iCit

**Missing — to download:**
- Dellermann, D., Ebel, P., Söllner, M., & Leimeister, J. M. (2019). Hybrid intelligence. *Business & Information Systems Engineering, 61*(5), 637–643. `[J]` — Seminal definition. Springer paywall; arXiv search did not return a preprint. **[check institutional access]**
- Raisch, S., & Krakowski, S. (2021). Artificial intelligence and management: The automation–augmentation paradox. *Academy of Management Review, 46*(1), 192–210. `[J]` — AMR paywall. **[check institutional access]**
- Esteva, A., et al. (2017). Dermatologist-level classification of skin cancer with deep neural networks. *Nature, 542*, 115–118. `[J]`
- Ardila, D., et al. (2019). End-to-end lung cancer screening with low-dose chest computed tomography using three-dimensional deep learning. *Nature Medicine, 25*, 954–961. `[J]`
- Tschandl, P., et al. (2020). Human–computer collaboration for skin cancer recognition. *Nature Medicine, 26*, 1229–1234. `[J]` — newly cited in §2.1 to qualify the Esteva 2017 result.

**Audit notes (2026-05-11):**
- OpenAlex `cited_by_count` added to seven previously-pending preprint entries (AutoGen 147; Fang 19; Daniotti 0; Wang 0; Jeong 0; Walsh book chapter 0; Bensch book chapter 1). OpenAlex used instead of Semantic Scholar per STEERING.md tri-source directive (2026-05-05) — avoids the S2 rate-limit bottleneck encountered in the prior cycle.
- Walsh-Wang-Ying (2025) and Bensch et al. (2025) both resolved as chapters in Springer's *Handbook of Human-Centered Artificial Intelligence* (Springer Nature Singapore; ISBN 978-981-97-8440-0). Walsh author initials previously listed as T./B./R. corrected to S./Q./L. Bensch venue resolved from `[P]/[C]` ambiguity.
- Jeong et al. (2024, arXiv:2410.12010) misattribution detected: the actual paper is *Bias Similarity Measurement: A Black-Box Audit of Fairness Across LLMs* (Jeong, Ma & Houmansadr), a cross-model fairness audit. The Draft O §2.6 in-text claim ("bias amplification in AI-assisted decisions") does not match. In-text citation removed pending re-attribution to Angwin et al. (2016) / Dressel & Farid (2018) / Fogliato et al. (2021), to be selected in the next cycle.
- Retraction check (CrossRef `update-to` field) clean for Topol 2019 (10.1038/s41591-018-0300-7), Walsh 2025 (10.1007/978-981-97-8440-0_6-1), Bensch 2025 (10.1007/978-981-97-8440-0_40-1).
- No Wikipedia citations present in this draft (Wikipedia rule satisfied).

---

## What Still Needs Work

- [ ] Search and download Dellermann 2019 and Raisch & Krakowski 2021
- [ ] Add the non-downloadable items to `_linked_sources.md`
- [ ] Expand 2.1 (medicine) with newer meta-analyses of HI vs. AI alone
- [ ] Find studies specifically on HI in the education sector (under-represented in the draft)
- [ ] Add legal/COMPAS literature with concrete source references
- [ ] Consider whether to split the draft: one on single-domain studies, one on cross-cutting findings
- [ ] Cross-ref to `g-agentic-hi-collaboration.md` Part 6 (measurement)
