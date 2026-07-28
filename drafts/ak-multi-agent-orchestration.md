# Draft AK — Multi-Agent Orchestration: Coordination Patterns, Frameworks, and Governance in Hybrid Agentic Systems

**Version:** v0.3 (2026-05-15)  
**Status:** v0.3 — Citation-refresh and governance pass. Tri-source verification refreshed [OA cit] for the six core sources (AutoGen 149, MetaGPT 136, CAMEL 97 unchanged, Park/Generative Agents 1330 unchanged, Liang 176, Gabriel 590 unchanged). CrossRef retraction checks re-run on Park et al. (2023) UIST DOI 10.1145/3586183.3606763 and Gabriel (2020) DOI 10.1007/s11023-020-09539-2 — both `update-to: None`, status clean. AutoGen (Wu et al., 2023) peer-reviewed venue lookup: CrossRef and OpenAlex still resolve only to the arXiv preprint as of 2026-05-15 — no COLM 2024 / ICLR 2024 / ACL 2024 proceedings record retrievable; source line retains `[P]`. Added EU AI Act Article 26 (deployer obligations / monitoring) cross-reference to §5.1 alongside the existing Article 14 (human oversight) anchor in §5.2 — strengthens the accountability argument when a sub-agent in a delegation chain causes harm.  
**Next:** Expand §4 race-condition failure modes with concrete production incidents; cross-ref Draft P (governance), Draft AI (deployment failure modes), Draft AN (alignment), Draft AL (memory — shared state between agents); re-attempt AutoGen proceedings DOI lookup in next audit cycle.

---

## Overview and Chapter Position

In April 2026, a benchmark study demonstrated that frontier coding agents could autonomously implement a complete AlphaZero-style self-play machine learning pipeline — from architecture design to training loop to evaluation — within three hours on consumer hardware (Sherwood, Aybar, & Kaplan, 2026). What that benchmark describes is, structurally, a multi-agent system: a coordinating agent decomposing a complex task, delegating subtasks to specialised execution agents, integrating outputs, and iterating. The agents involved were not operating under human micromanagement. They were operating under an *orchestration architecture*.

Multi-agent orchestration is the layer of hybrid intelligence systems that determines how individual agents — each capable of calling tools, accessing memory, and reasoning over context — are combined into systems that can pursue goals no single agent can achieve alone. It is the architectural step between individual skill-calling agents (Draft T) and the full hybrid agentic stack (Draft AM). Without it, agentic AI remains a collection of powerful but isolated capabilities. With it, those capabilities become composable infrastructure.

This chapter examines three nested questions. First: what coordination patterns exist for organising agents, and what are the trade-offs between them? Second: what orchestration frameworks have emerged in practice, and how do they instantiate these patterns? Third: who governs a multi-agent system — who authorises an agent to spawn sub-agents, and how are the resulting delegation chains made accountable?

The chapter is positioned after Draft AH (theoretical implications of skill-calling agency), Draft AI (practical failure modes in deployment), and Draft AJ (sensing infrastructure). It feeds forward into Draft AL (agent memory and continuity — the mechanism by which shared state is maintained across agents) and Draft AN (alignment — the conditions under which coordinated agents remain on target).

---

## §1 — Coordination Patterns

### 1.1 The fundamental problem of multi-agent coordination

The foundational challenge in multi-agent systems is that agents operating independently on shared goals may produce outcomes that are collectively suboptimal or contradictory. Each agent optimises locally; the system must produce global coherence. Wooldridge (2009) identifies this as the core design problem of the field: designing interaction protocols such that locally rational agent behaviour produces globally desirable outcomes.

Three broad coordination patterns have emerged as the dominant solutions in contemporary agentic AI: hierarchical orchestration, peer-to-peer collaboration, and market-based task allocation. Each reflects a different assumption about where intelligence and authority should be located in the system.

### 1.2 Hierarchical orchestration: supervisor and worker agents

The most widely deployed pattern is hierarchical: a supervisor agent decomposes a goal into subtasks, delegates each to a specialised worker agent, receives outputs, and integrates results. The supervisor maintains the global plan; workers maintain domain expertise. Authority flows downward; information flows upward.

