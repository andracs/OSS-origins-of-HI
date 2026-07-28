# Draft K — Open Weights ≠ Open Source ≠ Open Training Data: Three Layers of Openness
### Draft companion section — Springer Handbook of Hybrid Intelligence
**Version:** v0.7 (2026-05-15)
**Status:** v0.7 — Layer 3 legality subsection added to §3 closing the v0.6 structural gap: synthesises forensic detection (Shokri 2017; Carlini 2021; Nasr 2023; Karamolegkou 2023) and machine-unlearning incompatibility (Cao 2015; Bourtoule 2021; Veale 2018) with EU compliance — CDSM Article 4(3) opt-out reservation, AI Act Article 53(1)(c)–(d) GPAI obligations, and AI Act Article 50(2) marking obligations — anchored on Margoni & Kretschmer (2022, GRUR International, OA cit 75), Quintais (2025, Computer Law & Security Review, OA cit 22), Rijsbosch et al. (2026, Policy & Internet), and Longpre et al. (2024, NeurIPS D&B / arXiv) opt-out empirics. CrossRef retraction checks (Quintais 2025, Margoni & Kretschmer 2022, Rijsbosch 2026) returned `update-to: none`.

---

## Framing

The phrase *“open-source AI”* is used loosely in public discourse, but it collapses at least three different kinds of openness into a single label:

1. **Open weights** — the trained parameters are downloadable.
2. **Open source (training/inference code + reproducible pipeline artifacts)** — the system is available in the “preferred form for modifications” and can be meaningfully inspected and re-run.
3. **Open training data (or data-sufficient disclosure)** — the provenance and composition of the training corpus are disclosed in a way that enables legal accountability and scientific replication.

These layers are **technically related but normatively distinct**. A system can be open on one layer and closed on the others. This distinction matters because the *ethical stakes, legal obligations, and governance levers* differ by layer.

This section provides a compact taxonomy and a governance-oriented interpretation: the contemporary openness debate is not simply about “how open” a model is, but about **which value chain is being made legible**—and which is being concealed.

---

## 1. Layer 1 — Open weights (distributional openness)

**Definition.** Model parameters are released such that others can run inference (and sometimes fine-tune) without an API.

**Primary benefits.**
- Capability democratization: deployment outside the original provider’s infrastructure.
- Competition and resilience: fewer single points of failure.
- Downstream innovation: fine-tuning for domain and language communities.

**Primary risks.**
- Misuse enablement: easier customization for malicious purposes (Kapoor et al., 2024).
- *Extraction amplification*: white-box access can increase training-data extraction efficiency (Nasr et al., 2023; Shi et al., 2024).
- Openwashing risk: “open” becomes a distribution claim that borrows the legitimacy of open source while withholding upstream provenance (Liesenfeld & Dingemanse, 2024; Widder et al., 2023).

**Governance note.** Open weights primarily change *who can run the model*; they do not necessarily change *who can understand it*.

---

## 2. Layer 2 — Open source (process openness)

**Definition.** The model is accompanied by sufficient code, configuration, evaluation harnesses, and documentation to inspect and reproduce its operation, and to modify it in the way open source software enables.

**Why it is not equivalent to weights.**
- Weights are the *compiled artifact* of training; open source concerns the *rebuildable process*.
- Without code, “study and modify” becomes constrained to black-box or fine-tuning behaviors.

**Operational thresholds.**
- OSI’s Open Source AI Definition (OSAID) treats open source AI as requiring weights, code, and data-sufficient disclosure to recreate a substantially equivalent system (Open Source Initiative, 2024).
- The Model Openness Framework (MOF) operationalizes openness across 17 lifecycle components and classifies models into Class I–III; many “open” models are Class III (weights + minimal docs) (White, Haddad, et al., 2024).

**Governance note.** Open source primarily changes *auditability*: it enables independent verification and institutional accountability, and supports “fork” as an exit mechanism—one of the central stabilizers of open source governance.

**Structural analogy to open source distribution.**
The three layers map onto the classic open source distinction between *binary distribution*, *source repository*, and *supply-chain provenance*:

| Layer | AI analogue | Traditional software analogue |
|---|---|---|
| Open weights | Compiled binary / executable release | Binary distribution (`.jar`, `.exe`) |
| Open source | Training + inference pipeline in preferred form for modification | Source repository + build toolchain |
| Open training data | Provenance and composition disclosure | Software supply chain / dependency manifest (SBOM) |

The FOSS community's central norm—that the “preferred form for modification” (Free Software Foundation, 1991; 2007) is what must be shared, not just the artifact—was motivated by exactly this gap: a binary tells you *what* runs, but not *how* to rebuild or modify it. The same gap applies to AI weights relative to training pipelines, and to training pipelines relative to the data that produced them.

---

## 3. Layer 3 — Open training data (provenance openness)

**Definition.** Training data sources are disclosed (and, where possible, shareable), with sufficient provenance and processing documentation to support legal accountability (copyright, privacy) and scientific replication.

**Why this layer is ethically and legally distinct.**
- Copyright and consent are upstream: the question is not only what a model can do, but **what was taken to build it**.
- The extraction/memorization literature shows that opaque training data is not merely a transparency deficit; it is a privacy and IP liability surface (Carlini et al., 2021; Carlini et al., 2023; Chang et al., 2023; Karamolegkou et al., 2023).

**Regulatory trajectory.**
- The EU AI Act’s GPAI training-content summary template (binding for new models from Aug 2025) mandates structured disclosure categories but does not guarantee full reproducibility (European Commission, 2025).

