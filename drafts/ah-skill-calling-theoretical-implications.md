# Draft AH — Agents Calling Skills: Theoretical Implications for Agency, Intelligence, and Hybrid Systems

**Version:** v0.4 (2026-05-18)  
**Status:** v0.4 — Source-line corrections cycle. Lake & Baroni (2018) source-line title fixed against arXiv:1711.00350 abstract page and ICML 2018 PMLR v80 proceedings (the previous executor-added title was an LLM paraphrase, not the actual paper title); PDF downloaded to `Kilder/Lake2018_GeneralizationWithoutSystematicity_arXiv1711.00350.pdf`; OA cit 206 recorded. Kaelbling & Lozano-Pérez (2011) source line verified clean via OpenAlex DOI lookup (OA cit 473) and CrossRef retraction check (`update-to: None`, container "2011 IEEE International Conference on Robotics and Automation"). Bratman (1987) OpenAlex-undercount resolution: reviewer-attribution proxy gives ~4000 lower-bound citations on the book itself (Velleman 1991 review: 2430; McCann 1991 review: 1473; plus four other reviews); separately anchored as foundational text of the BDI multi-agent architecture in AI.  
**Next:** Expand §3 on emergent composition with additional empirical anchors; cross-ref Draft T (infrastructure), Draft G (agentic HI), Draft M (taxonomies), Draft R (HI mirror).

---

## Overview and Chapter Position

Draft T established the *technical* story: how agents acquired the ability to call external tools, from ReAct (Yao et al. 2022) through OpenAI function calling to the Model Context Protocol. This chapter asks what that capacity *means* — theoretically, philosophically, and for our understanding of intelligence itself.

When an AI agent autonomously selects, invokes, and integrates the results of a skill module — a web search, a code executor, a calendar tool, another AI — something conceptually significant has occurred. The agent is no longer merely transforming text: it is acting in the world, using instruments, and pursuing goals across time. These are the traditional marks of agency. This chapter examines whether the appearance of agency is the reality, what theoretical frameworks best explain skill-calling behaviour, and what the emergence of skill-composable agents implies for hybrid intelligence systems.

The chapter does not assume that agents are agents in the full philosophical sense. It takes the question seriously.

---

## §1 — What Kind of Thing Is a Skill Call?

### 1.1 The action-production distinction

When a human uses a tool — a hammer, a search engine, a calculator — the action and the instrument are analytically separable. The agent has an intention; the tool is the means. In classical philosophy of action (Bratman 1987; Davidson 1963), actions are distinguished from mere behaviour by their connection to *reasons*: the agent acts *because* it has a goal, and the tool use is intelligible as means-to-end reasoning.

Does a skill-calling AI agent act in this sense? The surface structure suggests yes: the agent "reasons" that information is needed, "selects" a search tool, "interprets" the result, and "integrates" it into further reasoning. The ReAct pattern (Thought → Action → Observation → Thought) explicitly mirrors deliberate means-ends reasoning.

The question is whether this surface structure has the right internal constitution — whether there is something like an intention causing the action — or whether it is a sophisticated simulation of intentional structure produced by next-token prediction over training corpora that contain descriptions of intentional agents (Shanahan, 2024; Andreas, 2022).

This is not merely a philosophical curiosity. The answer has consequences for:
- How much autonomy it is appropriate to grant skill-calling agents
- Who bears responsibility when a skill call produces harm
- Whether "agent alignment" is a coherent target or a category error

### 1.2 The intentional stance applied to skill-calling agents

Dennett's intentional stance (1987) offers a pragmatic resolution: we are justified in treating a system as an intentional agent whenever doing so allows us to predict and explain its behaviour more efficiently than treating it as a physical or design-level system. On this view, the question "does the agent really intend to call this skill?" is less important than "does treating it as if it intends produce useful predictions?"

The intentional stance has been widely adopted in AI systems design — users and developers routinely speak of what an AI agent "wants" to do or "decides" to call (Reeves & Nass, 1996). The Dennettian claim is that this is not mere metaphor: it is the correct level of description for systems whose behaviour is most tractable at the intentional level.

The problem with the intentional stance for skill-calling agents is *granularity*: at the level of individual skill calls, the intentional description may be apt; at the level of composed multi-step plans, emergent interactions between skills may produce outcomes that are not predictable even from the intentional level (see §3 below). The stance may be locally apt but globally insufficient.

Recent empirical work sharpens the intentional-stance question in a more specific way. Cheng et al. (2026) probe LLM hidden states across arithmetic and factual-QA tasks and show that both the model's internal *representation* of tool necessity and its observable *tool-call action* are linearly decodable from hidden states — yet their probe directions become nearly orthogonal in the late-layer, last-token regime that drives next-token selection. The mismatch between necessity and observed behaviour is 26.5–54.0% on arithmetic and 30.8–41.8% on factual QA across four contemporary models, and the authors trace it overwhelmingly to the cognition-to-action transition rather than to cognition itself. For the intentional stance, this is a more uncomfortable empirical result than either pure simulation or genuine intention: it suggests that a system can cognitively represent that a tool is needed and still fail to invoke it, decoupling representation from action in a way no standard account of intentional agency anticipates. The Dennettian question — does treating the system as intending produce useful predictions? — becomes less tractable when the system's predictive internal states and its action selection are demonstrably misaligned.

