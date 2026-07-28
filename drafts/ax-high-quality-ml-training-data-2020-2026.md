# Draft AX: High-Quality ML Training Data Resources 2020–2026 — A Practitioner's Reference

**Version:** v0.4 | **Status:** Draft — The Stack v1/v2 figures reconciled against published papers (Kocetkov 2022; Lozhkov 2024), §8.1 FineWeb-Edu token figure brought in line with §2.5 and the paper abstract, Lozhkov 2024 (Stack v2) added to sources (2026-05-11)
**Handbook:** Springer Handbook of Hybrid Intelligence
**Character:** Reference/survey chapter — table-heavy, practitioner-oriented
**Related drafts:** AW (dataset economy), C (training data memorization), K (openness layers), S (knowledge platforms), V (two paradigms — scaling hypothesis)

---

## Abstract

The period 2020–2026 is the pivotal era of ML training data: it begins with The Pile (EleutherAI, 2020) and the T5/C4 datasets establishing what "large-scale open training data" means, and ends with a landscape in which trillion-token corpora, systematic curation benchmarks, and specialized instruction-tuning and alignment datasets are routinely released — some open, some closed, most with incomplete provenance documentation. This chapter provides a practitioner's reference to the high-impact training data resources of this period, organized by function: foundation model pretraining corpora, instruction-tuning and RLHF datasets, code corpora, multimodal datasets, domain-specific collections, and evaluation benchmarks. For each resource, the chapter documents: release date, scale, quality methodology, license status, provenance transparency, and the models that trained on it. The chapter argues that the 2020–2026 period saw a decisive **curation turn** — the empirical discovery that data quality filtering yields better models than raw scale, shifting the frontier from "collect everything" toward selective, documented, high-quality corpus construction. Drawing on Longpre et al.'s "Consent in Crisis" audit and the FMTI's transparency measurements, it also documents the widening gap between openly documented datasets (Dolma, FineWeb, DCLM-Baseline) and the opaque proprietary corpora of frontier commercial models.

---

## §1 Why 2020–2026 Is the Pivotal Period

Three developments define this window:

**The scaling hypothesis vindicated and stressed.** GPT-3 (Brown et al., 2020) demonstrated that scaling pretraining data and compute produced qualitatively new capabilities without architectural innovation. This created an immediate demand for pretraining corpora orders of magnitude larger than anything the research community had assembled. The Pile (2020) was a direct response; the subsequent explosion of trillion-token datasets was the consequence.

**The open/closed split widened.** In 2020, the research community could largely replicate frontier model training; GPT-2's training data (WebText) was documented, and comparable open datasets existed. By 2024, the training corpora for GPT-4, Claude 3, and Gemini Ultra are entirely undisclosed. The FMTI (Bommasani et al., 2024; Wan et al., 2025) documents training data as consistently the most opaque category across all major model developers. Concurrently, the open research community produced increasingly high-quality documented alternatives — creating a two-tier dataset ecosystem.

**The curation turn.** Early scaling-era datasets were built on "collect and minimally filter" principles. By 2023–2024, empirical evidence accumulated that quality filtering outperforms raw scale: FineWeb (Penedo et al., 2024) demonstrated that 15T tokens of quality-filtered web text produces better models than larger unfiltered corpora; the Phi series (Microsoft, 2023–2024) showed that GPT-4-quality synthetic data could train small models to outperform much larger models on benchmarks; DCLM-Baseline (Li et al., 2024) established systematic curation as a reproducible science. The lesson: for a given compute budget, better data beats more data.

---

## §2 Foundation Model Pretraining Corpora

### 2.1 The Pile (EleutherAI, 2020)

**Release:** January 2021 | **Size:** 825 GB / ~300B tokens | **License:** MIT
**arXiv:** 2101.00027 (Gao et al., 2020) [OA cit: 484]