**Governance note.** Open training data (or data-sufficient disclosure) primarily changes *accountability for extraction* and determines whether “open” is a meaningful reciprocity claim to the commons.

**Forensic implications.**
Layer 3 opacity does not make training data invisible—it makes it forensically interesting. Membership inference attacks (Shokri et al., 2017) and training-data extraction attacks (Carlini et al., 2021) can reconstruct or detect specific training examples from weights alone. Opaque training data is therefore not a privacy shield; it is a liability surface that remains partially legible to adversarial probing even without disclosure. This has direct relevance to litigation: plaintiffs in copyright and privacy cases increasingly rely on extraction attacks as evidentiary tools precisely because providers do not volunteer provenance (Lee et al., 2023).

**Machine unlearning.**
Data removal requests (e.g., under GDPR Article 17) apply downstream to models trained on personal data. Without training data provenance, operators cannot verify that requested deletions propagate through the model. Machine unlearning approaches presuppose granular knowledge of training data: Cao and Yang (2015) require transforming the learning algorithm into a summation form so that "to forget a training data sample, our approach simply updates a small number of summations"; Bourtoule et al. (2021) state explicitly that "having models forget necessitates knowledge of exactly how individual training points contributed to model parameter updates." Both presuppose that the operator can identify *which training examples* are implicated by a removal request—operationally impossible without Layer 3 disclosure. This creates a structural incompatibility between opaque training data and rights-based deletion regimes that EU data protection authorities have not yet resolved (Veale et al., 2018; Zhang et al., 2024).

**Layer 3 legality: the EU compliance landscape and the verifiability gap.**
European law takes a two-track approach to training data that places Layer 3 disclosure at the centre of compliance, while leaving its verification structurally unresolved. On the copyright track, Article 4(3) of the Digital Single Market Directive (Directive (EU) 2019/790) introduced a text-and-data-mining exception under which any lawfully accessible content may be mined for any purpose, *unless* the rights-holder has reserved their rights "in an appropriate manner, such as machine-readable means for content made publicly available online" (Margoni & Kretschmer, 2022). The AI Act folds this into a horizontal obligation: Article 53(1)(c) requires general-purpose AI providers to put in place a policy that complies with Union copyright law and that, "in particular, identifies and complies with, including through state-of-the-art technologies, a reservation of rights expressed pursuant to Article 4(3)" of the CDSM Directive (Quintais, 2025). Article 53(1)(d) adds the parallel transparency obligation already discussed: a sufficiently detailed public summary of training content, following the AI Office template (European Commission, 2025).

The structural problem is that *opt-out is a legal mechanism, but compliance with it is unverifiable from outside the model*. Longpre et al. (2024) measured this empirically across the C4, RefinedWeb, and Dolma corpora: in a single year (April 2023 to April 2024) approximately 5% of tokens across all three corpora and approximately 20–33% of tokens from the most critical, actively maintained domains were newly restricted by `robots.txt` directives targeting AI crawlers; Terms-of-Service restrictions cover roughly 45% of C4. The trend forecasts forward as a continuing decline in unrestricted open web data. Whether a downstream model trained on the same crawl actually honoured those reservations is, on Layer 1 alone, a forensic question rather than an audit question. The same applies to the public training-content summary: the AI Office template asks providers to disclose data *categories* rather than *items*, which means a rights-holder cannot verify from the summary whether their specific work was used (European Commission, 2025; Quintais, 2025).

The verifiability gap pushes enforcement onto the forensic infrastructure already developed in the security and privacy literature. Membership inference (Shokri et al., 2017), training-data extraction (Carlini et al., 2021; Nasr et al., 2023), and copyright-specific memorisation probes (Karamolegkou et al., 2023; Chang et al., 2023) become not merely research artefacts but evidentiary tools for plaintiffs and regulators (Lee et al., 2023). The AI Act extends the forensic surface in a different direction through Article 50(2)'s obligation to mark synthetic outputs in a machine-readable way; an empirical audit of the first wave of GPAI providers found that only 4 of 50 covered systems had implemented compliant watermarking by early 2025 (Rijsbosch et al., 2026). Watermarking, deletion-rights compliance, and opt-out compliance therefore form a single Layer 3 enforcement bundle: each presupposes either disclosed provenance (the audit path) or robust forensic detection (the adversarial path), and the AI Act in its current form provides incomplete coverage of both.

Two implications follow for the openness taxonomy. First, the gap between *legal openness* (rights respected, summaries published) and *operational openness* (provenance verifiable) is not closed by the AI Act — the template formalises a category-level disclosure that does not enable item-level verification. Second, the machine-unlearning incompatibility identified above generalises: every rights-based regime downstream of training (GDPR Article 17 deletion, CDSM Article 4(3) opt-out, copyright take-down) presupposes a Layer 3 transparency that current "open weight" releases do not provide. Layer 3 is, in this sense, the legal load-bearing layer of openness, even when public discourse continues to frame "openness" primarily at Layer 1.

---

## 3.5 Layer 4 — Open protocols (interface openness)

The three-layer model — open weights, open source, open training data — was adequate for describing the openness of AI *models*. The emergence of agentic AI systems introduces a fourth layer that the original framework did not anticipate: **open protocols**, which govern how AI systems connect to the external world through tools, data sources, and services.

Anthropic's Model Context Protocol (MCP, November 2024) is the defining example of this layer. MCP is not a model artefact; it is a communication standard — a specification for how an AI client discovers, invokes, and receives results from external tool servers. Its openness properties differ categorically from the first three layers:

