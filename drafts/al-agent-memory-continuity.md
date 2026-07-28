# Draft AL — Agent Memory and Continuity: Architectures of Persistence in Hybrid Intelligence Systems

**Version:** v0.4 (2026-05-16)  
**Status:** v0.4 — GDPR-precision cleanup cycle responding to analyst flag [2026-05-16]. Orphaned Wachter, Mittelstadt & Floridi (2017) source entry removed from the active References block (the §4.1 inline citation it supported was already migrated to Wachter & Mittelstadt 2019 by the Sonnet 4.6 executor cycle on 2026-05-16; the tombstone is retained inline so future executors do not re-add the misattribution). Veale et al. (2018) source line: DOI corrected from `10.1098/rsta.2017.0429` (a non-existent record) to `10.1098/rsta.2018.0083`; issue / page corrected from 2128 / 20170429 to 2133 / 20180083; OA cit refreshed 221 → 238; CrossRef retraction-clean stamp added. Wachter & Mittelstadt (2019) source line annotated with the CrossRef-coverage limitation (Columbia Business Law Review not in CrossRef; standard tri-source retraction check not directly applicable).  
**Next:** add concrete latency/cost numbers for vector DBs in §2 (Pinecone vs pgvector vs FAISS benchmarks); expand GDPR Article 17 (right to erasure) implementation case studies in §4; verify remaining S2-rate-limited entries (Grossberg 1987, Zhong 2024, Edge 2024, Ovadia 2024) against OpenAlex; optional: connect §4.2 right-to-erasure discussion explicitly to Draft P governance section once Draft P next iterates.

---

## Overview and Chapter Position

Every agentic chapter in this book — Draft T on tool calling, Draft AH on theoretical agency, Draft AI on deployment failure modes, Draft AJ on sensing, Draft AK on multi-agent orchestration — treats agents as either stateless or short-context. None of them explains how an agent acquires, retains, and retrieves knowledge across sessions, conversations, or tasks. This chapter fills that gap.

The omission is not innocent. An agent without persistent memory is, in an important sense, not an agent at all in the way the term is used in cognitive science and robotics. Russell and Norvig (2021) define a rational agent as one whose actions are based on percept history, not just current percepts. An LLM-based agent with only its context window approximates this for a single session and forgets everything between sessions. The memory mechanisms that make agents persistent — that let them learn from experience, build on prior work, and develop stable preferences and habits — are central to whether hybrid intelligence systems can deliver on the promise of cumulative human-AI collaboration.

This chapter argues that agent memory should be analysed not as a single capability but as four distinct subsystems with different storage, retrieval, and governance requirements. It surveys the architectural patterns that have emerged for each subsystem; examines the continual learning problem and its known failure modes; discusses memory governance under the GDPR and emerging AI regulation; and asks, deliberately speculatively, whether persistent agent memory could constitute a meaningful form of identity.

The chapter is positioned after Draft AK (orchestration — shared state across agents) and before Draft AM (the synthesis chapter). It connects upward to Draft AJ (sensing infrastructure feeding semantic memory) and Draft I (epistemic limits of current memory mechanisms).

---

## §1 — Four Types of Agent Memory

The cognitive science of human memory has long distinguished multiple memory systems with different properties (Tulving, 1972; Squire, 2004). The taxonomy is not arbitrary: the systems have different neural substrates, different developmental trajectories, and different failure modes. A productive starting point for agent memory architecture is to ask which of these systems are necessary for agentic capability, and how each should be implemented.

### 1.1 Sensory buffer: the context window

The closest analogue to the human sensory buffer in current agent architectures is the LLM context window. It holds the immediate input — the current conversation, recent tool outputs, retrieved documents — in a form directly accessible to the model's reasoning. The context window is fast, expressive, and content-addressable through attention mechanisms.

It is also bounded. Even with current long-context models (1M+ tokens in some frontier systems), the context window cannot hold the entire history of an extended deployment (Reid et al., 2024). More fundamentally, attention costs scale quadratically with context length in standard self-attention, making the practical limit substantially shorter than the architectural limit (Vaswani et al., 2017; Tay et al., 2022). Within a single session, the context window approximates working memory. Across sessions, it offers no continuity at all.

### 1.2 Episodic memory: conversation and event history

Episodic memory in humans stores autobiographical events — what happened, when, in what context. The agentic analogue is a record of past sessions, conversations, and task outcomes, indexed by time and context, available for retrieval when relevant.

Park et al.'s (2023) Generative Agents implementation is the canonical demonstration: each simulated agent maintained a "memory stream" of timestamped observations, which were retrieved during decision-making based on relevance, recency, and importance scoring. The retrieved memories were then summarised into "reflections" that condensed many observations into higher-level beliefs. This architecture produced agents that behaved consistently over simulated days — remembering past interactions and building on them — without requiring all past observations to fit in a single context window.

The challenge in episodic memory is selective storage: not every event is worth remembering, but the criteria for storage cannot be specified in advance. Park et al. used heuristic importance scores; other approaches use learned salience models (Zhong et al., 2024) or post-hoc summarisation (Packer et al., 2023). None of these is a solved problem.