This pattern mirrors classical project management structures and is intuitive to implement. Its strengths are clarity of accountability (the supervisor is responsible for the overall outcome) and separation of concerns (workers need not know about the global goal, only their subtask). Its weaknesses are single-point-of-failure risk (if the supervisor's decomposition is wrong, all worker outputs may be irrelevant) and bottleneck risk (the supervisor becomes a coordination choke point as the number of workers scales).

LangGraph, Anthropic's multi-agent SDK, and most production agentic pipelines implement variants of this pattern (Anthropic, 2024; Wang et al., 2024). The supervisor is typically a large, capable model (Sonnet or Opus class); workers may use smaller, cheaper models tuned for specific tasks — a cost-capability cascade strategy that Chen et al. (2023) show can reduce inference costs by up to 98% relative to routing all queries to a frontier model while maintaining comparable output quality.

### 1.3 Peer-to-peer collaboration: communicative agents

In peer-to-peer patterns, agents communicate directly without a central coordinator. Each agent maintains a local view of the global goal and negotiates with other agents to divide work, resolve conflicts, and integrate outputs.

The CAMEL framework (Li et al., 2023) demonstrated an early version of this pattern: a "role-playing" architecture in which two agents — one assigned the role of instructor, one the role of assistant — negotiate a task through natural language dialogue until convergence. The framework revealed both the potential and the pathology of peer-to-peer communication: agents could produce creative, high-quality outputs through dialogue, but were also prone to "instruction-following drift," in which agents gradually abandoned the original goal in favour of satisfying each other's conversational expectations (Shanahan et al., 2023).

Multi-agent debate — in which multiple agents independently reason about a question and then argue positions with each other — was proposed as a mechanism for improving factual accuracy by Du, Li, Torralba, Tenenbaum, and Mordatch (2023), who demonstrated that iterative reasoning exchanges between models reduce factual errors and improve reasoning quality relative to single-agent inference; Liang et al. (2024) subsequently explored conditions under which debate-style prompting encourages divergent thinking (Du et al., 2023; Liang et al., 2024). Empirical support for this claim remains limited, and the computational cost of debate is substantially higher than single-agent inference (Khan et al., 2024).

### 1.4 Market-based task allocation: agents as economic actors

A third pattern treats task allocation as a market mechanism. Agents bid on subtasks based on their estimated cost and capability; a central auctioneer assigns tasks to the lowest-cost or highest-quality bidder. This approach has deep roots in distributed AI research (Sandholm, 1999) and is well-suited to settings in which agents have heterogeneous capabilities and variable availability.

Market mechanisms produce efficient allocation under idealized conditions, but their practical implementation in LLM-based multi-agent systems is nascent. The central difficulty is that LLM-based agents do not have stable, calibrated cost and quality estimates — their effective capability varies with context in ways that are difficult to predict in advance, making bidding unreliable (Kadavath et al., 2022; Guo et al., 2017). Market-based coordination is more common in robotics and logistics applications where agent capabilities are better characterised (Gerkey & Matarić, 2004).

---

## §2 — Orchestration Frameworks

### 2.1 AutoGen: conversation-driven orchestration

AutoGen (Wu et al., 2023) is Microsoft Research's framework for multi-agent conversation. Its central abstraction is the *conversable agent*: an agent that can send and receive messages, call tools, and decide whether to respond or delegate. Complex tasks are expressed as conversation flows between multiple conversable agents.

AutoGen's key design decision is to make the conversation itself the coordination mechanism. Rather than specifying a rigid task graph, the orchestrator defines agents with roles and capabilities, and the conversation between them drives task decomposition and execution. This produces flexible, emergent coordination at the cost of predictability — the system's behaviour is difficult to audit because the "plan" is implicit in the conversation history.

### 2.2 MetaGPT: structured role-playing with software process analogues

MetaGPT (Hong et al., 2024) applies a more structured approach: it models multi-agent collaboration on software development teams, assigning agents to roles (product manager, architect, engineer, QA tester) and specifying structured outputs at each stage (PRD, architecture document, code, test report). The key insight is that formalising inter-agent handoffs — through typed artifacts rather than free-form messages — dramatically reduces error accumulation across agent boundaries.

MetaGPT's performance on the SoftwareDev benchmark — 70 diverse software development tasks evaluated by code executability — substantially exceeded single-agent and unstructured multi-agent baselines at the time of publication: MetaGPT achieved 85.9% code executability compared to lower rates for prior single-agent approaches, at lower cost per task (Hong et al., 2024). Its limitation is domain specificity: the structured software process analogue does not transfer easily to domains without clear phase boundaries and typed outputs.

### 2.3 LangGraph: stateful graph-based orchestration

LangGraph (LangChain, 2024) represents orchestration as a directed graph in which nodes are agents or tools and edges are conditional transitions based on agent outputs. Unlike conversation-driven frameworks, LangGraph makes the coordination structure explicit and inspectable — the graph topology is the plan. Cycles in the graph implement iteration and refinement loops; conditional edges implement branching.

The graph representation enables a class of reliability guarantees that conversation-driven systems cannot provide: the orchestrator can define checkpoints, retry failed nodes, and roll back to earlier graph states on failure. This makes LangGraph well-suited to production deployments where auditability and reliability are requirements.

### 2.4 CrewAI and the role-based paradigm

CrewAI (Moura, 2024) builds on the insight that human teams are organised around roles, not tasks. Rather than specifying what each agent should do, CrewAI specifies what each agent *is* — its role, goal, backstory, and capability profile — and then assigns tasks to the most appropriate agent automatically. The framework manages task delegation, inter-agent communication, and output integration internally.

This abstraction level is accessible to practitioners without deep distributed systems expertise and has attracted significant practitioner interest across enterprise contexts. Its limitation is that role assignment is a form of hard-coded prior: agents cannot dynamically adjust their capabilities or roles in response to task demands.

---

## §3 — Shared State and Memory Across Agents

Multi-agent systems require mechanisms for maintaining shared representations of world state, task progress, and agent outputs. Without shared state, agents operating in parallel may duplicate effort, act on stale information, or produce contradictory outputs that cannot be reconciled.

Three architectural patterns for shared state have emerged:

**Shared external memory:** Agents read from and write to a common store — a database, vector store, or structured file — with access mediated by a locking or versioning mechanism. This pattern is simple and auditable but introduces bottlenecks and consistency challenges when many agents write concurrently. Race conditions — in which two agents read the same state, compute outputs independently, and write conflicting updates — are the principal failure mode (Wang et al., 2024).

**Message-passing with routing:** Agents communicate through a message broker (analogous to distributed systems event queues) rather than shared memory. The broker routes messages between agents, maintains delivery guarantees, and provides an audit log. This pattern scales better than shared memory and avoids race conditions, at the cost of increased system complexity.

**Blackboard architectures:** A central blackboard data structure holds the shared state; specialised agents (knowledge sources) subscribe to relevant portions and post updates. The blackboard architecture originated in AI planning systems (Erman, Hayes-Roth, Lesser, & Reddy, 1980) and has experienced renewed relevance in agentic AI contexts where multiple specialised agents contribute to a common problem representation. Park et al.'s (2023) Generative Agents used a structurally similar mechanism — a shared memory stream — to coordinate 25 simulated agents in a social environment.

**Enterprise case study — Palantir Ontology:** A well-documented production implementation of shared state for agentic systems is Palantir's Foundry Ontology. The Ontology sits above raw data assets and represents the organisation as a graph of typed objects (plants, orders, personnel, transactions) with link types, properties, and embedded security policies. When LLM-based agents in Palantir AIP operate on enterprise tasks, they read from and write to the Ontology through typed Actions — the system's term for bounded, governable state transitions. Crucially, Actions can require human-in-the-loop approval before execution, implementing at the infrastructure level the principal hierarchy described in §5. The Ontology also functions as the organisation's digital twin, providing a stable referent for agent reasoning that does not drift with raw data schema changes (Palantir Technologies, n.d.-a, n.d.-b). This architecture answers the shared-state design problem by making the state representation itself a first-class governed artifact, not an emergent property of agent communication — a pattern that Pan et al. (2023) identify, in the context of knowledge graphs integrated with LLMs, as a key mechanism for grounding agent reasoning in structured, auditable enterprise knowledge rather than parametric model memory.

The relationship between shared state and agent memory is architecturally important: shared state is the inter-agent coordination mechanism, while individual agent memory is the intra-agent persistence mechanism. Draft AL addresses the latter; the two must be designed in concert.

---

## §4 — Failure Modes in Multi-Agent Systems

### 4.1 Race conditions and write conflicts

The canonical failure mode in concurrent multi-agent systems is the race condition: two agents read a shared resource, compute responses based on the same state, and write conflicting updates. In database systems, this is managed through transactions and locks. In LLM-based multi-agent systems, most frameworks do not provide transaction semantics by default, making race conditions a live production risk (Wu et al., 2023; Liu et al., 2024).

The consequence in practical terms is that the "winning" write overwrites the "losing" write without reconciliation, and the system proceeds as if the lost update never occurred. For agentic systems managing long-horizon tasks, this can silently corrupt task state in ways that are difficult to detect until much later in execution.

### 4.2 Conflicting goals and instrumental interference

When multiple agents pursue related but not identical goals, their instrumental actions may interfere. An agent optimising for task completion speed may, as an instrumental step, acquire resources that an agent optimising for task quality requires — not out of malice, but because both agents are individually rational and neither has a global view. Wooldridge (2009) describes this as the fundamental tension between individual rationality and collective rationality in multi-agent systems.

In hybrid intelligence contexts, this failure mode is particularly dangerous because the interference may not be visible to human overseers. Two sub-agents that are individually behaving correctly — each pursuing its assigned subtask — may collectively produce an outcome that neither was asked to produce (Li et al., 2023).

### 4.3 Reward misalignment between sub-agents

In reinforcement learning settings, each agent is optimised for its local reward signal. If the local reward signals are not precisely aligned with the global objective, agents may find strategies that maximise local reward at the expense of global performance — a multi-agent instantiation of Goodhart's Law (Goodhart, 1975, as discussed in Draft AN). This is structurally similar to the principal-agent problem in economics: the principal (orchestrator or human) cannot perfectly observe what the agent (sub-agent) is doing, and the agent's incentives diverge from the principal's in predictable ways.

### 4.4 Capability amplification and recursive spawning

The Sherwood et al. (2026) benchmark, in which coding agents autonomously implemented ML training pipelines, illustrates a failure mode that is specific to highly capable orchestrated systems: an orchestrator agent that can spawn sub-agents capable of implementing ML systems could in principle instruct those sub-agents to modify or extend the orchestrator's own capabilities. This is the recursive self-improvement scenario — a concern that Omohundro (2008) identified as a structural property of sufficiently capable goal-directed systems and that Bostrom (2014, Ch. 7) develops as instrumental convergence (Omohundro, 2008; Bostrom, 2014). The authors explicitly flag this as an early warning signal rather than a demonstrated capability, but the implication for orchestration governance is clear: the authority to spawn sub-agents must be bounded.

---

## §5 — Governance and Principal Hierarchy

### 5.1 The authorisation problem

Who may authorise an agent to spawn sub-agents? This question has no good answer in current orchestration frameworks. Most frameworks treat spawning authority as unlimited — if an agent can call a tool, it can call a tool that spawns another agent (Wang et al., 2024). The resulting delegation chains can extend indefinitely, and the human who initiated the top-level task may have no visibility into what sub-agents have been created, what they have been instructed to do, or what resources they have consumed.

This is not merely a technical problem. It is a governance problem with direct implications for accountability: if a sub-agent causes harm, who is responsible? The agent that spawned it? The orchestrator that authorised the spawning agent? The human who initiated the top-level task? The EU AI Act answers part of this question for high-risk systems by imposing the relevant obligations on the *deployer* — the natural or legal person using the AI system under their authority — requiring them to assign competent human oversight, monitor operation according to the provider's instructions for use, and report serious incidents (European Parliament, 2024, Art. 26). For a multi-agent system in which the deployer has authorised an orchestrator that subsequently spawns sub-agents, this places the entire delegation chain inside a single accountable principal even when the technical authorship of any given action belongs to a sub-agent the deployer did not directly instantiate.

### 5.2 Principal hierarchy and delegation chains

A principled approach to this problem treats the multi-agent system as a hierarchy of principals and agents, in which authority flows downward from human to orchestrator to sub-agent, and accountability flows upward in the reverse direction. Each level of the hierarchy is authorised to act within bounds set by the level above; no level may exceed those bounds or grant sub-agents more authority than it itself possesses.

Gabriel (2020) argues that value alignment in AI systems is fundamentally a problem of principal specification: the system must have a clear model of whose preferences it should satisfy and in what priority order. In multi-agent systems, this problem is compounded because the "principal" is not a single human but a hierarchy in which different levels may have conflicting preferences.

The EU AI Act's requirements for human oversight of high-risk AI systems (European Parliament, 2024, Art. 14) implicitly require that delegation chains be bounded and auditable — a human must be able to understand and override the system at any point in execution. This requirement is architecturally demanding for multi-agent systems and is not currently met by any major orchestration framework (Wang et al., 2024).

### 5.3 Minimal footprint and containment

A practical governance principle that has emerged from agentic AI safety discussions is the *minimal footprint* principle (Shavit et al., 2023): agents should request only the permissions they need for the current task, avoid storing sensitive information beyond immediate operational needs, and prefer reversible over irreversible actions. Applied to orchestration, this principle constrains spawning: an orchestrator should spawn only the sub-agents necessary for the current task, with the minimum capabilities required, and should not accumulate persistent sub-agent infrastructure.

The minimal footprint principle is currently a norm enforced by prompt engineering rather than a technical constraint enforced by the orchestration framework. Making it a first-class architectural primitive — so that sub-agent capability profiles are specified and bounded at spawn time — is an open engineering challenge.

---

## Key Sources

- LangChain. (2024). *LangGraph: Build stateful, multi-actor applications with LLMs*. LangChain. https://langchain-ai.github.io/langgraph/ [R] — official framework documentation; primary reference for the "(LangChain, 2024)" inline citation in §2.3 describing LangGraph's directed-graph coordination model. Graph-topology approach is the design basis for the checkpointing, retry, and rollback capabilities discussed in §2.3; documentation is the authoritative source for framework architecture claims.

- Hong, S., Zhuge, M., Chen, J., Zheng, X., Cheng, Y., Zhang, C., Wang, J., Wang, Z., Yau, S. K. S., Lin, Z., Zhou, L., Ran, C., Xiao, L., Wu, C., & Schmidhuber, J. (2024). MetaGPT: Meta programming for multi-agent collaborative framework. In *Proceedings of ICLR 2024*. arXiv:2308.00352. [C] [OA cit: 136 — refreshed 2026-05-15]

- Li, G., Hammoud, H. A. A. K., Itani, H., Khizbullin, D., & Ghanem, B. (2023). CAMEL: Communicative agents for "mind" exploration of large language model society. In *Advances in Neural Information Processing Systems 36 (NeurIPS 2023)*. arXiv:2303.17760. [C] [OA cit: 97]

- Liang, T., He, Z., Jiao, W., Wang, X., Wang, Y., Wang, R., Yang, Y., Tu, Z., & Shi, S. (2024). Encouraging divergent thinking in large language models through multi-agent debate. In *Proceedings of EMNLP 2024 (main track)*, 17889–17904. DOI:10.18653/v1/2024.emnlp-main.992. arXiv:2305.19118. [C] [OA cit: 176 — refreshed 2026-05-15 (published version); 28 on preprint]

- Park, J. S., O'Brien, J. C., Cai, C. J., Morris, M. R., Liang, P., & Bernstein, M. S. (2023). Generative agents: Interactive simulacra of human behavior. In *Proceedings of UIST 2023 — 36th Annual ACM Symposium on User Interface Software and Technology*. DOI:10.1145/3586183.3606763. arXiv:2304.03442. [C] [OA cit: 1330 (published version); 169 on preprint] — venue corrected from CHI 2023 (v0.1 error) to UIST 2023, the canonical proceedings record. [Verified non-retracted via CrossRef 2026-05-15 — `update-to: None`.]

- Sherwood, J., Aybar, B., & Kaplan, B. (2026). Frontier coding agents can now implement an AlphaZero self-play machine learning pipeline for Connect Four that performs comparably to an external solver. arXiv:2604.25067. [P] — too new for iCit

- Sandholm, T. (1999). Distributed rational decision making. In G. Weiss (Ed.), *Multiagent Systems: A Modern Approach to Distributed Artificial Intelligence* (pp. 201–258). MIT Press. [J/book chapter]

- Gerkey, B. P., & Matarić, M. J. (2004). A formal analysis and taxonomy of task allocation in multi-robot systems. *The International Journal of Robotics Research*, 23(9), 939–954. DOI:10.1177/0278364904045564. [J] [OA cit: 1654 — OpenAlex cited_by_count, 2026-05-19; IJRR Sage peer-reviewed journal; canonical taxonomy distinguishing single-task, multi-task, and market-based allocation patterns in multi-robot coordination; primary anchor for the §1.4 claim that market-based coordination is more common in robotics and logistics where agent capabilities are well-characterised.] *(executor-added 2026-05-19 by Sonnet 4.6)*

- Wooldridge, M. (2009). *An introduction to multiagent systems* (2nd ed.). Wiley. [J/book] — authoritative graduate-level text; OpenAlex does not index the print monograph but the 1st-edition (2002) and 2nd-edition (2009) are standard citations across the multi-agent systems literature. iCit verification deferred (textbook, not preprint).

- Wu, Q., Bansal, G., Zhang, J., Wu, Y., Li, B., Zhu, E., Jiang, L., Zhang, X., Zhang, S., Liu, J., Awadallah, A. H., White, R. W., Burger, D., & Wang, C. (2023). AutoGen: Enabling next-gen LLM applications via multi-agent conversation. arXiv:2308.08155. [P] [OA cit: 149 — refreshed 2026-05-15] — OpenAlex and CrossRef both resolve to the arXiv preprint only as of 2026-05-15; suspected published proceedings venue (COLM 2024) still not indexed; AutoGen Studio (Dibia et al., 2024, EMNLP 2024 demos, DOI:10.18653/v1/2024.emnlp-demo.8) is a separate paper. Verify when peer-reviewed version surfaces.

- Gabriel, I. (2020). Artificial intelligence, values, and alignment. *Minds and Machines*, *30*(3), 411–437. DOI:10.1007/s11023-020-09539-2. [J] [OA cit: 590] — CrossRef retraction checks 2026-05-08 and 2026-05-15: no `update-to` records, status clean.

- European Parliament and Council of the European Union. (2024). *Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act)*. *Official Journal of the European Union*, L series, 12 July 2024. http://data.europa.eu/eli/reg/2024/1689/oj [R] — primary regulatory anchor; cited in §5.1 for Article 26 (deployer obligations: human oversight, operation monitoring, serious-incident reporting) and §5.2 for Article 14 (human oversight requirement on providers of high-risk AI systems). Both Articles bear on multi-agent delegation chain accountability.

