# Draft N — The AI/ML Ecosystem: Who Makes What

**Version:** v0.4 (2026-05-18)  
**Status:** v0.4 — STEERING focus-1 cross-link integration. §3.2 extended with explicit cross-references to AV (behavioural-surplus second extraction layer) and AW (commercial dataset economy: labelling marketplaces, premium corpora, synthetic-data vendors). Part 4 closes with a feedback-loop note cross-linking to BF (homogenisation pressure as downstream consequence of the ecosystem mapped here). Five citations re-verified via OpenAlex this cycle (Cottier 2024 OA cit 19; Sevilla 2022 OA cit 40; Gofman & Jin 2024 OA cit 98; Longpre 2024 OA cit 10; Villalobos 2024 OA cit 79) — counts unchanged since v0.3. CrossRef retraction check Gofman & Jin (`update-to: None`) confirms record remains clean.

---

## Overview and Chapter Position

The AI/ML field is often presented as one coherent "field" — but is in reality a layered, political-economic system with very unequal power distribution. This draft maps *who makes what*: which actor types exist, what do they produce, and which dependencies and power relations structure the system?

The draft is the chapter's political-economic panorama. It connects three threads: the open commons argument from `a-commons-accumulation-history.md` (who has access to *use* the commons), the extraction argument from `f-commons-extraction-inequality.md` (who *harvests* the value), and the openness typology from `k-openness-layers.md` (what producers actually release). It answers the question: *who actually sits at the table in hybrid intelligence?*

---

## Part 1: Supply chain — from silicon to application

The AI/ML production chain has at least six layers, each with its own actors and power concentrations:

```
[1] Chips & hardware
        ↓
[2] Compute infrastructure (cloud)
        ↓
[3] Training data
        ↓
[4] Foundation models (pretraining)
        ↓
[5] Fine-tuning, RLHF, alignment
        ↓
[6] Applications & deployment
```

Power concentration varies markedly: layers 1 and 2 are extremely concentrated (oligopoly), layer 4 is moderately concentrated (handful of frontier labs + open source), layer 6 is relatively fragmented (thousands of application developers). This is not random — it reflects the capital-intensity gradients: pretraining frontier models costs billions of dollars and requires hardware that only very few organisations have access to.

---

## Part 2: Actor types and what they produce

### 2.1 Frontier Labs (closed/semi-closed)

The five organisations that consistently define the state of the art in foundation models:

| Organisation | Ownership structure | Primary outputs | Openness |
|---|---|---|---|
| OpenAI | Capped-profit / Microsoft | GPT series, o-series, API | Low (weights closed) |
| Anthropic | PBC / Amazon, Google | Claude series | Low (weights closed) |
| Google DeepMind | Corporate / Alphabet | Gemini, AlphaFold, Gemma | Mixed |
| Meta AI | Corporate | Llama series | High weights, closed data |
| xAI | Corporate / Musk | Grok | Low |

Common characteristics: very large compute access, proprietary datasets, closed pretraining, selective opening (typically weights but not data — cf. `k-openness-layers.md`).

### 2.2 European and non-American frontier candidates

| Organisation | Country | Output | Note |
|---|---|---|---|
| Mistral AI | France | Mistral, Mixtral | Open weights, closed data |
| Aleph Alpha | Germany | Luminous | Primarily enterprise |
| 01.AI / Qwen / Baidu | China | Yi, Qwen, ERNIE | Growing capacity, state relations |
| DeepSeek | China | DeepSeek series | High openness, efficiency breakthrough 2025 |
| Samsung / NAVER | South Korea | HyperCLOVA | Regional markets |

Implication: AI/ML capacity is becoming geographically distributed, but compute dependence on NVIDIA and US cloud providers remains a structural constraint.

### 2.3 Open source community — the HuggingFace axis

HuggingFace is becoming the AI/ML field's GitHub: a platform for model sharing, datasets and evaluation infrastructure. Central actors at this layer:

- **HuggingFace**: infrastructure (model hub, datasets, Transformers library)
- **EleutherAI**: nonprofit; produces open models (GPT-Neo, GPT-J, Pythia) and open datasets (The Pile)
- **Allen Institute for AI (AI2)**: OLMo, the Dolma dataset — a fully open pipeline
- **LAION**: open datasets (LAION-5B for images, used by Stable Diffusion)
- **Contributing individuals**: fine-tuned models, lora adapters, evaluation scripts

This layer is the chapter's primary connection to the commons argument: the open source AI community produces public goods (open models, datasets, benchmarks), but is structurally dependent on frontier labs' releases and cloud compute donations.

### 2.4 Cloud providers — the hidden infrastructure layer

AWS, Google Cloud and Azure are not primarily model producers, but they control access to the compute necessary for pretraining. Their strategic position:

- Investments in frontier labs (Microsoft/OpenAI, Amazon/Anthropic, Google/Anthropic) provide preferential access
- Proprietary inference infrastructure (e.g. AWS Inferentia, Google TPUs) creates lock-in for the deployment layer
- Cloud providers are the only actors that can offer frontier-scale pretraining to third parties (via services such as Azure AI Studio)

### 2.5 Hardware — NVIDIA and the global chip oligopoly

NVIDIA controls about 80–90% of the market for AI training accelerators (H100, A100, GB200). This is the most concentrated part of the supply chain:

- **NVIDIA** (USA): dominant GPU producer
- **AMD** (USA): rising competitor (MI300X)
- **Google** (TPU): proprietary, only available via Google Cloud
- **Intel Gaudi**: niche actor
- **Huawei Ascend** (China): alternative for circumventing US export controls

US export-control legislation (October 2022, updated 2023) restricts the export of advanced chips to China, forcing Chinese labs to work with inferior hardware or domestic alternatives — a direct state intervention in the AI/ML supply chain.

### 2.6 Academic institutions

Traditionally the centre of AI research, but increasingly marginalised in foundation-model competition due to compute access. Academia's current roles:

- **Benchmark production**: MMLU, BIG-Bench, HELM, GLUE/SuperGLUE
- **Evaluation infrastructure**: LMSYS Chatbot Arena, AlpacaEval
- **Safety research**: interpretability, alignment, robustness
- **Critical analysis**: bias audits, social-impact studies
- **Education**: primary source of frontline-researcher talent