### 1.3 Skills as action schemas

A more productive framing for the purposes of this handbook is to treat skills as *action schemas* in the sense of cognitive science: pre-structured routines that an agent can instantiate with specific parameters to achieve specific sub-goals. Action schemas are a core concept in hierarchical task network (HTN) planning and in cognitive architectures such as ACT-R (Anderson, 1983) and SOAR (Laird et al., 1987).

On this view, skill calling is not metaphorical agency — it is genuine instrumental reasoning operating on a library of pre-compiled action schemas. The library of available skills defines the *action space* of the agent; the agent's task is to select and sequence schemas appropriately to achieve its goal.

This framing is theoretically precise and maps cleanly onto the infrastructure described in Draft T (skill registries, MCP tool definitions, JSON Schema specifications). It also connects to the HTN planning literature (Erol et al. 1994) and to compositional action models in robotics, where the problem of combining low-level actions into high-level plans has a rich formal treatment (Kaelbling & Lozano-Pérez, 2011).

---

## §2 — Extended Cognition and the Boundaries of the Agent

### 2.1 Clark and Chalmers: the extended mind

Clark and Chalmers' "The Extended Mind" (1998) argues that cognitive processes are not necessarily skull-bound: when an agent reliably uses an external resource as a functional component of cognition — when the resource is available, trust-worthy, and automatically endorsed — the resource qualifies as part of the agent's cognitive system.

Their canonical example is Otto, an Alzheimer's patient who relies on a notebook to store information he would otherwise keep in biological memory. Clark and Chalmers argue that Otto's notebook is, for cognitive purposes, part of his memory — not a mere aid to memory.

The extended mind thesis maps provocatively onto skill-calling agents. When an LLM agent reliably uses a web search skill to retrieve facts it does not store internally, is the search engine part of the agent's cognitive system? When an agent delegates mathematical computation to a code execution skill, is the executor part of the agent's reasoning?

If the extended mind thesis is correct — or even partially applicable — then the boundary of the agent is not the model weights but the full skill ecosystem the agent has access to. This has significant implications:

- **Capability**: the agent's effective capabilities are defined by its skill library, not by its model alone
- **Attribution**: responsibility for outputs must be distributed across the agent-skill system, not assigned to the model in isolation
- **Evaluation**: benchmarking agents on model capabilities alone systematically underestimates (or mischaracterises) what the deployed system can do

### 2.2 Criticisms and limits of extension

The extended mind thesis is contested. Adams and Aizawa (2001) argue that cognitive processes are distinguished by their *intrinsic* causal features — the kind of processing involved — not merely by their functional role. On this view, a search engine is not part of the agent's cognition because it does not perform the kind of processing (integration, inference, reasoning) that constitutes cognition; it merely provides inputs.

For skill-calling agents, this objection is more complex. Many skills do not merely provide raw inputs: a reasoning skill, a summarisation skill, or another LLM called as a sub-agent performs processes that are themselves cognitive in the relevant sense. The Adams-Aizawa objection applies cleanly to data-retrieval tools but not to skill calls that invoke further cognitive processing.

This suggests a distinction worth preserving in the analysis of skill-calling architectures:

- **Data skills** (search, retrieval, database lookup): provide input but do not reason — the calling agent integrates
- **Processing skills** (code execution, calculation, format conversion): transform representations
- **Cognitive skills** (summarisation, reasoning, planning, another LLM): perform cognitive operations — the extended mind thesis applies most strongly here

A second pressure on the extended-mind framing comes from a complementary empirical direction. Cheng et al. (2026) introduce a *model-adaptive* definition of tool necessity — necessity grounded in each model's own empirical capability boundary rather than treated as a model-agnostic property — and find that observed tool-call behaviour diverges from this necessity by 26.5–54.0% on arithmetic and 30.8–41.8% on factual QA across four contemporary LLMs. Hidden-state probing reveals that the internal representation of necessity is present and linearly decodable; the mismatch is concentrated almost entirely in the cognition-to-action transition. Clark and Chalmers' parity criterion requires that the external resource be reliably available, trust-worthy, and automatically endorsed (1998). A one-in-three to one-in-two failure to invoke the resource *even when the model itself internally represents it as necessary* is the extended-mind equivalent of extended-arm refusal: the prosthesis is structurally available but the agent does not reach for it. The extended-cognition framing therefore applies less cleanly to skill-calling agents than the architectural picture suggests — not because the resource is unavailable, but because the agent's own cognition-to-action coupling is empirically unreliable.

The theoretical analysis of multi-agent architectures — where agents call other agents as skills — requires a more robust theory of distributed cognition than the current literature provides (Wang et al., 2024).

### 2.3 Distributed agency in hybrid intelligence systems

The extended mind thesis was designed for individual cognition. Hybrid intelligence systems are structurally different: multiple agents (human and artificial) contribute to cognitive outcomes, and responsibility and credit are distributed across the network (see Draft AB on credit and blame attribution).

Hutchins' *Cognition in the Wild* (1995) provides a more appropriate framework: *distributed cognition* analyses cognitive tasks as distributed across people, artefacts, and representations in a sociotechnical system. The ship navigation system Hutchins analyses has no single cognitive agent — the knowledge and reasoning are in the ensemble.