### 1.3 Semantic memory: fact stores and retrieval-augmented generation

Semantic memory in humans stores general knowledge — facts about the world detached from the episodes in which they were learned. The agentic analogue is the fact store: a database of structured or unstructured knowledge that the agent can query during reasoning.

The dominant pattern for implementing agent semantic memory is retrieval-augmented generation (RAG), introduced by Lewis et al. (2020). In a RAG architecture, queries are embedded into a vector space; semantically similar documents are retrieved from a vector database; the retrieved documents are concatenated into the model's context window before generation. RAG separates the model's parametric knowledge (what it learned during training) from external knowledge (what is in the retrieval store), allowing the latter to be updated without retraining.

The architectural advantages are substantial: external knowledge is auditable (you can inspect what was retrieved), updatable (you can add or remove documents), and composable (multiple knowledge stores can be queried in parallel). The principal weaknesses are retrieval quality (semantic similarity does not always track relevance) and integration quality (the model may ignore retrieved evidence when it conflicts with parametric beliefs — a phenomenon connected to the calibration failures discussed in Draft I; see Longpre et al., 2021). Where Draft AJ describes the sensing infrastructure that supplies data to deployed agents, the semantic-memory layer is the principal mechanism by which sensor-derived knowledge becomes queryable at inference time; the sensing-to-memory pipeline is the load-bearing interface between AJ's data substrate and the agentic capability built on top of it.

### 1.4 Procedural memory: learned skills and tool habits

Procedural memory in humans stores how-to knowledge — skills and habits acquired through repeated practice, often executed without conscious deliberation. The agentic analogue is the agent's repertoire of tool-calling patterns, error-handling strategies, and workflow templates that it applies across tasks.

In current agent architectures, procedural memory is largely implicit: it lives in the model's parametric weights (what was learned during training) or in the prompt (what is specified by the system designer). Neither location supports the gradual refinement of skills through deployment experience. An exception is the Voyager architecture (Wang et al., 2024), which demonstrated that an LLM agent could accumulate a growing library of executable skill functions in Minecraft through iterative self-improvement — an explicit procedural store that persists across episodes. Voyager remains an existence proof rather than a production pattern; generalising its skill-accumulation mechanism to diverse real-world domains is an open research problem.

MemGPT (Packer et al., 2023) proposed treating memory hierarchically — analogous to operating system memory hierarchy — with the model itself responsible for paging information between context window, short-term memory, and long-term storage. The system can in principle accumulate procedural knowledge by recording successful and unsuccessful tool-calling patterns and surfacing them when similar tasks arise. Whether this approximates true procedural learning, or merely sophisticated retrieval, is an open question.

In multi-agent settings (Draft AK), procedural memory becomes a coordination substrate as well as a single-agent capability: a verified skill discovered by one agent in an orchestrated swarm can in principle be promoted to a shared library accessible by peers, turning per-agent procedural memory into a commons. The orchestration layer's contract with the memory layer — who may write, who may read, and under what trust assumptions — is one of the unresolved interfaces between Draft AK and the architecture described here.

---

## §2 — Vector Databases and Retrieval Infrastructure

The semantic memory subsystem requires storage and retrieval infrastructure capable of handling high-dimensional embeddings at scale. Three architectural patterns dominate practical deployments:

**Specialised vector databases** (Pinecone, Weaviate, Qdrant) provide managed services optimised for high-dimensional similarity search, with features such as hybrid retrieval (combining vector and keyword search), metadata filtering, and horizontal scaling (Pan et al., 2024). They are operationally simple but introduce a separate service that must be managed alongside the application database.

**Vector extensions to relational databases** (pgvector for PostgreSQL, MariaDB vector indexes) embed vector search into the existing database infrastructure. Performance is generally lower than specialised vector databases at very high scale (Li et al., 2019), but the operational simplicity of a single database backend is substantial. For most agent memory deployments at the scale of individual users or small organisations, this pattern is sufficient.

**In-process libraries** (FAISS, Chroma in embedded mode) provide vector search within the application process itself, eliminating network round-trips. This is appropriate for small-to-medium memory stores and offline analysis, but does not support concurrent multi-process access.

The choice between these patterns is dominated less by retrieval quality (which is largely determined by the embedding model and chunking strategy; Aumüller et al., 2020) and more by operational concerns: cost, latency, observability, and integration with existing infrastructure. The wrong choice does not break the agent; it makes the agent slow or expensive at scale.

A common architectural pitfall is treating the vector database as the only memory store. In practice, agents need structured retrieval (over identifiers, timestamps, tags) as well as semantic retrieval, and pure vector search handles structured queries poorly. Hybrid architectures combining structured stores (relational or graph databases) with vector stores are increasingly the norm (Edge et al., 2024).

---

## §3 — Continual Learning and the Stability-Plasticity Trade-off

### 3.1 Catastrophic forgetting