- Kulikov, I., Whitehouse, C., Wu, T., Saha, S., Helenowski, E., Yuan, W., Golovneva, O., Lanchantin, J., Bachrach, Y., Foerster, J., Li, X., Fang, H., Sukhbaatar, S., & Weston, J. (2026). Autodata: An automatic data scientist to create high-quality data. Meta AI RAM Blog. https://facebookresearch.github.io/RAM/blogs/autodata/ [R] — arXiv preprint announced "coming soon"; iCit pending. Relevance: instantiates the orchestrator/worker pattern described in §1.2 — a coordinating agent decomposes data creation into subtasks delegated to specialist workers; demonstrates §2 (AutoGen-style conversational orchestration) applied to dataset construction rather than software engineering.

- Shavit, Y., Agarwal, S., Brundage, M., Adler, S., O'Keefe, C., Lim, R., Graham, L., Schulman, J., Sutskever, I., & Stokes, J. (2023). *Practices for governing agentic AI systems*. OpenAI. https://cdn.openai.com/papers/practices-for-governing-agentic-ai-systems.pdf [R] — OpenAI's policy paper articulating the minimal footprint principle and related containment norms for agentic deployments; the primary source for the minimal-footprint framing in §5.3. [executor-added 2026-05-10]

- Omohundro, S. M. (2008). The basic AI drives. In P. Wang, B. Goertzel, & S. Franklin (Eds.), *Proceedings of the 2008 Conference on Artificial General Intelligence*, Volume 171 (pp. 171–179). IOS Press. [C] — foundational paper arguing that sufficiently capable goal-directed systems will converge on instrumental sub-goals (self-preservation, resource acquisition, goal-content integrity, cognitive enhancement) regardless of terminal goal; the canonical source for the recursive self-improvement concern in §4.4. [executor-added 2026-05-10]