The problem: the most talented ML researchers are aggressively recruited by frontier labs at salaries that academia cannot match. Gofman and Jin (2024, *Journal of Finance*) document an "unprecedented brain drain" of AI faculty from US universities between 2004 and 2018 and show that it has measurable downstream effects: students from affected universities subsequently founded fewer AI startups and raised less venture funding, with the effect strongest for departures of tenured professors, professors from top universities, and deep-learning specialists. The causal channel they identify is that departing faculty take with them the AI knowledge that successful student-led startup formation depends on. The phenomenon is intensified by the compute asymmetry — academic labs cannot run the experiments their alumni now run inside frontier labs, so the talent flow is one-directional. *(Note: the prior version of this draft cited Daniotti et al. 2025 here, then a misattributed PhD-placement statistic to Gofman & Jin 2024; the paper actually studies faculty — not new-PhD — career trajectories, and the canonical 21%→70% PhD-to-industry figure originates from Stanford's AI Index reports, not Gofman & Jin.)*

### 2.7 States and public actors

States are not neutral observers but active actors:

- **USA**: export controls (chip embargo), NIST AI RMF, executive orders on AI safety, funding the National AI Research Resource (NAIRR)
- **EU**: AI Act (risk categorisation), funding EuroHPC (compute infrastructure), General-Purpose AI regulation
- **China**: national AI strategy, state-funded lab sector, parallel chip-development programme
- **UK**: AI Safety Institute, frontier-lab inspection regime
- **UAE/Saudi Arabia**: massive compute investment, strategic AI capacity build-up

Mazzucato's "entrepreneurial state" argument (cf. `f-commons-extraction-inequality.md`) applies directly here: US state basic research (DARPA, NSF) funded many of the algorithms and frameworks that enabled current frontier models — but the value has been accumulated privately.

---

## Part 3: Power analysis — concentration and dependency

**3.1 Compute concentration**  
Fewer than ten organisations globally have access to frontier-scale pretraining. Cottier et al. (2024, Epoch AI) develop a hardware-energy-staff cost model from 45 frontier models and report that the most expensive publicly-announced training runs to date are OpenAI's GPT-4 at approximately $40 million and Google's Gemini Ultra at approximately $30 million (amortised hardware + energy, final training run only), and that the amortised training cost of frontier models has grown at 2.4× per year since 2016 (95% CI: 2.0×–3.1×). Extrapolating this trend, Cottier and colleagues estimate that the largest training runs will cost over a billion dollars by 2027 — placing frontier training beyond the reach of any actor without dedicated tens-of-billions-of-dollars investment. The *compute* underlying these training runs has scaled even faster: Sevilla et al. (2022) date the start of a "Large-Scale Era" to late 2015 and find that training compute in this era has been doubling roughly every six months — i.e. growing about 4× per year, far faster than Moore's law (which doubled compute roughly every 20 months before 2010). Combined with NVIDIA's near-monopoly on training accelerators, these cost and compute trajectories form an exclusion barrier that effectively limits frontier competition to capital-rich actors.

**3.2 Data concentration**  
The most valuable training datasets — Common Crawl (web), Books1/Books2, GitHub data, proprietary RLHF data — are controlled by either a nonprofit (Common Crawl Foundation), a single firm (OpenAI), or aggregated without permission from copyright holders (cf. `c-training-data-extraction.md`). Longpre et al.'s *Consent in Crisis* (2024) documents how rapidly the open web is being foreclosed: in a single year (2023–2024) ~5% of all tokens in the C4 corpus, and 28%+ of its most actively maintained sources, became fully restricted via robots.txt — and 45% of C4 is now restricted under Terms of Service. The result is that openly accessible training data is shrinking just as the largest firms have already finished crawling it, hardening incumbents' first-mover advantage. Villalobos et al. (2024) reach a complementary structural conclusion: at current trends, the stock of public human-generated text will be effectively exhausted between 2026 and 2032, after which the marginal training token will increasingly come from synthetic generation or licensed proprietary corpora — both of which favour actors who already control frontier models.

Two further data tiers sit outside the open commons but are decisive for what frontier actors can train on, and are treated in detail in companion drafts. First, the *behavioural surplus* held by commercial social platforms — Meta's Family of Apps, YouTube, X, LinkedIn, TikTok, Reddit — is, by every public scale indicator, an order of magnitude larger than the open commons that web-scale crawls capture, and is being repurposed from advertising substrate into generative-AI training substrate under Terms-of-Service consent regimes that the EU AI Act and GDPR were not designed to govern (cf. `av-social-media-training-data.md` §§1–3). This is a second extraction layer beyond the open-knowledge commons documented in Draft F, and it is accessible only to the platforms themselves and their licensees. Second, the *commercial dataset economy* — labelling marketplaces (Scale AI, Sama, Appen), domain-premium corpora (Bloomberg Terminal, Refinitiv, MIMIC-III), and the emerging synthetic-data vendors (Gretel, Tonic, Mostly AI) — supplies the curated, annotated, quality-controlled inputs that pretraining-only data cannot provide (cf. `aw-commercial-ml-datasets.md` §§1, 4–6). Both tiers are concentrating at the same actors that already dominate compute and pretraining: the same firms that finished crawling the open web before robots.txt closed it now also own the platform behavioural records and can pay the per-task rates that frontier-grade annotation requires.

**3.3 Talent concentration**  
ML talent is globally distributed but institutionally concentrated: most of the most-cited ML researchers are employed by or affiliated with a handful of organisations. This creates knowledge monopolies that are hard to distribute via openness alone.

**3.4 Benchmark power**  
The organisation that sets the standard for evaluation implicitly defines what counts as "good AI". Frontier labs have strong incentives to influence benchmarks favourably — and have the resources to "game" them. Academic benchmark producers are dependent on labs' cooperation to be able to evaluate closed models.

---

## Part 4: Connection to the chapter's 3-stage model

| Stage | Who is the actor? | What is produced? |
|---|---|---|
| **Accumulation** | Open source community, academia, internet users | Commons (code, text, data) |
| **Mining & Refinement** | Frontier labs, cloud providers, hardware oligopoly | Foundation models, alignment |
| **Augmentation & Feedback** | Application developers, end users, agentic systems | Fine-tuned models, RLHF data, new commons |

Key observation: the three stages involve *very* different actors with very unequal power positions. Those who *accumulate* the commons (stage 1) are not the same as those who *harvest* its value (stage 2). This is the political-economic core of the extraction argument.

A further dynamic operates inside stage 3 itself: the text, code, and behavioural signal that augmented humans and agentic systems generate is increasingly the substrate that *future* pretraining and fine-tuning runs consume. The feedback loop is not symmetric — the actors who deploy the agentic and assistive systems at the deployment layer (frontier labs, platforms with embedded assistants) are also the actors best positioned to retain, curate, and re-ingest that output. Draft BF (`bf-hybrid-text-transformation.md`) treats the qualitative consequence of this loop — a progressive homogenisation pressure as AI-generated text moves from edge case to majority share across websites, code repositories, academic prose, and community discussion — which is the downstream signal-degradation problem that the ecosystem mapped above produces by design.

---

## Open Questions

1. **Who owns the infrastructure for hybrid intelligence?** If HI systems require frontier-model access via API, all HI applications are dependent on a handful of providers. Is this a structural problem for HI democratisation?

2. **Will the compute concentration dissolve?** Specialised AI chips from new actors (e.g. Groq, Cerebras, SambaNova) and efficiency breakthroughs (DeepSeek's lower compute requirements) challenge NVIDIA dominance. Are we moving toward more distributed compute access?

3. **What is the right role for the public sector?** NAIRR and EuroHPC are attempts at public compute infrastructure. Is this sufficient to rebalance the power distribution — or is it symbolic policy?

4. **Open source as Trojan horse?** Meta releases the Llama models — but this is a strategic decision that undermines OpenAI's and Anthropic's API business model. When is open source altruism and when is it competitive strategy?

5. **Benchmark capture**: Are there signs of systematic benchmark gaming by frontier labs, and what are the consequences for the credibility of academic evaluation?

---

## Sources (Anchors — to be verified)

- [P] Longpre, S., et al. (2025). *Economies of Open Intelligence: Tracing Power & Participation in the Model Ecosystem*. arXiv:2512.03073. — **[already in Kilder]** — *scope note: this paper documents concentration in the Hugging Face open-model hub, not training-corpus economics; cite for §2.3 and §3.4, not §3.2.*
- [C] Longpre, S., et al. (2024). *Consent in Crisis: The Rapid Decline of the AI Data Commons*. NeurIPS 2024 Datasets & Benchmarks Track. — **[already in Kilder as `Longpre 2024 - Consent in Crisis.pdf`]** — primary anchor for §3.2 data concentration claims.
- [C] Villalobos, P., Ho, A., Sevilla, J., Besiroglu, T., Heim, L., & Hobbhahn, M. (2024). *Will we run out of data? Limits of LLM scaling based on human-generated data*. ICML 2024. arXiv:2211.04325. — **[already in Kilder as `Villalobos 2024.pdf`]** — anchor for the data-exhaustion projection in §3.2.
- [R] Bommasani, R., et al. (2024). *The Foundation Model Transparency Index*. Stanford CRFM/HAI report. — **[already in Kilder]**
- [R] Wan, K., et al. (2025). *Foundation Model Transparency Index 2025*. Stanford CRFM/HAI report. — **[already in Kilder]**
- [C] Liesenfeld, A., Lopez, A., & Dingemanse, M. (2024). *Rethinking open source generative AI: Open-washing and the EU AI Act*. FAccT 2024. — **[already in Kilder]**
- [R] White, M., Haddad, I., Osborne, C., Yanglet, X.-Y. L., Abdelmonsef, A., & Varghese, S. (2024). *The Model Openness Framework*. Linux Foundation / GenAI Commons. — **[already in Kilder]**
- [P] Kapoor, S., et al. (2024). *On the societal impact of open foundation models*. arXiv:2403.07918. — **[already in Kilder]** — *iCit pending S2 query (rate-limited this cycle).*
- [P] Daniotti, S., Wachs, J., Feng, X., & Neffke, F. (2025). *Who is using AI to code? Global diffusion and impact of generative AI*. arXiv:2506.08945. — **[already in Kilder]** — *scope note: covers geographic adoption of AI coding tools by GitHub users; do NOT cite for academia→industry brain drain.*
- [C] Hoffmann, J., et al. (2022). *Training compute-optimal large language models* (Chinchilla scaling laws). NeurIPS 2022. — **[already in Kilder]**
- [R] Mazzucato, M. (2013). *The Entrepreneurial State: Debunking Public vs. Private Sector Myths*. Anthem Press. — **[BOOK — add to _linked_sources.md]**
- [J] Lerner, J., & Tirole, J. (2002). *Some simple economics of open source*. Journal of Industrial Economics, 50(2), 197–234. — **[already in Kilder]**
- [C] Solaiman, I. (2023). *The gradient of generative AI release: Methods and considerations*. FAccT 2023. — **[already in Kilder]**
- [P] Cottier, B., Rahman, R., Fattorini, L., Maslej, N., Besiroglu, T., & Owen, D. (2024). *The rising costs of training frontier AI models*. arXiv:2405.21015. [OA cit: 19] — **[in Kilder as `Cottier2024_RisingCostsFrontierAIModels_arXiv2405.21015.pdf`]** — anchor for §3.1 cost figures (GPT-4 ≈ $40M, Gemini Ultra ≈ $30M; 2.4×/year cost growth since 2016).
- [P] Sevilla, J., Heim, L., Ho, A., Besiroglu, T., Hobbhahn, M., & Villalobos, P. (2022). *Compute Trends Across Three Eras of Machine Learning*. arXiv:2202.05924. [OA cit: 40] — **[in Kilder as `Sevilla2022_ComputeTrendsThreeEras_arXiv2202.05924.pdf`]** — anchor for §3.1 compute-growth claim (~6-month doubling time in Large-Scale Era post-2015; ~20-month doubling pre-2010 under Moore's law).
- [J] Gofman, M., & Jin, Z. (2024). Artificial Intelligence, Education, and Entrepreneurship. *The Journal of Finance*, 79(1), 631–667. https://doi.org/10.1111/jofi.13302 [OA cit: 98; CrossRef retraction check: no updates 2026-05-11] — **[PDF gated behind Wiley/SSRN paywall; abstract and citation metadata verified via CrossRef + OpenAlex]** — anchor for §2.6 faculty brain drain. *Scope note: the paper studies AI faculty departures from US universities 2004–2018 and their downstream effect on student startup formation — not new-PhD career placement. The often-cited "21%→70% AI PhDs to industry" trajectory is from the Stanford AI Index reports (Maslej et al., HAI), not from this paper.*

---

## What Still Needs Work

- [ ] Add current market-share figures for NVIDIA, cloud providers (2025) — primary source still needed (commonly cited 80–90% is Jon Peddie / Mercury Research).
- [ ] Anchor the "21%→70% PhD-to-industry" trajectory directly to Stanford AI Index 2024 (Maslej et al., HAI) — currently only mentioned as the canonical source for that figure; report PDF to be fetched.
- [ ] Expand the China section: Qwen, DeepSeek, Baidu ERNIE — specific openness grades.
- [ ] Add Mazzucato to `_linked_sources.md`.
- [ ] Consider section on *standardisation organisations* (ISO, IEEE, NIST) as actor type.
- [ ] Cross-ref to `b-closed-models-risks.md` — concentration risks as societal problem.
- [ ] Run S2 iCit lookups on Cottier 2024, Sevilla 2022, Gofman & Jin 2024 once Semantic Scholar quota resets (this cycle was rate-limited at 429).