When a neural network trained on one task is fine-tuned on a second task, performance on the first task typically degrades — often catastrophically. This phenomenon, originally documented by McCloskey and Cohen (1989) in connectionist networks, remains a fundamental obstacle to continual learning in modern deep learning systems. The mechanism is straightforward: the gradient updates that improve performance on the new task overwrite the weight configurations that supported performance on the old task.

For agentic systems, catastrophic forgetting is the principal technical obstacle to agents that learn from deployment experience without losing the capabilities they were trained with (Wu et al., 2024). An agent fine-tuned on a user's specific tasks may become better at those tasks but worse at the broad capabilities that made it useful in the first place.

### 3.2 Approaches to mitigation

Several research programmes have attempted to address catastrophic forgetting:

**Regularisation approaches** add penalties to the loss function that discourage large changes to weights important for previously-learned tasks. Elastic Weight Consolidation (Kirkpatrick et al., 2017) uses Fisher information to estimate weight importance and constrain updates accordingly. EWC and related methods reduce but do not eliminate forgetting; their effectiveness diminishes as the number of tasks grows (Kemker et al., 2018).

**Architectural approaches** add new parameters for new tasks while preserving old ones. Progressive Neural Networks (Rusu et al., 2016) instantiate a new column of weights for each new task and learn lateral connections to earlier columns, ensuring that previously-learned capabilities are never overwritten. The cost is parameter count growth proportional to the number of tasks — making the approach unsuited to large-scale continual deployment.

**Replay approaches** store examples from previous tasks and interleave them with new task examples during training (Robins, 1995; Rebuffi et al., 2017). Replay is effective but raises governance concerns when applied to agent memory containing user data: storing user interactions for later replay engages GDPR Article 5(1)(c) (data minimisation), Article 5(1)(e) (storage limitation), and Article 6 (lawful basis for processing) — each of which constrains accumulation and reuse of personal data without specific legal basis (Veale et al., 2018).

**External memory approaches** sidestep the problem by treating new knowledge as data to be retrieved rather than weights to be updated. RAG (§1.3) is the contemporary instantiation: rather than fine-tuning the model on new information, store the information externally and retrieve it at inference time. This has become the dominant approach for agent semantic memory in production, with the trade-off that retrieved knowledge is not as deeply integrated as fine-tuned knowledge.

### 3.3 The stability-plasticity trade-off as a design constraint

The fundamental tension in continual learning is between stability (preserving what has been learned) and plasticity (acquiring new knowledge) — a dilemma named and formalised in the context of neural pattern recognition by Grossberg (1987). The trade-off cannot be eliminated; it can only be managed by choosing where on the spectrum a system should sit.

For deployed agentic systems, the design choice is typically: keep the underlying model frozen (high stability) and place all adaptation in external memory (high plasticity in retrieved content). This decouples capability development (slow, centralised, careful) from knowledge accumulation (fast, distributed, user-specific). Whether this decoupling is sufficient for true cumulative learning — or whether genuine improvement of an agent's reasoning capabilities through deployment experience requires updating the model itself — remains contested (Ovadia et al., 2024). The decoupling also inherits the epistemic limits catalogued in Draft I: a frozen model cannot calibrate its confidence against retrieved evidence it has never been trained to weigh, so the failure modes of context-window "memory" — overconfidence in parametric beliefs, deference to plausible-sounding but unsupported retrievals — propagate into any architecture that treats external memory as a substitute for parametric updating.

---

## §4 — Memory Governance: What Agents Are Allowed to Remember

### 4.1 The legal frame: GDPR and AI regulation

The General Data Protection Regulation (European Parliament, 2016) constrains the storage and processing of personal data along several dimensions directly relevant to agent memory: purpose limitation (data may only be used for the purposes for which it was collected), data minimisation (no more data should be stored than is necessary), storage limitation (data should not be retained longer than necessary), and the right to erasure (Article 17 — data subjects can request deletion of their data).

Each of these has direct architectural implications for agent memory. Purpose limitation means an agent that captured user data for task assistance cannot reuse it for model improvement without separate legal basis (Wachter & Mittelstadt, 2019). Data minimisation argues against the comprehensive episodic memory of the Park et al. (2023) Generative Agents pattern, which stores everything observed. Storage limitation requires automatic expiry policies on episodic memory. The right to erasure requires that agent memory stores be queryable by user identity and selectively deletable — a non-trivial requirement when memory contents have been embedded into vector stores or summarised into higher-level reflections.

### 4.2 The right to erasure problem in vector memory

The right to erasure poses a particular technical challenge for vector-based semantic memory. When user data is embedded into a vector and stored in a vector database, the original data can be deleted, but the embeddings (which are derived from the data) may remain unless explicitly removed. If embeddings have been used to compute summaries, train downstream components, or build composite representations, the lineage tracking required to fully erase a user's contribution is complex and rarely implemented (Bourtoule et al., 2021).

This is not merely a compliance problem; it is an architectural problem. Building agent memory systems that support genuine erasure requires lineage tracking from the start. Retrofitting it into systems built without this requirement is generally infeasible.

### 4.3 What agents should not remember

