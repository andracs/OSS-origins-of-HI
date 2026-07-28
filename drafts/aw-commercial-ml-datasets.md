# Draft AW: The Dataset Economy — Commercially Available Machine Learning Datasets, Labeling Infrastructure, and the Market for Training Data

**Version:** v0.6 | **Status:** Draft — §1 GLUE/SuperGLUE inline citations now anchored to full Key Sources entries (Wang et al., 2018 EMNLP BlackboxNLP; Wang et al., 2019); §2 Sama/OpenAI Kenyan-moderator paragraph anchored to Perrigo (2023) *TIME* with explicit cross-link to Draft AF §2.3; OA cit metrics refreshed on Sambasivan (650) and Pushkarna (170); GLUE (Wang 2018) and Krizhevsky (2012 CACM) CrossRef retraction-clean as of 2026-05-18.
**Handbook:** Springer Handbook of Hybrid Intelligence
**Related drafts:** C (training data memorization), F (commons extraction), K (openness layers), N (AI/ML ecosystem), AF (invisible workforce), AV (social media training data)

---

## Abstract

Machine learning models do not train on raw data — they train on *curated, labeled, and quality-controlled* datasets that require substantial human and computational effort to produce. This chapter maps the ecosystem of commercially available ML training datasets: from the foundational academic benchmarks (ImageNet, SQuAD, GLUE) whose curation shaped what AI systems learn to do, through the crowdsourced labeling markets (Scale AI, Sama, Appen) that produce annotated training data at industrial scale, to domain-specific premium datasets (Bloomberg Terminal, Refinitiv, MIMIC-III) that encode expert knowledge inaccessible to web scraping, and the emerging synthetic data market (Gretel, Tonic, Mostly AI) that offers privacy-preserving alternatives to real user data. The chapter argues that the dataset economy is the largely invisible infrastructure layer of AI — less discussed than foundation models, less scrutinized than model outputs, but constitutively determining what those models can know, do, and get wrong. Drawing on Gebru et al.'s "Datasheets for Datasets" framework, Sambasivan et al.'s finding that data quality problems account for the majority of AI deployment failures, and Longpre et al.'s "Consent in Crisis" audit of dataset provenance on Hugging Face, the chapter establishes that the transition from academic dataset curation to commercial dataset production has created new points of concentration, new consent failures, and new quality risks — while also creating the only viable path to domain-specific AI capability in medicine, law, finance, and the physical sciences.

---

## §1 From Academic Benchmarks to Commercial Infrastructure

The history of ML datasets follows a trajectory from scarcity to abundance that mirrors but lags the history of compute. For most of the discipline's first four decades, datasets were small, hand-curated, and published as research contributions alongside the models they were meant to evaluate.

The **ImageNet moment** (2009–2012) marks the inflection point. Fei-Fei Li and collaborators built a dataset of 14 million labeled images across 22,000 categories using Amazon Mechanical Turk — the first large-scale use of crowdsourced annotation for a dataset that would become standard infrastructure. The ImageNet Large Scale Visual Recognition Challenge (ILSVRC), launched in 2010, created the benchmarking culture that still structures AI evaluation: a fixed, publicly held test set; annual leaderboards; and performance improvement as proxy for progress. When AlexNet (Krizhevsky, Sutskever & Hinton, 2012) won ILSVRC 2012 with a top-5 error rate of 15.3% — compared to the previous year's best of 26.2% — it validated both the deep learning approach and the dataset-as-benchmark methodology. ImageNet's labeling methodology, its Western sampling bias, and its hierarchical category structure shaped a decade of computer vision research in ways that were not fully articulated until Birhane and Prabhu (2021) documented the dataset's extensive encoding of racial and gendered stereotypes — including pornographic, derogatory, and racist labels in the WordNet-derived category hierarchy that the original ImageNet curators had inherited without auditing.