The first large-scale openly documented pretraining corpus assembled specifically for LLM training. Composed of 22 named sub-datasets including Common Crawl (filtered), PubMed Central, arXiv, GitHub, Books3 (later removed under copyright pressure), OpenWebText2, Wikipedia, DM Mathematics, FreeLaw, Enron emails, and others. The explicit documentation of all 22 components made The Pile the first dataset in the LLM era that enabled genuine replication and auditability. Books3's subsequent removal and replacement illustrated the copyright governance challenges facing any corpus that includes books.

Models trained on it: GPT-Neo, GPT-J, GPT-NeoX-20B (all EleutherAI); used as reference in dozens of academic LLM papers.

### 2.2 C4 — Colossal Clean Crawled Corpus (Google, 2020)

**Release:** 2020 (with T5 paper) | **Size:** ~800 GB / ~156B tokens | **License:** ODC-BY
**arXiv:** 1910.10683 (Raffel et al., 2020, *JMLR* 21(140)) [OA cit: 8,327]

Produced for training T5 (Text-to-Text Transfer Transformer). Derived from Common Crawl with extensive filtering: removed pages with low proportions of natural language, pages with profanity (using a word list), deduplicated at sentence level, removed lorem ipsum and boilerplate. The filtering methodology was documented in the T5 paper and has been widely replicated. C4 established the standard approach of starting from Common Crawl and applying quality heuristics — the approach subsequently adopted by The Pile, RefinedWeb, Dolma, and FineWeb.

Models trained on it: T5 (all sizes), Flan-T5, and many academic models.

### 2.3 RedPajama-v1 and v2 (Together AI, 2023)

**Release:** v1 April 2023, v2 October 2023 | **Size:** v1 ~1.2T tokens; v2 ~30T tokens (unfiltered) | **License:** Various (component-dependent)
**Source:** github.com/togethercomputer/RedPajama-Data

The first attempt to openly reproduce LLaMA's training data composition. RedPajama-v1 replicated LLaMA's seven-component mixture (Common Crawl, C4, GitHub, Wikipedia, Books, arXiv, StackExchange) at scale. RedPajama-v2 extended to a much larger unfiltered Common Crawl snapshot with quality annotations (but no pre-filtered version released by default). The project demonstrated that frontier model training data can be approximately reproduced from public sources — directly challenging the "proprietary data moat" narrative. Quality signals in v2 allow downstream users to construct filtered subsets; the unfiltered release reflects a philosophy of "provide the raw material and let the community filter."

### 2.4 Dolma (Allen Institute for AI / AI2, 2024)

**Release:** February 2024 | **Size:** ~3T tokens | **License:** ImpACT (tiered by use case)
**arXiv:** 2402.00159 (Soldaini et al., 2024) [OA cit: 9]

The most carefully documented large pretraining corpus released as of 2025. Dolma was designed as a fully open, reproducible corpus with explicit documentation of every data source, every filtering decision, and every quality heuristic applied. Components: Common Crawl (filtered), GitHub, Reddit, Semantic Scholar Open Research Corpus (ORCS), Project Gutenberg, Wikipedia/Wikibooks, and C4. Each component is separately documented with provenance, filtering methodology, and license analysis. The ImpACT license distinguishes low-risk (academic research, non-commercial) from higher-risk uses — a more nuanced governance model than blanket open licenses.

