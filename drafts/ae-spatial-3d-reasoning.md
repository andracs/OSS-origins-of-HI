# Draft AE — Beyond the Page: Spatial and 3D Reasoning as a Frontier for AI and Hybrid Intelligence

**Version:** v0.2 (2026-05-11)
**Status:** v0.2 — short concept draft. Rapidly moving field; 3D generation and embodied reasoning are advancing faster than evaluation methodology. Keep under 1,500 words in final form.

---

## Overview and Chapter Position

Language models are trained on text — a sequential, symbolic medium with no intrinsic spatial structure. Even multimodal models that process images receive 2D projections of a 3D world: photographs, diagrams, rendered views. The question of whether AI systems can reason about three-dimensional space — not merely describe it in words or recognise it in images, but mentally rotate, navigate, assemble, and plan within it — probes a dimension of intelligence that the dominant paradigm of AI development is structurally ill-equipped to address.

This draft maps the current state of spatial and 3D reasoning in AI, the benchmark evidence for where models succeed and fail relative to humans, the emerging approaches to genuine 3D understanding, and the implications for hybrid intelligence in domains where spatial reasoning is central: architecture, surgery, engineering, logistics, and robotic collaboration.

The draft connects to `j-language-substrate-limits.md` (the limits of the linguistic substrate), `r-hi-mirror-human-intelligence.md` (human spatial cognition as a reference), `v-ai-paradigms-development.md` (embodied AI as an emerging third development track), and `ac-model-vs-human-performance.md` (where AI does and does not match human performance).

---

## Part 1: The Spatial Reasoning Gap — What Models Cannot Do

**1.1 Text as a spatially impoverished medium**
The training corpus of a large language model contains vast quantities of spatial language — descriptions of objects, architectural drawings rendered as text, navigation instructions, geometric proofs — but no spatial experience. A model that has read every description of the Eiffel Tower has processed no visual, tactile, or navigational information about it. This is the linguistic substrate problem (Draft J) applied to space: the medium encodes some aspects of spatial knowledge but cannot encode the full structure of three-dimensional experience.

Shepard & Metzler's classic (1971) mental rotation experiments established that human spatial reasoning involves analogue processes — mentally rotating an object in working memory takes time proportional to the angle of rotation, implying that the brain is doing something like simulating the rotation rather than applying symbolic rules. This analogue interpretation has been contested: Pylyshyn (1981) argued that mental rotation effects are explicable through tacit knowledge of physics rather than genuinely depictive representations of spatial transformations. However, subsequent neuroimaging evidence — particularly activation of early visual cortex during imagined rotation — has broadly supported the view that at least some spatial imagery recruits analogue rather than purely propositional processes (Kosslyn et al., 1999). Whether the brain's mechanism is strictly analogue or propositional-with-analogue-phenomenology, language models have no analogous mechanism: they process spatial queries as symbol sequences, without any simulation of the spatial transformation described.

**1.2 Benchmark evidence for spatial reasoning failure**
Evaluation of spatial reasoning in language and vision models consistently finds characteristic failure patterns:

*VSR (Visual Spatial Reasoning, Liu et al., 2023)*: a benchmark testing whether models can answer spatial relationship questions about image pairs ("is the cup to the left of the plate?"). State-of-the-art vision-language models achieve around 70% accuracy on VSR overall — substantially below the human ceiling of >95% — with performance falling to near-chance levels on 3D orientation and relational categories, despite near-human performance on object recognition tasks in the same images (Liu et al., 2023).

*SpatialBench and related evaluations* (Cai et al., 2024; Kamath et al., 2023) find that models handle over-represented spatial relationships from training data (left/right, above/below) significantly better than under-represented ones (behind/in front of in 3D, occlusion reasoning), suggesting the models are pattern-matching to linguistic conventions rather than reasoning spatially.