The NLP equivalent is the **GLUE/SuperGLUE lineage** (Wang et al., 2018; Wang et al., 2019), which packaged multiple natural language understanding tasks into a single benchmarking framework. GLUE saturated within two years of publication — models exceeded human performance on most tasks — triggering the creation of SuperGLUE, which similarly saturated. The benchmark treadmill this created — datasets published, saturated, replaced — is now recognized as a structural problem: benchmark saturation measures model performance on the benchmark, not necessarily on the underlying capability, and optimizing for benchmark performance can diverge from real-world utility (Raji, Bender, Paullada et al., 2021).

The transition from academic to commercial dataset production happened not through a single event but through the scaling of annotation infrastructure.

---

## §2 The Labeling Market: Scale AI, Sama, Appen, and the Crowdsourced Annotation Economy

Between the raw data (scraped web content, sensor readings, user-generated media) and the labeled training dataset lies a labor-intensive annotation process: humans must identify objects in images, transcribe speech, classify sentiment, rate response quality, or answer questions about content. For large-scale datasets, this work cannot be performed by academic research teams — it requires industrial annotation infrastructure.

**Scale AI** (founded 2016) is the dominant provider of data labeling services for AI training. Its clients include OpenAI, Meta, Microsoft, the US Department of Defense, and most major autonomous vehicle companies. Scale AI's platform manages a global workforce of data labelers who annotate images, video, text, audio, and 3D sensor data to produce training datasets. The company's CEO has described its business as "the data layer of AI" — an infrastructure layer that is essential to AI capability but almost entirely invisible to end users.

**Sama** (formerly Samasource, founded 2008) pioneered the ethical sourcing model for annotation labor, explicitly targeting workers in Sub-Saharan Africa and Southeast Asia. Its governance model emphasizes living wages, skill development, and community investment — a contrast to Mechanical Turk's piece-rate structure. Sama publicly lists major technology platforms among its clients; the company drew international scrutiny in 2023 after the *TIME* investigation by Perrigo (2023) documented that Kenyan workers contracted via Sama to label toxic text for OpenAI's content-classifier pipeline earned between $1.32 and $2.00 per hour and described the work — which included explicit descriptions of sexual abuse, violence, and self-harm — as psychologically damaging; Sama subsequently terminated the OpenAI contract early, citing its own welfare policies (see Draft AF §2.3 for the broader analysis of RLHF and content-moderation labor conditions in Kenya, the Philippines, and Latin America).

**Appen** (ASX: APX, founded 1996) is one of the oldest and largest annotation companies, with a global crowd of more than one million contributors. Its services span data collection, annotation, and model evaluation. Appen's clients are primarily the major technology platforms; its work includes annotating search results for relevance, evaluating AI assistant responses, and producing speech training data in hundreds of languages.

**Amazon Mechanical Turk (MTurk)** remains the foundational crowdsourcing platform for annotation tasks, used extensively in academic research and by smaller AI companies. MTurk's pay structure — piece-rate microtasks — is documented as producing effective pay rates well below the US federal minimum wage for most workers. Hara et al. (2018, *CHI*) recorded 2,676 workers performing 3.8 million tasks and found a median hourly wage of approximately $2/hour, with only 4% of workers earning more than the US federal minimum wage of $7.25/hour — even though average requester *postings* paid more than $11/hour, because lower-paying requesters posted disproportionately more work. The gap between posted rates and realized wages reflects unpaid time spent searching for tasks, completing tasks that are rejected, and abandoning tasks that are never submitted.

The ghost work analysis of Draft AF applies with particular force to the annotation economy: the human intelligence that makes AI systems function — the millions of hours of object identification, content rating, and preference labeling — is structurally invisible in AI products and marketing, with workers facing precarious employment, algorithmic management, and no ownership stake in the systems their labor enables (Gray & Suri, 2019).

---

## §3 Domain-Specific Premium Datasets

Web-scraped text captures the general knowledge commons. It does not capture the specialized knowledge that makes AI systems useful in high-stakes domains. Domain-specific ML datasets represent a distinct market: curated, cleaned, and licensed data from fields where expertise and access are both scarce.