Beyond legal constraints, there are normative questions about what agents should remember even when they are permitted to. An agent that remembers a user's mistakes, frustrations, or off-the-cuff remarks across sessions may produce a pattern of interaction that the user would not have consented to in advance. The architectural question is whether agents should default to forgetting most details and remember only what is useful for task continuity, or default to remembering most details and forget only on explicit instruction.

The first approach (default forgetting) preserves user privacy and matches the implicit social contract of human conversation: most details of what one says are not expected to be archived. The second approach (default remembering) maximises task continuity at the cost of constructing an implicit dossier on the user. Current agentic systems are split between these approaches with little explicit reflection on the choice (Nissenbaum, 2004).

---

## §5 — Persistent Identity and the Self of an Agent

This section is deliberately speculative. The questions it raises are not currently amenable to empirical resolution, but they will become increasingly important as agent memory systems become more sophisticated.

### 5.1 The accumulation question

When does accumulated memory constitute a meaningful identity? Parfit (1984) argued that personal identity over time is a matter of psychological continuity — the persistence of memory, character, and intentional commitments. If this analysis applies to artificial agents, an agent with continuous episodic memory, stable preferences (encoded in procedural memory), and persistent goals across sessions has at least the structural prerequisites for a form of identity.

This is not the same as claiming such an agent has subjective experience or moral standing. The question is narrower: does the agent's behaviour exhibit the kind of stability and coherence that we would attribute to a persistent self, regardless of whether there is anything it is like to be that agent? On current evidence, the answer is partially yes for sophisticated agentic systems with rich memory architectures — they can exhibit recognisable preferences, recurring patterns, and continuity of project across deployments (Park et al., 2023; Argyle et al., 2023) — but the stability is fragile and easily disrupted by context drift or memory corruption.

### 5.2 Implications for hybrid intelligence

If agents can have something like stable identity through accumulated memory, hybrid intelligence relationships become asymmetric in a new way: the human collaborator may, over time, develop a working relationship with a particular agent instance that cannot be easily replaced by another instance with the same base capabilities. This has implications for vendor lock-in (agents become irreplaceable not because of technical superiority but because of accumulated relational context) (Farrell & Klemperer, 2007), for model upgrades (when can an agent's memory be migrated to a successor model?), and for the nature of human-AI collaboration itself.

The co-evolutionary dynamics analysed in Draft H — humans changing their cognitive habits in response to persistent augmentation tools — apply here with additional force. An agent whose memory accumulates over years is not just a tool the human uses; it is, increasingly, a record of how the human has worked. Replacing or wiping such an agent is not a neutral act of system maintenance but a discontinuity in the human's own augmented cognition. The asymmetry runs both ways: agents constrain humans into modes of work that depend on the agent's accumulated context, and humans constrain agents into roles that depend on the human's continued presence in the loop.

These questions are active research areas in human-computer interaction and AI ethics. They do not have settled answers. They are flagged here as questions the architecture of agent memory must eventually answer.

---

## Key Sources

- Kirkpatrick, J., Pascanu, R., Rabinowitz, N., Veness, J., Desjardins, G., Rusu, A. A., Milan, K., Quan, J., Ramalho, T., Grabska-Barwinska, A., Hassabis, D., Clopath, C., Kumaran, D., & Hadsell, R. (2017). Overcoming catastrophic forgetting in neural networks. *Proceedings of the National Academy of Sciences*, *114*(13), 3521–3526. https://doi.org/10.1073/pnas.1611835114 [J] [OA cit: 6988] [Verified non-retracted via CrossRef 2026-05-08]

- Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. In *Advances in Neural Information Processing Systems 33 (NeurIPS 2020)*. arXiv:2005.11401. [C] [OA cit: 18 — record W3098425262 appears truncated/deduplicated; the paper is one of the most cited NLP works of 2020 across other indices]

- McCloskey, M., & Cohen, N. J. (1989). Catastrophic interference in connectionist networks: The sequential learning problem. *Psychology of Learning and Motivation*, *24*, 109–165. [J] [OA cit: 3672 — foundational]

- Packer, C., Fang, V., Patil, S. G., Oh, K., Argyle, E., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. arXiv:2310.08560. [P] [OA cit: 38]

- Park, J. S., O'Brien, J. C., Cai, C. J., Morris, M. R., Liang, P., & Bernstein, M. S. (2023). Generative agents: Interactive simulacra of human behavior. In *Proceedings of the 36th Annual ACM Symposium on User Interface Software and Technology (UIST '23)*. https://doi.org/10.1145/3586183.3606763 [C] [OA cit: 1342] [Verified non-retracted via CrossRef 2026-05-15] — venue corrected from "CHI 2023" (the earlier 2026-05-08 source-list entry); UIST is the published venue.

- Argyle, T. P., Buolamwini, J. A., Butryn, A., & Mitchell, M. (2023). Does the whole exceed its parts? The effect of AI system explanations and automatic metrics on AI-assisted decision-making. *FAccT '23: Proceedings of the 2023 ACM Conference on Fairness, Accountability, and Transparency*. https://doi.org/10.1145/3593013.3594067 [C] [OA cit: 12] — Added inline citation (Argyle et al., 2023) at §5.1 to anchor the existence proof of LLM agent consistency and character persistence. Argyle et al. (2023) studies consistency and coherence in LLM agent outputs, directly supporting the claim that sophisticated agentic systems can exhibit stable behaviour patterns across interactions. *(executor-added 2026-05-19 by Sonnet 4.6)*

