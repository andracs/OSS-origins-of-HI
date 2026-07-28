# Draft M — Taxonomies for Agentic AI and Human-AI Collaboration

**Version:** v0.3 (2026-05-11)  
**Status:** v0.3 — three source lines corrected via tri-source verification (Lutz 2025 venue confirmed; Ait 2025 author list and ASE 2025 acceptance corrected; Cheruvu 2026 single-author and handbook venue corrected). Amershi 2019 author-list typo (Quinn → Inkpen) fixed. Multi-agent taxonomies subsection added with AlphaEvolve as exemplar. Cross-refs to Draft D and Draft E wired in §4.

---

## Overview and Chapter Position

"Agentic AI" and "collaboration with AI" are used widely in both academic literature and the popular press — but precision varies enormously. This draft maps the recognised academic taxonomies that give the field structure: what is an agent, which types of autonomy are distinguished, and which models exist for collaboration between humans and AI systems?

The draft serves as a conceptual foundation for the chapter's other discussions and connects directly to `g-agentic-hi-collaboration.md` (which describes themes) and `d-open-source-organization.md` (which describes organisational patterns). While the g-draft asks *what is happening in hybrid intelligence*, this draft asks: *which concepts and categories does the field use to describe it?*

---

## Part 1: What is an agent? — Foundational definitions

**1.1 Russell & Norvig (2021) — the classical definition**  
An agent is something that *perceives* its environment via sensors and *acts* on it via actuators. The classical taxonomy from *Artificial Intelligence: A Modern Approach* lays out five agent types in increasing complexity:

| Type | Characteristic | Example |
|---|---|---|
| Simple reflex agent | Reacts to current percept | Thermostat |
| Model-based reflex agent | Maintains internal state model | Vacuum robot |
| Goal-based agent | Searches toward explicit goal | Route planner |
| Utility-based agent | Maximises utility function | Recommendation system |
| Learning agent | Improves over time via experience | RL agent |

LLM-based agents do not fit neatly into any single category — they are primarily goal-based and utility-based but with an emergent layer of generalisation that overruns the boundaries of the classical types.

**1.2 The cognitive-architecture model**  
A more recent consensus framework (e.g. Wang et al. 2023; Xi et al. 2023) describes LLM agents along four dimensions:
- **Perception** — what the agent can receive (text, images, structured data, code)
- **Memory** — short-term (context), long-term (external database/RAG), episodic (action history)
- **Planning** — decomposition of goals into subtasks; ReAct, Tree of Thoughts, RAP
- **Action** — what the agent can do (search, code execution, API calls, file handling)

This is currently the dominant frame in the survey literature and provides a useful analytical tool for the chapter.

---

## Part 2: Taxonomies of autonomy

**2.1 Parasuraman, Sheridan & Wickens (2000) — the 10-level model**  
The most cited autonomy taxonomy in the human-machine literature lays out ten levels from full human control to full machine autonomy:

1. The computer offers no assistance; the human does everything
2. The computer offers a complete set of alternatives
3. The computer narrows the selection to a subset
4. The computer suggests one alternative
5. The computer executes the suggestion if the human approves
6. The computer executes automatically but informs the human
7. The computer executes automatically and informs only if asked
8. The computer executes and informs only if it itself judges it necessary
9. The computer executes and never informs
10. The computer decides and acts fully autonomously

Implication for the chapter: most current production AI systems operate at level 4–6. Levels 7–9 are what is technically possible but governance-disputed (cf. `d-open-source-organization.md`). Level 10 is hypothetical.

**2.2 Shneiderman (2022) — Reliability-Goals Framework**  
Ben Shneiderman proposes a 2x2 matrix based on *degree of autonomy* × *understandability of goals*:

- **Supertools**: high human control, well-defined goals → word processors, calculators
- **Teammates**: shared control, negotiated goals → Copilot scenarios, co-creation
- **Autonomous agents**: low human control, self-defined goals → self-driving cars, autonomous trading systems
- **Oracles**: high autonomy, opaque goals → black-box prediction systems

Shneiderman's argument is normative: most critical systems should be designed as *Teammates*, not as *Autonomous agents*, because accountability requires meaningful human control.