**Finance.** Bloomberg LP's financial data terminal holds the most comprehensive machine-readable record of financial news, earnings transcripts, analyst reports, and market data in existence. Bloomberg's partnership with AI developers — including the BloombergGPT project (Wu et al., 2023, arXiv:2303.17564), which trained a 50-billion parameter model on a financial corpus assembled in part from Bloomberg's archives augmented with public financial text — represents a model of institutional data licensing for domain-specific AI. Refinitiv (now LSEG) and FactSet offer comparable financial data products with AI licensing terms.

**Medicine.** MIMIC (Medical Information Mart for Intensive Care) is the most widely used clinical AI training dataset — de-identified electronic health records from intensive care units at Beth Israel Deaconess Medical Center, maintained by MIT's Laboratory for Computational Physiology. Access requires formal data use agreements and human subjects training, creating a governance layer absent from most commercial datasets. MIMIC-III contains records for more than 40,000 patients; MIMIC-IV extends the time range to 2022. The dataset's use in training clinical decision support AI systems raises questions about demographic representativeness — MIMIC's patient population reflects a single Boston academic medical center, limiting generalization to other populations and healthcare settings (the underlying PhysioNet infrastructure that hosts MIMIC was established by Goldberger et al., 2000, *Circulation*).

**Law.** Legal AI training data is particularly sensitive: court documents, contracts, and legal opinions are often technically public but contain personally identifying information, confidential business details, and jurisdiction-specific constraints on reproduction. PACER (Public Access to Court Electronic Records) in the US contains federal court documents; commercial providers including LexisNexis, Westlaw, and vLex have entered AI licensing arrangements. Harvey AI (legal AI startup) has a data partnership with Allen & Overy; Casetext, acquired by Thomson Reuters in 2023, brought its CoCounsel legal AI assistant under the same corporate umbrella as Westlaw — consolidating legal AI tooling and the legal text corpus on which it relies into a single commercial entity.

**Scientific literature.** Elsevier, Springer Nature, and Wiley — the three largest academic publishers — collectively control access to the majority of peer-reviewed scientific literature. Each has launched AI licensing programs that allow foundation model developers to license journal content for training, at fees that have not been publicly disclosed. The academic open-access movement partially counters this: PubMed Central (free access to biomedical literature), arXiv (physics, mathematics, computer science, quantitative biology), and SSRN (social sciences) provide substantial open training corpora in specific fields.

---

## §4 The Hugging Face Datasets Hub: Democratization and Its Limits

Hugging Face's Datasets Hub, launched in 2019, is the most significant development in ML dataset accessibility since ImageNet. It hosts more than 100,000 datasets spanning NLP, computer vision, audio, multimodal, and reinforcement learning tasks, all accessible through a unified API and version control system. The Hub has democratized dataset access for academic researchers and small organizations in a manner analogous to what GitHub did for code.

However, Longpre et al.'s "Consent in Crisis" (2024) audit of the Hub's contents documented a structural governance problem: a large proportion of the most widely used datasets have unclear or absent provenance documentation — missing information about the copyright status of source material, whether consent was obtained for the specific use, and whether licensing terms permit commercial use. The audit (Longpre et al., 2024, arXiv:2407.14933) examined nearly 14,000 web domains and approximately 4,000 datasets across the dominant pretraining corpora (C4, RefinedWeb, Dolma) and found that licensing terms had become more restrictive over time — the proportion of fully permissively licensed tokens declined from a clear majority in earlier corpora to a substantially smaller share by 2023–2024, while a growing fraction of source domains have explicitly disallowed AI training in their `robots.txt` or terms of service.

The Hub's design reflects an interesting governance tension: it provides infrastructure for dataset sharing analogous to GitHub's infrastructure for code sharing, but the dataset equivalent of a software license — a clear statement of permitted uses, attribution requirements, and distribution terms — is frequently absent, ambiguous, or inconsistently applied.

---