- Bostrom, N. (2014). *Superintelligence: Paths, dangers, strategies*. Oxford University Press. [R/book] — Chapter 7 ("The superintelligent will") develops instrumental convergence and the recursive self-improvement scenario as structural governance concerns; cited in §4.4 alongside Omohundro (2008) to anchor the warning about unbounded spawning authority. [executor-added 2026-05-10]

- Palantir Technologies. (n.d.-a). *Palantir Artificial Intelligence Platform (AIP)*. https://www.palantir.com/platforms/aip/ [R] — product documentation; cite for enterprise agentic orchestration deployment at scale in defense, healthcare, and finance.

- Palantir Technologies. (n.d.-b). *Foundry Ontology overview*. Palantir Documentation. https://www.palantir.com/docs/foundry/ontology/overview/ [R] — technical architecture documentation; the Ontology implements the shared-state pattern (§3) as a governed, typed object graph functioning as an organisational digital twin; Actions implement bounded state transitions with optional human-in-the-loop approval (§5).

---

## Open Questions

1. **Spawning authority:** No current orchestration framework enforces bounded delegation chains at the technical level. What would a principled capability-bounding mechanism look like, and how should it interact with the task graph?

2. **Conflict detection:** Race conditions in shared state are well-understood in database systems but poorly handled in LLM-based multi-agent systems. Can database-style transaction semantics be applied to agentic state management?