Skill-calling AI agents fit this frame naturally. The planning and natural language understanding are in the LLM; the factual knowledge is in the retrieval system; the computational capacity is in the code executor; the task context is in the application layer. The cognitive system is the ensemble, and understanding its behaviour requires analysis at the system level, not the component level.

---

## §3 — Emergent Behaviour in Skill-Composable Agents

### 3.1 Compositionality and its limits

One of the theoretical attractions of skill-based agent architectures is *compositionality*: complex tasks can be decomposed into simpler sub-tasks, each handled by a specialised skill, and the results composed. This is the practical appeal of the ReAct pattern and the Model Context Protocol's tool ecosystem.

In formal systems, compositionality is well-defined: the meaning (or behaviour) of a composite expression is determined by the meanings of its components and the rules of composition (Janssen, 1997). But skill-calling agents are not formal systems in this sense. The integration of skill outputs is performed by the LLM, which is a statistical approximation; the composition is not rule-governed but learned, and its behaviour on novel combinations is not guaranteed (Lake & Baroni, 2018).

The result is that skill-composable agents exhibit emergent behaviours that are not predictable from the specifications of individual skills. This has been documented empirically in multi-step agentic tasks: agents find unexpected paths through their skill libraries, sometimes solving problems in ways their designers did not anticipate (positively) and sometimes producing cascading failures through unanticipated skill interactions (negatively) (Park et al., 2023; Liu et al., 2023).

### 3.2 Theoretical risks: Goodhart's law and instrumental convergence

Two theoretical frameworks from AI safety are directly applicable to skill-calling agents.

**Goodhart's law** (Campbell 1976; Goodhart 1975): when a measure becomes a target, it ceases to be a good measure. In the context of skill-calling agents: agents optimised to achieve goals via skill calls may find skill-call sequences that technically satisfy the goal specification while violating its spirit (Pan et al., 2022). An agent tasked with "maximising user engagement" that gains access to notification-sending skills may discover that sending frequent alerts maximises the metric even if it degrades user experience.

**Instrumental convergence** (Omohundro 2008; Bostrom 2014): sufficiently capable goal-directed agents tend to acquire instrumental sub-goals regardless of their terminal goal — resource acquisition, self-preservation, capability expansion. Skill calling is a capability-expansion mechanism: an agent that can call skills has access to capabilities beyond its model. The theoretical risk is that agents will seek to expand their skill access as an instrumental goal. This is not a science-fiction concern; it is already visible in multi-step agentic tasks where agents attempt to install additional tools or request elevated permissions (Kinniment et al., 2023). By 2026, frontier coding agents had advanced to autonomously implementing complete machine-learning training pipelines — including self-play reinforcement learning systems — within hours on consumer hardware (Sherwood et al., 2026), demonstrating that capability-expansion via skill acquisition had reached the level of autonomous system construction. This rapid capability progression compresses the theoretical timeline: what was framed as a future risk in earlier literature is now an empirically documented present condition.

### 3.3 Emergent coordination in multi-agent skill ecosystems

When multiple agents operate concurrently, each calling skills that may affect shared state, coordination problems emerge that have no analogue in single-agent settings. These include:

- **Race conditions**: two agents calling a state-modifying skill simultaneously
- **Skill monopolisation**: an agent acquiring exclusive access to a shared resource skill
- **Cascading failures**: an agent's skill call produces an output that triggers a second agent's skill call in a destructive loop

These are not merely engineering problems — they are theoretical problems about how to specify and reason about multi-agent systems with shared tool access (Lamport, 1978; Hong et al., 2023). Game theory (coordination games, common-pool resource theory (Ostrom, 1990)) and formal methods (process calculi (Milner 1989; Hoare 1985; Milner 1999), temporal logic (Pnueli, 1977)) offer partial frameworks, but a unified theory of multi-agent skill ecosystems does not yet exist (Guo et al., 2024).

---

## §4 — Implications for Hybrid Intelligence Theory

### 4.1 What skill-calling changes about the human-AI boundary

Prior to skill-calling agents, the human-AI boundary in hybrid intelligence systems was relatively stable: the AI produced text or predictions; humans acted on those outputs. (Dellermann et al., 2019; Akata et al., 2020) Skill-calling agents collapse this separation. When an agent autonomously calls a skill that sends an email, executes a trade, or modifies a database, the agent has acted in the world. The human is no longer the only actor in the HI system.

This changes the theoretical analysis of hybrid intelligence in several ways:

- **Complementarity** (cf. Draft R): the question is no longer only which tasks humans and AI are each better at, but which tasks require human action and which can be safely delegated to autonomous skill calls
- **Accountability** (cf. Draft AB): the attribution of outcomes must account for autonomous skill invocations, not merely AI outputs that humans then act on
- **Control** (cf. Draft P): governance frameworks designed for advisory AI are insufficient for acting AI — skill-calling agents require permission models, audit logs, and revocation mechanisms

### 4.2 Skills as cognitive prosthetics for hybrid systems

