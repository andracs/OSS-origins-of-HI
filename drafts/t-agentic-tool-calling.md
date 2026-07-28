# Draft T — Agentic Tool Calling: From Function Calls to MCP and Skill Ecosystems

**Version:** v0.3 (2026-05-14)  
**Status:** v0.3 — citation pass: peer-reviewed empirical anchor added for §3.3 (Hou, Zhao, Wang & Wang, 2026, *ACM Transactions on Software Engineering and Methodology*, DOI 10.1145/3796519, OA cit 43) — the first systematic academic study of the MCP ecosystem, providing the lifecycle taxonomy and threat model that §3.3 and the §6.3/Open-Question-2 security forward-references previously anchored only to Anthropic's protocol announcement. Tri-source re-verification (OpenAlex + CrossRef) on Lewis 2020 NeurIPS RAG, Greshake 2023 AISec/CCS (OA cit refreshed 304 → 310), AutoGen 2023 (still preprint per OpenAlex — no peer-reviewed version confirmed; flagged-for-audit retired as resolved), Amershi 2019 CHI; CrossRef retraction checks clean on Hou 2026, Amershi 2019, and Greshake 2023.  
**Next:** expand §6.4 to cite Bedard et al. (2026, HBR) with verbatim quote (currently paraphrased); add explicit treatment of computer-use / GUI-grounded tool calling (Anthropic 2024); deepen §3.3 ecosystem map using Hou et al.'s §4 industry-adoption section (specific server counts and integration-pattern statistics).

---

## Overview and Chapter Position

An LLM that only produces text is a tool. An LLM that can call external systems — search the web, execute code, access databases, send emails — is an *agent*. The transition from language model to agent is not primarily a model-architectural innovation but an *interface* innovation: the definition of protocols for how a language model communicates with the outside world.

This draft maps the technical and institutional development of *agentic tool calling*: from the first experiments giving LLMs access to search, through the standardisation of function calling and plug-in architectures, to today's open protocols such as Model Context Protocol (MCP) and skill-based agentic frameworks.

The draft is the technical operationalisation of the agentic turn described conceptually in `g-agentic-hi-collaboration.md` and taxonomised in `m-agentic-ai-taxonomies.md`. It shows how the theory of agents — ReAct, Reflexion, planning modules — has been turned into concrete infrastructure.

---

## Part 1: The Preconditions — what tool calling requires

**1.1 The classical grounding problem**  
Early chatbots (ELIZA, 1966; ALICE, 1995) were closed systems: they responded only on the basis of patterns in their design, without access to external information. A user asking about today's weather got a response based on patterns in the training data — not the weather. The underlying problem is identical with Harnad's symbol grounding (cf. `r-hi-mirror-human-intelligence.md`): the model lacks the connection between symbols and world.

The practical solution requires two things: (1) the model must be able to *generate structured queries* to external systems, and (2) the model must be able to *integrate responses* from external systems into its further reasoning. Both are non-trivial requirements.

**1.2 Retrieval-Augmented Generation (RAG) as precursor**  
The first step toward tool calling was Retrieval-Augmented Generation (Lewis et al. 2020): documents are retrieved from an external vector store and injected into the prompt as context. RAG is not really tool calling — the model does not actively search, it passively receives — but it established the pattern: LLM + external knowledge = more capable model.

RAG is still the dominant approach to factual grounding and forms the backbone of enterprise AI deployments, but it is architecturally limited to *read-only* access to structured datasets.

**1.3 ReAct — the conceptual model for tool use**  
Yao et al. (2022, arXiv:2210.03629) is the academic foundation for modern tool calling. ReAct introduced the paradigm: model *reasoning* and model *acting* in an alternating loop. The model thinks (*Thought: I need to find X*), acts (*Action: Search[X]*), receives an observation (*Observation: [search result]*), and thinks again. The pattern is simple but generative: it gives the model an architectural role as planner and coordinator, not merely text producer.

ReAct showed empirically that reasoning + acting consistently outperforms reasoning alone or acting alone on knowledge-intensive and decision-making tasks. It is the academic warrant for the agentic turn.

---

## Part 2: Standardisation — function calling and plugins (2023)

