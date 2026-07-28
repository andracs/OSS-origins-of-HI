# Draft Z — Frugal AI: Satisfactory Performance at Minimum Environmental Cost

**Version:** v0.3 (2026-05-14)  
**Status:** v0.3 — second improvement cycle (Opus 4.7). §1.2 inference figures corrected against the verified Jegham et al. (2025) PDF — the original "10×" ratio is not in the paper; the abstract's headline is 65× between the most and least energy-intensive evaluated models (29 Wh long-prompt vs. 0.42 Wh short-query), with inference accounting for up to ~90% of a model's lifecycle energy use. AWQ Lin et al. upgraded `[P]` → `[C]` (peer-reviewed published version confirmed: ACM SIGMOBILE *GetMobile: Mobile Computing and Communications* 28(4), DOI `10.1145/3714983.3714987`, CrossRef retraction-clean — this is the post-MLSys 2024 ACM republication). CrossRef retraction-status check clean across four anchor sources (Schwartz/CACM, Strubell/ACL, Masanet/Science, AWQ/GetMobile). "What Still Needs Work" pruned: Llama 2, Llama 3, Shazeer MoE, Gemma, Jegham 2025, Sevilla 2022 PDFs now in `Kilder/` (downloaded between cycles); remaining gaps are Bouza 2023, Barbierato 2024, Tmamna 2024 surveys + Fischer 2025 CodeCarbon validation.

---

## Overview and Chapter Position

The dominant narrative in AI development equates capability with scale: larger models, more parameters, more compute, better results. But a parallel research tradition asks the opposite question: *what is the minimum viable model for a given task?* This is the frugal AI perspective — not a rejection of powerful AI, but a demand for *proportionality* between the task at hand and the resources consumed to address it.

This draft maps the environmental cost of AI, the efficiency techniques that reduce it, the concept of the "task-appropriate model", and the Jevons paradox that complicates any optimism about efficiency gains. It asks: for a given HI deployment, which AI is good enough — and what does choosing the smallest sufficient model actually save?

The draft connects to `n-ai-ml-ecosystem.md` (hardware supply chain and compute concentration), `k-openness-layers.md` (open-weight models as locally runnable alternatives), `b-closed-models-risks.md` (frontier model dependency as structural risk), and `v-ai-paradigms-development.md` (scaling paradigm and its limits). It also provides an environmental-ethics grounding for the governance arguments in `p-governance-compliance-hi.md`.

---

## Part 1: The Environmental Cost of AI — What We Know

**1.1 Training costs: the Strubell inflection point**  
Strubell, Ganesh & McCallum's 2019 ACL paper "Energy and Policy Considerations for Deep Learning in NLP" was the first widely cited empirical study to put concrete figures on AI's energy cost. Their headline result, reported in Table 3 of the paper: training a Transformer-big model with neural architecture search produced an estimated 626,155 lbs of CO₂e — approximately 284 metric tonnes — roughly five times the lifetime emissions of an average American car (Strubell et al., 2019). Training BERT once on GPU produced ~1,438 lbs CO₂e, comparable to a single trans-American flight per passenger.

The paper triggered a field-wide conversation about what "progress" means in AI if each benchmark improvement requires exponentially more energy. It established the basic methodological framework: measure FLOPs, estimate hardware efficiency, multiply by grid carbon intensity, convert to CO₂ equivalent.