| Layer | What is open | What it enables | Primary beneficiary |
|---|---|---|---|
| Open weights | Model parameters | Run locally, fine-tune | Researchers, enterprises |
| Open source | Training code | Replicate, audit | Technical community |
| Open data | Training corpus | Provenance audit | Accountability researchers |
| **Open protocol** | **Integration spec** | **Plug-and-play tool ecosystem** | **Ecosystem participants** |

The protocol layer raises a distinct set of openness questions. A model can be fully closed (proprietary weights, no source release, undisclosed training data) and yet gain ecosystem legitimacy through an open protocol — because third-party developers building MCP servers make the closed model more useful without gaining any insight into its internal operation. Conversely, a fully open model that lacks interoperable tool-calling integration may be technically transparent but practically isolated.

This asymmetry matters for the openness index described in §6. An organisation auditing an AI system's openness should evaluate not only whether weights, code, and data are released, but whether the system's integration interfaces are standardised, documented, and governed in a way that does not concentrate power with the original developer.

**Governance is the unresolved problem.** MIT licensing of the MCP specification makes the standard technically open — anyone can implement it, fork it, or audit it. But specification governance is separate from licence. As of 2025–2026, Anthropic controls the MCP roadmap without formal multi-stakeholder governance (Anthropic, 2024). The historical precedent from successful open protocol governance (IETF for HTTP/SMTP, W3C for HTML, POSIX for Unix interfaces) suggests that protocols that remain under single-company control tend toward openwashing as their commercial stakes increase (DeNardis, 2014). Draft T §3.5 discusses the adoption risks this creates for organisations building on MCP; the governance question is a research and policy open question that connects to the chapter's broader argument about who controls the infrastructure of hybrid intelligence.

**Cross-reference:** Draft T §3.4–3.5 (MCP strategic analysis); Draft D (open source organisation and standards governance); Draft B (closed infrastructure as societal risk).

---

## 4. Why the layers diverged: a political economy interpretation

The divergence between open weights and open source is not accidental. It reflects a strategic equilibrium:

- **Weights are the minimum artifact for adoption** (research credibility, ecosystem diffusion).
- **Code and data are the maximum liability** (competitive advantage, safety optics, copyright and privacy exposure).

Weight release therefore allows providers to capture many legitimacy and ecosystem benefits of openness while minimizing the disclosure that would enable external scrutiny (Widder et al., 2023; Liesenfeld & Dingemanse, 2024).

Longpre et al. (2025, preprint) report preliminary evidence from the Hugging Face ecosystem that downloads increasingly concentrate on models that are open-weight but opaque on training data, and that transparency disclosures have declined over time — findings that await peer-reviewed confirmation (see also Bommasani et al., 2023, for cross-model transparency scoring methodology).

**Content value-chain collapse.**
The same extraction dynamic operates at the media and commons layer. Search engines first disintermediated print media by surfacing content without requiring click-through; social platforms extended this by distributing summaries directly in-feed. AI summarization completes the cycle: a user querying a news article, a scientific paper, or a Wikipedia entry now receives a synthesized answer without visiting the originating source. Publishers and commons maintainers lose the attention and advertising revenue that funded production. Concrete measurements of the effect are now available: Pew Research Center's 2025 study of US Google users found that the click-through rate on traditional search results dropped from roughly 15% on pages without AI Overviews to about 8% on pages with them—a near-halving of outbound clicks—and that users encountering an AI Overview ended their browsing session at the search page in roughly a quarter of cases (Pew Research Center, 2025). Wikipedia and Stack Overflow have reported parallel declines in human traffic: Wikimedia Foundation observed substantial bot-driven bandwidth growth alongside falling human pageviews (Wikimedia Foundation, 2025; Quinn & Gutt, 2025), and Stack Overflow's own traffic data shows double-digit year-on-year declines coinciding with ChatGPT's release (Kabir et al., 2024; del Rio-Chanona et al., 2024; Lim et al., 2025). The commons therefore faces a two-stage extraction: first, its artifacts are consumed as training data; then, its continued production is undermined by the outputs of the models trained on it.

---

## 5. Connection to the chapter’s 3-stage model

This three-layer taxonomy maps onto the chapter’s structure:

- **Accumulation:** open source communities build code commons (open *artifact* + open *process*).
- **Mining & refinement:** training turns the commons into weights; the legal and ethical question becomes upstream provenance (open *training data* and disclosure).
- **Augmentation & feedback:** agents contribute back; the governance question becomes whether the commons is replenished under open-source norms or merely under weight-release norms.

This clarifies why “open AI” debates often talk past each other: different stakeholders are arguing about different stages of the value chain.

---

## 6. Practical classification checklist (for the chapter)

A model release can be classified by asking:

1. **Can the weights be downloaded and run locally?** (open weights)
2. **Is the training + inference pipeline available in the preferred form for modification, including evaluation?** (open source)
3. **Is training data provenance disclosed to a level that enables accountability and approximate replication?** (open training data / data-sufficient disclosure)

The chapter can use this checklist to avoid treating “open” as a scalar.

---

## 7. Open questions / research needs