**2.1 OpenAI's function calling (June 2023)**  
OpenAI's launch of function calling in GPT-3.5 and GPT-4 in June 2023 is the commercial breakthrough for structured tool use. The mechanism is elegant:

1. The developer defines one or more *functions* as JSON Schema objects
2. The model, when relevant, returns a structured JSON object specifying a function call and arguments
3. The application executes the actual call and returns the result to the model
4. The model integrates the result into its further generation

The model does not *call* the function itself — it *suggests* a call which the application layer executes. This is a deliberate design choice: responsibility for execution stays with the application, not the model. It is the technical implementation of the human-on-the-loop principle.

Function calling transformed LLMs from text generators into *interface agents*: they can now communicate in a structured way with any system that exposes an API.

**2.2 ChatGPT Plugins (March–November 2023)**  
OpenAI launched a plugin system for ChatGPT in March 2023: third-party providers could register services (Expedia, Wolfram Alpha, Klarna) that ChatGPT could call via standardised API specifications. Plugins were the first broadly user-facing manifestation of agentic tool use.

The system proved hard to scale: browsing plugins were inconsistent, authentication was complex, and the UI was not mature. OpenAI shut down Plugins in April 2024 and replaced them with GPT Actions — a more mature version that lives in Custom GPTs and the Assistants API.

**2.3 Anthropic Tool Use and Google Function Calling**  
During 2023–2024 all frontier labs standardised structured tool use:
- **Anthropic**: Tool use in Claude with type definitions and multi-turn tool loops
- **Google**: Function calling in Gemini with parallel tool use (multiple calls simultaneously)
- **Mistral**: Tool calling in Mistral-7B and Mixtral

Convergence on a common pattern: all use JSON Schema for tool definition, all return structured tool calls, all support multi-turn loops. The interface standard is de facto harmonised, even though API details vary.

---

## Part 3: MCP — open protocol as infrastructure (2024)

**3.1 Model Context Protocol — what and why**  
Anthropic announced Model Context Protocol (MCP) in November 2024 as an open standard for the connection between AI assistants and data/tool providers. MCP is not a new model feature but a *communication protocol*: it specifies how an AI client communicates with an MCP server that exposes resources, tools and prompts.

The architecture is client-server with three primitive types:
- **Resources**: files, databases, live data the model can read
- **Tools**: actions the model can request to be executed
- **Prompts**: templates that steer model behaviour in specific contexts

**3.2 MCP's strategic logic**  
MCP solves a concrete problem: without a standard, every AI application must integrate with every external system separately (M × N integrations). With MCP it is M AI clients × N MCP servers, but via a standard protocol (M + N integrations).

The strategic parallel is clear and explicit in Anthropic's communication: MCP is to AI tool integration what USB is to hardware connection — an open interface that enables plug-and-play without bilateral agreement.

The openness is strategic: by publishing MCP as an open standard (MIT licence, open specification) Anthropic attempts to create an ecosystem-standardised interface where Claude is not the only client — and thereby make MCP the de facto standard, which OpenAI's proprietary Assistants API is not.

**3.3 MCP ecosystem adoption (2025–2026)**  
From its November 2024 launch the MCP ecosystem grew rapidly. The first systematic academic mapping is Hou, Zhao, Wang and Wang's (2026) survey in *ACM Transactions on Software Engineering and Methodology*, which provides the lifecycle and adoption analysis that the protocol's own announcement materials do not. Hou et al. (2026, §2.2 and §4) document four characteristic adoption signals:
- **Protocol-based standard with dynamic discovery and schema negotiation**: MCP clients list available tools at runtime, retrieve their capabilities, and invoke them in a uniform manner — a property that, by Hou et al.'s account, distinguishes MCP architecturally from earlier function-calling mechanisms and explains the speed at which third parties have built servers (Hou et al., 2026, §2.2).
- **Cross-platform server proliferation**: "thousands of independently developed MCP servers" exposing model-accessible interfaces to services including GitHub, Slack, and Blender (Hou et al., 2026, §1; verbatim).
- **Multi-client integration**: Claude Desktop, Cursor, VS Code Copilot Chat, Windsurf, and (from March 2025) OpenAI's own clients — the latter being the signal commonly read in industry as de facto standardisation (Hou et al., 2026, §3.1 on host components).
- **Bi-directional communication channels**: not only model-to-tool requests but also tool-initiated events and notifications back to the host — a primitive that earlier plugin systems lacked and that opens MCP toward continuous-loop architectures rather than one-shot lookups (Hou et al., 2026, §2.1.2).