Models trained on it: OLMo (Allen Institute's fully open LLM series) — the only frontier-scale model with fully documented, reproducible training.

### 2.5 FineWeb (Hugging Face, 2024)

**Release:** April 2024 | **Size:** 15T tokens (full); ~1.3T tokens (FineWeb-Edu filtered) | **License:** ODC-BY
**arXiv:** 2406.17557 (Penedo et al., 2024) [OA cit: 19]

A landmark in the curation turn. FineWeb is derived from 96 Common Crawl snapshots with a documented multi-stage filtering pipeline: URL-based filtering, text extraction (trafilatura), quality heuristics (repetition filters, stop-word ratios, character-level statistics), deduplication (MinHash at paragraph level). The key finding: models trained on FineWeb-filtered data outperform models trained on larger unfiltered Common Crawl subsets, demonstrating quality > quantity at constant compute. FineWeb-Edu applies an additional educational-quality classifier, further improving benchmark performance for reasoning tasks.

FineWeb is arguably the highest-quality openly documented web-text pretraining corpus available as of 2025.

### 2.6 DCLM-Baseline (DataComp-LM, 2024)

**Release:** June 2024 | **Size:** 3.8T tokens | **License:** Various
**arXiv:** 2406.11794 (Li et al., 2024) [OA cit: 7]

DataComp-LM established dataset curation as a reproducible experimental science. The project ran controlled training runs varying the curation pipeline while holding model architecture and compute constant — analogous to DataComp for multimodal models. DCLM-Baseline is the best-performing curation pipeline identified: it applies an English language filter, quality heuristics, deduplication, and — critically — a model-based quality filter trained on high-quality text (OpenHermes instructions). The finding: model-based quality filtering substantially outperforms heuristic filtering, at the cost of requiring an initial high-quality seed dataset to train the filter.

---

## §3 Code Corpora

### 3.1 The Stack (BigCode / Hugging Face, 2022–2024)

**Release:** v1 November 2022; v2 February 2024 | **Size:** v1 3.1 TB / 30 programming languages (Kocetkov et al., 2022); v2 training set 4× larger across 619 programming languages, 3.3–4.3T training tokens for StarCoder2 (Lozhkov et al., 2024) | **License:** Custom (RAIL)
**arXiv:** 2211.15533 (Kocetkov et al., 2022) [OA cit: 38] · 2402.19173 (Lozhkov et al., 2024) [OA cit: 60]

The reference corpus for code LLM training. The Stack v1 contains 3.1 TB of source code in 30 programming languages scraped from GitHub repositories with permissive licenses, with near-deduplication shown to substantially improve downstream performance (Kocetkov et al., 2022). Even v1 shipped with a rights-aware governance layer — an "Am I in The Stack" tool plus a documented code-removal process. The Stack v2 (Lozhkov et al., 2024), built in partnership with Software Heritage on top of its source-code archive, expands coverage to 619 programming languages, adds high-quality auxiliary sources (GitHub pull requests, Kaggle notebooks, code documentation), and releases Software Heritage persistent IDentifiers (SWHIDs) for the training corpus — the strongest transparency posture of any production-scale code dataset. Take-up rates of opt-out and the practical impact on model capability remain unstudied.

Models trained on it: StarCoder, StarCoder2 (3B/7B/15B trained on 3.3–4.3T tokens of Stack v2), CodeLlama (Meta), and most open-source code LLMs.

### 3.2 GitHub public repository snapshots

Used in: LLaMA (Meta), GPT-3 (OpenAI). Exact composition undisclosed for most commercial models. GitHub data has been a component of most frontier LLM training runs, but the specific snapshot dates, filtering criteria, and deduplification methodology are not publicly documented for GPT-4, Claude, or Gemini.

---

## §4 Instruction Tuning and Alignment Datasets

| Dataset | Year | Size | Source | License | Notable use |
|---------|------|------|--------|---------|-------------|
| FLAN collection (Google) | 2021–2022 | ~1,800 tasks | Assembled from existing NLP datasets | Various | Flan-T5, Flan-PaLM instruction tuning |
| Alpaca (Stanford) | 2023 | 52K instructions | GPT-3.5 generated via self-instruct | CC BY-NC | Alpaca-7B; popularized synthetic instruction data |
| OpenAssistant (LAION) | 2023 | ~161K conversations | Human-annotated conversations | Apache-2.0 | First large-scale open RLHF-style dataset |
| HH-RLHF (Anthropic) | 2022 | 169K comparisons | Human preference judgments | MIT | Foundation for RLHF research; widely replicated |
| UltraFeedback | 2023 | 256K instructions | GPT-4 rated multiple model outputs | MIT | High-quality preference data for DPO |
| OpenHermes 2.5 | 2023 | 1M instructions | Synthetic from GPT-4 and open models | CC BY 4.0 | High-quality general instruction following |
| WizardLM Evol-Instruct | 2023 | Various sizes | GPT-4 evolved instructions | Various | Capacity evolution approach to synthetic data |
| Tulu 2 (AI2) | 2023 | 326K instructions | Curated mixture from multiple sources | ODC-BY | Systematic study of instruction mix effects |

**Key pattern:** The instruction tuning landscape bifurcated sharply in 2022–2023. The closed track (OpenAI, Anthropic, Google) uses proprietary human preference data at scale — the composition undisclosed. The open track produced an ecosystem of increasingly high-quality synthetic datasets generated by prompting closed models — raising the circularity concern that open models fine-tuned on GPT-4 outputs are constrained by GPT-4's capabilities and biases.

---

## §5 Multimodal Datasets

### 5.1 LAION-5B (LAION e.V., 2022)

**Release:** October 2022 | **Size:** 5.85B image-text pairs | **License:** CC BY 4.0
**arXiv:** 2210.08402 (Schuhmann et al., *NeurIPS 2022*) [OA cit: 1,035]

The dataset that enabled the open-source image generation revolution. LAION-5B is a web-scraped collection of image-URL and alt-text pairs filtered by CLIP similarity score, providing a high-volume open alternative to Google's and OpenAI's proprietary image-text training sets. Used to train Stable Diffusion (Stability AI), OpenCLIP, and most major open image-generation models.

Critically: LAION-5B was found in December 2023 to contain links to child sexual abuse material (Stanford Internet Observatory report). LAION temporarily took the dataset offline and released Re-LAION-5B (2024 — exact release date unconfirmed in primary sources) with known CSAM URLs removed. The incident established the governance principle that web-scraped datasets require safety auditing by external parties, not just internal quality filtering.

### 5.2 DataComp (Gadre et al., 2023)

**Release:** 2023 | **Size:** 12.8B image-text pairs (raw pool); various filtered subsets | **License:** Various
**arXiv:** 2304.14108 (Gadre et al., *NeurIPS 2023* Datasets Track) [OA cit: 74]

DataComp established multimodal dataset curation as an experimental science with a systematic competition structure: fixed model architecture and compute, variable curation pipeline. The DataComp-1B filtered subset (1.28B pairs) trains CLIP models that match or exceed models trained on LAION-2B at equivalent scale, demonstrating that curation quality substantially outperforms raw size for multimodal data — parallel to the FineWeb finding for text.

---

## §6 Domain-Specific High-Quality Datasets

| Domain | Dataset | Year | Size | Notes |
|--------|---------|------|------|-------|
| Scientific literature | S2ORC (Semantic Scholar) | 2020 | 81M papers | Parsed full text from open-access papers |
| Scientific literature | PeS2o (AI2) | 2023 | 40M papers | Cleaned S2ORC for LLM pretraining |
| Mathematics | MATH (Hendrycks et al.) | 2021 | 12.5K problems | Competition math with step-by-step solutions |
| Mathematics | DM Mathematics | 2019/ongoing | Various | DeepMind synthetic mathematics curriculum |
| Formal proofs | Lean 4 / Mathlib | Ongoing | ~150K theorems | Machine-verifiable mathematical proofs |
| Medical | MIMIC-IV Notes | 2023 | ~330K clinical notes | Deidentified, requires DUA |
| Legal | FreeLaw / CourtListener | 2020+ | ~7M court opinions | US federal/state court decisions |
| Finance | BloombergGPT training data | 2023 | 363B tokens | Proprietary Bloomberg financial corpus; composition described in paper |
| Multilingual | mC4 (Google) | 2021 | 101 languages | Multilingual C4 variant from Common Crawl |
| Multilingual | ROOTS (BigScience) | 2022 | 1.6TB, 59 languages | Most linguistically diverse documented corpus |

---

## §7 Evaluation Benchmarks (2020–2026)

Benchmarks are not training data but shape training data selection — models are implicitly or explicitly optimized to perform well on them.

| Benchmark | Year | Tasks | Measures | Key finding/use |
|-----------|------|-------|----------|-----------------|
| MMLU (Hendrycks et al.) | 2020 | 57 academic subjects | Broad world knowledge | Standard measure of general capability; near-saturated by GPT-4 |
| HumanEval (OpenAI) | 2021 | 164 Python functions | Code generation | Standard code benchmark; near-saturated by 2023 |
| GSM8K (Cobbe et al.) | 2021 | 8.5K math word problems | Grade-school math reasoning | Chain-of-thought training target |
| MATH (Hendrycks et al.) | 2021 | 12.5K competition math | Advanced math reasoning | Still challenging as of 2025 |
| BIG-Bench (Google) | 2022 | 204 tasks | Diverse capabilities | Effort to go beyond NLP benchmarks |
| HELM (Stanford) | 2022 | 42 scenarios | Holistic model evaluation | Includes fairness, calibration, toxicity |
| MMMU | 2023 | 11.5K questions | Multimodal reasoning | Replaces image-specific benchmarks |
| GPQA (Rein et al.) | 2023 | 448 PhD-level science | Expert-level reasoning | Resists Google-assisted cheating |
| SWE-bench (Yang et al.) | 2024 | 2,294 GitHub issues | Real-world software engineering | Agentic coding capability |
| LiveBench | 2024 | Continuously updated | Anti-contamination | Monthly refresh to prevent memorization |

**Benchmark contamination note:** As evaluation benchmarks proliferate and their questions circulate widely online, the risk that benchmark questions appear in pretraining corpora increases. Several papers have documented anomalously high performance on specific benchmarks consistent with training data contamination (Golchin & Surdeanu, 2023, arXiv:2308.08493 [OA cit: 22]). LiveBench and dynamic benchmarks represent a governance response.

---

## §8 The Curation Turn: Quality Over Quantity

The most significant methodological shift of the 2020–2026 period is empirical confirmation that data quality matters more than data quantity at fixed compute budgets.

**Key evidence:**

1. **FineWeb vs. raw Common Crawl:** Penedo et al. (2024, arXiv:2406.17557) released FineWeb (15T tokens, 96 Common Crawl snapshots, multi-stage filtering pipeline) and demonstrated through controlled training runs that models trained on FineWeb-filtered data outperform those trained on competing open web corpora (RefinedWeb, C4, Dolma, SlimPajama) at matched compute. The paper does not claim a single "2× efficiency" number; rather, the gain varies by benchmark and is largest on knowledge-intensive tasks. The FineWeb-Edu subset (1.3T tokens, educational-quality classifier) yields further gains on reasoning benchmarks such as MMLU and ARC (Penedo et al., 2024, abstract).

2. **Phi series (Microsoft, 2023–2024):** Phi-1 (1.3B parameters), Phi-1.5 (1.3B), Phi-2 (2.7B), Phi-3 (3.8B) demonstrated that training on GPT-4-quality synthetic "textbook" data enabled small models to match or exceed much larger models on reasoning benchmarks. Abdin et al. (2024, arXiv:2404.14219, [OA cit: 150]) report that Phi-3-mini (3.8B parameters) reaches MMLU 69% and matches Mixtral 8x7B and GPT-3.5 across several benchmarks while small enough to run on a phone — a ~1/10× to 1/30× parameter advantage at parity for the specific benchmarks reported.

3. **DCLM competition:** The DataComp-LM systematic curation experiment showed that model-based quality filtering (training a filter on high-quality seed data) substantially outperforms heuristic filtering at constant compute.

4. **Dolma ablations:** Groeneveld et al. (2024, *Proc. ACL 2024 Long Papers*, arXiv:2402.00838 [OA cit: 52]) released OLMo together with Dolma's systematic ablations documenting the effect of each data source on downstream performance — the most rigorous publicly available evidence for training data composition effects, made possible because both model and corpus are fully open.

The implication for hybrid intelligence research: the most capable open models are no longer distinguished primarily by scale but by curation methodology. The competitive frontier has shifted from "who can process the most data" toward "who has the best curation pipeline" — a shift that opens genuine competition between well-resourced and less-resourced research groups.

---

## §9 Provenance, Consent, and Governance Landscape (2020–2026)

| Dataset | Provenance documented | License clear | Consent mechanism | Opt-out |
|---------|----------------------|---------------|-------------------|---------|
| The Pile | Yes (22 sources named) | Partial (Books3 removed) | None | No |
| C4 | Partial (Common Crawl + heuristics) | ODC-BY | None | Via robots.txt |
| Dolma | Full documentation | ImpACT tiered | None (public web) | Via robots.txt |
| FineWeb | Full pipeline docs | ODC-BY | None | Via robots.txt |
| The Stack v2 | Good | RAIL | None | **Yes — opt-out implemented** |
| LAION-5B / Re-LAION | URL sources listed | CC BY 4.0 | None | Spawning.ai |
| GPT-3/4 training data | Undisclosed | Proprietary | None | None |
| LLaMA 1/2/3 | Partially described | Custom | None | None |
| Claude training data | Undisclosed | Proprietary | None | None |

**Longpre et al. (2024, arXiv:2407.14933 [OA cit: 10]) "Consent in Crisis"** audited a corpus of widely used training datasets (drawing on a Data Provenance Initiative collection of ~14,000 web-data sources spanning C4, RefinedWeb, Dolma) and documented two interlocking trends: (i) a sharp rise since 2023 in robots.txt restrictions and ToS prohibitions on commercial AI training, with the most-trafficked domains restricting the fastest; and (ii) a persistent inconsistency between robots.txt-level restrictions and the broader ToS, leaving rights-holder intent ambiguous. The audit also documents the broader provenance gap for instruction-tuning and RLHF data, where original rights-holder consent is rarely traceable.

**The Stack opt-out** is the only large-scale implementation of a rights-based opt-out mechanism in production. As of 2024, hundreds of thousands of developers had submitted opt-out requests; the practical effect on model capability has not been publicly evaluated.

---

## §10 What Is Missing: Gaps in the 2020–2026 Dataset Landscape

**High-quality multilingual data.** Despite mC4 and ROOTS, the gap between English and other languages in training data quality and quantity remains large. The ROOTS corpus (Laurençon et al., *NeurIPS 2022 Datasets Track*, arXiv:2303.03915) — 1.6 TB across 59 languages — remains the most linguistically diverse documented pretraining corpus, but its non-English components are an order of magnitude smaller than English C4 and FineWeb. Models trained predominantly on English data exhibit systematic performance degradation on other languages, and the gap is most pronounced for low-resource and non-Latin-script languages.

**Domain-specific open datasets for professional fields.** Legal, medical, and financial training data of documented quality and appropriate governance exists primarily as proprietary assets. The open alternatives (FreeLaw, PubMed, S2ORC) are valuable but incomplete.

**Longitudinal/temporal training data.** Most large pretraining corpora are snapshots; models trained on them have a knowledge cutoff and cannot update incrementally. Dynamic training data infrastructure — allowing models to incorporate new information without full retraining — is an active research gap.

**Behavioral and interaction data.** RLHF preference data, the primary mechanism for aligning LLMs with human values, remains almost entirely proprietary. The most capable alignment datasets (Anthropic HH-RLHF is a partial exception) are not published; the alignment of open models depends on either distilling from closed models (raising circularity concerns) or on volunteer annotation efforts of limited scale.

---

## Key Sources

- Gao, L., Biderman, S., Black, S., Golding, L., et al. (2020). The Pile: An 800GB dataset of diverse text for language modeling. arXiv:2101.00027. [P] [PDF: Kilder/Gao2020_ThePile_arXiv2101.00027.pdf] [OA cit: 484]
- Raffel, C., Shazeer, N., Roberts, A., Lee, K., et al. (2020). Exploring the limits of transfer learning with a unified text-to-text transformer. *Journal of Machine Learning Research, 21*(140), 1–67. arXiv:1910.10683. [J] [PDF: Kilder/Raffel2020_T5_JMLR_arXiv1910.10683.pdf] [OA cit: 8,327]
- Penedo, G., Malartic, Q., Hesslow, D., Cojocaru, R., et al. (2023). The RefinedWeb dataset for Falcon LLM: Outperforming curated corpora with web data, and web data only. arXiv:2306.01116. [P] [PDF: Kilder/Penedo2023_RefinedWeb_arXiv2306.01116.pdf] [OA cit: 156]
- Soldaini, L., Kinney, R., Bhagia, A., Schwenk, D., et al. (2024). Dolma: An open corpus of three trillion tokens for language model pretraining research. arXiv:2402.00159. [P] [PDF: Kilder/Soldaini2024_Dolma_arXiv2402.00159.pdf] [OA cit: 9]
- Penedo, G., Kydlíček, H., Ben Allal, L., Lozhkov, A., et al. (2024). The FineWeb datasets: Decanting the web for the finest text data at scale. arXiv:2406.17557. [P] [PDF: Kilder/Penedo2024_FineWeb_arXiv2406.17557.pdf] [OA cit: 19]
- Li, J., Fang, A., Smyrnis, G., Ivgi, M., et al. (2024). DataComp-LM: In search of the next generation of training sets for language models. arXiv:2406.11794. [P] [PDF: Kilder/Li2024_DCLM_arXiv2406.11794.pdf] [OA cit: 7]
- Kocetkov, D., Li, R., Ben Allal, L., Li, J., et al. (2022). The Stack: 3 TB of permissively licensed source code. arXiv:2211.15533. [P] [PDF: Kilder/Kocetkov2022_TheStack_arXiv2211.15533.pdf] [OA cit: 38] [OpenAlex `is_retracted`: False, checked 2026-05-11]
- Lozhkov, A., Li, R., Ben Allal, L., Cassano, F., et al. (2024). StarCoder 2 and The Stack v2: The next generation. arXiv:2402.19173. [P] [PDF: Kilder/Lozhkov2024_StarCoder2_TheStackV2_arXiv2402.19173.pdf] [OA cit: 60] [OpenAlex `is_retracted`: False, checked 2026-05-11] — primary source for The Stack v2 (619 programming languages; SWHIDs released for training corpus).
- Schuhmann, C., Beaumont, R., Vencu, R., Gordon, C., et al. (2022). LAION-5B: An open large-scale dataset for training next generation image-text models. *Advances in Neural Information Processing Systems, 35* (NeurIPS 2022 Datasets Track). arXiv:2210.08402. [C] [PDF: Kilder/Schuhmann2022_LAION5B_NeurIPS2022_arXiv2210.08402.pdf] [OA cit: 1,035]
- Gadre, S. Y., Ilharco, G., Fang, A., Hayase, J., et al. (2023). DataComp: In search of the next generation of multimodal datasets. *Advances in Neural Information Processing Systems, 36* (NeurIPS 2023 Datasets Track). arXiv:2304.14108. [C] [PDF: Kilder/Gadre2023_DataComp_arXiv2304.14108.pdf] [OA cit: 74]
- Hendrycks, D., Burns, C., Basart, S., Zou, A., et al. (2021). Measuring massive multitask language understanding. *International Conference on Learning Representations (ICLR 2021)*. arXiv:2009.03300. [C] [PDF: Kilder/Hendrycks2020_MMLU_arXiv2009.03300.pdf] [OA cit: 276]
- Longpre, S., Mahari, R., Lee, A., Lund, C., et al. (2024). Consent in crisis: The rapid decline of the AI data commons. arXiv:2407.14933. [P] [PDF: Kilder/Longpre2024_ConsentInCrisis_arXiv2407.14933.pdf] [OA cit: 10]
- Groeneveld, D., Beltagy, I., Walsh, P., Bhagia, A., et al. (2024). OLMo: Accelerating the science of language models. *Proceedings of the 62nd Annual Meeting of the ACL (Volume 1: Long Papers)*, 15789–15809. arXiv:2402.00838. https://doi.org/10.18653/v1/2024.acl-long.841. [C] [PDF: Kilder/Groeneveld2024_OLMo_ACL2024_arXiv2402.00838.pdf] [OA cit: 52] [CrossRef `update-to: None`, re-checked 2026-05-11; OpenAlex `is_retracted`: False]
- Abdin, M., Aneja, J., Awadalla, H., Awadallah, A., et al. (2024). Phi-3 technical report: A highly capable language model locally on your phone. arXiv:2404.14219. [R] (technical report) [PDF: Kilder/Abdin2024_Phi3_arXiv2404.14219.pdf] [OA cit: 150]
- Golchin, S., & Surdeanu, M. (2023). Time travel in LLMs: Tracing data contamination in large language models. arXiv:2308.08493. [P] [PDF: Kilder/Golchin2023_TimeTravelInLLMs_arXiv2308.08493.pdf] [OA cit: 22]
- Laurençon, H., Saulnier, L., Wang, T. J., Akiki, C., et al. (2022). The BigScience ROOTS corpus: A 1.6 TB composite multilingual dataset. *Advances in Neural Information Processing Systems, 35* (NeurIPS 2022 Datasets Track). arXiv:2303.03915. [C] [OA cit: 65]
- Bommasani, R., et al. (2024). The Foundation Model Transparency Index v1.1: May 2024. arXiv:2407.12929. [P] [PDF: Kilder/Bommasani2024_FoundationModelTransparencyIndex.pdf] [OA cit: 7] — preprint; the 2023 v1.0 (arXiv:2310.12941) carries the higher citation counts. See also Wan et al. (2025), arXiv:2501.16024, for the 2025 update.
- Wan, A., et al. (2025). The Foundation Model Transparency Index 2025. arXiv:2501.16024. [P] — 2025 update, 18 developers.

---

## §11 Synthesis: What the 2020–2026 Dataset Landscape Means for Hybrid Intelligence

The central finding of this period is that ML capability is, at its foundation, a data curation problem. The scaling hypothesis was correct that more data and compute produce better models — but the curation turn demonstrated that better-selected, better-filtered, better-documented data produces substantially better models than raw volume at equivalent compute. The frontier of AI capability in 2025 is not primarily constrained by compute availability or architectural innovation; it is constrained by the availability of high-quality, well-curated, domain-appropriate training data.

For hybrid intelligence research — systems that combine human and machine capabilities — this has a specific implication: the alignment between human values, knowledge, and judgment, and the behavior of AI components, is itself a data problem. RLHF preference data is largely proprietary. Instruction-tuning datasets for open models are mostly synthetic, generated by closed models, creating circularity. The behavioral data that shapes what foundation models know about human reasoning, professional practice, and social norms is held by a small number of commercial platforms with minimal regulatory transparency.

The two-tier dataset ecosystem documented here — open, reproducible, well-governed (Dolma, FineWeb, The Stack) alongside closed, opaque, commercially controlled (GPT-4, Claude, Gemini training corpora) — mirrors the broader hybrid intelligence challenge: open scientific research cannot easily replicate, audit, or improve upon systems whose foundations are undisclosed. Addressing this gap requires both governance mechanisms that require training data documentation (as the EU AI Act begins to do) and sustained investment in high-quality open data infrastructure as a public good.

---

*Iteration history: see `Chapter drafts/changelogs/ax-changelog.md`.*