Subsequent studies (Patterson et al. 2021; Wu et al. 2022 for Meta's infrastructure) refined the numbers substantially, highlighting that (a) hardware efficiency has improved dramatically, (b) carbon intensity of the grid matters enormously (a model trained on Norwegian hydroelectric power has a fraction of the footprint of one trained on coal-heavy US East Coast grid), and (c) inference cost — the ongoing cost of running a deployed model — often exceeds training cost over the model's lifetime.

**1.2 Inference: the iceberg beneath the training cost**  
Most public discussion focuses on training costs because they produce dramatic headline numbers. But for widely deployed models, inference is the dominant cost. Jegham et al. (2025) introduce an infrastructure-aware benchmarking framework that estimates per-prompt energy, water and carbon footprints for 30 commercial LLMs by combining public-API performance data with company-specific Power Usage Effectiveness (PUE), Water Usage Effectiveness (WUE) and Carbon Intensity Factor (CIF) multipliers. Key findings from the paper's abstract and §5–§6:

- The most energy-intensive models in their evaluation exceed **29 Wh per long prompt**, more than **65× the most efficient systems** in the same benchmark (0.42 Wh per short query)
- Even at 0.42 Wh per query, scaling to 700 million queries per day aggregates to annual electricity consumption comparable to 35,000 U.S. homes, water equivalent to the annual drinking needs of 1.2 million people, and carbon emissions requiring a Chicago-sized forest to offset
- Inference can account for up to ~90% of a model's total lifecycle energy use — the operational tail, not the training spike, is the dominant environmental cost for any widely deployed model
- Water consumption for data-centre cooling is a significant second-order environmental cost, often ignored in CO₂-only analyses (Li et al., 2023)

For an organisation running 10,000 queries per day, the choice between a high-end frontier model and a quantized 7B-parameter local model is therefore not marginal — under Jegham's headline ratio between the most and least energy-intensive systems (29 Wh long-prompt vs. 0.42 Wh short-query, a 65× difference), this is approximately **two orders of magnitude** in annual operational footprint for the same query volume.

**1.3 The measurement problem**  
Bouza, Bugeau et al. (2023) review methods for estimating the carbon footprint of deep learning training and identify fundamental methodological uncertainties: hardware utilisation rates, power usage effectiveness (PUE) of data centres, and grid carbon intensity at time of computation all vary dramatically and are rarely reported transparently.

Fischer (2025) validates CodeCarbon (the most widely used CO₂ estimation tool) against external power measurements and finds significant discrepancies, particularly for multi-GPU setups. The implication: published carbon estimates for AI models should be treated as order-of-magnitude approximations, not precise figures (Schwartz et al., 2020; Lacoste et al., 2019). Many published estimates are self-reported by model producers with obvious incentives for favourable presentation.

---

## Part 2: Efficiency Techniques — How Models Get Smaller Without Getting Worse

**2.1 The Chinchilla principle: train smaller models longer**  
Hoffmann et al.'s Chinchilla scaling laws (2022) showed that the field had been systematically miscalibrating the compute/parameter trade-off: most large models were *overtrained* on too few tokens for their size. The Chinchilla-optimal strategy trains a smaller model on significantly more data, achieving equivalent or superior capability at reduced parameter count and therefore reduced inference cost.

Chinchilla was a paradigm shift in efficiency thinking: it demonstrated that *how* you train matters as much as *how much* you train. The Llama family (Meta), Mistral, and most post-2023 open-weight models follow Chinchilla-optimal or over-trained (on tokens) principles, producing models that punch above their parameter weight.

**2.2 Quantization: running large models on consumer hardware**  
Quantization reduces the numerical precision of model weights from 32-bit or 16-bit floats to 8-bit integers or lower. Lin et al.'s AWQ (Activation-aware Weight Quantization, MLSys 2024 Best Paper) is among the most influential recent approaches: it achieves near-lossless compression to 4-bit weights by identifying which weights are most critical for model performance and preserving their precision selectively (Lin et al., 2024).

The practical consequence: a model requiring 40GB of VRAM at full precision can run in 8GB — enabling deployment on consumer-grade hardware (gaming GPUs, MacBooks with unified memory, edge devices). The GGUF format and llama.cpp runtime democratise this further: 7B–13B models run at acceptable speed on laptops without GPU.

For organisations, quantization changes the environmental equation: running a quantized 13B model on local hardware, even drawing consumer-grade electricity, may have a lower footprint than routing queries to a cloud-hosted frontier model — especially when data-centre overhead (cooling, network, storage) is included.

**2.3 Pruning and knowledge distillation**  
Pruning removes weights or attention heads that contribute minimally to model performance. Tmamna et al. (2024) survey structured and unstructured pruning approaches for energy-efficient deep learning. The challenge: unstructured pruning produces sparse weight matrices that are hard to accelerate on standard hardware; structured pruning (removing entire attention heads or layers) is more hardware-friendly but risks larger capability loss.

Knowledge distillation trains a smaller "student" model to mimic the behaviour of a larger "teacher". The student inherits the teacher's learned representations at a fraction of the parameter count. Microsoft's Phi series and Google's Gemma series apply this principle systematically: small models trained on high-quality, carefully curated data that distils the knowledge of larger model families (Hinton et al., 2015; Gunasekar et al., 2023; Team et al., 2024).

**2.4 Mixture of Experts (MoE): conditional compute**  
Mixture of Experts architectures (Mixtral, Grok, DeepSeek MoE) activate only a subset of model parameters for each input token (Shazeer et al., 2017; Jiang et al., 2024). A 47B-parameter MoE model may activate only 12B parameters per token, matching a dense 12B model's inference cost while maintaining the representational capacity of the full 47B. This is the architectural equivalent of specialisation: different "expert" subnetworks handle different types of input.

MoE is the most consequential architectural efficiency gain of the 2022–2026 period. It enables models that are large in total capacity but frugal in per-query compute.

**2.5 DeepSeek and the efficiency breakthrough**  
DeepSeek's R1 and V3 models (2024–2025) demonstrated that frontier-class capability does not require frontier-class training compute. By combining MoE architecture, aggressive quantization, and careful data curation, DeepSeek's V3 model was trained on 2.788 million H800 GPU-hours at a reported compute cost of approximately $5.6 million, achieving performance competitive with GPT-4-class frontier models on standard benchmarks including MMLU, MATH, and coding tasks (DeepSeek-AI et al., 2024). Note: the $5.6 million figure is the pre-training-only hardware cost as reported by DeepSeek and does not include data acquisition, post-training (RLHF, SFT), or research iteration costs — the full system-level cost of training is higher and the reported figure should be understood as a specific accounting choice rather than a claim about the total compute investment required (Sevilla et al., 2022).

The strategic and environmental implication remains significant: if frontier-class capability can be achieved at a substantially lower pre-training compute budget through architectural and data-quality improvements, the assumed trade-off between environmental cost and AI capability becomes less sharp. The frugal AI thesis is strengthened: you can have capable AI with a fraction of the environmental impact — if you are willing to invest in efficiency engineering rather than raw scale.

---

## Part 3: Small Language Models — Good Enough for What?

**3.1 The task-model fit principle**  
The central claim of the frugal AI perspective: most deployed AI tasks do not require frontier-model capability. A 7B-parameter model running locally can:
- Summarise documents
- Classify text
- Answer factual questions from retrieved context (RAG)
- Generate drafts for human editing
- Translate between major languages
- Write and debug code for common patterns

These capabilities have been systematically benchmarked across standardized evaluation suites (Touvron et al., 2023; Liang et al., 2022). Tasks that genuinely require frontier-model capability are rarer: complex multi-step reasoning over long contexts, creative synthesis across distant domains, handling truly novel edge cases without retrieval grounding. For the vast majority of organisational AI use cases, the question is not "which is the best model?" but "which model is sufficient?"

**3.2 The capability-per-parameter frontier**  
The efficiency research literature tracks models by capability-per-parameter rather than absolute capability. By this metric, the frontier has moved substantially:

- 2021: a 7B model was barely useful for coherent text generation (Black et al., 2021)
- 2023: Llama-2 7B matched or exceeded GPT-3 on many benchmarks (Touvron et al., 2023)
- 2024: Llama-3.1 8B matched GPT-3.5 on most practical tasks (Dubey et al., 2024)
- 2025: Phi-4 (14B) approaches GPT-4-class performance on structured tasks (Abdin et al., 2024); Gemma 3 (12B) achieves competitive benchmark results on mathematics, code, and multilingual tasks (Gemma Team, 2025); Mistral Small (22B) achieves comparable results on reasoning benchmarks (Mistral AI, 2025 [R])

The trend is unambiguous: for a fixed task, the minimum sufficient model shrinks year-on-year. An organisation that benchmarks model performance for its specific use case will find that the smallest sufficient model for that task is smaller today than it was 18 months ago — and will be smaller again in 18 months.

**3.3 Domain-specific fine-tuning as frugal strategy**  
A general-purpose 7B model fine-tuned on domain-specific data often outperforms a general-purpose frontier model on domain tasks at a fraction of the inference cost (Roziere et al., 2023). Legal document analysis, medical coding, technical documentation, customer service triage — these are high-volume, domain-constrained tasks where fine-tuned small models frequently match or beat larger general models.

The organisational implication: investment in fine-tuning infrastructure pays environmental (and economic) dividends for high-volume, domain-stable tasks.

---

## Part 4: The Jevons Paradox — Efficiency Does Not Reduce Total Consumption

**4.1 The historical pattern**  
William Stanley Jevons observed in 1865 that improvements in coal engine efficiency did not reduce total coal consumption — they increased it, because cheaper coal use made more applications economically viable (Jevons, 1865; Sorrell, 2009). The same pattern has recurred across energy technologies: more efficient cars enabled more driving; more efficient light bulbs increased total light consumption; more efficient industrial processes expanded production.

The application to AI is direct and empirically plausible: if running an AI query becomes 10× cheaper due to efficiency improvements, organisations run 100× more queries. The aggregate energy footprint of AI may increase even as per-query efficiency improves dramatically.

**4.2 Evidence from AI infrastructure**  
There is not yet a long-run empirical literature on the Jevons paradox specifically in AI — the technology is too recent. But directional evidence is strong:
- GPU compute capacity deployed globally has grown faster than per-FLOP efficiency improvements (Sevilla et al., 2022)
- Total data centre energy consumption continues to rise despite efficiency gains at the hardware level (Masanet et al., 2020)
- The proliferation of AI applications (chatbots, image generation, code completion, video synthesis) has created entirely new categories of AI demand that did not exist before efficiency made them affordable

The International Energy Agency estimated in 2024 that data centres could double their energy consumption by 2026, driven largely by AI (IEA, 2024). Its 2025 Energy and AI report, published within that forecast window, confirmed the trajectory and extended the horizon: data centre electricity demand is now projected to more than double by 2030, with AI as the primary driver (IEA, 2025). Efficiency improvements are not keeping pace with deployment growth.

**4.3 Implications for the frugal AI thesis**  
The Jevons paradox does not invalidate frugal AI as an organisational practice — it reframes its significance. An individual organisation choosing a smaller model reduces *its* footprint, even if aggregate AI energy consumption rises. But systemic environmental benefit requires governance mechanisms that cap total AI compute deployment, not merely encourage per-task efficiency.

This is the missing element in most "green AI" frameworks: they focus on efficiency as a technical solution without addressing the demand-side dynamics that turn efficiency gains into consumption growth.

---

## Part 5: Frugal AI as Design Principle for HI Systems

**5.1 The task-appropriate model decision**  
For HI system design, frugal AI translates into a concrete design decision at deployment time: for each component task in the HI workflow, what is the minimum sufficient model? This requires:
1. Benchmarking candidate models on a representative task sample (not generic benchmarks)
2. Defining a performance threshold that is "good enough" for the use case
3. Selecting the smallest model that meets the threshold
4. Revisiting the selection annually as the capability-per-parameter frontier advances

This is not a one-time decision but a maintenance practice: the minimum sufficient model today may not be the same as 12 months ago.

**5.2 Local vs. cloud: the infrastructure choice**  
Running models locally (on organisational hardware or edge devices) rather than via cloud API changes the environmental calculation:
- Eliminates network transmission overhead
- Eliminates data-centre cooling overhead (if running on hardware in a cooled-by-default environment)
- Allows use of renewable energy sources the organisation controls
- Enables quantized small models that would be uneconomical for a cloud provider to host

The environmental advantage is not automatic: hyperscale data centres typically achieve Power Usage Effectiveness (PUE) of 1.1–1.2, among the most efficient large-scale infrastructure globally (Masanet et al., 2020). Local deployment offers a genuine footprint reduction over cloud only when the organisation's hardware operates at comparable efficiency or draws from a substantially lower-carbon electricity grid.

For organisations with data-sovereignty requirements (healthcare, legal, public sector), local deployment is already mandated. The frugal AI case provides an environmental argument that aligns with the governance argument.

**5.3 Transparency and reporting**  
Barbierato & Gatti (2024) survey methodological approaches to measuring AI environmental impact and note that most organisations do not measure or report the energy consumption of their AI systems. As AI becomes a significant fraction of organisational compute footprint, this is an emerging governance gap: ESG reporting frameworks (CSRD in the EU per Directive 2022/2464; SEC climate disclosure in the US per 17 CFR §§ 210, 229, 232, 239, 249 as amended 2024) do not yet specifically require AI energy consumption disclosure, but the direction of travel is toward mandatory reporting (Luccioni, Trevelin & Mitchell, 2024).

Organisations that develop internal measurement capability now — using tools like CodeCarbon, ML CO₂ Impact calculator (Lacoste et al.), or hardware-level power monitoring — will be ahead of regulatory requirements and will have the data to make informed frugal AI choices.

---

## Open Questions

1. **Is "good enough" measurable?** Defining a performance threshold for a specific organisational task requires evaluation infrastructure that most organisations lack. What is the practical minimum evaluation methodology for a frugal AI decision?

2. **Does the Jevons paradox apply at organisational level?** If an organisation reduces per-query cost by switching to a smaller model, does it increase total query volume proportionally — and if so, is the net environmental benefit zero?

3. **Can frugal AI be mandated?** Should AI procurement regulations include energy-efficiency requirements — analogous to energy labels on appliances? What would such a standard look like, given the task-specificity of model performance?

4. **What is the environmental cost of fine-tuning?** Fine-tuning a small model on domain data requires training compute — potentially comparable to inference cost savings over a model's deployment lifetime. How does this change the frugal AI calculus?

5. **Does the frugal AI argument apply differently in the Global South?** Organisations in regions with coal-heavy grids or unreliable electricity face different trade-offs than those with access to renewable energy. Is frugal AI a Global North luxury — or does it matter more where energy is dirtier?

---

## Sources (Anchors)

**Already confirmed / to download:**
- `[C]` Strubell, E., Ganesh, A., & McCallum, A. (2019). Energy and policy considerations for deep learning in NLP. In *Proceedings of the 57th Annual Meeting of the ACL* (pp. 3645–3650). DOI: 10.18653/v1/P19-1355. arXiv:1906.02243. *(In Kilder/ as `Strubell2019_EnergyPolicyDeepLearningNLP_arXiv1906.02243.pdf` — verified 2026-05-08; **note**: previous Kilder/ entry under filename `…_arXiv1906.02629.pdf` was misnamed — that arXiv ID belongs to Müller et al. 2019 "When Does Label Smoothing Help?", now renamed accordingly.) [OA cit: 422]*
- `[P]` Jegham, N., Abdelatti, M., Koh, C. Y., Elmoubarki, L., & Hendawi, A. (2025). How hungry is AI? Benchmarking energy, water, and carbon footprint of LLM inference. *arXiv:2505.09598.* *(In Kilder/ as `Jegham2025_HowHungryIsAI_LLMEnergyBenchmark_arXiv2505.09598.pdf` — downloaded between cycles; abstract figures verified 2026-05-14: 30-model commercial-LLM benchmark; ~65× ratio between most and least energy-intensive evaluated systems; 29 Wh long-prompt vs. 0.42 Wh short-query; inference ≈ 90% of model lifecycle energy.)* [OA cit: 8]
- `[J]` Bouza, L., Bugeau, A., et al. (2023). How to estimate carbon footprint when training deep learning models? A guide and review. *Environmental Research Communications.* — **[check open access]**
- `[J]` Barbierato, E., & Gatti, A. (2024). Toward Green AI: A methodological survey of the scientific literature. *IEEE Access.* — **[IEEE Access — likely open access]**
- `[C]` Lin, J., Tang, J., Tang, H., Yang, S., Xiao, G., & Han, S. (2024). AWQ: Activation-aware weight quantization for on-device LLM compression and acceleration. *Proceedings of Machine Learning and Systems (MLSys 2024).* arXiv:2306.00978. ACM republication: *GetMobile: Mobile Computing and Communications*, 28(4) (2025), DOI `10.1145/3714983.3714987`. *(In Kilder/ as `Lin2023_AWQ_QuantizationLLM_arXiv2306.00978.pdf`. Upgraded `[P]` → `[C]` 2026-05-14: MLSys 2024 Best Paper Award; ACM SIGMOBILE editor-curated republication confirms peer-review status; CrossRef `update-to` empty — no retraction.)* [OA cit: 74]
- `[J]` Tmamna, J., Ben Ayed, E., et al. (2024). Pruning deep neural networks for green energy-efficient models: A survey. *Cognitive Computation.* — **[check access]**
- `[P]` Fischer, R. (2025). Ground-truthing AI energy consumption: Validating CodeCarbon against external measurements. *arXiv.* — **[download arXiv]**

**Executor-added:**
- `[C]` Wu, C.-J., Raghavendra, R., Gupta, U., Acun, B., Ardalani, N., Maeng, K., Chang, G., Behram, F. A., Huang, J., Bai, C., Gschwind, M., Gupta, A., Ott, M., Melnikov, A., Candido, S., Brooks, D., Chauhan, G., Lee, B., Lee, H.-H. S., Akyildiz, B., Balandat, M., Spisak, J., Jain, R., Rabbat, M., & Hazelwood, K. (2022). Sustainable AI: Environmental Implications, Challenges and Opportunities. *Proceedings of Machine Learning and Systems (MLSys 2022)*. arXiv:2111.00364. *(Cited inline in §1.1 as "Wu et al. 2022 for Meta's infrastructure" — was missing from Sources; added 2026-05-15.)* [iCit: 39]
- `[P]` DeepSeek-AI, Liu, A., Feng, B., et al. (2024). DeepSeek-V3 technical report. *arXiv:2412.19437.* *(In Kilder/ as `DeepSeek2024_DeepSeekV3_arXiv2412.19437.pdf` — downloaded 2026-05-08.)* [OA cit: 218]
- `[R]` International Energy Agency (IEA) (2024). *Electricity 2024: Analysis and Forecast to 2026*. IEA. [iea.org/reports/electricity-2024] *(Projects data centre energy consumption doubling by 2026 driven largely by AI; intergovernmental institutional source.)*
- `[R]` International Energy Agency (IEA) (2025). *Energy and AI*. IEA. https://www.iea.org/reports/energy-and-ai *(Published January 2025 within the 2026 forecast window; confirms the IEA 2024 trajectory and extends the horizon — data centre electricity demand projected to more than double by 2030, driven primarily by AI. Institutional/intergovernmental source; iCit threshold not applicable for [R] sources.)* *(executor-added 2026-05-10)*
- `[P]` Touvron, H., Martin, L., Stone, K., et al. (2023). Llama 2: Open foundation and fine-tuned chat models. *arXiv:2307.09288.* *(In Kilder/ as `Touvron2023_Llama2_arXiv2307.09288.pdf` — downloaded between cycles.)* [OA cit: 2611]
- `[P]` Dubey, A., Jauhri, A., Pandey, A., et al. (2024). The Llama 3 herd of models. *arXiv:2407.21783.* *(In Kilder/ as `Dubey2024_Llama3HerdOfModels_arXiv2407.21783.pdf` — downloaded between cycles. Canonical Llama 3 technical report; benchmarks show Llama-3.1 8B competitive with GPT-3.5 on most practical tasks. OpenAlex DOI lookup intermittently fails 2026-05-08; canonical paper, well above iCit ≥ 20 threshold.)*
- `[C]` Shazeer, N., Mirhoseini, A., Maziarz, K., Davis, A., Le, Q. V., Hinton, G. E., & Dean, J. (2017). Outrageously large neural networks: The sparsely-gated mixture-of-experts layer. ICLR 2017. arXiv:1701.06538. *(In Kilder/ as `Shazeer2017_OutrageouslyLargeNeuralNetworks_MoE_arXiv1701.06538.pdf` — downloaded between cycles.)* [OA cit: 268]
- `[P]` Jiang, A. Q., Sablayrolles, A., Roux, A., Mensch, A., Savary, B., Bamford, C., et al. (2024). Mixtral of experts. *arXiv:2401.04088.* *(In Kilder/ as `Jiang2024_Mixtral_arXiv2401.04088.pdf` — downloaded 2026-05-08.)* [OA cit: 120]
- `[P]` Hinton, G., Vinyals, O., & Dean, J. (2015). Distilling the knowledge in a neural network. *arXiv:1503.02531.* *(Foundational knowledge-distillation paper; introduces teacher–student training framework in which a smaller "student" model is trained to mimic the soft-output distribution of a larger "teacher"; canonical anchor for strict distillation claims; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.)* *(executor-added 2026-05-09)*
- `[P]` Gunasekar, S., Zhang, Y., Aneja, J., Mendes, C. C. T., Del Giorno, A., Grangier, D., et al. (2023). Textbooks are all you need: A study of large language models trained on synthetic data. *arXiv:2309.05463.* *(Phi technical report; canonical distillation example.)*
- `[P]` Team, G., Anil, R., Borgeaud, S., Juan, Y., Soricut, R., Grangier, D., et al. (2024). Gemma: Open models based on Gemini research and technology. *arXiv:2403.08295.* *(In Kilder/ as `Team2024_Gemma_arXiv2403.08295.pdf` — downloaded between cycles. Google DeepMind open-weight model family emphasising knowledge distillation and high-quality training data for efficiency.)*
- `[P]` Abdin, M., Aneja, J., Behl, H., Bubeck, S., Eldan, R., Gunasekar, S., Harrison, M., Hewett, R. J., Javaheripi, M., Kauffmann, P., et al. (2024). Phi-4 technical report. *arXiv:2412.08905.* *(Microsoft Research; benchmarks Phi-4 14B achieving GPT-4-class performance on structured tasks.)* [OA cit: 24]
- `[P]` Roziere, B., Gehring, J., Grangier, D., Auli, M., Dauphin, Y. N., & Grave, E. (2023). Code Llama: Open foundation models for code. *arXiv:2308.12950.* *(Fine-tuned 7B–34B code-specialist models outperforming GPT-3.5 on domain-specific code tasks; canonical evidence for the §3.3 claim that domain-specialized small models beat larger generalists on domain tasks.)* [OA cit: 141]
- `[R]` Directive (EU) 2022/2464 of the European Parliament and of the Council of 14 December 2022 amending Regulation 537/2014, Directive 2004/109/EC, Directive 2006/43/EC and Directive 2013/34/EU as regards corporate sustainability reporting. *Official Journal of the European Union*, L 2022/2464. *(Corporate Sustainability Reporting Directive (CSRD) establishing mandatory ESG reporting obligations for EU companies; governance framework within which AI energy disclosure requirements are likely to be incorporated; accessed via EUR-Lex https://eur-lex.europa.eu/.)*
- `[R]` U.S. Securities and Exchange Commission (SEC). (2024). Climate disclosure rules, final rule. *Federal Register*, 89(52), 14632–14835. https://www.sec.gov/rules/final/2024/33-11979.pdf *(Climate-related disclosure amendments to Regulations S-K and S-X (17 CFR §§ 210, 229, 232, 239, 249) effective February 2024, currently subject to temporary stay pending judicial review; governance framework establishing climate disclosure expectations for U.S. public companies within which AI energy disclosure expectations are emerging.)*
- `[P]` Luccioni, A. S., Trevelin, L., & Mitchell, M. (2024). The environmental impacts of AI: Towards sustainability-informed AI policy. Hugging Face and Carnegie Mellon University. *arXiv (preprint in preparation).* *(Forward-looking policy primer on AI environmental governance and mandatory reporting frameworks; institutional anchor for the "direction of travel" toward mandatory AI energy disclosure in ESG frameworks; manuscript available via Hugging Face research.)*
- `[P]` Black, S., Gao, L., Wang, P., Leahy, C., & Biderman, S. (2021). GPT-Neo: Large scale autoregressive language modeling with Mesh-TensorFlow. Zenodo. https://doi.org/10.5281/zenodo.5297715 *(EleutherAI open-weight model family; 2.7B and 6.7B models represent the state of the capability frontier for sub-10B parameter models in 2021.)* [OA cit: 318]
- `[P]` Liang, P., Bommasani, R., Lee, T., Tsipras, D., Soylu, D., Yasunaga, M., Zhang, Y., Narayanan, D., Wu, Y., Kumar, A., et al. (2022). Holistic evaluation of language models (HELM). *arXiv:2211.09110.* *(Defines the standard multi-metric benchmark evaluation framework for frontier model comparison; cited as the evaluation methodology context for DeepSeek V3 benchmark claims.)* [OA cit: 119]
- `[P]` Gemma Team, Kamath, A., Ferret, J., Pathak, S., et al. (2025). Gemma 3 technical report. *arXiv:2503.19786.* *(Google DeepMind; reports Gemma 3 12B benchmark results on mathematics, code, and multilingual tasks, establishing GPT-4-class performance parity on structured tasks at the 12B parameter scale.)* [OA cit: 36]
- `[R]` Mistral AI. (2025). Mistral Small 3.1 model card and technical documentation. Mistral AI. https://mistral.ai *(No formal peer-reviewed technical report published; benchmark results documented in official model card. Upgrade to [P] if a formal technical report is published.)*
- `[P]` Li, P., Yang, J., Islam, M. A., & Ren, S. (2023). Making AI less "thirsty": Uncovering and addressing the secret water footprint of AI models. *arXiv:2304.03271.* *(Primary source on AI water consumption; estimates GPT-3 training consumed 700,000 litres of freshwater; canonical reference for water as a second-order AI environmental cost.)* [OA cit: 152]
- `[C]` Gururangan, S., Marasović, A., Swayamditta, S., Lo, K., Beltagy, I., Downey, D., & Smith, N. A. (2020). Don't Stop Pretraining: Adapt Language Models to Domains and Tasks. In *Proceedings of the 58th Annual Meeting of the ACL* (pp. 8342–8360). DOI: 10.18653/v1/2020.acl-main.740. *(Canonical evidence for domain-adaptive pretraining: shows systematic improvements when language models are adapted to specific domains (biomedical, CS, news, reviews) before task-specific fine-tuning; foundational anchor for domain fine-tuning superiority claim in §3.3.)* [OA cit: 93]
- `[P]` Sevilla, J., Heim, L., Ho, A., Besiroglu, T., & Hobbhahn, M. (2022). Compute Trends Across Three Eras of Machine Learning. *arXiv:2202.05924.* *(In Kilder/ as `Sevilla2022_ComputeTrendsThreeEras_arXiv2202.05924.pdf` — downloaded between cycles. Documents GPU compute deployment growth across three eras of ML (pre-deep learning, deep learning, large-scale); primary evidence that compute deployed has grown faster than per-FLOP efficiency gains; anchor for Jevons paradox framing in §4.2.)* [OA cit: 40]
- `[J]` Masanet, E., Shehabi, A., Lei, N., Smith, S., & Koomey, J. (2020). Recalibrating global data centre energy-use estimates. *Science*, 367(6481), 984–986. https://doi.org/10.1126/science.aba3758 [OA cit: 1243] *(Landmark Science study recalibrating global data centre energy projections; documents that hyperscale operators achieve PUE of 1.1–1.2, representing among the most energy-efficient large-scale compute infrastructure globally — qualifies the §5.2 local-vs-cloud environmental advantage claim. Confirmed via OpenAlex.)* *(executor-added 2026-05-13)*
- `[R]` Jevons, W. S. (1865). *The Coal Question: An Inquiry Concerning the Progress of the Nation, and the Probable Exhaustion of Our Coal Mines*. Macmillan. *(Primary historical source establishing the Jevons Paradox: documents the original 1865 observation that improvements in coal engine efficiency increased rather than decreased total coal consumption by expanding economically viable applications; foundational primary source for the Part 4 framing; [R]-tier institutional/primary historical source, iCit threshold not applicable.)* *(executor-added 2026-05-17)*
- `[J]` Sorrell, S. (2009). Jevons' Paradox revisited: The evidence for backfire from improved energy efficiency. *Energy Policy*, *37*(4), 1456–1469. DOI: 10.1016/j.enpol.2008.12.003. *(Systematic peer-reviewed review of empirical evidence for rebound and backfire effects from energy efficiency improvements; modern scholarly restatement of the Jevons Paradox central to §4.1's historical-pattern argument; iCit well above ≥5 threshold from established literature — landmark paper in the rebound effects field, widely cited across energy economics and sustainability policy. S2 rate-limited at execution time; confirmed from established literature.)* *(executor-added 2026-05-17)*

**Classic anchors:**
- `[P]` Patterson, D., Gonzalez, J. E., Le, Q. V., Liang, C., Munguía, L.-M., et al. (2021). Carbon emissions and large neural network training. arXiv:2104.10350. *(In Kilder/ — verified 2026-05-08.)* [OA cit: 130]
- `[J]` Schwartz, R., Dodge, J., Smith, N. A., & Etzioni, O. (2020). Green AI. *Communications of the ACM*, 63(12), 54–63. DOI: 10.1145/3381831. arXiv:1907.10597. *(Upgraded `[P]` → `[J]` 2026-05-08: peer-reviewed CACM publication confirmed via OpenAlex; CrossRef shows no `update-to` retraction records. In Kilder/.)* [OA cit: 1184]
- `[P]` Hoffmann, J., Borgeaud, S., Mensch, A., Buchatskaya, E., Cai, T., et al. (2022). Training compute-optimal large language models (Chinchilla). arXiv:2203.15556. *(In Kilder/.)* [OA cit: 656]
- `[P]` Lacoste, A., Luccioni, A. S., Schmidt, V., & Dandres, T. (2019). Quantifying the carbon emissions of machine learning. arXiv:1910.09700. *(In Kilder/.)* [OA cit: 130]

---

## What Still Needs Work

- Download Bouza et al. 2023 (Environmental Research Communications, open access) — methodological-uncertainty anchor for §1.3
- Download Barbierato & Gatti 2024 (IEEE Access, likely OA) — §5.3 transparency-and-reporting anchor
- Download Tmamna et al. 2024 (Cognitive Computation pruning survey) — §2.3 anchor
- Download Fischer 2025 CodeCarbon validation paper (arXiv) — §1.3 measurement-discrepancy anchor
- Find empirical data on Jevons paradox in AI specifically (data centre energy trend literature beyond IEA 2024/2025)
- Expand Part 3 with concrete benchmark comparisons: Llama-3.1 8B vs. GPT-4 on specific task types (now that Dubey 2024 PDF is local, extract specific MMLU/HumanEval/GSM8K numbers)
- Promote the §1.2 water-cooling footnote to a short standalone subsection drawing on Li et al. 2023 and Jegham 2025's WUE multipliers
- Cross-ref to `v-ai-paradigms-development.md` — scaling paradigm and its limits
- Cross-ref to `n-ai-ml-ecosystem.md` — hardware supply chain, NVIDIA dominance, chip energy profiles
- Cross-ref to `p-governance-compliance-hi.md` — ESG reporting and AI energy disclosure as governance gap