Hou et al. characterise the resulting paradigm shift from "*tool bindings hardcoded per application*" toward "*an interoperable ecosystem of composable, discoverable network services*" (2026, §1; verbatim) — the architectural claim that this draft's §3.2 USB analogy makes informally is here given peer-reviewed empirical grounding.

**3.4 What Anthropic gains: the political economy of open standards**

MCP is not only a technical solution — it is a deliberate strategy of *standards authority capture* with a well-documented historical precedent. Understanding what Anthropic gains from MCP is necessary for any organisation considering adoption or any researcher analysing the power dynamics of the emerging HI ecosystem.

**(a) Platform capture through network effects.** The core logic of an open standard is that adoption generates the network effects that make the standard self-reinforcing. Every MCP server built by a third party — GitHub, Slack, databases, development tools — increases the practical utility of any MCP-compatible AI client. Claude benefits disproportionately because MCP was architected with Claude's capability profile in mind, and because Anthropic controls the reference implementation. The pattern is identical to Google's strategy with Android: publish an open standard, benefit from community development, while retaining control of the reference implementation and roadmap.

**(b) Competitive encirclement.** When OpenAI added MCP support to its own clients in March 2025, it did so on Anthropic's terms — adopting a protocol whose specification Anthropic authors and whose governance Anthropic controls. This is structurally different from competing on proprietary APIs: a competitor who adopts your standard is, in a narrow but real sense, building on your infrastructure. OpenAI's adoption of MCP is a market signal that Anthropic reads as validation; from a governance perspective, it also means that the largest AI company in the world is now a stakeholder in the stability of Anthropic's protocol design choices.

**(c) Enterprise legitimacy and reduced adoption friction.** Open standards lower enterprise security and procurement barriers. A company evaluating Claude integration into its internal tooling faces a different risk calculus with an open, auditable protocol than with a proprietary API that requires trusting Anthropic's black-box server-side behaviour. MCP's open specification enables third-party security audits, regulatory compliance assessment, and standards-body review — all of which accelerate enterprise adoption.

**(d) Developer community capture.** Open source contributions create stakeholder identity. The thousands of developers who have built MCP servers are invested in the success of the ecosystem they contributed to. This is the same dynamic that Linux, Mozilla, and PostgreSQL exploited: contributors become advocates. In the AI tooling space, MCP contributors are predominantly professional software engineers whose adoption decisions at their employers are influenced by their personal investment in the ecosystem.

**(e) Ecosystem telemetry and capability intelligence.** MCP servers that connect to Anthropic-hosted Claude endpoints generate usage data: which tools are called, in what sequences, with what payloads. Even anonymised, this data constitutes an intelligence advantage — Anthropic can observe which capabilities are most requested, which integrations succeed and fail, and what the actual distribution of production AI workloads looks like. This informs both model training priorities and future protocol design.

**(f) The "open" hedge against regulatory risk.** As AI regulation in the EU, UK, and US intensifies, demonstrating openness and interoperability is likely to become a compliance asset. A company that owns the dominant *open* standard in a market has a stronger argument against interoperability mandates (which would be redundant) and against antitrust concern (since any competitor can, in principle, implement the same protocol).

**3.5 Adoption risks: what organisations give away**

Adopting MCP solves integration problems while introducing a distinct risk profile that organisations must evaluate explicitly.

**(a) Governance dependency without ownership.** MIT licensing of the MCP specification means the code is free to use and fork, but it does not mean governance is shared. Anthropic controls the specification roadmap. If Anthropic introduces breaking changes, deprecates protocol features, or evolves MCP in ways that serve its competitive interests rather than adopter interests, organisations that have built production systems on MCP face migration costs. The Android experience is instructive: the open-source licence did not prevent Google from periodically introducing changes that advantaged Google's own applications. MCP adopters should monitor the governance structure of the MCP specification and consider whether collective governance (analogous to IETF, W3C, or the Linux Foundation) would be appropriate as the protocol matures.