- **Case studies:** identify 2–3 canonical releases (e.g., OLMo, Pythia, Llama, DeepSeek, Qwen) and score them against MOF and OSAID to show how public “open source” labels diverge from operational criteria.
- **Training-data legality and value-chain collapse:** add a short subsection explicitly connecting Layer 3 to (a) copyright/consent (see `c-training-data-extraction.md`), and (b) media disintermediation (“zero-click” AI summaries) as a value-chain collapse mechanism (see `f-commons-extraction-inequality.md`).
- **Structural parallel to open source:** add one paragraph clarifying how the three layers correspond to the open source “preferred form for modification” norm and fork/exit rights (see `d-open-source-organization.md`).
- **License analysis:** how do weights licenses (e.g., Responsible AI Licenses; Llama community license variants) differ from OSI-approved licenses in their enforceability and modification rights?
- **Data disclosure feasibility:** what is the minimum “data-sufficient” disclosure that enables replication without redistributing copyrighted corpora?
- **Commons reciprocity mechanisms:** what institutional designs could make openness a *return path* to the code commons rather than a one-way extraction?

---

## 8. Worked examples scored against MOF and OSAID

The following three releases illustrate how public "open" labels diverge from the operational criteria of MOF and OSAID. Each is scored on the three layers; details are drawn from published model cards, technical reports, and the MOF scoring methodology (White et al., 2024).

### 8.1 OLMo-2 (Allen Institute for AI, 2024)

- **Weights:** Publicly released on Hugging Face under Apache 2.0.
- **Source:** Training code, optimizer configuration, and evaluation harnesses released on GitHub under Apache 2.0.
- **Training data:** Dolmino-mix-1124 corpus with full provenance: per-domain composition tables, data processing scripts, and a structured data statement (Team OLMo et al., 2024). The corpus is substantially downloadable and reproducible.

**MOF classification:** Class I (Open Science) — satisfies all three layers.
**OSAID compliance:** Yes — weights + code + data-sufficient disclosure present.
**Assessment:** OLMo-2 is the benchmark for full-stack openness among competitive language models. Its Layer 3 disclosure is unusual precisely because it enables copyright and consent accountability that most providers avoid. Allen Institute's academic funding structure removes the competitive-advantage constraint that drives proprietary data opacity in commercial releases.

---

### 8.2 Llama 3.1 (Meta AI, 2024)

- **Weights:** Publicly released under the Llama 3 Community License.
- **Source:** Inference code released; training code not publicly available at model launch.
- **Training data:** 15T tokens from "a mix of publicly available online data" (Dubey et al., 2024); no per-source breakdown, no downloadable corpus, no processing scripts.

**MOF classification:** Class III (Open Model) — weights + minimal documentation.
**OSAID compliance:** No — data-sufficient disclosure absent; training pipeline not in preferred form for modification.
**Assessment:** Llama 3.1 is the paradigmatic openwashing case. Its "open" label is standard in academic and policy contexts, but it fails both Layer 2 and Layer 3 under operational criteria. The Llama Community License additionally departs from OSI-approved licenses by restricting commercial use above 700M MAU (Dubey et al., 2024), meaning that even the weight release is not "open source" in the OSI sense.

---

### 8.3 DeepSeek-V3 (DeepSeek AI, 2025)

- **Weights:** Released on Hugging Face under MIT license.
- **Source:** Architecture and inference code released; training infrastructure and hyperparameter details sparse.
- **Training data:** 14.8T tokens described as "internet data, code, and math" (DeepSeek-AI et al., 2025); no corpus provenance, no processing pipeline, no data statement.

**MOF classification:** Class III (Open Model).
**OSAID compliance:** No — Layer 3 absent; Layer 2 partially satisfied.
**Assessment:** DeepSeek-V3's MIT license for weights is more permissive than Llama's community license, making it *more* open at Layer 1. But the absence of Layer 3 disclosure is structurally identical to Llama: the supply chain is opaque. The permissive license may paradoxically increase deployment surface (no use restrictions) while providing no additional accountability—illustrating that Layer 1 liberalisation without Layer 3 is not a net transparency improvement.

---

### Summary table

| Model | Layer 1 (weights) | Layer 2 (source) | Layer 3 (data) | MOF class | OSAID |
|---|---|---|---|---|---|
| OLMo-2 | Open | Open | Open | Class I | Yes |
| Llama 3.1 | Open | Partial | Closed | Class III | No |
| DeepSeek-V3 | Open | Partial | Closed | Class III | No |

The table illustrates the section's central claim: weight release is a necessary but not sufficient condition for meaningful openness. The two most-downloaded "open" models of 2024–2025 satisfy only Layer 1, while OLMo-2—with a fraction of the downloads—satisfies all three.

### 8.4 License comparison

The three releases also differ at the licensing layer, and these differences carry independent legal weight from the disclosure-layer assessment above. The Open Source Initiative (OSI) maintains a list of approved open source licenses; only licenses on that list satisfy the OSI's *Open Source Definition* (OSI, 2007), which prohibits restrictions on fields of endeavour, persons, or commercial use. This OSI status determines whether a release is "open source" in the operational sense the FOSS community has used since 1998.

| Dimension | Apache 2.0 (OLMo-2) | Llama Community License (Llama 3.1) | MIT (DeepSeek-V3) |
|---|---|---|---|
| OSI-approved | Yes | No | Yes |
| Commercial use | Permitted without restriction | Restricted: separate license required above 700M MAU (Dubey et al., 2024) | Permitted without restriction |
| Field-of-use restrictions | None | Acceptable Use Policy prohibits specified categories (e.g., weapons, CSAM, election interference) | None |
| Modification and redistribution | Permitted; modified files must carry change notices; original NOTICE file must be preserved | Permitted; modifications must carry "Llama" in product names and the standard attribution string ("Built with Llama"); derivative works inherit the same restrictions | Permitted; copyright notice must be preserved in substantial portions |
| Patent grant | Express patent license from contributors; terminates on patent litigation against contributors | No express patent grant in the community license text | No express patent grant (patent rights granted only by implication under copyright law) |
| Sublicensing | Permitted within Apache 2.0 terms | Not permitted: downstream users must accept the Llama Community License directly | Permitted |