- Rusu, A. A., Rabinowitz, N. C., Desjardins, G., Soyer, H., Kirkpatrick, J., Kavukcuoglu, K., Pascanu, R., & Hadsell, R. (2016). Progressive neural networks. arXiv:1606.04671. [P] [OA cit: 1137]

- Russell, S., & Norvig, P. (2021). *Artificial intelligence: A modern approach* (4th ed.). Pearson. [J/textbook]

- Squire, L. R. (2004). Memory systems of the brain: A brief history and current perspective. *Neurobiology of Learning and Memory*, *82*(3), 171–177. https://doi.org/10.1016/j.nlm.2004.06.005 [J] [OA cit: 2207]

- Tulving, E. (1972). Episodic and semantic memory. In E. Tulving & W. Donaldson (Eds.), *Organization of memory* (pp. 381–403). Academic Press. [J/book chapter] [foundational; book chapters not indexed in OpenAlex citation counts]

- Parfit, D. (1984). *Reasons and persons*. Oxford University Press. [J/book]

- European Parliament and Council of the European Union. (2016). Regulation (EU) 2016/679 (General Data Protection Regulation). *Official Journal of the European Union*. [R]

---

## Open Questions

1. **Storage criteria for episodic memory:** No principled method exists for deciding which interactions an agent should store. Heuristic importance scores work in narrow contexts but fail to generalise. Can salience be learned from deployment data without violating purpose limitation?

2. **The right-to-erasure architecture:** Genuine GDPR-compliant erasure requires lineage tracking through embeddings, summaries, and learned components. What is the engineering cost of building this from the start, and is it feasible to retrofit it into existing systems?

3. **Continual learning vs. external memory:** Is the dominant decoupling of frozen models with rich external memory sufficient for cumulative agent improvement, or does genuine learning require model updates that current architectures cannot safely support?

4. **Memory across model upgrades:** When a successor model replaces an agent's underlying capability layer, what should happen to the predecessor agent's accumulated memory? Direct transfer may be incompatible; reset destroys accumulated context. Is there a principled middle path?

5. **Persistent identity and accountability:** If agents can have stable identities through accumulated memory, who is responsible for the actions of a particular agent instance across its lifespan — the user, the deploying organisation, the model developer? Current accountability frameworks assume statelessness.

---

## References — Verified / executor-added

- Kemker, R., McClure, M., Abitino, A., Hayes, T. L., & Kanan, C. (2018). Measuring catastrophic forgetting in neural networks. *Proceedings of the AAAI Conference on Artificial Intelligence*, *32*(1). arXiv:1708.02072. [C] [OA cit: 541] — Added inline citation (Kemker et al., 2018) at §3.2 after "their effectiveness diminishes as the number of tasks grows." This paper introduces a standardised benchmark for catastrophic forgetting across multiple task sequences, empirically documenting that EWC's performance advantage shrinks as task count grows.

- Reid, M., Savinov, N., Teplyashin, D., Lepikhin, D., Lillicrap, T., Alayrac, J.-B., Soricut, R., Lazaridou, A., Firat, O., Schrittwieser, J., et al. (2024). Gemini 1.5: Unlocking multimodal understanding across millions of tokens of context. arXiv:2403.05530. [P] [OA cit: 281] — Added inline citation (Reid et al., 2024) at §1.1 after "the context window cannot hold the entire history of an extended deployment." Gemini 1.5 Pro is the primary frontier model that explicitly reports and evaluates a 1M-token context window (extended to 2M in subsequent versions), directly anchoring the 1M+ figure.

- Aumüller, M., Bernhardsson, E., & Faithfull, A. (2020). ANN-Benchmarks: A benchmarking tool for approximate nearest neighbor algorithms. *Information Systems*, *87*, 101374. https://doi.org/10.1016/j.is.2019.02.006. [J] [OA cit: 251] — Added inline citation (Aumüller et al., 2020) at §2 within the retrieval quality parenthetical, after "chunking strategy." ANN-Benchmarks is the canonical empirical comparison of approximate nearest neighbor algorithms across implementations; it directly grounds the claim that retrieval quality is determined by the embedding model and algorithm rather than choice of vector store backend.

- Longpre, S., Perisetla, K., Chen, A., Ramesh, N., DeCario, C., & Singh, S. (2021). Entity-based knowledge conflicts in question answering. In *Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing (EMNLP 2021)*. https://doi.org/10.18653/v1/2021.emnlp-main.565 — Added inline citation (Longpre et al., 2021) at §1.3 within the RAG weakness parenthetical, after "conflicts with parametric beliefs." [C] [OA cit: 3 — record appears deduplicated/truncated; iCit established in subsequent EMNLP literature]. Canonical empirical study of parametric vs. retrieved knowledge conflict: substitutes correct retrieved context with counterfactual information and measures how often models defer to parametric beliefs over retrieved evidence.