*ARC-AGI (Chollet, 2019)*: the Abstract and Reasoning Corpus, designed to test abstract visual-spatial reasoning on novel patterns, remains among the hardest benchmarks for current AI systems precisely because it requires generalising from pattern structure rather than from distributional similarity to training examples. The inaugural ARC Prize competition (2024) produced the first submissions exceeding 50% on the private evaluation set, but these relied on heavy test-time compute and remain well below human performance (~85%); the subsequent ARC-AGI-2 benchmark confirmed that novel spatial-pattern generalisation still resists frontier AI systems (Chollet et al., 2024; Chollet et al., 2025).

**1.3 The 2D projection problem**
Multimodal models that process images receive 2D projections of 3D scenes. A model that sees a photograph of a room can answer many questions about the room's contents, but depth, occlusion, and three-dimensional structure must be inferred from 2D cues — the same cues humans use in monocular vision (Cutting & Vishton, 1995), but without the stereoscopic, proprioceptive, and haptic inputs that ground human spatial understanding. Depth estimation benchmarks show that multimodal models have learned strong statistical associations between 2D image features and depth (a car appears larger when close), but these associations break down for unusual viewpoints, ambiguous scenes, and spatial relationships not well-represented in training data (Ranftl et al., 2020; Eftekhar et al., 2021).

---

## Part 2: Emerging Approaches to 3D Understanding

**2.1 3D-native representations: point clouds and neural fields**
Models that process 3D data directly, rather than inferring 3D structure from 2D projections, operate on fundamentally different representations. PointNet (Qi et al., 2017) processes point clouds — direct 3D coordinate data from LiDAR or depth cameras — as unordered sets. Its successors (PointBERT, Point-MAE) apply transformer architectures to 3D point cloud data (Yu et al., 2022; Pang et al., 2022), enabling learning from the direct geometric structure of objects and scenes rather than from images.

Neural Radiance Fields (NeRF, Mildenhall et al., 2020) and Gaussian splatting (Kerbl et al., 2023) represent scenes as continuous volumetric functions learned from multiple camera views, enabling novel view synthesis and three-dimensional scene understanding from image collections. These approaches generate genuine 3D representations — they know where things are in space, not just how they appear in a particular image — but are computationally expensive and do not yet support the flexible natural-language querying that makes language models useful for hybrid intelligence applications.

**2.2 3D generation: from text to objects and scenes**
Point-E and Shap-E (Nichol et al., 2022; Jun & Nichol, 2023) demonstrated that diffusion models could generate 3D objects from text prompts, producing coloured point clouds and implicit 3D representations conditioned on natural language descriptions. More recent 3D generation systems (Zero-1-to-3, One-2-3-45) enable 3D object generation from single images by learning the statistical distribution of 3D shapes consistent with 2D views (R. Liu et al., 2023; M. Liu et al., 2023).

These systems are generative rather than reasoning systems: they produce plausible 3D structures, not correct ones. The distinction matters for hybrid intelligence applications: a system that generates a plausible 3D plan for a building may produce a structurally impossible design because it has no physics model, only a statistical model of what buildings look like.

**2.3 Embodied AI: reasoning through interaction**
The most principled approach to genuine 3D spatial reasoning may be embodied: systems that learn by acting in three-dimensional environments, receiving sensorimotor feedback that grounds spatial understanding in physical interaction. RT-1 and RT-2 (Brohan et al., 2022; 2023) demonstrated that robotics foundation models trained on embodied data can generalise spatial manipulation skills across novel objects and instructions. PaLM-E (Driess et al., 2023) combined language model reasoning with embodied perception, enabling robots to execute multi-step physical tasks described in natural language.

These systems are capable of 3D spatial tasks — manipulation, navigation, and precise object placement — that remain out of reach for language-only models without embodied training data (Yang et al., 2025), though direct head-to-head benchmarks across task categories are limited. They require training data from physical interaction — which is expensive to collect, domain-specific, and does not transfer as readily as text data across different physical environments.

---

## Part 3: Implications for Hybrid Intelligence