## §5 Synthetic Data: The Emerging Alternative

The consent, privacy, and provenance problems of real-world training data have driven substantial investment in **synthetic data** — algorithmically generated data that preserves the statistical properties of real data without containing real individuals' information.

**Gretel AI**, **Tonic.ai**, **Mostly AI**, and **YData** are the primary commercial synthetic data providers. Their products generate tabular data, text, images, and time series that can substitute for real training data in contexts where privacy regulations (GDPR, HIPAA) or commercial sensitivity prohibit sharing real data. Healthcare and financial services are the primary markets: a hospital that cannot share patient records can generate synthetic patient records that preserve the clinical distribution without containing identifiable information.

The technical quality of synthetic data has improved substantially with generative model advances. Diffusion models can generate synthetic medical images (X-rays, pathology slides, MRI scans) that radiologists cannot reliably distinguish from real images; language models can generate synthetic financial narratives, legal documents, and customer service transcripts. The primary risk is **distributional mismatch**: synthetic data preserves the statistical properties of the training distribution used to generate it, but may fail to capture rare but important edge cases. A synthetic patient dataset generated from a particular hospital's records will inherit the demographic and clinical biases of that hospital.

The use of large language models to generate synthetic training data for smaller models — "model distillation through synthetic data" — has become a significant technique. Microsoft's Phi series of small models (Phi-1, Phi-1.5, Phi-3) was trained primarily on synthetic data generated to embody "textbook quality" — filtered and augmented web text plus GPT-3.5/4-generated educational content (Gunasekar et al., 2023, "Textbooks Are All You Need," arXiv:2306.11644; Li et al., 2023, "Textbooks Are All You Need II," arXiv:2309.05463; Abdin et al., 2024, "Phi-3 Technical Report," arXiv:2404.14219). The technique achieves remarkable performance per parameter on benchmarks, but also concentrates distributional bias from the generating model into the trained model.

---

## §6 The Dataset Market: Economics and Power

The commercial dataset market is poorly understood in economic terms because most transactions are not public. What is known:

**Reddit's licensing deals** (2024) provide the only public pricing anchor for large-scale text corpora. Reuters first reported the Reddit–Google arrangement at approximately $60 million per year (Reuters, 2024); Reddit's S-1 registration statement filed with the SEC shortly thereafter disclosed aggregate data-licensing contracts of approximately $203 million with terms of two to three years (Reddit, Inc., 2024). Applied as a per-token price to comparable user-generated platforms, the figure would value social media data at tens of billions of dollars — a stark contrast to the zero compensation actually paid to the users whose posts and comments constitute the licensed asset (see Draft AV §3.6 for the platform-side analysis; Draft AV §4 for the consent-architecture argument).

**Scale AI's scale** is most reliably anchored to its May 2024 Series F: the company raised $1 billion at a reported post-money valuation of approximately $13.8 billion, with the round led by Accel and including Nvidia, Amazon, Meta, Intel Capital, and AMD Ventures among the syndicate (Scale AI, 2024). Independent trade-press reporting placed annualized revenue in the high hundreds of millions of dollars at the time of the round (Konrad, 2024, *Forbes*). The implied magnitude — a single annotation vendor with valuation in the tens of billions of dollars and revenue approaching the $1 billion threshold — makes the broader annotation industry a multi-billion-dollar global market that is structurally absent from the AI value chain as typically described.

**Academic datasets** remain largely free, but the infrastructure to host and serve them is not. The compute costs of running the ImageNet download servers, the MIMIC access management system, or the Hugging Face Dataset Hub represent real infrastructure subsidized by universities, nonprofits, and venture capital. The sustainability of this free infrastructure at scale is not guaranteed.

**Benchmark contamination** — the inadvertent or deliberate inclusion of benchmark test sets in training data — is an increasing concern as the internet fills with benchmark questions and answers. If GPT-4 was trained on pages containing MMLU questions and answers, its MMLU performance measures memorization rather than capability. Detecting contamination is technically difficult; disclosure norms are weak; and the competitive incentives push against voluntary contamination disclosure.