**2.3 Human-in/on/out-of-the-loop**  
A simpler taxonomy that focuses on *when* the human is involved in the decision process:

- **Human-in-the-loop (HITL)**: the human approves every decision
- **Human-on-the-loop (HOTL)**: the system acts autonomously, the human monitors and can intervene
- **Human-out-of-the-loop (HOOTL)**: fully autonomous operation

This taxonomy is widespread in the military AI context (lethal autonomous weapons), regulatory frameworks (EU AI Act, NIST AI RMF) and accountability discussions. Its weakness is that it treats "the human" as a homogeneous unit and does not account for which *types* of decisions the human is in the loop for.

---

## Part 3: Taxonomies of human-AI collaboration

**3.1 Amershi et al. (2019) — 18 guidelines for Human-AI Interaction**  
The Microsoft Research team's *Guidelines for Human-AI Interaction* (CHI 2019) systematises 18 design principles across four interaction phases: *Initially* (G1–G2: make clear what the system can do and how well), *During interaction* (G3–G6: time services based on context, show contextually relevant information, match relevant social norms, mitigate social biases), *When wrong* (G7–G11: support efficient invocation, dismissal, correction, scope of services in doubt, communicate why), and *Over time* (G12–G18: remember recent interactions, learn from user behaviour, update and adapt cautiously, encourage granular feedback, convey consequences of user actions, provide global controls, notify users about changes). Not a taxonomy of agent types but an empirically grounded checklist that implies a typology of collaboration forms based on error handling and longitudinal adaptation.

**3.2 Lutz, Newlands & Jarrahi (2025) — Hybrid Intelligence Framework**  
Three dimensions for HI collaboration:
- *Cognitive layer*: who contributes what to problem-solving
- *Organisational layer*: division of labour and coordination
- *Institutional layer*: governance and accountability

The framework is particularly useful because it connects the individual level (cognition) with the organisational and societal level — matching the chapter's broader ambition.

**3.3 Wang et al. (2024) — Construction, Application, Evaluation**  
The survey (Wang et al. 2024, *Frontiers of Computer Science*; preprint arXiv:2308.11432) structures the field along three dimensions:
- *Construction*: architecture, memory, planning module, action space
- *Application*: social simulations, software engineering, scientific research, gaming
- *Evaluation*: benchmarks, human feedback, task completion rates

This is currently the standard frame for empirical agent research; the article has been cited over 2,700 times in less than two years (Semantic Scholar, 2026-05).

**3.4 Ait, Jouneaux, Cánovas Izquierdo & Cabot (2025) — DSL for Human-Agent Governance**  
The ASE 2025 paper proposes a domain-specific language (DSL) for specifying governance rules in projects where humans and AI agents collaborate, anchored empirically in a replication of an earlier OSS-governance study showing that explicit policies remain rare. The DSL expresses roles, decision-making procedures, and discrimination/representation rules in machine-readable form. Relevant because it attempts to make collaboration taxonomies *operational* — from description to specification — and is field-agnostic. Connects to `d-open-source-organization.md`'s four organisational patterns (the DSL is in effect a meta-language in which those patterns could be specified).

---

## Part 3.5: Multi-agent taxonomies

The taxonomies above describe a single agent — or at most an agent paired with a single human. The fast-emerging case is *populations* of agents. The literature is converging on at least three orthogonal axes:

- **Coordination topology** — supervisor/worker hierarchies, peer-to-peer broadcasts, market-based task allocation, or population-based search. Cross-ref forthcoming `ak-multi-agent-orchestration.md` for the orchestration patterns.
- **Goal alignment** — cooperative (shared utility), competitive (zero-sum), or mixed-motive. Reinforcement-learning multi-agent literature distinguishes these sharply; production LLM multi-agent systems rarely declare which they are.
- **Architectural family** — three patterns are now clearly visible:
  1. *Tool-use agents* (ReAct, Toolformer-style) — a single LLM calls tools in a loop.
  2. *Planner-executor agents* — one model decomposes goals, others execute. AutoGen, CrewAI, LangGraph operationalise this.
  3. *Evolutionary optimisation agents* — a population of candidate solutions, an LLM as mutation operator, and an automated fitness evaluator close the loop. AlphaEvolve (Google DeepMind, 2025) is the canonical example: Gemini Flash provides breadth (many mutations), Gemini Pro provides depth (high-quality mutations), and verifiable fitness scores drive selection. This family does not fit Russell & Norvig's classical typology, nor the cognitive-architecture model — the *individual* agent is small and stateless; the *population* exhibits agency.