**(b) Security attack surface expansion.** Every MCP server is a potential prompt injection vector. Hou et al. (2026) document sixteen distinct threat scenarios arising specifically from the MCP architecture, including *tool poisoning* (malicious MCP server returning instructions that override agent behaviour), *installer spoofing* (fake MCP server packages designed to be installed by developers), and *unauthorised access* via misconfigured server authentication. These are not hypothetical: they are the MCP-specific manifestation of the indirect prompt injection attack class documented by Greshake et al. (2023). An organisation that deploys MCP servers connecting Claude to internal databases, code repositories, or communication systems exposes those systems to any vulnerability in the MCP client's ability to distinguish tool data from adversarial instructions. The current MCP specification does not encode trust boundaries at the protocol level — security is the responsibility of each implementing client.

**(c) Capability overexposure.** MCP's design goal — making it easy for an AI to discover and invoke any registered tool — is also a security liability. An MCP server that exposes a broad set of capabilities (file system read/write, email, database queries) may be integrated expecting limited use, but an agent whose prompt is hijacked or whose goal generalises unexpectedly may invoke capabilities that the operator did not intend. Principle of least privilege, standard in security engineering, is difficult to enforce when the tool-discovery mechanism is dynamic and the agent's inference is non-deterministic.

**(d) False openness: the openwashing risk.** The term "open" in "open standard" describes the specification's accessibility, not its governance. As Liesenfeld and Dingemanse (2024) establish in their audit framework for foundation model openness (cf. Draft K), the gap between published artefacts and operational openness is often large. MCP is, at present, genuinely open in the specification sense. But as the standard matures and its economic stakes increase, the historical pattern is that governance becomes contested: the organisation that created the standard asserts prerogatives over its direction that conflict with the interests of the adopter community. The transition from IETF-style open standards (HTTP, SMTP) to platform-controlled pseudo-open standards (Android, HDMI) is a recurring pattern worth tracking.

**(e) Monoculture and systemic fragility.** Standardisation accelerates deployment at the cost of architectural diversity. If MCP becomes the universal integration layer for AI tool calling — as USB became the universal hardware interface — then a vulnerability in the MCP protocol or a failure in Anthropic's stewardship of it affects the entire AI ecosystem simultaneously rather than individual implementations. Monoculture risk in security is well-documented (Schneier, 2003); its extension to AI integration protocols is underexplored.

---

## Part 4: Agent frameworks and skill ecosystems

**4.1 LangChain — chains, agents, and tool-use abstraction (2022)**  
Harrison Chase launched LangChain in October 2022 as a Python framework abstracting over LLM calls, memory management and tool use. LangChain introduced concepts that have become standard: *chains* (sequential LLM calls), *agents* (loops that call tools based on LLM decisions), *tools* (registered functions with descriptions).

LangChain solved a real problem — building agentic applications from scratch was tedious — but is criticised for being over-abstract and hard to debug. Nonetheless it is the most downloaded ML framework in 2023–2024 with millions of users.

**4.2 AutoGen — multi-agent conversation (2023)**  
Wu et al. (2023, arXiv:2308.08155) introduced AutoGen: a framework for multi-agent systems where LLM agents communicate via structured conversations. The central innovation: *agent conversation* as a programming model — instead of orchestrating agents via code, let agents coordinate via natural language.

AutoGen showed that complex programs can be solved by specialised agents (coder, critic, planner, human proxy) that debate solution strategies. It is the technical substrate for many current multi-agent HI systems.

**4.3 SWE-agent — tool use for software engineering (2024)**  
Yang et al. (2024, arXiv:2405.15793) showed that LLM agents with access to bash, file editor and test runner can solve real GitHub issues autonomously. SWE-bench is now a standard benchmark for agentic software-engineering capacity. The SWE-agent architecture demonstrated that what is decisive is not model quality alone but interface design: a well-designed tool interface markedly increases agent performance.