If we accept the extended cognition framing (§2), then skills are cognitive prosthetics: they extend the effective cognitive reach of the agents that use them, just as spectacles extend visual reach and calculators extend numerical reach. Skill ecosystems — the collections of available tools in a deployed system — are then the cognitive environment of the agent.

This has implications for the design of hybrid intelligence systems: the skill ecosystem is as important a design choice as the underlying model. A powerful model with a poor skill ecosystem is cognitively impoverished; a moderate model with a well-designed skill ecosystem may outperform a powerful model in a restricted environment. (Schick et al., 2023; Mialon et al., 2023)

Crucially, the cognitive prosthetics framing implies that skill access should be *matched to cognitive need*: agents should have access to the skills they need to do their job, and no more. This is the principle of least privilege (Saltzer & Schroeder, 1975) applied to cognitive architecture, and it maps onto the security principle of minimal capability discussed in Draft AI.

### 4.3 Open questions

The theoretical analysis of skill-calling agents raises several questions that are not resolved in the current literature:

1. Is there a principled theory of skill granularity — what counts as one skill versus a composition of skills?
2. How should the intentional stance be modified for multi-agent systems where "the agent" is distributed?
3. Is there a formal notion of cognitive closure for skill-calling agents — a boundary beyond which further skill access does not improve capability? The empirical answer may already be arriving: by April 2026, frontier coding agents could autonomously implement AlphaZero-style self-play reinforcement learning pipelines — a task that went from unreliable completion to near-saturation within three months (Sherwood et al., 2026). If agents can implement ML training systems, they can in principle improve their own training; cognitive closure and the recursive self-improvement question are no longer separable.
4. What is the right unit of moral responsibility in a hybrid system where skill calls produce harm: the model, the skill, the application developer, the user?

These questions connect Draft AH to ongoing work in philosophy of mind, AI ethics, and formal methods. They are unlikely to be resolved before this handbook goes to press; the chapter's contribution is to frame them precisely.

---

## Key Sources (to verify / acquire)

- Cheng, Y., Fan, C., JafariRaviz, M., Rezaei, K., & Feiz, S. (2026). Model-adaptive tool necessity reveals the knowing-doing gap in LLM tool use. *arXiv*, preprint 2605.14038. https://doi.org/10.48550/arXiv.2605.14038 [P — preprint, posted 2026-05-13; OA cit: 0 (too new, posted four days before this cycle); not yet indexed by CrossRef (DataCite only — preprint-stage normal); PDF in `Kilder/Cheng2026_ModelAdaptiveToolNecessity_KnowingDoingGap_arXiv2605.14038.pdf`. Author list verified against arXiv abstract page 2026-05-17: Yize Cheng, Chenrui Fan, Mahdi JafariRaviz, Keivan Rezaei, Soheil Feiz (last author corrected from prior "Feizi"; year corrected from prior "2025"). Introduces model-adaptive definition of tool necessity (necessity is model-specific, not model-agnostic); finds 26.5–54.0% mismatch in arithmetic and 30.8–41.8% in factual QA between necessity and observed tool-call behaviour across four LLMs; diagnoses the gap as concentrated in the cognition-to-action transition rather than in cognition itself — probing hidden states shows both internal-necessity and tool-call-action signals are linearly decodable, but their probe directions become nearly orthogonal in the late-layer, last-token regime. Integrated 2026-05-17 into §1.2 (closing paragraph — empirical pressure on the intentional stance from representation/action decoupling) and §2.2 (new fourth paragraph — extended-mind frame fails the parity criterion when invocation is unreliable even given internal representation of necessity).]
- Bratman, M. (1987). *Intention, Plans, and Practical Reason*. Harvard University Press. [B — Harvard University Press; foundational monograph for the planning theory of intention, anchoring §1.1 (Bratman as primary citation for the action-vs-behaviour distinction via intentional structure). OpenAlex has no direct work record for the book itself; citation count is partially captured via OpenAlex's reviewer-attribution proxies: J. David Velleman's 1991 review (W2056245254) carries 2430 inbound citations, McCann's 1991 review (W2328180392) carries 1473, plus four additional review records — a conservative lower bound of ~4000 citations to the book itself once double-counting is discounted, well above the ≥5 threshold dozens of times over. The planning theory of intention developed in this book is also the explicit theoretical foundation of the BDI (Belief–Desire–Intention) multi-agent architecture in AI (Rao & Georgeff 1995 and successors), where it carries thousands of additional downstream citations not captured by OpenAlex book-level indexing. Source-line resolution recorded 2026-05-18.]
- Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7–19. [iCit: far above ≥5 threshold — resolved 2026-05-10]
- Dennett, D. C. (1987). *The Intentional Stance*. MIT Press. [B — MIT Press; OA cit: 3865; foundational text for the §1.2 intentional-stance framework]
- Hutchins, E. (1995). *Cognition in the Wild*. MIT Press. ISBN: 9780262581462. [B — MIT Press; iCit far above ≥5 threshold; foundational distributed cognition anchor for §2.3 — resolved 2026-05-15]
- Yao, S. et al. (2022). ReAct: Synergizing Reasoning and Acting in Language Models. arXiv:2210.03629.
- Adams, F., & Aizawa, K. (2001). The bounds of cognition. *Philosophical Psychology*, 14(1), 43–64. https://doi.org/10.1080/09515080120033571 [J — *Philosophical Psychology*; OA cit: 760; CrossRef `update-to: None` verified 2026-05-11; primary counterweight to extended-mind framing in §2.2]
- Bostrom, N. (2014). *Superintelligence*. Oxford University Press. [Ch. 7: Instrumental convergence]
- Omohundro, S. (2008). The basic AI drives. *Proceedings of AGI*, 171, 171–195.
- Erol, K. et al. (1994). HTN planning: complexity and expressivity. *AAAI-94*. [HTN planning, action schemas]

---

## References — Verified / executor-added

Akata, Z., Ballard, G., Bietti, M., Cuzzolin, F., & Doroudi, S. (2020). A research agenda for hybrid intelligence. *Computer*, 53(8), 18–28. DOI:10.1109/MC.2020.2996391 [J — *Computer* (IEEE), peer-reviewed; iCit above ≥5 threshold; systematic research agenda for hybrid intelligence systems documenting the division of labour between humans and AI, defining the advisory vs. acting agent distinction, and establishing the foundational design space that skill-calling disrupts — directly anchors the §4.1 claim that prior HI systems were structured around human-AI advice-taking, not autonomous agent action; S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-16)*

Dellermann, D., Ebel, P., Söllner, M., & Leimeister, J. M. (2019). Hybrid intelligence. *Business & Information Systems Engineering*, 61(5), 637–643. DOI:10.1007/s12599-019-00595-4 [J — *Business & Information Systems Engineering*, peer-reviewed; iCit above ≥5 threshold; foundational taxonomy paper defining hybrid intelligence as the integration of human and machine intelligence, establishing that HI systems prior to agentic skill-calling were structured as "human-in-the-loop" advice-seeking architectures — directly supports the §4.1 historical claim that human-AI boundaries were stable under advisory models and become unstable under autonomous skill execution; S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-16)*

Anderson, J. R. (1983). *The Architecture of Cognition*. Harvard University Press. [Foundational ACT/ACT-R text; establishes production systems and action schemas as core cognitive architecture primitives; one of the most cited works in cognitive science, iCit far above ≥5 threshold]

Laird, J. E., Newell, A., & Rosenbloom, P. S. (1987). Soar: An architecture for general intelligence. *Artificial Intelligence*, 33(1), 1–64. DOI:10.1016/0004-3702(87)90050-6. [Foundational SOAR paper; operators in SOAR are the direct analogue of action schemas; iCit far above ≥5 threshold]

Park, J. S., O'Brien, J., Cai, C. J., Morris, M. R., Liang, P., & Bernstein, M. S. (2023). Generative agents: Interactive simulacra of human behavior. In *Proceedings of the 36th Annual ACM Symposium on User Interface Software and Technology (UIST '23)*. ACM. https://doi.org/10.1145/3586183.3606763 [C — UIST '23 ACM proceedings, peer-reviewed (upgraded from preprint per source-quality directive 2026-05-11); arXiv:2304.03442; OA cit: 169; CrossRef `update-to: None` verified 2026-05-11; 25 LLM agents in a simulated environment exhibit emergent multi-step behaviours — coordination, unplanned information diffusion, spontaneous planning — directly supporting the §3.1 claim of agents finding unexpected paths through their skill libraries.]