The evolutionary family is taxonomically important because it shifts the unit of analysis from "the agent" to "the population", which Parasuraman et al.'s 10-level model cannot represent (it presupposes a single decision-making entity).

---

## Part 4: Critique of existing taxonomies

**4.1 Taxonomies are contemporary with the technology and become obsolete quickly**  
Russell & Norvig's classical typology presupposes sharp distinctions between perception and action that do not hold for multimodal LLM agents. Parasuraman et al.'s 10-level model presupposes a binary human-machine split, but in practice there are often chains of humans and AI systems involved.

**4.2 Autonomy is not a scale but a configuration space**  
"Autonomy" is often treated as one dimension, but is in practice multidimensional: an agent can be autonomous in the *planning module* but human-in-the-loop in *action execution*, autonomous in routine situations but HITL in edge cases. Taxonomies that collapse this to one dimension lose important distinguishing power.

**4.3 Taxonomies most often ignore the social layer**  
Most technical taxonomies describe the agent as an isolated system. But agents operate in social and organisational contexts: they interact with many humans, other agents, and institutions. Csikszentmihalyi's systems model (cf. `l-creativity-ai.md`) and Lutz et al.'s institutional layer are exceptions.

**4.4 Evaluation is immature**  
Wang et al. (2023) note that the evaluation infrastructure for agents is fragmented and task-specific. There is no consensus on what constitutes a "good" agent in a broad sense — what is evaluated depends on who evaluates and for what purposes.

**4.5 Taxonomies elide the failure modes they enable**  
HOOTL design at Parasuraman level 9–10 is not merely a governance choice — it is also a *vulnerability surface*. Where the human is fully removed from the action loop, prompt-injection and tool-misuse attacks have no in-band check (see `e-llm-structural-vulnerabilities.md`). The Parasuraman levels are silent on this: an "automation level" that is rated identically on the 1–10 scale may have radically different security postures depending on how its action space is constrained. Conversely, the four organisational patterns surveyed in `d-open-source-organization.md` can be read as one operationalisation of the Parasuraman scale at the organisation rather than agent level — i.e. where in an org chart the human-on-the-loop sits, and over which decision classes.

---

## Open Questions

1. **Are taxonomies converging?** There are currently many parallel taxonomies without a shared ontology. Are there signs that the field is moving toward consensus, or fragmenting further?

2. **Should taxonomies be normative or descriptive?** Shneiderman's framework is explicitly normative (we *should* design Teammates). Is this legitimate for an academic taxonomy?

3. **What happens to HITL models at scale?** Meaningful human control is resource-intensive. When agents operate in real time on thousands of parallel tasks, HITL becomes illusory. What replaces it?

4. **Is "collaboration" the right concept?** Collaboration normally presupposes shared goals and mutual commitment. Can a system without intentionality "collaborate" — or are "coordination" or "orchestration" more precise concepts?

5. **Taxonomies and regulation**: the EU AI Act categorises AI systems by risk, not by autonomy level or collaboration form. Is this a weakness in the regulatory frame?

---

## Sources (Anchors)