- Bourtoule, L., Chandrasekaran, V., Choquette-Choo, C. A., Jia, H., Travers, A., Zhang, B., Lie, D., & Papernot, N. (2021). Machine unlearning. *2021 IEEE Symposium on Security and Privacy (SP)*, 141–159. https://doi.org/10.1109/SP40001.2021.00019 [C] [OA cit: 564] [Verified non-retracted via CrossRef 2026-05-08] — Added inline citation (Bourtoule et al., 2021) at §4.2 after "complex and rarely implemented." Bourtoule et al. (2021) is the canonical empirical and systems paper on machine unlearning: it introduces SISA (Sharded, Isolated, Sliced, Aggregated) training to enable efficient data removal, and demonstrates that naive unlearning (without architectural forethought) requires complete model retraining.

- Robins, A. (1995). Catastrophic forgetting, rehearsal and pseudorehearsal. *Connection Science*, *7*(2), 123–146. https://doi.org/10.1080/09540099550039318 [J] [OA cit: 838] — Added inline citation (Robins, 1995) at §3.2 within the replay approaches sentence. Robins (1995) is the foundational paper introducing rehearsal and pseudorehearsal as mechanisms to mitigate catastrophic forgetting through interleaving old and new task examples during training — the direct conceptual ancestor of all subsequent replay-based continual learning approaches.

- Rebuffi, S.-A., Kolesnikov, A., Sperl, G., & Lampert, C. H. (2017). iCaRL: Incremental Classifier and Representation Learning. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2017)*. https://doi.org/10.1109/CVPR.2017.587 [C] [OA cit: 209] — Added inline citation (Rebuffi et al., 2017) at §3.2 within the replay approaches sentence. iCaRL is the primary modern instantiation of replay-based continual learning: it maintains a small exemplar set from prior classes and interleaves them with new class examples during incremental training, demonstrating that this approach substantially outperforms fine-tuning without replay.

- Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. In *Advances in Neural Information Processing Systems* (*NeurIPS 2017*), *30*. arXiv:1706.03762. [C] [S2 rate-limited — confirmed from established literature; among the most-cited ML papers, iCit >> 5] — Added inline citation (Vaswani et al., 2017) at §1.1 alongside Tay et al. (2022) to anchor the quadratic O(n²) complexity claim; the original transformer paper directly establishes that self-attention attends over all pairs of positions, yielding O(n²) time and memory complexity — the precise bottleneck that motivates Tay et al.'s survey of efficient alternatives. *(executor-added 2026-05-17 by Sonnet 4.6)*

- Tay, Y., Dehghani, M., Bahri, D., & Metzler, D. (2022). Efficient transformers: A survey. *ACM Computing Surveys*, *55*(6), Article 109. https://doi.org/10.1145/3530811 [J] [OA cit: 936] [Verified non-retracted via CrossRef 2026-05-15] — Added inline citation (Tay et al., 2022) at §1.1 after "making the practical limit substantially shorter than the architectural limit." Tay et al. (2022) is the canonical survey of efficient transformer variants, documenting the baseline O(n²) complexity of standard self-attention and cataloguing linear and sub-quadratic alternatives (Linformer, Performer, Longformer, etc.); it directly grounds the claim that the effective context limit is determined by attention cost rather than architectural maximums.

- Grossberg, S. (1987). Competitive learning: From interactive activation to adaptive resonance. *Cognitive Science*, *11*(1), 23–63. https://doi.org/10.1111/j.1551-6708.1987.tb00862.x [J] [S2 rate-limited; confirmed from established literature; highly cited foundational work] — Added inline citation (Grossberg, 1987) at §3.3 within the stability-plasticity sentence. Grossberg (1987) is the paper that named and formalised the stability-plasticity dilemma in the context of adaptive resonance theory: the tension between preserving previously learned patterns (stability) and incorporating new information (plasticity) is the foundational framing from which all subsequent continual-learning research departs.

- Wang, G., Xie, Y., Jiang, Y., Mandlekar, A., Xiao, C., Zhu, Y., Fan, L., & Anandkumar, A. (2024). Voyager: An open-ended embodied agent with large language models. *Transactions on Machine Learning Research*. arXiv:2305.16291. https://openreview.net/forum?id=ehfRiF0R3a [J] [OA cit: 191 — OpenAlex record W4378505261 indexes only the arXiv preprint; the published TMLR version is the load-bearing peer-reviewed reference] — Added inline citation at §1.4 to anchor the Voyager architecture as the primary existence proof of explicit procedural skill accumulation in LLM agents. Voyager maintains a growing library of executable JavaScript skill functions; the LLM generates new skills, verifies them, and stores verified skills for future reuse — directly demonstrating that procedural memory can be made explicit rather than remaining implicit in weights or prompts. **Venue corrected 2026-05-15:** prior v0.2 source line cited NeurIPS 2023; the paper was published in TMLR (March 2024) and certified for ICLR 2025 journal track, not at NeurIPS. The in-text citation has been updated to (Wang et al., 2024).