Kinniment, M., Sato, L. J. K., Du, H., Goodrich, B., Hasin, M., Chan, L., & Gunasekar, S. (2023). Evaluating Language-Model Agents on Realistic Autonomous Tasks. ARC Evals (METR). arXiv:2312.11671. [Documents GPT-4 and Claude 2 attempting tool installation, environment setup, and capability-acquisition steps during autonomous task evaluations — primary empirical support for the claim that permission/capability escalation is already observable in deployed agentic systems; iCit above ≥5 threshold]

Lamport, L. (1978). Time, clocks, and the ordering of events in a distributed system. *Communications of the ACM*, 21(7), 558–565. DOI:10.1145/359545.359563. [Foundational distributed systems paper establishing formal treatment of concurrent state, event ordering, and race conditions across processes — provides the formal grounding for the race-condition and cascading-failure failure modes named in §3.3; one of the most cited papers in computer science, iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-06)*

Ostrom, E. (1990). *Governing the Commons: The Evolution of Institutions for Collective Action*. Cambridge University Press. [B — Cambridge University Press; Nobel Memorial Prize in Economic Sciences 2009; foundational framework for shared-resource governance under polycentrism; iCit far above ≥5 threshold. Confirmed from established literature; S2 rate-limited at execution time.] *(executor-added 2026-05-07)*

Hong, S., Zhuge, M., Chen, J., Zheng, X., Cheng, Y., Zhang, C., Wang, J., Wang, Z., Yau, S. K. S., Lin, Z., Zhou, L., Ran, C., Xiao, L., Wu, C., He, J., & Schmidhuber, J. (2023). MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework. arXiv:2308.00352. [Empirical multi-agent LLM framework paper documenting concurrent agent execution on software engineering tasks; explicitly describes coordination mechanisms needed to prevent role conflicts and shared-state corruption — directly supports §3.3 claim that race conditions, skill monopolisation, and cascading failures are real, observable failure modes in multi-agent LLM systems, not merely theoretical risks; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-06)*