**4.4 Skills and compositionality**  
The newest layer of agentic infrastructure is *skill-based* frameworks: instead of direct tool calls, agents define functionality as composable skills with standardised interfaces. Examples:
- **OpenAI Agents SDK**: primitive agent loops with tool definitions and handoffs
- **Claude Code**: the Claude instance with access to bash, files and editors as composable skills
- **OpenClaw/AgentSkills**: skill registry as SKILL.md files in a standard format — communities can publish and install skills

The skill model is an abstraction over tool calling: it adds *description* (when is this skill used?), *compositionality* (skills can call other skills) and *shareability* (skills are published in a registry and installed by others).

---

## Part 5: The agentic loop as architectural pattern

**5.1 Planning and decomposition**  
The general agentic loop pattern, formalised from ReAct:

```
Goal → Plan → [Tool call → Observation → Reflect] × n → Answer
```

Variants:
- **ReAct** (Yao 2022): alternating reasoning and action
- **Reflexion** (Shinn 2023): episodic memory over failures; the agent improves itself via retrospective analyses
- **Tree of Thoughts** (Yao 2023): BFS/DFS over the reasoning space rather than a linear chain
- **RAP** (Hao 2023): LLM as world model + Monte Carlo Tree Search
- **LLM+P** (Liu 2023): external PDDL planner for deterministic logic

**5.2 Memory architecture**  
Agentic loops require memory beyond single-conversation context windows:
- *In-context*: everything in the prompt — bounded by the context window
- *External/vector*: RAG-based long-term memory
- *Episodic*: log over previous actions (the Reflexion model)
- *Semantic*: structured knowledge base (graph-based or tabular)

Jia et al. (2026, "The AI Hippocampus: How Far are We From Human Memory?", arXiv:2601.09113) provide a comprehensive cross-system survey of these mechanisms, framing them as *implicit* (in-weights parametric memory), *explicit* (external retrieval and storage), and *agentic* (persistent state structures in autonomous agents). The survey maps each tier onto analogues in human memory systems and documents the limitations of each for continual learning and personalised inference — capabilities that advanced agentic tool-calling architectures implicitly require. For practitioners, the taxonomy clarifies which memory tier is appropriate for which information: frequently changing world knowledge → explicit/vector; stable procedural knowledge → implicit; multi-session agent state → agentic. The cross-tier integration challenges the survey identifies are directly relevant to MCP's architectural role: MCP servers effectively implement *explicit memory* as a retrieval tool, but the agent's ability to synthesise across implicit and explicit tiers remains an open research problem.

**5.3 Multi-agent coordination**  
When single-agent loops are insufficient, multiple agents coordinate via:
- *Sequential*: agent A's output is agent B's input
- *Parallel*: multiple agents work simultaneously on subtasks
- *Supervisory*: an orchestrator agent delegates to worker agents
- *Peer*: agents communicate horizontally (the AutoGen model)