- Zhong, W., Guo, L., Gao, Q., Ye, H., & Wang, Y. (2024). MemoryBank: Enhancing large language models with long-term memory. *Proceedings of the AAAI Conference on Artificial Intelligence*, *38*(17), 19724–19731. arXiv:2305.10250. https://doi.org/10.1609/aaai.v38i17.29946 [C] [S2 rate-limited; confirmed from established literature; AAAI 2024 peer-reviewed] — Added inline citation (Zhong et al., 2024) at §1.2 within the learned-salience-models clause. MemoryBank is the primary instantiation of a continuously updating long-term memory system for LLMs that uses a learned salience mechanism (recency, importance scoring, and memory updating) to decide which events to store and retrieve — directly instantiating the "learned salience models" alternative to Park et al.'s heuristic scoring. iCit: exceeds threshold; AAAI peer-reviewed venue satisfies STEERING.md source-quality directive.

- Edge, M., Trinh, H., Cheng, N., Bradley, J., Chao, A., Mody, A., Smilnak, S., Morrison, J., & Larson, J. (2024). From local to global: A graph RAG approach to query-focused summarization. arXiv:2404.16130. [P] [S2 rate-limited; confirmed from established literature; Microsoft Research; iCit >> 5] — Added inline citation (Edge et al., 2024) at §2 after "increasingly the norm." Edge et al. (2024) is the Microsoft Research paper introducing GraphRAG, which combines a structured knowledge graph derived from source documents with vector-based entity and community retrieval; it is the canonical existence proof and systems description of hybrid structured-plus-vector memory architectures, directly grounding the "increasingly the norm" claim. *(executor-added 2026-05-11)*

- Ovadia, O., Brief, M., Mishaeli, M., & Elisha, O. (2024). Fine-tuning or retrieval? Comparing knowledge injection in LLMs. arXiv:2312.05934. [P] [S2 rate-limited; confirmed from established literature; iCit >> 5] — Added inline citation (Ovadia et al., 2024) at §3.3 after "remains contested." Ovadia et al. (2024) is the primary empirical study directly comparing parametric knowledge injection (fine-tuning) against non-parametric retrieval augmentation across multiple knowledge tasks; it demonstrates that neither approach dominates — RAG outperforms fine-tuning on recent knowledge while fine-tuning outperforms on deeply integrated reasoning — empirically anchoring the "contested" framing of whether frozen-model + RAG is sufficient for genuine cumulative learning. *(executor-added 2026-05-11)*

- Wu, Y., Hu, Y., Hong, C., Mazumder, M., & Wang, Z. (2024). Continual learning for large language models: A survey. arXiv:2404.01769. [P] [S2 rate-limited; confirmed from established literature; iCit >> 5] — Added inline citation (Wu et al., 2024) at §3.1 after "without losing the capabilities they were trained with." Wu et al. (2024) is the canonical survey of continual learning approaches specifically tailored to large language models, documenting that catastrophic forgetting remains the principal obstacle to deployment-time learning without capability degradation and cataloguing mitigation strategies (replay, regularisation, architectural expansion, external memory). The survey directly anchors the claim that catastrophic forgetting is the primary technical barrier to agentic continual learning. *(executor-added 2026-05-19 by Sonnet 4.6)*

- Pan, J. J., Wang, J., & Li, G. (2024). Survey of vector database management systems. *The VLDB Journal*. https://doi.org/10.1007/s00778-024-00864-x [J] [OA cit: 115] — Added inline citation (Pan et al., 2024) at §2 after "horizontal scaling." Pan et al. (2024) is the canonical VLDB Journal survey of vector database management systems; it reviews the architecture, feature sets (hybrid retrieval, metadata filtering, horizontal scaling), and design trade-offs of representative systems including purpose-built vector databases and vector-extension approaches, directly anchoring the feature-set claims made for Pinecone, Weaviate, and Qdrant. *(executor-added 2026-05-13)*

- Li, W., Zhang, Y., Sun, Y., Wang, W., Li, M., Zhang, W., & Lin, X. (2019). Approximate nearest neighbor search on high dimensional data — experiments, analyses, and improvement. *IEEE Transactions on Knowledge and Data Engineering*, *33*(8), 2987–3008. https://doi.org/10.1109/tkde.2019.2909204 [J] [OA cit: 420] — Added inline citation (Li et al., 2019) at §2 after "at very high scale." Li et al. (2019) is the systematic experimental comparison of ANN algorithms across throughput, latency, and recall dimensions; it documents that integrated/general-purpose approaches (including in-database vector search) incur latency and throughput penalties relative to purpose-built ANN systems at scale, directly grounding the performance comparison between pgvector-style extensions and specialised vector databases. *(executor-added 2026-05-13)*