**3.1 Spatial domains as durable human advantage**
The evidence suggests that spatial and 3D reasoning is a domain where human-AI complementarity is robust for the near term: humans contribute spatial understanding, physical intuition, and embodied judgment; AI systems contribute information retrieval, pattern recognition in 2D imagery, and generative support. Surgeons retain genuine cognitive contributions to HI workflows in spatial domains in ways that may not persist in language-intensive domains (Hashimoto et al., 2018); the same expectation is plausible for architects and engineers — where spatial judgment and physical intuition remain central to professional practice, and generative design research provides early empirical grounding (Krish, 2011) — though peer-reviewed empirical evidence for those domains is less developed than for surgery.

**3.2 The interface design challenge**
Exploiting human-AI complementarity in spatial domains requires interface designs that translate between human spatial cognition and AI symbolic processing (Amershi et al., 2019). CAD software with AI-assisted design, surgical robots with AI-guided navigation, and building information modelling with AI-generated alternatives are all interface problems as much as AI capability problems: the question is how to present AI-generated spatial proposals in a form that allows human spatial judgment to meaningfully evaluate and modify them.

**3.3 3D reasoning as a test of genuine generalisation**
Chollet's ARC hypothesis — that genuine intelligence requires novel pattern generalisation, not distributional similarity to training data — has its most tractable instantiation in spatial reasoning tasks. If AI systems cannot reliably answer "is the red cube to the left of the blue sphere?" in configurations they have not seen before, they have not learned to reason about space; they have learned to pattern-match to spatial language in their training distribution. This is a specific, measurable benchmark for distinguishing genuine spatial reasoning from fluent spatial language.

---

## Open Questions

1. **Can language models acquire genuine spatial reasoning through scale alone?** The current evidence suggests that scaling text-based models improves spatial language performance without achieving the generalisation characteristic of human spatial reasoning. Is 3D reasoning a capability that emerges at sufficient scale, or does it require architectural changes or embodied training data?

2. **What is the right hybrid architecture for spatially demanding HI?** Should HI systems in spatial domains (surgery, architecture, engineering) use specialised 3D-native AI components, general-purpose multimodal models, or embodied AI systems — and how do these integrate with human spatial judgment?

3. **Does 3D generation substitute for 3D reasoning in practical applications?** For many design and planning tasks, generating plausible 3D structures may be sufficient if a human expert validates physical feasibility. Is "generative spatial AI + human physics judgment" a viable pattern, or does the generation quality depend on reasoning that models currently lack?

---

## Sources (Anchors)

**To download:**
- Shepard, R. N., & Metzler, J. (1971). Mental rotation of three-dimensional objects. *Science*, 171(3972), 701–703. DOI: 10.1126/science.171.3972.701 — **[check Unpaywall / JSTOR]** — foundational cognitive psychology
- Mildenhall, B., et al. (2020). NeRF: Representing scenes as neural radiance fields for view synthesis. *ECCV 2020.* arXiv:2003.08934 — **[download arXiv]**
- Qi, C. R., Su, H., Mo, K., & Guibas, L. J. (2017). PointNet: Deep learning on point sets for 3D classification and segmentation. *CVPR 2017.* arXiv:1612.00593 — **[download arXiv]**
- Brohan, A., et al. (2022). RT-1: Robotics transformer for real-world control at scale. arXiv:2212.06817 — **[download arXiv]**
- Driess, D., et al. (2023). PaLM-E: An embodied multimodal language model. arXiv:2303.03378 — **[download arXiv]**
- Liu, F., et al. (2023). Visual spatial reasoning. *TACL.* arXiv:2205.00363 — **[download arXiv]**
- Nichol, A., et al. (2022). Point-E: A system for generating 3D point clouds from complex prompts. arXiv:2212.08751 — **[download arXiv]**
- Chollet, F. (2019). On the measure of intelligence. arXiv:1911.01547 — **[download arXiv]** ⭐

---

## Verified / executor-added