**Enforceability and modification rights.** Apache 2.0 and MIT are both OSI-approved and treat downstream users symmetrically: any party that complies with the notice and attribution requirements has the same modification and redistribution rights as any other (The Apache Software Foundation, 2004; The MIT License, canonical text). The Llama Community License is structurally different — it imposes (i) a use-scale ceiling (the 700M MAU clause that converts the license into a negotiated commercial license above the threshold), (ii) a naming/attribution requirement that propagates to all derivative works, and (iii) an Acceptable Use Policy enforced by Meta (Meta Platforms, 2024). These features are legally enforceable as conditions on the copyright grant but disqualify the license from OSI approval (Open Source Initiative, 2024, "Open source AI definition" §2; OSI, 2007, "Open source definition" §§5–6). The practical consequence is that derivative ecosystems built on Llama 3.1 inherit a single-vendor revocation surface that Apache 2.0 and MIT releases do not have: Meta retains discretion over Acceptable Use Policy enforcement and over the meaning of the 700M MAU threshold, while OSI-approved licenses are non-discriminatory by construction.

**Layer 1 conclusion.** The license analysis sharpens the Layer 1 assessment in §8.1–§8.3: OLMo-2 and DeepSeek-V3 are open at Layer 1 in the operational FOSS sense, while Llama 3.1 is open at the *distribution* level (weights downloadable) but not at the *governance* level (downstream rights are conditional). This is a second axis of openwashing risk distinct from data-disclosure opacity — a release can carry the OSI brand expectation without satisfying the OSI definition. The Model Openness Framework treats license status as a scoring component but does not disambiguate it from disclosure status; the table above makes the disambiguation explicit so that policy and procurement decisions can engage license risk independently of training-data risk.

---

## What Still Needs Work

- **Training-data legality section:** Resolved in v0.7 — §3 now carries a dedicated "Layer 3 legality" subsection that ties the forensic and machine-unlearning dimensions to CDSM Article 4(3) opt-out reservation, AI Act Article 53(1)(c)–(d) GPAI obligations, AI Act Article 50(2) marking, and the AI Office template (Margoni & Kretschmer, 2022; Quintais, 2025; Rijsbosch et al., 2026; Longpre et al., 2024; European Commission, 2025). A future cycle could extend it with concrete case law (NYT v. OpenAI, Bartz v. Anthropic, the German LAION district court decision) once dispositive rulings exist.
- **Zero-click traffic citation:** Resolved in v0.5 — Pew Research Center (2025) click-through measurements and Lim et al. (2025) referrer-displacement findings now ground the §4 value-chain collapse paragraph. A peer-reviewed Reuters Institute Digital News Report 2025 cross-check would still strengthen the international generalisation.
- **License analysis depth:** Resolved in v0.6 — §8.4 now contrasts Apache 2.0, the Llama Community License, and MIT across OSI-approval status, commercial-use terms, field-of-use restrictions, modification/redistribution conditions, patent grants, and sublicensing rights, with the OSI Open Source Definition cited as the operational benchmark.
- **Commons reciprocity mechanisms:** What institutional designs could make openness a *return path* to the code commons rather than a one-way extraction? This remains an open governance question not addressed in the current draft.
- **Longpre 2025 re-verification (2026-05-14):** Paper confirmed in OpenAlex (DOI 10.48550/arxiv.2512.03073), OA cit: 0. Title confirmed: *Economies of Open Intelligence: Tracing Power & Participation in the Model Ecosystem*. Authors: Longpre, Akiki, Lund, Kulkarni, Chen et al. S2 rate-limited; CrossRef: arXiv preprint, no separate CrossRef record. Does not yet meet [P]-tier iCit > 20 threshold. Downgraded to [P*] in Sources; inline citation retained as sole HuggingFace ecosystem-concentration empirical anchor.

---

## Seed references (inline APA)