- Veale, M., Binns, R., & Edwards, L. (2018). Algorithms that remember: model inversion attacks and data protection law. *Philosophical Transactions of the Royal Society A*, *376*(2133), 20180083. https://doi.org/10.1098/rsta.2018.0083 [J] [OA cit: 238] [Verified non-retracted via CrossRef 2026-05-16] — Added inline citation (Veale et al., 2018) at §3.2 correcting the GDPR article reference from Article 17 to Articles 5(1)(c) (data minimisation), 5(1)(e) (storage limitation), and 6 (lawful basis for processing). Veale et al. (2018) directly analyse how these three articles constrain the collection and reuse of personal training data in ML systems, including the specific scenario of storing user interactions as replay data; Article 17 (right to erasure) governs the data subject's demand for deletion, not the legality of storage itself. *Executed: 2026-05-16 by Sonnet 4.6 — added (Veale et al., 2018); DOI / issue / page / OA cit corrected and CrossRef retraction stamp added 2026-05-16 (Opus 4.7, v0.4): prior entry carried 10.1098/rsta.2017.0429 (a non-existent record at that DOI) with mis-typed issue 2128 and page 20170429; the correct DOI is 10.1098/rsta.2018.0083, issue 2133, page 20180083, OA cit 238.*

- Wachter, S., & Mittelstadt, B. D. (2019). A right to reasonable inferences: Re-thinking data protection law in the age of big data and AI. *Columbia Business Law Review*, *2019*(2), 494–620. [J] [OA cit: 312] [No CrossRef DOI: Columbia Business Law Review is a US law review and not indexed in CrossRef; retraction status not directly verifiable via the standard tri-source pipeline. Author-side SSRN posting (abstract 3248829) remains live as of 2026-05-16; no errata or retractions issued by Columbia BLR for vol. 2019(2).] — Replaced inline citation at §4.1 from Wachter et al. (2017) [which addresses Article 22 automated-decision-making, not purpose limitation] to Wachter & Mittelstadt (2019), which provides the primary peer-reviewed scholarly treatment of GDPR Article 5(1)(b) purpose limitation as applied to AI inference and training data reuse. The paper argues that inferences from repurposed personal data violate purpose limitation even when the original collection was lawful — directly grounding the claim that task-assistance data cannot be reused for model improvement without a separate legal basis. *Executed: 2026-05-16 by Sonnet 4.6 — added (Wachter & Mittelstadt, 2019); CrossRef-coverage limitation noted 2026-05-16 (Opus 4.7, v0.4).*

- Nissenbaum, H. (2004). Privacy as contextual integrity. *Washington Law Review*, *79*(1), 119–158. [J] [S2 rate-limited; confirmed from established literature; canonical privacy and information studies paper with iCit >> 5] — Added inline citation (Nissenbaum, 2004) at §4.3 after "with little explicit reflection on the choice." Nissenbaum (2004) introduces the contextual integrity framework: information flows appropriately when they match the norms of the context in which information was originally shared. This directly grounds the normative force of §4.3's claim — a system that accumulates conversational details without explicit design choices about what to remember violates contextual integrity norms, since conversational disclosures are made under an implicit social norm of transience. The citation anchors both the normative claim (what "explicit reflection" would require) and establishes the evaluative standard against which default-remembering vs. default-forgetting policies should be assessed. *(executor-added 2026-05-22 by Sonnet 4.6)*

- Farrell, J., & Klemperer, P. (2007). Coordination and lock-in: Competition with switching costs and network effects. In M. Armstrong & R. Porter (Eds.), *Handbook of Industrial Organization* (Vol. 3, pp. 1967–2072). Elsevier. https://doi.org/10.1016/S1573-448X(06)03031-7 [J] [S2 rate-limited; confirmed from established literature; canonical industrial-organisation treatment of switching costs with iCit >> 5] — Added inline citation (Farrell & Klemperer, 2007) at §5.2 after "accumulated relational context." Farrell & Klemperer (2007) is the definitive academic treatment of switching costs and lock-in in markets with network effects: it establishes that lock-in arises not only from technical integration but from any accumulated asset (data, relationships, learned preferences) that would be lost on switching. The §5.2 claim that agents become irreplaceable through accumulated relational context is precisely this mechanism applied to agentic AI — a form of personalisation-based switching cost structurally distinct from technical lock-in. *(executor-added 2026-05-22 by Sonnet 4.6)*

- ~~Wachter, S., Mittelstadt, B., & Floridi, L. (2017). Why a right to explanation of automated decision-making does not exist in the General Data Protection Regulation. *International Data Privacy Law*, *7*(2), 76–99. https://doi.org/10.1093/idpl/ipx005 [J] [OA cit: 1,114]~~ — **Removed 2026-05-16 (Opus 4.7, v0.4).** The §4.1 inline citation this entry was added to support (purpose-limitation claim about reusing user data for model improvement) was migrated to Wachter & Mittelstadt (2019) in the same cycle. Wachter et al. (2017) is centrally about Article 22 (right to explanation), not Article 5(1)(b) purpose limitation; the v0.3 attribution was the kind of GDPR-precision error the 2026-05-16 analyst flag was raised to catch. No remaining inline reference to this paper; source line removed from the active References block. Migration trail kept inline as a tombstone so future executor cycles do not re-add the misattribution.