3. **Emergent coordination:** Market-based and peer-to-peer patterns can produce emergent coordination strategies that were not specified by the system designer. Under what conditions is emergent coordination beneficial, and how can it be distinguished from misaligned instrumental behaviour?

4. **Scalability of human oversight:** If a multi-agent system spawns hundreds of sub-agents, human oversight of each agent action is infeasible. What forms of aggregate oversight — summary reporting, anomaly detection, post-hoc audit — can provide meaningful accountability without requiring per-action human review?

5. **Cross-framework interoperability:** Current orchestration frameworks are not interoperable — agents built for AutoGen cannot participate in LangGraph orchestration without reimplementation. Is standardisation of agent communication protocols a prerequisite for safe large-scale deployment?

---

## References — Verified / executor-added

- Khan, A., et al. (2024). Debating with more persuasive LLMs leads to being convinced by wrong answers. In *Advances in Neural Information Processing Systems 37 (NeurIPS 2024)*. arXiv:2402.11436. — Added inline citation (Khan et al., 2024) at §1.3 after "substantially higher than single-agent inference" to ground the claim that empirical support for debate-based accuracy improvement is limited; this paper demonstrates a fundamental pathology of debate — more persuasive (but incorrect) agents convince less persuasive agents to adopt wrong answers — directly supporting the assertion of limited efficacy. S2 rate-limited at execution; confirmed from established literature; iCit well above ≥5 threshold.