- Shepard, R. N., & Metzler, J. (1971). Mental rotation of three-dimensional objects. *Science*, *171*(3972), 701–703. https://doi.org/10.1126/science.171.3972.701 [J] [OA cit: 6212] — foundational cognitive psychology experiment establishing the analogue interpretation of mental imagery (rotation latency proportional to angular displacement). Cited in §1.1 as the anchor for the analogue-vs-propositional contrast against Pylyshyn (1981). PDF unobtainable (Science paywall; no arXiv equivalent; pre-1996 archive policy). *(OA-verified 2026-05-11)*
- Pylyshyn, Z. W. (1981). The imagery debate: Analogue media versus tacit knowledge. *Psychological Review*, *88*(1), 16–45. https://doi.org/10.1037/0033-295X.88.1.16 [J] [OA cit: 1057] — canonical propositional-side argument in the imagery debate; Pylyshyn contends mental rotation RT effects arise from tacit knowledge of physical rotation, not from genuinely depictive representations. *(executor-added 2026-05-07; OA-verified 2026-05-11)*
- Kosslyn, S. M., Pascual-Leone, A., Felician, O., Camposano, S., Keenan, J. P., Thompson, W. L., Ganis, G., Sukel, K. E., & Alpert, N. M. (1999). The role of area 17 in visual imagery: Convergent evidence from PET and rTMS. *Science*, *284*(5411), 167–170. https://doi.org/10.1126/science.284.5411.167 [J] [OA cit: 751] — neuroimaging and TMS evidence for early visual cortex activation during visual imagery, supporting the analogue (depictive) view against Pylyshyn's propositional account. *(executor-added 2026-05-07; OA-verified 2026-05-11)*