---

## §7 Cross-Reference: AV (Social Platforms) and AW (Commercial Datasets) — The Spectrum

Draft AV and Draft AW together map a spectrum from **unlicensed extraction** to **commercial licensing**:

| Source type | Consent | Compensation | Governance | Example |
|-------------|---------|--------------|------------|---------|
| Open commons (web, GitHub, Wikipedia) | None | None | Weak (ToS, robots.txt) | Common Crawl, The Pile |
| Social platform data (AV) | ToS-implied, contested | None to users | Regulatory enforcement emerging | Meta/Llama, xAI/Grok |
| Reddit-style licensing | Platform-level, no user consent | Platform, not contributors | Emerging market norms | Reddit/Google ($60M/yr, $203M aggregate; Reuters, 2024; Reddit, Inc., 2024) |
| Crowdsourced annotation (AW) | Task-level consent | Piece-rate labor | Platform-managed, precarious | Scale AI, MTurk |
| Domain-specific licensed (AW) | Institutional agreements | Institutional | Data use agreements | Bloomberg, MIMIC |
| Synthetic data (AW) | No original data subjects | N/A | Provider terms | Gretel, Mostly AI |

The spectrum reveals that "training data" is not a single legal or governance category. The challenges for open-commons data (provenance, consent, extractive asymmetry) are structurally different from those for crowdsourced annotation data (labor rights, piece-rate pay, algorithmic management) or domain-licensed data (access concentration, market power). Governance proposals that address one point on the spectrum often fail to address others.

---

## §8 Governance Frameworks for Dataset Production

**Datasheets for Datasets** (Gebru et al., 2018/2021) proposed that ML datasets should be accompanied by standardized documentation — analogous to datasheets for electronic components — covering motivation, composition, collection process, preprocessing, uses, distribution, and maintenance. The framework has been widely cited but inconsistently adopted; the Hugging Face Dataset Hub's "Dataset Cards" system is the closest implementation at scale.

**Data Cards** (Pushkarna, Zaldivar & Kjartansson, 2022, *FAccT*) extend the datasheet concept with a focus on transparency for ML practitioners, providing structured templates for recording provenance, known biases, evaluation results, and usage recommendations.

**The EU AI Act's GPAI provisions** require training data disclosure for general-purpose AI models above a compute threshold, including whether copyrighted material was used and whether rights holders' permissions were obtained. This creates a direct regulatory demand for the kind of documentation that Datasheets for Datasets proposed voluntarily in 2018.

**The FMTI (Bommasani et al., 2024; Wan et al., 2025)** measures training data transparency as one of its ~100 indicators and consistently finds it among the most opaque categories — even among developers who achieve high overall transparency scores. The 2024 index (v1.1, arXiv:2407.12929) expanded coverage to 14 developers; the 2025 update (Wan et al., 2025, arXiv:2501.16024) extended to 18 developers with broadly similar findings.

---

## §9 Open Questions

1. **Is the annotation labor market a structural chokepoint for AI capability?** If Scale AI, Sama, and Appen collectively produce the RLHF preference data for most frontier models, do they constitute a concentration risk for the AI supply chain?

2. **Can synthetic data close the domain expertise gap at scale?** The Phi results suggest synthetic data can achieve remarkable benchmark performance; whether this translates to genuine domain capability in medicine, law, and science — where edge cases matter — is empirically unresolved.

3. **What does benchmark saturation signal?** If models exceed human performance on GLUE, SuperGLUE, MMLU, and HumanEval, but real-world deployment still fails on basic reasoning tasks, what is the correct unit of evaluation? Are benchmarks measuring anything meaningful about capability, or primarily measuring distributional fit to the benchmark itself?

4. **How should the dataset economy redistribute value to data contributors?** Reddit's licensing deal distributes value to Reddit shareholders, not to the users whose posts constitute the licensed asset. What governance architecture would route compensation to individual contributors at scale — and is this technically feasible?