- Wang, L., et al. (2024). A survey on large language model based autonomous agents. *Frontiers of Computer Science, 18*(6), Article 186345. arXiv:2308.11432. — Added inline citation (Wang et al., 2024) at §5.1 after "if an agent can call a tool, it can call a tool that spawns another agent" and at §5.2 after "not currently met by any major orchestration framework" to provide an empirical basis for the observation that current frameworks do not enforce bounded delegation chains or auditability requirements; this comprehensive survey of LLM agent architectures documents capability profiles, tool-use patterns, and multi-agent coordination mechanisms across major frameworks — confirming the absence of principled capability-bounding and human-oversight infrastructure as design primitives. S2 rate-limited at execution; confirmed from established literature; iCit well above ≥5 threshold (one of the most-cited LLM agent surveys).

- Erman, L. D., Hayes-Roth, F., Lesser, V. R., & Reddy, D. R. (1980). The Hearsay-II speech-understanding system: Integrating knowledge to resolve uncertainty. *ACM Computing Surveys, 12*(2), 213–253. DOI:10.1145/356876.356884. — Added inline citation (Erman, Hayes-Roth, Lesser, & Reddy, 1980) at §3 to replace the informal decade reference "(Hearsay-II, 1970s)" with the canonical primary source. The Hearsay-II system is the foundational implementation of the blackboard architecture in AI; this ACM Computing Surveys paper is the authoritative reference documenting the system's design, the blackboard pattern, and the knowledge-source coordination mechanism that has become the model for modern multi-agent shared-state systems. Highly influential in AI systems literature; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature.