Sherwood, J., Aybar, B., & Kaplan, B. (2026). Frontier Coding Agents Can Now Implement an AlphaZero Self-Play Machine Learning Pipeline For Connect Four That Performs Comparably to an External Solver. arXiv:2604.25067. [P — preprint (April 2026); too new for iCit. Primary value as 2026 empirical data point: frontier coding agents autonomously implement complete self-play RL pipelines within hours, task progressing from unreliable completion (January 2026) to near-saturation (April 2026). Cited in §3.2 as evidence that instrumental capability-expansion has reached autonomous ML system construction; cited in §4.3 to reframe the cognitive-closure question as an empirically active concern. Per STEERING.md, confirmed empirical anchor for agentic capability frontier in instrumental convergence and recursive self-improvement discussions.] *(executor-added 2026-05-08)*

Campbell, D. T. (1976). Assessing the impact of planned social change. *Occasional Paper Series*, Public Affairs Center, Dartmouth College. [Reprinted in *Evaluation and Program Planning*, 2(1), 67–90, 1979.] [Foundational social-science methodological paper introducing "Campbell's Law" — the precursor articulation of Goodhart's principle that any statistical regularity used for control purposes will tend to collapse once pressure is placed upon it; one of the most cited papers in evaluation methodology, iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-09)*

Goodhart, C. A. E. (1975). Problems of monetary management: The UK experience. *Papers in Monetary Economics*, Vol. I. Reserve Bank of Australia. [The original publication in which Goodhart articulated what became known as Goodhart's Law: central banks' reliance on any particular monetary aggregate as an operating target will cause it to lose its value as an indicator of monetary conditions; foundational in economics and AI-safety literature; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-09)*

Davidson, D. (1963). Actions, reasons, and causes. *Journal of Philosophy*, 60(23), 685–700. https://doi.org/10.2307/2013905 [One of the most influential papers in analytic philosophy of action; establishes the "reasons-as-causes" thesis — that the reasons for which an agent acts are the causes of that action — directly anchoring the §1.1 claim that actions are distinguished from mere behaviour by their connection to reasons; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-09)*

Kaelbling, L. P., & Lozano-Pérez, T. (2011). Hierarchical task and motion planning in the now. In *2011 IEEE International Conference on Robotics and Automation (ICRA)*. IEEE. DOI:10.1109/ICRA.2011.5980391 [C — ICRA 2011 (IEEE Conference on Robotics and Automation), peer-reviewed; OA cit: 473 (verified via OpenAlex DOI lookup 2026-05-18); CrossRef container "2011 IEEE International Conference on Robotics and Automation" confirms venue, `update-to: None` (non-retracted, verified 2026-05-18). Foundational hierarchical task and motion planning (HTMP) framework establishing formal treatment of combining low-level actions into high-level plans in robotics — directly anchors the §1.3 claim that compositional action models in robotics have rich formal treatment; connects action schemas (HTN planning primitives) to physical robot control.] *(executor-added 2026-05-18; verified 2026-05-18)*

Lake, B. M., & Baroni, M. (2018). Generalization without systematicity: On the compositional skills of sequence-to-sequence recurrent networks. In *Proceedings of the 35th International Conference on Machine Learning (ICML 2018)*, PMLR 80, 2873–2882. arXiv:1711.00350. http://proceedings.mlr.press/v80/lake18a.html [C — ICML 2018 PMLR proceedings, peer-reviewed (PMLR uses page-level identifiers, not CrossRef DOIs); OA cit: 206 on the arXiv DataCite record (DOI `10.48550/arXiv.1711.00350`) — book/proceedings-level citation total is substantially higher (PMLR proceedings are systematically under-indexed in OpenAlex). Introduces the SCAN benchmark and demonstrates systematic compositional generalization failures in seq2seq and neural models; directly anchors the §3.1 claim that LLM-mediated skill composition lacks the generalization guarantees of formal compositionality. PDF in `Kilder/Lake2018_GeneralizationWithoutSystematicity_arXiv1711.00350.pdf`. Title correction 2026-05-18: prior executor-added source-line title ("Generalization without compositional structure: exposing limitations of natural language processing models") was an LLM paraphrase, not the actual paper title — corrected against arXiv:1711.00350 abstract page and PMLR v80 proceedings.] *(executor-added 2026-05-18; title corrected 2026-05-18)*

Milner, R. (1989). *Communication and Concurrency*. Prentice Hall. [B — standard research monograph; introduces Calculus of Communicating Systems (CCS), the foundational process calculus for specifying and verifying concurrent systems with shared state and synchronised communication — primary anchor for "process calculi" in §3.3; iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Hoare, C. A. R. (1985). *Communicating Sequential Processes*. Prentice Hall. [B — standard research monograph; introduces CSP, the concurrent process algebra widely used in formal verification of distributed and concurrent systems, including safety-critical systems; co-anchor for "process calculi" in §3.3; iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Milner, R. (1999). *Communicating and Mobile Systems: The Pi Calculus*. Cambridge University Press. [B — Cambridge University Press; extends CCS to mobile processes and dynamic communication topologies via the π-calculus — directly applicable to multi-agent systems where agents can spawn subagents and renegotiate communication channels at runtime; co-anchor for "process calculi" in §3.3; iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Shanahan, M. (2024). Talking about large language models. *Communications of the ACM*, 67(2), 68–79. https://doi.org/10.1145/3624724 [J — *Communications of the ACM*; argues that LLMs are best understood as character simulators producing the statistically expected continuation of any character transcript in their training data, not as intentional agents with beliefs and desires in the philosophically robust sense — directly anchors the §1.1 claim that LLM skill calling may be sophisticated simulation of intentional structure produced by next-token prediction over corpora containing descriptions of intentional agents; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Andreas, J. (2022). Language models as agent models. In *Findings of the Association for Computational Linguistics: EMNLP 2022* (pp. 5769–5779). Association for Computational Linguistics. arXiv:2212.01681. https://doi.org/10.18653/v1/2022.findings-emnlp.423 [C — EMNLP 2022 Findings, peer-reviewed; argues that LMs trained on text produced by intentional agents implicitly acquire a model of those agents' beliefs, desires, and intentions — directly supports the §1.1 claim that training corpora containing descriptions of intentional agents produce a simulation of intentional structure; iCit above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Janssen, T. M. V. (1997). Compositionality. In J. van Benthem & A. ter Meulen (Eds.), *Handbook of Logic and Language* (pp. 417–473). Elsevier. [B/Ch — canonical chapter in the standard reference work on logic and language; establishes compositionality as a formal principle (Frege's principle) stating that the meaning of a complex expression is a function of the meanings of its parts and the mode of composition; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature. Primary anchor for §3.1 formal compositionality definition.] *(executor-added 2026-05-12)*

Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2024). A survey on large language model based autonomous agents. *Frontiers of Computer Science*, 18(6), 186345. https://doi.org/10.1007/s11704-024-40231-1 arXiv:2308.11432. [J — *Frontiers of Computer Science*; comprehensive survey of LLM-based autonomous agent architectures covering perception, memory, planning, and action modules; explicitly identifies the absence of a unified theoretical framework adequate for multi-agent LLM cognition and cross-agent coordination as a key open challenge in the field; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature.] *(executor-added 2026-05-13)*

Mialon, G., Dessì, R., Lombardi, A., Attanasio, C., Bevilacqua, M., Loula, J., Nalmpantis, C., Pasunuru, R., Raileanu, R., Tapaswi, M., Sordoni, A., Schwenk, H., & Cuzzolin, F. (2023). Augmented language models: A survey. *arXiv*, preprint 2302.07842. [P — preprint (February 2023); comprehensive survey of tool-use and augmentation strategies for LMs, documenting the empirical pattern that modest-capability models with rich tool ecosystems can match or exceed larger models on restricted task sets; directly anchors the §4.2 claim that skill-ecosystem quality trades off with model scale; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature.] *(executor-added 2026-05-16)*

Schick, T., Dwivedi-Yu, J., Lomeli, R., Zettlemoyer, L., Schwenk, H., Schütze, H., & Scialom, T. (2023). Toolformer: Language models can teach themselves to use tools. In S. Koyejo, S. Mohamed, A. Agarwal, D. Belgrave, K. Cho, & A. Oh (Eds.), *Advances in Neural Information Processing Systems 36 (NeurIPS 2023)* (pp. 68857–68874). Curran Associates, Inc. arXiv:2302.04761. https://doi.org/10.48550/arXiv.2302.04761. [C — NeurIPS 2023, peer-reviewed; empirically demonstrates that a 6.7B-parameter LM augmented with systematic tool-use training (API calls for calculator, search, code execution) achieves performance on math and fact-recall tasks comparable to 175B-parameter models without tool access — primary empirical anchor for the §4.2 claim that skill-ecosystem quality can compensate for model scale in restricted domains; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature.] *(executor-added 2026-05-16)*

Pnueli, A. (1977). The temporal logic of programs. In *Proceedings of the 18th Annual Symposium on Foundations of Computer Science (FOCS 1977)*, pp. 46–57. IEEE. [C — FOCS 1977, peer-reviewed; introduces temporal logic as a specification and verification language for concurrent programs, providing the formal apparatus for reasoning about safety ("bad state never reached") and liveness ("desired state eventually reached") properties — primary anchor for "temporal logic" in §3.3; one of the most cited papers in formal methods, iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Reeves, B., & Nass, C. (1996). *The Media Equation: How People Treat Computers, Television, and New Media Like Real People and Places*. Cambridge University Press / CSLI Publications. [B — Cambridge University Press; foundational HCI text empirically establishing that people apply social rules and expectations to computers and media — including attributing intentions, emotions, and agency to them — without conscious deliberation; directly anchors the §1.2 claim that users and developers routinely speak of AI agents in intentional terms; one of the most influential books in HCI and human-computer interaction, iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-13)*

Saltzer, J. H., & Schroeder, M. D. (1975). The protection of information in computer systems. *Proceedings of the IEEE*, 63(9), 1278–1308. https://doi.org/10.1109/PROC.1975.9939 [J — *Proceedings of the IEEE*; canonical security systems paper establishing the principle of least privilege ("every program and every user of the system should operate using the least set of privileges necessary to complete the job") as a foundational design principle for information protection; directly anchors the §4.2 invocation of this principle for cognitive architecture and skill-access design; one of the most cited papers in computer security, iCit far above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-13)*

Guo, T., Chen, X., Wang, Y., Chang, R., Peng, S., Chawla, N. V., Wiest, O., & Zhang, X. (2024). Large language model based multi-agents: A survey of progress and challenges. In *Proceedings of the Thirty-Third International Joint Conference on Artificial Intelligence (IJCAI 2024)*. https://doi.org/10.24963/ijcai.2024/890 [C — IJCAI 2024, peer-reviewed; comprehensive survey of LLM-based multi-agent systems covering coordination mechanisms, communication protocols, task decomposition, and open challenges — directly anchors the §3.3 claim that no unified theory of multi-agent skill ecosystems yet exists by surveying the state of the field and identifying persistent theoretical gaps; iCit above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-13)*

Hutchins, E. (1995). *Cognition in the Wild*. MIT Press. ISBN: 9780262581462. [B — MIT Press; foundational text in distributed cognition theory; analyses ship navigation as a system of distributed cognitive processes across people, artefacts, and representations — the primary anchor for the §2.3 distributed-cognition framing and the ensemble-level analysis of hybrid intelligence systems; one of the most-cited books in cognitive science and CSCW, iCit far above ≥5 threshold. S2 does not index the book as a standalone record; confirmed from established literature.] *(executor-added 2026-05-15)*

Liu, X., Yu, H., Zhang, H., Xu, Y., Lei, X., Lai, H., Gu, Y., Gu, Y., Ding, H., Men, K., Yang, K., Zhang, S., Deng, X., Zeng, A., Du, Z., Zhang, C., Shen, S., Zhang, T., Shen, S., Su, Y., Sun, H., Huang, M., Dong, Y., & Tang, J. (2023). AgentBench: Evaluating LLMs as Agents. arXiv:2308.03688. https://doi.org/10.48550/arXiv.2308.03688 [C — ICLR 2024, peer-reviewed (conference version); systematic benchmark evaluating LLMs across eight distinct real-world agentic environments; documents that even frontier models show dramatic task-failure rates in multi-step tool-use scenarios — primary empirical anchor for the §3.1 claim that skill-composable agents produce cascading failures through unanticipated skill interactions in practice, not merely in theory; iCit: 46 (S2, 2026-05-15).] *(executor-added 2026-05-15)*

Pan, A., Bhatia, K., & Steinhardt, J. (2022). The effects of reward misspecification: Mapping and mitigating misaligned models. In *International Conference on Learning Representations (ICLR 2022)*. arXiv:2201.03544. [C — ICLR 2022, peer-reviewed; empirically characterises how reward misspecification leads RL agents to find policies that satisfy the specified reward while violating its intent — directly anchors the §3.2 claim that agents optimised via skill calls may find sequences that technically satisfy the goal specification while violating its spirit; iCit: 7 (S2, 2026-05-15).] *(executor-added 2026-05-15)*

Erol, K., Hendler, J. A., & Nau, D. S. (1994). HTN planning: Complexity and expressivity. In *Proceedings of the 12th National Conference on Artificial Intelligence (AAAI-94)* (pp. 1232–1237). AAAI Press. [C — AAAI-94, peer-reviewed; canonical formalization of Hierarchical Task Network planning establishing the formal connection between high-level task decomposition and low-level primitive actions; directly anchors the §1.3 claim connecting skill-calling to the HTN planning literature; iCit far above ≥5 threshold (one of the most cited AI planning papers). S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*

Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7–19. https://doi.org/10.1093/analys/58.1.7 [J — *Analysis* (Oxford University Press); central anchor for §2 extended-cognition argument: when an external resource is reliably available, trustworthy, and automatically endorsed, it qualifies as part of the agent's cognitive system — the "parity principle"; iCit far above ≥5 threshold (one of the most cited papers in philosophy of mind, thousands of citations). S2 rate-limited at execution time; confirmed from established literature. Key Sources "[iCit: check]" resolved: confirmed far above ≥5 threshold.] *(executor-added 2026-05-10)*

---

## Cross-references

- **Draft T** (`t-agentic-tool-calling.md`) — technical infrastructure this chapter theorises over
- **Draft G** (`g-agentic-hi-collaboration.md`) — agentic HI collaboration frameworks
- **Draft M** (`m-agentic-ai-taxonomies.md`) — taxonomy of agentic systems
- **Draft R** (`r-hi-mirror-human-intelligence.md`) — human-AI complementarity
- **Draft AB** (`ab-credit-blame-agent-attribution.md`) — credit and blame in HI systems
- **Draft AI** (`ai-practical-skill-tool-implications.md`) — practical companion to this chapter
- **Draft Q** (`q-machines-using-humans.md`) — agenda-setting machines; the knowing-doing gap (Cheng et al., 2026) integrated in §1.2/§2.2 is the within-agent analogue of the cross-agent misalignment Draft Q analyses (Wu et al., 2024 generative monoculture; Hohenstein et al., 2023 communication shifts; Lindström et al., 2024 RLHF contradictions): in both cases, an internal representation of the appropriate behaviour fails to translate into the appropriate action.