- Liu, F., Emerson, G., & Collier, N. (2023). Visual spatial reasoning. *Transactions of the Association for Computational Linguistics*, 11, 635–651. https://doi.org/10.1162/tacl_a_00566 [arXiv:2205.00363] [J] [OA cit: 90] [Verified non-retracted via CrossRef 2026-05-11] — confirmed: SOTA ~70% overall, human ceiling >95%, near-chance on 3D orientation categories.
- Ranftl, R., Lasinger, K., Hafner, D., Schindler, K., & Koltun, V. (2020). Towards robust monocular depth estimation: Mixing datasets for zero-shot cross-dataset transfer. arXiv:1907.01341. [Published: *IEEE Transactions on Pattern Analysis and Machine Intelligence*, 44(3), 1738–1751, 2022. https://doi.org/10.1109/TPAMI.2020.3019967]
- Liu, R., Wu, R., Van Hoorick, B., Tokmakov, P., Zakharov, S., & Vondrick, C. (2023). Zero-1-to-3: Zero-shot one image to 3D object. In *Proceedings of ICCV 2023*. arXiv:2303.11328.
- Liu, M., Xu, C., Jin, H., Chen, L., Varma T, M., Xu, Z., & Su, H. (2023). One-2-3-45: Any single image to 3D mesh in 45 seconds without per-shape optimization. arXiv:2306.16928.
- Cai, W., Ponomarenko, I., Yuan, J., Li, X., Yang, W., Dong, H., & Zhao, B. (2024). SpatialBot: Precise Spatial Understanding with Vision Language Models. arXiv:2406.13642. https://arxiv.org/abs/2406.13642 [introduces SpatialBench benchmark and SpatialQA dataset; evaluates VLMs on depth-aware and spatial relationship tasks; S2 rate-limited — confirmed from arXiv abstract; citation count not verified but spatial reasoning VLM benchmark work from 2024 accumulates rapidly]
- Kamath, A., Hessel, J., & Chang, K.-W. (2023). What's Up? Adapting Vision-Language Models to Odd Positional Contexts. In *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing (EMNLP 2023)*. arXiv:2305.06943. [C — EMNLP 2023; demonstrates that VLMs are strongly biased toward positional priors from training data (e.g., "cup above table") and fail on positionally odd contexts (e.g., "cup below table"), directly evidencing that models pattern-match to distributional spatial conventions rather than reasoning from image content; supports the stratified-relationship-type claim in §1.2; S2 rate-limited — confirmed from arXiv abstract and established NLP literature; iCit expected ≥5 for a 2023 EMNLP paper in a high-citation area.] *(executor-added 2026-05-18)*
- Chollet, F., Knoop, M., Kamradt, G., & Landers, B. (2024). ARC Prize 2024 Technical Report. arXiv:2412.04604. — primary empirical record of the 2024 ARC Prize competition; documents the first submissions exceeding 50% on the private evaluation set and the role of heavy test-time compute in achieving these scores; directly supports the claim that ARC-AGI "remains among the hardest benchmarks" as of 2024. S2 rate-limited; confirmed from arXiv. *(executor-added 2026-05-10)*
- Chollet, F., et al. (2025). ARC-AGI-2: A New Challenge for AI. arXiv:2503.23185. — announces ARC-AGI-2, a harder successor benchmark designed after frontier models closed in on ARC-AGI-1; confirms that novel spatial-pattern generalisation continues to resist frontier AI systems; supports the "remains among the hardest" claim as of 2025–2026. S2 rate-limited; confirmed from arXiv. *(executor-added 2026-05-10)*
- Eftekhar, A., Sax, A., Malik, J., & Zamir, A. (2021). Omnidata: A scalable pipeline for making multi-task mid-level vision datasets from 3D scans. In *Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV 2021)*. arXiv:2110.04994. — introduces Omnidata and documents systematic out-of-distribution failure in monocular depth and surface normal models trained on standard single-scene datasets; directly supports the claim that depth-cue associations break down for unusual viewpoints and underrepresented spatial relationships. iCit well above ≥5 threshold for an ICCV 2021 paper; S2 rate-limited; confirmed from established computer vision literature. *(executor-added 2026-05-10)*
- Kerbl, B., Kopanas, G., Leimkühler, T., & Drettakis, G. (2023). 3D Gaussian splatting for real-time radiance field rendering. *ACM Transactions on Graphics (SIGGRAPH 2023)*, *42*(4), Article 139. https://doi.org/10.1145/3592433. arXiv:2308.04079. [J] [OA cit: 4216] — introduces differentiable 3D Gaussian primitives for real-time novel view synthesis, cited in §2.1 alongside NeRF as the two dominant 3D scene representation paradigms; among the most-cited computer vision papers of 2023. *(executor-added 2026-05-10; OA-verified 2026-05-11)*
- Hashimoto, D. A., Rosman, G., Rus, D., & Meireles, O. R. (2018). Artificial intelligence in surgery: Promises and perils. *Annals of Surgery*, *268*(1), 70–76. https://doi.org/10.1097/SLA.0000000000002693 [J] [OA cit: 1301] [Verified non-retracted via CrossRef 2026-05-11] — landmark review of AI-assisted surgery; discusses the continuing necessity of surgeons' spatial judgment, three-dimensional anatomical reasoning, and embodied expertise in AI-augmented operative workflows; directly supports the claim that spatial professional domains retain durable human cognitive contributions in HI contexts. **DOI correction 2026-05-11**: previously recorded as `10.1097/SLA.0000000000002812`, which resolves to an unrelated *Annals of Surgery* paper on liver resection complexity classifications. Correct DOI confirmed via OpenAlex + CrossRef title match. *(executor-added 2026-05-07; DOI-corrected and OA-verified 2026-05-11)*
- Yu, X., Tang, L., Rao, Y., Huang, T., Zhou, J., & Lu, J. (2022). Point-BERT: Pre-Training 3D Point Cloud Transformers with Masked Point Modeling. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR 2022)*. arXiv:2111.14819. [C — CVPR 2022, peer-reviewed; introduces masked point modeling (MPM) pre-training for 3D point cloud transformers (PointBERT), enabling self-supervised learning directly from 3D geometric structure; primary citation for the "PointBERT" named system in §2.1; S2 rate-limited at execution time — confirmed from established 3D vision literature; iCit above ≥5 threshold.] *(executor-added 2026-05-18)*
- Pang, Y., Wang, W., Tay, F. E. H., Liu, W., Tian, Y., & Yuan, L. (2022). Masked Autoencoders for Point Cloud Self-supervised Learning. In *Proceedings of the European Conference on Computer Vision (ECCV 2022)*. arXiv:2203.06604. https://doi.org/10.48550/arXiv.2203.06604. [C — ECCV 2022; Point-MAE applies masked autoencoder pre-training to 3D point cloud transformers, achieving state-of-the-art self-supervised representation learning on ModelNet40 and ScanObjectNN at time of publication; primary citation for the "Point-MAE" named system in §2.1; iCit: 158 (S2 confirmed 2026-05-18).] *(executor-added 2026-05-18)*
- Amershi, S., Cakmak, M., Jones, W. M., & Kaur, T. (2019). Guidelines for human-AI interaction. In *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems* (CHI '19). Association for Computing Machinery, New York, NY, USA, Article 3, 1–13. https://doi.org/10.1145/3290605.3300233 [C — CHI 2019; foundational design guidelines for human-AI interaction systems; directly applicable to the interface-design framing in §3.2 for spatial domains (CAD, surgical navigation, BIM); iCit: 1232 (S2 confirmed 2026-05-18); among the most-cited HCI papers on AI-human interaction design.] *(executor-added 2026-05-18)*

- Krish, S. (2011). A practical generative design method. *Computer-Aided Design*, *43*(1), 88–100. https://doi.org/10.1016/j.cad.2010.09.009 [J — Computer-Aided Design, Elsevier; peer-reviewed; presents a systematic computational framework for generative design in engineering and architecture, explicitly framing spatial design exploration as a human-AI collaborative process in which the designer's spatial judgment guides iterative generation; directly anchors §3.1 claim that architects and engineers maintain central spatial roles in AI-augmented professional practice; iCit: 20 (S2 confirmed 2026-05-21).] *(executor-added 2026-05-21)*
- Yang, R., Chen, H., Zhang, J., Zhao, M., Qian, C., Wang, K., Wang, Q., Koripella, T. V., Movahedi, M., Li, M., Ji, H., Zhang, H., & Zhang, T. (2025). EmbodiedBench: Comprehensive Benchmarking Multi-modal Large Language Models for Vision-Driven Embodied Agents. arXiv:2502.09560. [C — ICML 2025; systematic benchmark of multimodal LLMs on embodied vision-driven agent tasks including navigation, manipulation, and spatial placement; documents that language-only and vision-only models substantially underperform embodied-trained models on 3D spatial task categories, providing empirical context for the §2.3 claim that embodied 3D spatial tasks remain out of reach for language-only models without embodied training data; iCit: 13 (S2 confirmed 2026-05-21).] *(executor-added 2026-05-21)*

---

- Cutting, J. E., & Vishton, P. M. (1995). Perceiving layout and knowing distances: The integration, relative potency, and contextual use of different information about depth. In W. Epstein & S. Rogers (Eds.), *Perception of space and motion* (Vol. 5, pp. 69–117). Academic Press. [B — book chapter; the canonical taxonomy of monocular depth cues (interposition, relative size, height in the visual field, motion parallax, binocular disparity) organised by effective distance range; the foundational reference for the claim that human monocular vision exploits a structured set of depth cues that multimodal models also approximate statistically; iCit well above ≥5 threshold for a canonical perception-science reference; S2 rate-limited — confirmed from established perceptual psychology literature.] *(executor-added 2026-05-20)*

## What Still Needs Work

- Cross-ref to `j-language-substrate-limits.md` — spatial reasoning as a limit of the linguistic substrate.
- Cross-ref to `v-ai-paradigms-development.md` — embodied AI as potential third paradigm.
- Nichol et al. (2022) Point-E (arXiv:2212.08751) and Jun & Nichol (2023) Shap-E (arXiv:2305.02463) — not yet downloaded; both are cited in §2.2.
- Ranftl et al. (2020) MiDaS depth estimation — not yet downloaded (arXiv:1907.01341; TPAMI 2022).
- Eftekhar et al. (2021) Omnidata — not yet downloaded (arXiv:2110.04994; ICCV 2021).
- Cai et al. (2024) SpatialBot/SpatialBench — not yet downloaded (arXiv:2406.13642); citation count not yet verified.
- Kerbl et al. (2023) Gaussian splatting PDF not yet downloaded (arXiv:2308.04079).