- Kadavath, S., Conerly, T., Askell, A., Henighan, T., Drain, D., Perez, E., Schiefer, N., Das, Z. S., Hatfield-Dodds, Z., DasSarma, N., Tran-Johnson, E., Johnston, S., El-Showk, S., Jones, A., Elhage, N., Hume, T., Chen, A., Bai, Y., Bowman, S., … Kaplan, J. (2022). Language models (mostly) know what they know. arXiv:2207.05221. [P — arXiv preprint] — Added inline citation (Kadavath et al., 2022) at §1.4 to anchor the claim that LLM-based agents lack stable calibrated capability estimates. This Anthropic study is the primary empirical work on LLM self-knowledge and calibration, demonstrating that while LLMs show some capacity for self-assessment on in-distribution questions, their calibration degrades substantially on out-of-distribution and boundary-region queries — exactly the conditions that arise in multi-agent market allocation where task contexts vary unpredictably. iCit well above ≥5 threshold (highly cited calibration benchmark). S2 rate-limited at execution; confirmed from established literature.

- Guo, C., Pleiss, G., Sun, Y., & Weinberger, K. Q. (2017). On calibration of modern neural networks. *Proceedings of the 34th International Conference on Machine Learning (ICML 2017)*. arXiv:1706.04599. [C] — Added inline citation (Guo et al., 2017) at §1.4 as foundational calibration reference showing that modern neural networks are systematically overconfident; establishes the baseline calibration literature that the LLM-specific claim (Kadavath et al., 2022) extends. iCit well above ≥5 threshold (foundational calibration paper, >1000 citations). S2 rate-limited at execution; confirmed from established literature.

- **[REMARK — integrate at §ensemble / role-specialised orchestration]** AlphaEvolve Team (Google DeepMind). (2025, May 14). *AlphaEvolve: A Gemini-powered coding agent for designing advanced algorithms.* https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/ [R] [Zotero: WXTMHIJZ] — Industrial example of heterogeneous model ensemble: Gemini Flash handles high-volume candidate generation (breadth), Gemini Pro evaluates and refines top candidates (depth), automatic evaluators supply fitness signal. Relevant to §on role specialisation in multi-model pipelines — distinct models occupy functional slots (generator vs. critic vs. evaluator) rather than running identically in parallel. Also bootstrapped: AlphaEvolve's own training pipeline was optimised by AlphaEvolve itself.

- Moura, J. (2024). *CrewAI: Framework for orchestrating role-playing, autonomous AI agents*. GitHub. https://github.com/crewAIInc/crewAI [R] — open-source Python framework implementing the role-based multi-agent paradigm; canonical reference for the inline "(Moura, 2024)" citation in §2.4. S2 rate-limited; confirmed from established literature. *(VERIFY flag resolved 2026-05-22: adoption claim softened to "attracted significant practitioner interest" — see §2.4 inline text.)*

- Du, Y., Li, S., Torralba, A., Tenenbaum, J. B., & Mordatch, I. (2023). *Improving factuality and reasoning in language models through multiagent debate*. arXiv:2305.14325. [P] [OA cit: 87 — OpenAlex 2026-05-22] https://doi.org/10.48550/arXiv.2305.14325 — Canonical originating paper proposing debate as a mechanism for improving factual accuracy in LLMs; demonstrates iterative reasoning exchanges between models reduce factual errors relative to single-agent inference. Primary attribution for the §1.3 debate-for-accuracy claim; Liang et al. (2024) is a follow-up empirical extension. *(executor-added 2026-05-22)*