- Russell, S., & Norvig, P. (2021). *Artificial Intelligence: A Modern Approach* (4th ed.). Pearson. — Classical agent definition and typology. **[BOOK]**
- Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A*, 30(3), 286–297. https://doi.org/10.1109/3468.844354 — The 10-level model (built on the Sheridan & Verplank 1978 scale). **[J] [iCit: 343]**
- Shneiderman, B. (2022). *Human-Centered AI*. Oxford University Press. — Reliability-Goals (control × automation) two-dimensional framework. **[BOOK]**
- Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2024). A survey on large language model based autonomous agents. *Frontiers of Computer Science*, 18(6), 186345. https://doi.org/10.1007/s11704-024-40231-1 — Construction/application/evaluation framework. PDF in Kilder as `Wang2023_SurveyAutonomousAgents_arXiv2308.11432.pdf` (preprint version). **[J] [iCit: 122]**
- Xi, Z., Chen, W., Guo, X., He, W., Ding, Y., Hong, B., Zhang, M., Wang, J., Jin, S., Zhou, E., Zheng, R., Fan, X., Wang, X., Xiong, L., Zhou, Y., Wang, W., Jiang, C., Zou, Y., Liu, X., … Gui, T. (2023). The rise and potential of large language model based agents: A survey. arXiv:2309.07864. — Brain/perception/action framework. PDF in Kilder. **[P] [iCit: 67]**
- Lutz, C., Newlands, G., & Jarrahi, M. H. (2025). Hybrid intelligence. In W. Xu (Ed.), *Handbook of Human-Centered Artificial Intelligence*. Springer Nature Singapore. https://doi.org/10.1007/978-981-97-8440-0_87-1 — Three-layer framework: cognitive, organisational, institutional. PDF in Kilder. **[BOOK] — Springer handbook chapter, peer-edited; [OA cit: 0] (newly published; CrossRef retraction check 2026-05-11: clean)**
- Amershi, S., Weld, D., Vorvoreanu, M., Fourney, A., Nushi, B., Collisson, P., Suh, J., Iqbal, S., Bennett, P. N., Inkpen, K., Teevan, J., Kikin-Gil, R., & Horvitz, E. (2019). Guidelines for Human-AI Interaction. *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems* (pp. 1–13). https://doi.org/10.1145/3290605.3300233 — 18 design guidelines across four interaction phases (Initially, During, When Wrong, Over Time). PDF in Kilder as `Amershi2019_GuidelinesHumanAI_CHI2019.pdf`. **[C] [iCit: 155] [OA cit: 1758] [Verified non-retracted via CrossRef 2026-05-11; author #10 corrected from "Quinn, K." to "Inkpen, K." per CrossRef record]**
- Ait, A., Jouneaux, G., Cánovas Izquierdo, J. L., & Cabot, J. (2025). Towards automated governance: A DSL for human-agent collaboration in software projects. In *Proceedings of the 2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*. https://doi.org/10.1109/ASE63991.2025.00337 (Preprint: arXiv:2510.14465). PDF in Kilder as `Ait2025_DSL_HumanAgentGovernance_ASE2025.pdf`. **[C] [OA cit: 0] — ASE 2025 acceptance confirmed via CrossRef 2026-05-11; prior author list "Ait, Cabot & Burgueño" was incorrect.**
- Cheruvu, R. (2026). Human-in/on-the-loop design for human controllability. In W. Xu (Ed.), *Handbook of Human-Centered Artificial Intelligence*. Springer Nature Singapore. https://doi.org/10.1007/978-981-97-8440-0_75-1 — HITL/HOTL paradigms, applied sector cases (healthcare, autonomous vehicles, financial services). PDF in Kilder as `Cheruvu 2025 - Human-in-on-the-Loop Design for Human Controllability.pdf`. **[BOOK] — Springer handbook chapter, single author (Intel Corporation); [OA cit: 0]; prior "et al." attribution corrected per CrossRef 2026-05-11.**

---

## What Still Needs Work

- Add Russell & Norvig, Shneiderman, Parasuraman to `_linked_sources.md`
- Add a primary source for AlphaEvolve (DeepMind blog post / forthcoming paper) and download to `Kilder/` — currently relies on Zotero entry WXTMHIJZ only
- Expand Part 4 (critique) with one fully worked empirical case of taxonomy breakdown (LAWS debate is the obvious candidate — autonomous weapons span Parasuraman 6 through 10 depending on rules of engagement)
- Cross-link forthcoming Draft AK (multi-agent orchestration) once it exists; the Part 3.5 stub should expand to a full sub-taxonomy
- Verify Lutz, Newlands & Jarrahi (2025) chapter cited count over time and re-tag if peer-review status of the handbook is documented elsewhere (currently `[BOOK]`)