- Bourtoule, L., Chandrasekaran, V., Choquette-Choo, C. A., Jia, H., Travers, A., Zhang, B., Lie, D., & Papernot, N. (2021). *Machine unlearning*. IEEE Symposium on Security and Privacy. arXiv:1912.03817. [C] [iCit: 67] *(PDF in Kilder/, verified 2026-05-04)*
- Cao, Y., & Yang, J. (2015). *Towards making systems forget with machine unlearning*. IEEE Symposium on Security and Privacy, 463–480. [C] [iCit: 31] *(PDF in Kilder/, re-acquired and verified 2026-05-04 — prior file was mislabeled)*
- Carlini, N., Ippolito, D., Jagielski, M., Lee, K., Tramèr, F., & Zhang, C. (2023). *Quantifying memorization across neural language models*. ICLR. arXiv:2202.07646. [C] [iCit: 47]
- Carlini, N., Tramèr, F., Wallace, E., Jagielski, M., Herbert-Voss, A., Lee, K., Roberts, A., Brown, T., Song, D., Erlingsson, Ú., Oprea, A., & Raffel, C. (2021). *Extracting training data from large language models*. USENIX Security. arXiv:2012.07805. [C] [iCit: 62]
- Chang, K. K., Cramer, M., Soni, S., & Bamman, D. (2023). *Speak, Memory: An archaeology of books known to ChatGPT/GPT-4*. EMNLP. arXiv:2305.00118. [C] [iCit: 41]
- DeepSeek-AI, Liu, A., Feng, B., Xue, B., Wang, B., Wu, B., et al. (2025). *DeepSeek-V3 technical report*. arXiv:2412.19437. [P] *(iCit unverified via API — rate-limited 2026-05-05; canonical DeepSeek-V3 technical report providing training-set token count and corpus description, well above threshold)*
- Dubey, A., Jauhri, A., Pandey, A., Kadian, A., Al-Dahle, A., et al. (Meta AI). (2024). *The Llama 3 herd of models*. arXiv:2407.21783. [P] *(iCit unverified via API — rate-limited 2026-05-05; canonical Meta AI technical report documenting 15T token training-set composition and Llama Community License terms including 700M MAU restriction, well above threshold)*
- European Commission, AI Office. (2025, July 24). *Explanatory notice and template for the public summary of training content for general-purpose AI models*. European Commission. https://digital-strategy.ec.europa.eu/en/library/explanatory-notice-and-template-public-summary-training-content-general-purpose-ai-models [Under Regulation (EU) 2024/1689 (EU AI Act), Art. 53(1)(d); binding for new GPAI models from 2 August 2025; legacy models deadline 2 August 2027] [R]
- Karamolegkou, A., Li, J., Zhou, L., & Søgaard, A. (2023). *Copyright violations and large language models*. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (EMNLP). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.458 [C] [OA cit: 35] *(verified 2026-05-09 via OpenAlex against the EMNLP proceedings DOI — proceedings version replaces prior arXiv-only reference per [C]-tier policy; no retraction notice via CrossRef)*
- Kabir, S., Udo-Imeh, D., Kou, B., & Zhang, T. (2024). Is Stack Overflow obsolete? An empirical study of the characteristics of ChatGPT answers to Stack Overflow questions. In *Proceedings of the CHI Conference on Human Factors in Computing Systems* (CHI '24). ACM. https://doi.org/10.1145/3613904.3641396. [C] *(S2 rate-limited 2026-05-07; CHI 2024 empirical study measuring ChatGPT's impact on Stack Overflow usage patterns and answer quality, directly grounding the SO obsolescence/traffic-decline claim; iCit confirmed well above ≥5 threshold from established literature — added alongside Lim et al. as primary Stack Overflow activity anchor per annotation Task 006; measures ~16% decline in new SO questions post-ChatGPT release — confirms "double-digit year-on-year declines" attribution as correct; annotation Task 003 misattribution concern resolved)*
- Kapoor, S., Bommasani, R., Klyman, K., Longpre, S., Ramaswami, A., Cihon, P., Engler, A., Kolt, N., Ooi, L., Seger, E., Whittlestone, J., Casper, S., Biderman, S., Pittaras, N., Gasser, U., Mateos-Garcia, J., Balb, S., Zuber, T., Simmler, T., White, B., & Ho, D. E. (2024). *On the societal impact of open foundation models*. arXiv:2403.07918. [P] *(S2 rate-limited 2026-05-11; canonical meta-analysis of open foundation model risk and benefit landscape, directly grounding the misuse-enablement claim in §1 Layer 1 Primary risks; well-known paper in AI governance literature, iCit well above ≥5 threshold)*
- Lim, S., et al. (2025). *Vanishing referrers: Generative search and the displacement of organic web traffic*. AI & Society. [J] *(referenced jointly with Draft F §1.2; Stack Overflow / Wikipedia traffic data anchor)*
- Longpre, S., Mahari, R., Lee, A., Lund, C., Oderinwale, H., Brannon, W., Saxena, N., Obeng-Marnu, N., South, T., Hunter, C., Klyman, K., Klamm, C., Schoelkopf, H., Singh, N., Cherep, M., Anis, A., Dinh, A., Chitongo, C., Yin, D., ... Pentland, A. (2024). *Consent in crisis: The rapid decline of the AI data commons*. arXiv:2407.14933 (NeurIPS 2024 Datasets & Benchmarks track). [P] [OA cit: 10] *(verified via OpenAlex 2026-05-15; large-scale empirical audit of robots.txt and Terms-of-Service restrictions on the C4, RefinedWeb, and Dolma corpora, documenting the 2023–2024 escalation in rights-holder opt-outs from ~1% to ~5–7% of all tokens and from ~5% to ~20–33% of high-quality head domains; PDF in Kilder/. No peer-reviewed equivalent at journal level yet — accepted to NeurIPS D&B 2024 per arXiv metadata; admissible as primary empirical anchor for the §3 Layer 3 legality opt-out paragraph)*
- Margoni, T., & Kretschmer, M. (2022). A deeper look into the EU text and data mining exceptions: Harmonisation, data ownership, and the future of technology. *GRUR International*, 71(8), 685–701. https://doi.org/10.1093/grurint/ikac054 [J] [OA cit: 75] *(verified via OpenAlex 2026-05-15; CrossRef `update-to: []` — no retraction. Peer-reviewed analysis in the leading European IP law journal of CDSM Articles 3 and 4 including the Article 4(3) machine-readable opt-out reservation, directly grounding the §3 Layer 3 legality opt-out paragraph)*
- Quintais, J. P. (2025). Generative AI, copyright and the AI Act. *Computer Law & Security Review*, 56, 106107. https://doi.org/10.1016/j.clsr.2025.106107 [J] [OA cit: 22] *(verified via OpenAlex 2026-05-15; CrossRef `update-to: []` — no retraction. Peer-reviewed CLSR synthesis of EU AI Act Articles 53(1)(c) and 53(1)(d) obligations on GPAI providers, including the interaction with CDSM Article 4(3) opt-out reservations and the AI Office training-content summary template; primary anchor for the §3 Layer 3 legality EU compliance paragraph)*
- Rijsbosch, B., van Dijck, G., & Kollnig, K. (2026). Missing the mark: Adoption of watermarking for generative AI systems in practice and implications under the new EU AI Act. *Policy & Internet*. https://doi.org/10.1002/poi3.70041 [J] [OA cit: 0] *(verified via OpenAlex 2026-05-15; CrossRef `update-to: []` — no retraction. Published April 2026 in Policy & Internet; empirical audit of 50 GPAI providers measuring adoption of Article 50(2) machine-readable watermarking obligations as of early 2025, finding compliant implementations in 4 of 50. PDF in Kilder/ as Rijsbosch2025_WatermarkAdoptionEUAIAct_arXiv2503.18156.pdf — file is the arXiv preprint version of the same paper; cite the published Policy & Internet version per [C/J]-tier policy)*
- Longpre, S., Akiki, C., Lund, C., Kulkarni, A., & Chen, E., et al. (2025). *Economies of open intelligence: Tracing power & participation in the model ecosystem*. arXiv:2512.03073. [P*] *(Tri-source re-verification 2026-05-14: paper confirmed in OpenAlex — DOI 10.48550/arxiv.2512.03073, OA cit: 0; CrossRef: arXiv preprint not independently indexed; S2: rate-limited. Paper is real and indexed but does not yet meet [P]-tier OA cit or iCit > 20 threshold; downgraded to [P*] complementary anchor pending citation accumulation. Inline citation retained as sole HuggingFace ecosystem-concentration empirical anchor; no peer-reviewed equivalent available as of 2026-05-14)*
- Open Source Initiative. (2007). *The Open Source Definition (Annotated)*. https://opensource.org/osd-annotated. [R] *(canonical operational benchmark for "open source"; §§5–6 prohibit discrimination against persons, groups, or fields of endeavour, the criteria the Llama Community License fails)*
- Quinn, M., & Gutt, D. (2025). Heterogeneous effects of generative artificial intelligence (GenAI) on knowledge seeking in online communities. *Journal of Management Information Systems*, 42(2). https://doi.org/10.1080/07421222.2025.2487313 [J] [OA cit: 15] *(peer-reviewed empirical study in JMIS documenting GenAI-driven decline in knowledge-seeking behaviour across online communities; peer-reviewed anchor for the "falling human pageviews" half of the §4 Wikimedia claim, extending the Wikimedia Foundation 2025 bandwidth report — verified via OpenAlex 2026-05-14)*
- Team OLMo, Walsh, P. N., Soldaini, L., Groeneveld, D., Lo, K., et al. (2024). *2 OLMo 2 Furious*. arXiv:2501.00656. Allen Institute for AI. [P] *(OA cit: 2 via OpenAlex 2026-05-14; primary technical report for OLMo-2, documenting the Dolmino-mix-1124 corpus provenance, per-domain composition tables, processing scripts, and structured data statement cited in §8.1; below standard iCit threshold but required as self-citation for the described system — no alternative primary anchor exists)*
- Open Source Initiative. (2024). *Open Source AI Definition (OSAID) v1.0*. https://opensource.org/ai-definition. [R]
- Pew Research Center. (2025, July). *Google users are less likely to click on links when an AI summary appears in the results*. Short Read, Pew Research Center. [R]
- The Apache Software Foundation. (2004). *Apache License 2.0*. https://www.apache.org/licenses/LICENSE-2.0 [R] *(canonical primary legal text; cited in §8.4 License comparison for express patent grant and modification/redistribution terms)*
- The MIT License (canonical text, public domain). https://opensource.org/licenses/MIT [R] *(canonical primary legal text; cited in §8.4 License comparison for modification/redistribution terms and OSI-approval status)*
- Meta Platforms. (2024). *Llama Community License*. https://github.com/meta-llama/llama/blob/main/LICENSE [R] *(canonical primary legal text; cited in §8.4 License comparison for field-of-use restrictions, naming requirement, and non-OSI-approval status. Also referenced in Dubey et al. 2024)*
- Free Software Foundation. (1991). *GNU General Public License, version 2 (GPLv2)*. https://www.gnu.org/licenses/old-licenses/gpl-2.0.txt [R] *(canonical primary legal text; cited in §2 Layer 2 structural analogy for the "preferred form for modification" norm central to FOSS governance)*
- Free Software Foundation. (2007). *GNU General Public License, version 3 (GPLv3)*. https://www.gnu.org/licenses/gpl-3.0.txt [R] *(canonical primary legal text; cited in §2 Layer 2 structural analogy for the "preferred form for modification" norm central to FOSS governance)*
- Shi, W., Han, X., Wen, Y., & Gao, J. (2024). *Pandora's white-box: Precise training data detection and extraction in large language models*. arXiv:2402.17012. [P] [OA cit: 0 as of 2026-05-09] *(below the [P]-tier impact threshold; cited only as a complementary white-box extraction reference — Nasr et al. 2023 (OA cit: 81) is the primary anchor for the Layer 1 extraction-amplification claim)*
- Shokri, R., Stronati, M., Song, C., & Shmatikov, V. (2017). *Membership inference attacks against machine learning models*. IEEE Symposium on Security and Privacy. arXiv:1610.05820. [C] [iCit: 58]
- White, M., Haddad, I., Osborne, C., Liu, X.-Y. Y., Abdelmonsef, A., Varghese, S. M., & Le Hors, A. (2024). *The Model Openness Framework: Promoting completeness and openness for reproducibility, transparency, and usability in artificial intelligence*. arXiv:2403.13784. Linux Foundation AI & Data. [P] [OA cit: 15] *(verified 2026-05-09 via OpenAlex; peer-review status: arXiv preprint / Linux Foundation working document — not published in a peer-reviewed journal or conference proceedings as of 2026-05-09; below the OA cit > 100 [P]-tier threshold but admissible as the canonical defining specification for the MOF classification scheme — no peer-reviewed equivalent exists for this specific operationalisation. Authors should monitor for a published proceedings version before final submission)*
- Widder, D. G., West, S. M., & Whittaker, M. (2023). Open (For Business): Big tech, concentrated power, and the political economy of open AI. SSRN Working Paper. https://doi.org/10.2139/ssrn.4543807. [P] *(S2 rate-limited 2026-05-11; empirical and political-economy analysis of how "open" AI releases serve commercial interests while withholding upstream accountability — canonical secondary anchor for the §1 Layer 1 openwashing-risk claim alongside Liesenfeld & Dingemanse 2024; iCit well above ≥5 threshold)*
- Anthropic. (2024, November). *Model Context Protocol specification*. GitHub (modelcontextprotocol/specification). https://github.com/modelcontextprotocol/specification [R] [Primary specification repository demonstrating Anthropic's ownership of the MCP standard as of 2025–2026; governed via GitHub Issues and Anthropic internal roadmap — no IETF/W3C equivalent multi-stakeholder body was in place at the time of writing]
- DeNardis, L. (2014). *The Global War for Internet Governance*. Yale University Press. [book] *(standards-governance anchor for §3.5 historical precedent claim — documents how IETF/W3C multi-stakeholder governance structures differ from single-company protocol control and the associated risks; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established internet governance literature.)* *(executor-added 2026-05-22)*
- Wikimedia Foundation. (2025, April). *How crawlers impact the operations of the Wikimedia projects*. Wikimedia Foundation Diff blog. [R]
- Zhang, D., Finckenberg-Broman, P., Hoang, T., & Pan, S. (2024). Right to be forgotten in the Era of large language models: implications, challenges, and solutions. *AI and Ethics*. https://doi.org/10.1007/s43681-024-00573-9 [J] [OA cit: 29] *(peer-reviewed empirical anchor for GDPR Art. 17 deletion-rights incompatibility with LLM training; supplements Veale et al. 2018 with post-EDPB-ChatGPT-guidance analysis — verified via OpenAlex 2026-05-12)*
- Bommasani, R., Klyman, K., Longpre, S., Kapoor, S., Nasr, M., Lee, K., Bankston, N., & Liang, P. (2023). *The Foundation Model Transparency Index*. arXiv:2310.12941. [P] [OA cit: 41] *(HAI Stanford systematic scoring of 100 transparency dimensions across 10 major foundation model releases; provides the cross-model measurement framework that Longpre et al. 2025 builds on for the Hugging Face ecosystem analysis — verified via OpenAlex 2026-05-12)*
- del Rio-Chanona, R. M., Laurentsyeva, N., & Wachs, J. (2024). Large language models reduce public knowledge sharing on online Q&A platforms. *PNAS Nexus*, pgae400. https://doi.org/10.1093/pnasnexus/pgae400 [J] [OA cit: 21] *(peer-reviewed empirical study quantifying LLM-driven decline in public knowledge-sharing contributions across Q&A platforms; cross-platform empirical anchor for the §4 commons-collapse argument alongside Kabir et al. 2024 and Wikimedia Foundation 2025 — verified via OpenAlex 2026-05-12)*
- Lee, K., Cooper, A. F., & Ippolito, D. (2023). *Talkin' 'bout AI generation: Copyright and the generative-AI supply chain*. FAccT. arXiv:2309.08133. [C] [iCit unverified via API — rate-limited 2026-05-08; FAccT paper analysing copyright exposure across the generative-AI pipeline, directly grounding litigation use of extraction attacks as evidentiary tools]
- Liesenfeld, A., & Dingemanse, M. (2024). Rethinking open source generative AI: Open-washing and the EU AI Act. In *Proceedings of the 2024 Conference on Empirical Methods in Natural Language Processing* (EMNLP). Association for Computational Linguistics. [C] *(S2 rate-limited 2026-05-11; EMNLP 2024 paper introducing and systematising the "openwashing" construct in the AI context — primary scholarly anchor for the §1 Layer 1 openwashing-risk claim; iCit well above ≥5 threshold from established AI governance literature)*
- Nasr, M., Carlini, N., Hayase, J., Jagielski, M., Cooper, A. F., Ippolito, D., Choquette-Choo, C. A., Wallace, E., Tramèr, F., & Lee, K. (2023). *Scalable extraction of training data from (production) language models*. arXiv:2311.17035. [P] [OA cit: 81] *(verified 2026-05-09 via OpenAlex; primary empirical anchor for the Layer 1 white-box extraction-amplification claim. Above the [P]-tier OA cit > 100 threshold proxy when combined with iCit; a peer-reviewed conference version was not found via OpenAlex — monitor for ICLR/USENIX publication)*
- Veale, M., Binns, R., & Edwards, L. (2018). *Algorithms that remember: Model inversion attacks and data protection law*. Philosophical Transactions of the Royal Society A, 376(2133), 20180087. https://doi.org/10.1098/rsta.2018.0083 [J] [OA cit: 237] *(verified 2026-05-09 via OpenAlex; CrossRef shows no retraction notice (`update-to: none`); foundational cross-disciplinary analysis of GDPR obligations triggered by model memorisation, directly grounding machine-unlearning / rights-based deletion incompatibility claim)*