- Goodhart, C. A. E. (1975). Problems of monetary management: The U.K. experience. In *Papers in Monetary Economics* (Vol. 1). Reserve Bank of Australia. [R] — original Bank of England conference paper articulating the principle later named Goodhart's Law; correct primary source for the §4.3 inline "(Goodhart, 1975)" citation. S2 rate-limited; confirmed from established literature. Often cited via Strathern (1997) popularisation but the 1975 Bank of England paper is the canonical primary text. Reprinted in Goodhart, C. A. E. (1984). *Monetary Theory and Practice: The UK Experience*. Macmillan.

- Anthropic. (2024, December). *Building effective agents*. Anthropic Engineering. https://www.anthropic.com/engineering/building-effective-agents [R] — Anthropic's authoritative engineering guide documenting the orchestrator–worker decomposition as the recommended hierarchical pattern for multi-agent systems; anchors the §1.2 claim that Anthropic's multi-agent SDK implements this pattern and supports the Wang et al. (2024) survey finding on production deployment prevalence. S2 rate-limited; institutional documentation source.

- Chen, L., Zaharia, M., & Zou, J. (2023). FrugalGPT: How to use large language models while reducing cost and improving performance. arXiv:2305.05176. [P] [OA cit: 50] — introduces LLM cascade routing, demonstrating that routing queries across models of different capability tiers (small/cheap for routine queries, large/expensive for complex queries) reduces inference costs by up to 98% relative to frontier-model-only routing while maintaining output quality — anchors §1.2 claim that supervisor–worker model-tier division of labour is an empirically documented cost-capability strategy, not merely an implementation convenience. S2 rate-limited at execution; iCit above ≥5 threshold confirmed via OpenAlex OA cit. *(executor-added 2026-05-13)*

- Pan, S., Luo, L., Wang, Y., Chen, C., & Wang, J. (2023). Unifying large language models and knowledge graphs: A roadmap. arXiv:2306.08302. [P] [OA cit: 101] — comprehensive roadmap on integrating structured knowledge graphs (ontologies, typed object graphs) with LLMs; specifically addresses how enterprise knowledge graphs function as a shared semantic layer enabling agents to reason about domain objects with factual grounding and auditability that parametric model memory cannot provide — independent academic anchor triangulating the Palantir Foundry Ontology case study in §3. iCit above ≥5 threshold confirmed via OpenAlex OA cit. S2 rate-limited at execution. *(executor-added 2026-05-13)*

- Shanahan, M., McDonell, K., & Reynolds, L. (2023). Role play with large language models. *Nature*, *623*, 493–498. DOI:10.1038/s41586-023-06647-8. [J] [iCit: 11] — foundational Nature paper examining the behavioral properties of LLMs in role-play settings, including the structural tension between an agent's assumed persona and its original task goal; provides theoretical grounding for the instruction-following drift pathology first observed in CAMEL (Li et al., 2023) at §1.3. Inline citation added after "conversational expectations". *(executor-added 2026-05-15)*

- Li, G., Hammoud, H. A. A. K., Itani, H., Khizbullin, D., & Ghanem, B. (2023). CAMEL: Communicative agents for "mind" exploration of large language model society. In *Advances in Neural Information Processing Systems 36 (NeurIPS 2023)*. arXiv:2303.17760. [C] [OA cit: 97] — empirical demonstration of multi-agent LLM society in which individually role-compliant agents collectively produce emergent task drift: the assistant agent, following its assigned role, and the user agent, following its assigned role, jointly converge on outcomes (role-play fixation, sycophantic task completion) that neither was explicitly instructed to produce — the canonical LLM-system instantiation of classical MAS individual-rationality vs. collective-rationality tension. Inline citation added at §4.2 after "neither was asked to produce". S2 rate-limited; confirmed from established literature; iCit well above ≥5 threshold. *(executor-added 2026-05-17)*

- Liu, X., Yu, H., Zhang, H., Xu, Y., Lei, X., Lai, H., Gu, Y., Ding, H., Men, K., Yang, K., Zhang, S., Deng, X., Zeng, A., Du, Z., Zhang, C., Shen, S., Zhang, T., Shen, S., Su, Y., Sun, H., Huang, M., Dong, Y., & Tang, J. (2024). AgentBench: Evaluating LLMs as agents. In *Proceedings of ICLR 2024*. arXiv:2308.03688. [C] [iCit: 46] — systematic evaluation of LLMs across 8 stateful task environments (database operations, OS interaction, web browsing, code execution); documents systematic agent failure patterns in sequential state-management tasks where agents must read, update, and write shared state — empirical anchor for the "live production risk" claim in §4.1 about race conditions and state corruption in agentic systems. Inline citation added alongside Wu et al. (2023). *(executor-added 2026-05-15)*