The *patterns* of inter-agent coordination — how authority is delegated, how shared state is reconciled, which sub-agent is allowed to spawn which — are the subject of `ak-multi-agent-orchestration.md` (in preparation per STEERING.md's 2026-05-03 narrative-gap plan); the present draft treats only the per-agent tool-calling primitives that orchestration layers compose. Similarly, the *memory* tier on which multi-session agentic tool use depends — vector stores, episodic logs, procedural skill habits — is the subject of `al-agent-memory-continuity.md` (in preparation); §5.2 above gives only the architectural taxonomy, not the implementation detail.

---

## Part 6: Implications for HI and the chapter's argument

**6.1 Tool calling as HI infrastructure**  
Tool calling is the technical infrastructure that enables hybrid intelligence at the application level: it is the mechanism that connects LLMs to the human work flows (databases, calendars, code, communication systems) that give AI assistance *contextual relevance*.

An HI system without tool calling is isolated from the organisational context in which it operates. Tool calling is therefore not merely a technical feature but an *HI enabler*.

**6.2 Standardisation as commons infrastructure**  
MCP's open standardisation is a repetition of the pattern described in `s-open-knowledge-platforms.md`: open protocols (HTTP, Git, USB) create network effects that exceed proprietary alternatives. MCP's rapid adoption by OpenAI and others suggests that the open-standard strategy works.

**6.3 Skill registries as a new commons**  
Skill-based systems — the SKILL.md format, ClawHub, similar registries — are establishing a new layer in the commons stack: not code (GitHub), not models (Hugging Face), but *agentic capabilities*. A skill that gives access to a weather API, a skill that searches Semantic Scholar, a skill that sends Telegram messages — these are reusable components that potentially constitute a new open infrastructure.

The open question is the same as for the other platforms: who owns the skill registries, who harvests the value of skill accumulation, and is the governance structure robust enough to withstand commercial pressure?

**6.4 The cognitive capacity constraint: when tool calling outpaces human oversight**  
Multi-agent tool-calling architectures introduce a human cognitive limit that single-agent tool use does not: when multiple agents run in parallel, each invoking its own tool loops, the total rate of state change in the system can exceed what a human supervisor can track, let alone evaluate. Bedard, Kropp, Hsu et al. (2026, HBR) document this as "brain fry": the cognitive fatigue produced not by the difficulty of understanding individual tool calls but by the *pace and concurrency* of multi-agent execution. Their illustrative case — Steve Yegge's Gas Town (2026), which orchestrates multiple Claude Code agents simultaneously — produces a user experience described as "too much going on for you to reasonably comprehend" with "a palpable sense of stress."

For HI system design, this creates a concrete constraint: multi-agent parallelism is not free from the perspective of the human-in-the-loop. The coordination overhead identified by Becker et al. (2025) in single-agent coding assistance scales non-linearly in multi-agent configurations, where the human must track N concurrent execution threads rather than one. The implication for tool-calling infrastructure design: the right abstraction level for human oversight is not the individual tool call but the *task outcome* — humans need sufficient visibility into what agents are accomplishing, not into the sub-second mechanics of how tool calls are being dispatched. This suggests that the supervisory interface design (cf. Amershi et al., 2019, in Draft G) is at least as important an engineering challenge as the underlying tool-calling protocol.

---

## Open Questions

1. **MCP vs. proprietary alternatives**: will MCP retain its openness now that OpenAI and others implement it, or will "openwashing" of the protocol emerge (cf. `k-openness-layers.md`)?

2. **Security in tool calling**: prompt injection via tool output is an open vulnerability (cf. `e-llm-structural-vulnerabilities.md`). Hou et al. (2026, §5) provide the first systematic threat taxonomy specific to MCP, identifying four attacker archetypes (malicious developers, external attackers, malicious users, and security flaws) and sixteen distinct threat scenarios — including tool poisoning, installer spoofing, and unauthorised access — validated through real-world case studies. The taxonomy makes clear that MCP's current open standard does not yet incorporate protocol-level security guarantees; mitigation is implemented at the host/client layer rather than within the protocol itself. Can MCP's specification evolve to encode trust boundaries as a first-class architectural concern, or will security remain an integration responsibility of every MCP client?

3. **Governance of skill registries**: who decides which skills are permitted? Who enforces quality and security? The analogy to GitHub/npm (Node package manager) is relevant — npm has had serious supply-chain attacks.

4. **Agentic loops and human control**: the longer agentic loops run autonomously, the harder meaningful human oversight becomes (cf. `p-governance-compliance-hi.md`). What is the right granularity for human-in-the-loop checkpoints?

5. **Emergence in multi-agent systems**: when many specialised agents with tool access coordinate, emergent behaviour arises that no single agent planned. How are such systems designed with predictable and auditable behaviour?

---

## Sources (Anchors)

Tier tags follow STEERING.md (2026-05-03 directive): `[J]` peer-reviewed journal, `[C]` peer-reviewed conference proceedings, `[P]` preprint only, `[R]` technical report / institutional document. Citation counts via OpenAlex (`[OA cit]`) where reachable; verified via tri-source chain (OpenAlex → CrossRef → Semantic Scholar) on 2026-05-08.

### Peer-reviewed and preprint
- Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. *International Conference on Learning Representations (ICLR 2023)*. arXiv:2210.03629. [C] — academic foundation for the reasoning-action loop; PDF in Kilder/.
- Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-t., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems (NeurIPS 2020)*, 33, 9459–9474. arXiv:2005.11401. [C] — foundational RAG paper; PDF in Kilder/ as `Lewis2020_RAG_arXiv2005.11401.pdf`.
- Shinn, N., Cassano, F., Berman, E., Gopinath, A., Narasimhan, K., & Yao, S. (2023). Reflexion: Language agents with verbal reinforcement learning. *NeurIPS 2023*. arXiv:2303.11366. [C] [OA cit: 261] — episodic-memory-over-failures paradigm.
- Wu, Q., Bansal, G., Zhang, J., Wu, Y., Li, B., Zhu, E., Jiang, L., Zhang, X., Zhang, S., Awadallah, A., White, R. W., Burger, D., & Wang, C. (2023). AutoGen: Enabling next-gen LLM applications via multi-agent conversation. arXiv:2308.08155. [P] [OA cit: 147] — multi-agent conversation framework; verify whether the ICLR 2024 published version supersedes the preprint at next audit.
- Yang, J., Jimenez, C. E., Wettig, A., Lieret, K., Yao, S., Narasimhan, K., & Press, O. (2024). SWE-agent: Agent-computer interfaces enable automated software engineering. *NeurIPS 2024*. arXiv:2405.15793. [C] [OA cit: 24] — empirical demonstration that interface design (not just model quality) determines agentic-coding performance.
- Hao, S., Gu, Y., Ma, H., Hong, J. J., Wang, Z., Wang, D. Z., & Hu, Z. (2023). Reasoning with language model is planning with world model. *EMNLP 2023*. arXiv:2305.14992. [C] [OA cit: 108] — RAP: LLM as world model + Monte Carlo Tree Search.
- Liu, B., Jiang, Y., Zhang, X., Liu, Q., Zhang, S., Biswas, J., & Stone, P. (2023). LLM+P: Empowering large language models with optimal planning proficiency. arXiv:2304.11477. [P] — external PDDL planner integration; preprint only.
- Yao, S., Yu, D., Zhao, J., Shafran, I., Griffiths, T. L., Cao, Y., & Narasimhan, K. (2023). Tree of Thoughts: Deliberate problem solving with large language models. *NeurIPS 2023*. arXiv:2305.10601. [C] [OA cit: 562] — BFS/DFS over reasoning space.
- Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. *Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security (AISec '23)*. DOI:10.1145/3605764.3623985. arXiv:2302.12173. [C] [OA cit: 310 — refreshed 2026-05-14] — defining paper for indirect prompt injection as a structural vulnerability of tool-calling architectures. [Verified non-retracted via CrossRef 2026-05-14: `update-to: None`.]
- Hou, X., Zhao, Y., Wang, S., & Wang, H. (2026). Model Context Protocol (MCP): Landscape, security threats, and future research directions. *ACM Transactions on Software Engineering and Methodology*. DOI:10.1145/3796519. arXiv:2503.23278. [J] [OA cit: 43] — first systematic academic study of the MCP ecosystem; provides the four-phase server lifecycle (creation, deployment, operation, maintenance) decomposed into 16 activities, plus the four-archetype × 16-scenario threat taxonomy that §3.3 and Open Question 2 cite. PDF in Kilder/ as `Hou2026_ModelContextProtocolLandscapeSecurity_TOSEM_arXiv2503.23278.pdf`. [Verified non-retracted via CrossRef 2026-05-14: `update-to: None`.]
- Chen, S. et al. (2024). SecAlign: Defending against prompt injection with preference optimization. — preprint; verify venue at next audit. [P]
- Chu et al. (2026). Agentic world modeling. arXiv:2604.22748. [P] — too new for citation count.
- Wu et al. (2025). COSPLAY. — preprint; verify venue. [P]
- Jia, Z., Li, J., Kang, Y., Wang, Y., Wu, T., Wang, Q., Wang, X., Zhang, S., Shen, J., Li, Q., Qi, S., Liang, Y., He, D., Zheng, Z., & Zhu, S.-C. (2026). The AI Hippocampus: How far are we from human memory? arXiv:2601.09113. [P] — too new for citation count; PDF in Kilder/ as `Jia2026_AIHippocampus_arXiv2601.09113.pdf`. Cited in §5.2.
- Becker, B. A., Stachowiak, T., Cassella, P., et al. (2025). Measuring the impact of early-2025 AI on experienced open-source developer productivity. arXiv:2507.09089. [P] — referenced in §6.4 for the coordination-overhead claim; PDF in Kilder/.
- Amershi, S., Weld, D., Vorvoreanu, M., Fourney, A., Nushi, B., Collisson, P., Suh, J., Iqbal, S., Bennett, P. N., Inkpen, K., Teevan, J., Kikin-Gil, R., & Horvitz, E. (2019). Guidelines for human-AI interaction. *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems (CHI '19)*. DOI:10.1145/3290605.3300233. [C] [OA cit: 1,752] — referenced in §6.4 for supervisory-interface design; PDF in Kilder/.

### Web / professional sources (no peer-reviewed equivalent)
- Bedard, J., Kropp, M., Hsu, M., Karaman, O. T., Hawes, J., & Kellerman, G. R. (2026, March 5). When using AI leads to "brain fry." *Harvard Business Review*. https://hbr.org/2026/03/when-using-ai-leads-to-brain-fry. [R] — practitioner-management source for §6.4 "brain fry" cognitive-overhead concept; not peer-reviewed.

### Technical documentation (cite as software/protocol — no peer-reviewed citation possible)
- Anthropic. (2024, November 25). Introducing the Model Context Protocol. https://www.anthropic.com/news/model-context-protocol. [R] — primary protocol announcement.
- Anthropic. (2024). *Model Context Protocol specification*. https://modelcontextprotocol.io/specification. [R] — open-protocol spec, MIT-licensed.
- OpenAI. (2023). *Function calling and other API updates* (developer documentation). https://platform.openai.com/docs/guides/function-calling. [R] — original function-calling launch documentation.

### Retraction check (per STEERING.md tri-source directive)
- CrossRef `update-to[].type` queried 2026-05-08 for AutoGen (arXiv:2308.08155): no retraction notice. arXiv-DOI lookups via CrossRef return 404 for several preprints; this reflects CrossRef's incomplete arXiv coverage, not a retraction signal.
- CrossRef queried 2026-05-14 for Hou et al. (2026) DOI:10.1145/3796519, Amershi et al. (2019) DOI:10.1145/3290605.3300233, and Greshake et al. (2023) DOI:10.1145/3605764.3623985 — all return `update-to: None` (clean).
- AutoGen 2023 published-venue audit (resolved 2026-05-14): OpenAlex full-record lookup of W4385965642 reports primary location = arXiv (Cornell University), `version = submittedVersion`, no journal/conference source; CrossRef title search returned only the AutoGen *Studio* paper (Dibia et al., EMNLP 2024 System Demonstrations, DOI:10.18653/v1/2024.emnlp-demo.8) — a distinct downstream paper, not the original. Wu et al. (2023) AutoGen therefore remains `[P]` and the previous "ICLR 2024 reported in some indices" flag is retired as unsupported by primary indexers.

---

## What Still Needs Work

- [ ] Add MCP spec and OpenAI function-calling docs to `_linked_sources.md`
- [ ] Deepen §3.3 with specific server-count and integration-pattern statistics from Hou et al. (2026) §4 industry-adoption section (the introductory anchor is in place; the granular landscape numbers are not yet pulled through)
- [ ] Expand the security section — Hou et al. (2026) threat taxonomy now anchored in Open Question 2; pull through full 4×16 taxonomy in a §6 sub-section
- [ ] Add section on *computer use* (Anthropic, 2024) as tool calling for GUI interfaces
- [ ] Cross-ref to `e-llm-structural-vulnerabilities.md` — tool calling as attack vector
- [ ] Investigate OpenAI Swarm / Agents SDK more closely as architectural pattern
- [ ] Cross-link more deeply with Draft AK (multi-agent orchestration) once that draft exists, and Draft AL (agent memory and continuity), to align with the STEERING.md narrative-arc plan