5. **What happens to domain-specific AI when institutional dataset providers exit?** MIMIC depends on MIT and BIDMC funding; academic benchmark datasets depend on researcher time and grant funding. If the commercial value of AI datasets concentrates in proprietary systems, does the open-access research infrastructure that produced ImageNet, SQuAD, and GLUE become unsustainable?

---

## Key Sources

- Birhane, A., & Prabhu, V. U. (2021). Large image datasets: A pyrrhic win for computer vision? *2021 IEEE Winter Conference on Applications of Computer Vision (WACV)*, 1536–1546. https://doi.org/10.1109/WACV48630.2021.00158. [PDF: Kilder/Birhane2021_PyrrhicWin_WACV.pdf] [C] [OA cit: 246] [CrossRef retraction check 2026-05-18: clear]
- Gebru, T., Morgenstern, J., Vecchione, B., Vaughan, J. W., Wallach, H., Daumé III, H., & Crawford, K. (2021). Datasheets for datasets. *Communications of the ACM, 64*(12), 86–92. https://doi.org/10.1145/3458723. [J] [OA cit: 334] [CrossRef retraction check 2026-05-18: clear]
- Goldberger, A. L., Amaral, L. A. N., Glass, L., Hausdorff, J. M., Ivanov, P. C., Mark, R. G., Mietus, J. E., Moody, G. B., Peng, C.-K., & Stanley, H. E. (2000). PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals. *Circulation, 101*(23), e215–e220. https://doi.org/10.1161/01.CIR.101.23.e215. [J] [OA cit: 14318] [CrossRef retraction check 2026-05-05: clear]
- Gray, M. L., & Suri, S. (2019). *Ghost work: How to stop Silicon Valley from building a new global underclass*. Houghton Mifflin Harcourt. [R]
- Gunasekar, S., Zhang, Y., Aneja, J., Mendes, C. C. T., Del Giorno, A., Gopi, S., Javaheripi, M., Kauffmann, P., de Rosa, G., Saarikivi, O., Salim, A., Shah, S., Behl, H. S., Wang, X., Bubeck, S., Eldan, R., Kalai, A. T., Lee, Y. T., & Li, Y. (2023). *Textbooks are all you need*. arXiv:2306.11644. [PDF: Kilder/Gunasekar2023_TextbooksAllYouNeed_arXiv2306.11644.pdf] [P] [OA cit: 98]
- Hara, K., Adams, A., Milland, K., Savage, S., Callison-Burch, C., & Bigham, J. P. (2018). A data-driven analysis of workers' earnings on Amazon Mechanical Turk. *CHI 2018*. https://doi.org/10.1145/3173574.3174023. [C] [OA cit: 483] [CrossRef retraction check 2026-05-11: clear]
- Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks. *Advances in Neural Information Processing Systems 25 (NeurIPS 2012)*, 1097–1105. Reprinted (2017) in *Communications of the ACM, 60*(6), 84–90. https://doi.org/10.1145/3065386. [C/J] [OA cit: 75673] [CrossRef retraction check 2026-05-18: clear]
- Li, Y., Bubeck, S., Eldan, R., Del Giorno, A., Gunasekar, S., & Lee, Y. T. (2023). *Textbooks are all you need II: Phi-1.5 technical report*. arXiv:2309.05463. [P] [OA cit: 49]
- Longpre, S., Mahari, R., Lee, A., Lund, C., Oderinwale, H., Brannon, W., et al. (2024). *Consent in crisis: The rapid decline of the AI data commons*. arXiv:2407.14933. [PDF: Kilder/Longpre2024_ConsentInCrisis_arXiv2407.14933.pdf] [P] [OA cit: 10]
- Longpre, S., et al. (2025). Economies of open intelligence. arXiv:2512.03073. [PDF: Kilder/Longpre2025_EconomiesOpenIntelligence.pdf] [P] [iCit: 8]
- Bommasani, R., et al. (2024). The Foundation Model Transparency Index v1.1: May 2024. arXiv:2407.12929. [PDF: Kilder/Bommasani2024_FoundationModelTransparencyIndex.pdf] [P] [OA cit: 7] — preprint; no journal venue. Note: the 2023 v1.0 (arXiv:2310.12941) has higher citation counts (~41 OA cit); the [iCit: 174] figure in earlier entries referred to the v1.0.
- Wan, A., et al. (2025). The Foundation Model Transparency Index 2025. arXiv:2501.16024. [P] — 2025 update covering 18 developers.
- Konrad, A. (2024, May 21). Scale AI raises $1 billion at $13.8 billion valuation in funding round led by Accel. *Forbes*. [R] — trade-press anchor for the May 2024 Series F and the disclosed annualized revenue range; corroborated by simultaneous Reuters, Bloomberg, and WSJ reporting.
- Perrigo, B. (2023, January 18). Exclusive: OpenAI used Kenyan workers on less than $2 per hour to make ChatGPT less toxic. *TIME*. https://time.com/6247678/openai-chatgpt-kenya-workers/ [R] — investigative journalism; primary anchor for the Sama/OpenAI content-classifier labor case used in §2 here and developed in Draft AF §2.3.
- Pushkarna, M., Zaldivar, A., & Kjartansson, O. (2022). Data cards: Purposeful and transparent dataset documentation for responsible AI. *2022 ACM Conference on Fairness, Accountability, and Transparency (FAccT '22)*, 1776–1826. https://doi.org/10.1145/3531146.3533231. [C] [OA cit: 170] [CrossRef retraction check 2026-05-11: clear]
- Raji, I. D., Bender, E. M., Paullada, A., Denton, E., & Hanna, A. (2021). AI and the everything in the whole wide world benchmark. *NeurIPS 2021 Datasets and Benchmarks Track*. arXiv:2111.15366. [C] [OA cit: 15]
- Reddit, Inc. (2024, February 22). *Form S-1 Registration Statement*. SEC EDGAR. https://www.sec.gov/Archives/edgar/data/1713445/000162828024006294/reddits-1q423.htm. [R] — primary SEC disclosure of $203 million aggregate data-licensing contracts at terms of two to three years; mirrors the source used in Draft AV §3.6.
- Reuters. (2024, February 22). *Reddit in AI content licensing deal with Google*. [R] — first reporting of the $60M/year Reddit–Google deal; corroborated by Reddit's S-1 filing the same day.
- Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021). "Everyone wants to do the model work, not the data work": Data cascades in high-stakes AI. *CHI 2021*. https://doi.org/10.1145/3411764.3445518. [C] [OA cit: 650] [CrossRef retraction check 2026-05-11: clear]
- Wang, A., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2018). GLUE: A multi-task benchmark and analysis platform for natural language understanding. *Proceedings of the 2018 EMNLP Workshop BlackboxNLP: Analyzing and Interpreting Neural Networks for NLP*, 353–355. https://doi.org/10.18653/v1/W18-5446. [C] [OA cit: 3912] [CrossRef retraction check 2026-05-18: clear]
- Wang, A., Pruksachatkun, Y., Nangia, N., Singh, A., Michael, J., Hill, F., Levy, O., & Bowman, S. R. (2019). SuperGLUE: A stickier benchmark for general-purpose language understanding systems. *Advances in Neural Information Processing Systems 32 (NeurIPS 2019)*. arXiv:1905.00537. [C] [OA cit: 987] — published version in NeurIPS 2019 proceedings; the arXiv:1905.00537 preprint is the canonical citation in the literature.
- Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D., & Mann, G. (2023). *BloombergGPT: A large language model for finance*. arXiv:2303.17564. [PDF: Kilder/Wu2023_BloombergGPT_arXiv2303.17564.pdf] [P] [OA cit: 302]

---

## Changelog

See `Chapter drafts/changelogs/aw-changelog.md` for iteration history.
