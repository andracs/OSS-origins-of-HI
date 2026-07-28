## Draft AM — The Hybrid Agentic Stack: A Reference Architecture and Research Agenda

**Version:** v0.2 (2026-05-16)
**Status:** v0.2 — adds the EU AI Act Article anchor table to §2.6 (mapping Articles 9–55 onto the seven layers); expands §2.7 with the Bansal et al. (2021) / Amershi et al. (2019) HCI anchors; fixes attribution drift on the Kambhampati (2024) citation (anchor is Draft V, not Draft I — both are now named). Cross-checked six attributions against upstream drafts (Khan, Liang, Brown, Kambhampati, Lewis, Bansal/Amershi) — all verified present.
**Next:** v0.3 — expand §4 (commons dependency map) with the AlphaFold/AlphaProof case once Draft AO is created; add Draft AN (alignment) governance-layer extension once that draft exists; run a worked end-to-end example through all seven layers (candidate: GitHub Copilot Workspace or Anthropic computer-use); add retraction-status spot-check for at least one source per cycle (deferred from v0.2 — all sources already retraction-checked in upstream drafts but the AM-level audit log is not yet maintained).

---

# Draft AM — The Hybrid Agentic Stack: A Reference Architecture and Research Agenda

## Overview and Chapter Position

The preceding drafts of this volume cover hybrid intelligence one component at a time. Draft A traces the open source commons. Draft S maps the four open knowledge platforms — arXiv, Wikipedia, GitHub, Hugging Face — that collectively constitute the digital commons. Draft V analyses the two engines of AI progress, scaling and self-play, and the synthesis between them. Draft T documents agentic tool calling. Draft AJ describes sensing infrastructure. Draft AK examines multi-agent orchestration. Draft AL covers agent memory and continuity. Draft P maps governance frameworks. Draft AI catalogues deployment failure modes. Drafts G and M address human-AI collaboration patterns and taxonomies. Draft U treats epistemic infrastructure. Drafts AG and I treat the limits of intelligence and calibration in current systems.

Each of these drafts holds one thread. None of them assembles the threads. A reader finishing the volume cannot, from the chapters alone, answer the question: *what does a mature hybrid agentic system look like as an architecture*? This chapter is the missing answer.

The chapter has three jobs. First, it offers a **reference architecture** — a layered map of the components a hybrid agentic system contains, where they sit relative to one another, and where the human is positioned within each layer. Second, it traces the **commons dependency** through that architecture — which layers can be built only because the open knowledge commons exists, which can in principle operate without it, and what changes when the commons is enclosed. Third, it lays out a **research agenda** — the unsolved problems of 2026 that determine whether the next decade of hybrid intelligence will deliver on the promise sketched in the opening drafts of this volume or will run aground on architectural and governance failures the field has not yet learned to recognise.

The chapter's position in the volume is deliberately terminal. It assumes the reader has worked through the rest of the book; it does not re-derive what is established elsewhere. Its job is integration.

---

## §1 — Why a Reference Architecture Is Now Possible

For most of AI's history, the question "what is the architecture of an intelligent system?" was unanswerable in a portable way. Symbolic systems had architectures (knowledge bases, inference engines, planning modules) but limited capability. Neural systems had capability but their architectures collapsed into the model itself — there was no *system* of which the model was a part, only a model that produced output. The cognitive architectures proposed in the symbolic tradition — SOAR, ACT-R, the various blackboard systems — were research artefacts rather than deployable infrastructure.

Three developments between 2022 and 2026 changed this. The first was the maturation of *tool calling* (Draft T): the convergence on structured protocols — function calling, the OpenAI plugin format, Anthropic's Model Context Protocol (MCP) — that allow language models to invoke external systems through stable, declarable interfaces. This established the model as one component among many rather than the entire system. The second was the emergence of *frontier coding agents* capable of autonomously implementing complex software systems, demonstrated most clearly in Sherwood, Aybar and Kaplan's (2026) benchmark in which Claude Opus 4.7 implemented a complete AlphaZero training pipeline within three hours. This established that agents could not only call tools but compose them into self-modifying systems. The third was the consolidation of *retrieval-augmented generation* (Lewis et al., 2020) and the surrounding vector-database infrastructure into a stable layer for semantic memory (Draft AL). With these three pieces in place, the components of a hybrid agentic system could finally be named and stacked.

The architecture proposed below is therefore not a theoretical proposal but a description of the system that has actually emerged. Different deployments instantiate it differently — production systems at scale make different trade-offs from research prototypes — but the layers are recognisable across them.

---

## §2 — The Seven-Layer Reference Architecture

The hybrid agentic stack contains seven layers, each with a distinct function, distinct failure modes, and a distinct relationship to the human. The layers are presented from the bottom (closest to the world) to the top (closest to the human user), but the data and control flows are bidirectional throughout.

### 2.1 Sensing layer (Draft AJ)

The bottom layer is the system's interface with the physical and informational world: cameras, microphones, IoT sensor arrays, log streams, web crawls, and structured data feeds. Sensing is not passive collection. Draft AJ's central claim is that sensing is a *design choice* — what the system can sense determines what it can learn, what it can act on, and what blind spots it carries.

**Function:** Convert states of the world into representations the upper layers can process. Decisions at this layer (sampling rates, sensor placement, modalities chosen) propagate through every higher layer; a system that does not sense temperature cannot learn about temperature.

**Human position:** Humans are simultaneously the *designers* of sensing (choosing what to instrument) and a *sensed entity* themselves. Human interaction interfaces — keyboards, voice, gaze tracking, cursor movements — are sensors in this taxonomy. The choice of which human signals to capture is an ethical and political decision, not merely a technical one.

**Primary failure mode:** Distributional gaps. The system cannot learn what it cannot sense. Training on the data the sensors happen to produce, rather than the data needed for the task, is the root cause of a substantial fraction of HI deployment failures (Draft AI).

### 2.2 Knowledge and memory layer (Drafts AL, U)

Above sensing sits the system's representation of what it knows: persistent stores of facts, episodes, and skills. Draft AL distinguishes four memory subsystems — sensory buffer (context window), episodic (event history), semantic (RAG and fact stores), procedural (learned tool habits) — each with different storage, retrieval, and governance requirements. Draft U argues that the *quality* of this knowledge layer is the central determinant of whether the system hallucinates: a system without anchoring to verifiable, navigable, authoritative sources will confabulate.

**Function:** Hold the system's beliefs and history in forms that are queryable, auditable, updatable, and persistent across sessions.

**Human position:** Humans curate the knowledge stores (decide what is authoritative), audit them (decide what the system was permitted to remember), and govern them (decide what the system must forget). Draft U's framing is that the knowledge layer is *epistemic infrastructure* — and the political question of who builds and governs that infrastructure is at least as important as the technical question of how to build it.

**Primary failure mode:** Hallucination via inadequate grounding (Draft I, Draft U) and identity drift via uncontrolled memory accumulation (Draft AL §5).

### 2.3 Model capabilities layer (Drafts V, AG)

The third layer is the model itself — the parametric system that performs reasoning, generation, and prediction. Draft V argues that contemporary models live at the intersection of two paradigms: scaling on the human record (Paradigm I) and self-play on generated experience (Paradigm II). Draft AG distinguishes general intelligence as a psychometric concept (Spearman's g, Cattell-Horn Gf/Gc) from general intelligence as a benchmark target (Chollet's ARC-AGI, Legg & Hutter's universal intelligence).

**Function:** Provide the reasoning, generation, classification, and planning capabilities the system uses to act on its inputs. This is the layer at which most public discussion of AI focuses; it is one of seven.

**Human position:** Humans train the model (supplying data and feedback signal), evaluate it (running benchmarks, red-teaming, calibration tests), and constrain it (through alignment techniques discussed in the alignment chapter, planned as Draft AN).

**Primary failure mode:** Capability gaps masked by fluent output — the system *appears* to reason in a domain where it is actually pattern-matching (Drafts I, V; Kambhampati, 2024).

### 2.4 Tool and skill layer (Draft T)

The model alone cannot act on the world. The tool and skill layer provides the catalogue of external systems — search engines, code executors, databases, file systems, APIs, physical actuators — that the model can invoke. Draft T documents the standardisation of this layer through MCP and the emergence of *skill ecosystems* in which tools are versioned, signed, distributed, and composed.

**Function:** Translate the model's intent into action on external systems, and translate the results back into a form the model can integrate.

**Human position:** Humans build the tools (write the code, expose the APIs), authorise their use (through permission systems), and audit their effects. The tool layer is the *attack surface* discussed in Draft E (prompt injection) and the *commercial battleground* discussed in Draft B (closed tool ecosystems vs. open MCP).

**Primary failure mode:** Misuse — the model selects the wrong tool, supplies wrong arguments, or cascades through tools in ways that produce unintended effects (Draft AI).

### 2.5 Orchestration layer (Draft AK)

When more than one agent is involved — supervisor and workers, peers in dialogue, market-based bidders — the orchestration layer governs their coordination. Draft AK identifies three coordination patterns (hierarchical, peer-to-peer, market-based), surveys the framework ecosystem (LangGraph, AutoGen, CrewAI, Anthropic's multi-agent SDK), and catalogues the failure modes specific to multi-agent settings: race conditions, conflicting goals, instruction-following drift, and reward misalignment between sub-agents.

**Function:** Decompose complex goals across multiple agents; route information between agents; integrate their outputs into a coherent system response.

**Human position:** Humans design the coordination protocols (decide which pattern fits the task), authorise delegation (decide which agents may spawn which sub-agents), and arbitrate when agents disagree.

**Primary failure mode:** Cascading errors. A misalignment in one agent propagates through the system, often amplified by the other agents' attempts to satisfy it (Draft AK §4; Bansal et al., 2021 on appropriate reliance applies a fortiori in multi-agent settings).

### 2.6 Governance layer (Drafts P, AI)

The sixth layer is not technical but institutional. The governance layer specifies who is accountable for what the system does, what the system is permitted to do, what records it must keep, what redress is available when it fails, and how human oversight is maintained. Draft P maps the regulatory frameworks (EU AI Act, NIST AI RMF, ISO/IEC 42001, sectoral regulation). Draft AI catalogues the deployment failure modes that governance is meant to anticipate.

**Function:** Define and enforce the constraints under which all lower layers operate — what the system may sense, remember, reason about, call as a tool, and coordinate. Governance is a cross-cutting concern, not a top layer in the strict sense; it intersects every other layer.

**Human position:** Humans are the principals to whom the system is ultimately accountable. Santoni de Sio and van den Hoven's (2018) "meaningful human control" is the conceptual anchor: humans must be able to understand, intervene in, and revise the system's behaviour at a sufficient level of granularity to bear moral responsibility for it. Draft AB on credit and blame attribution and the planned Draft AN on alignment both extend this layer's analysis.

**Primary failure mode:** Responsibility gaps (Matthias, 2004; Santoni de Sio & Mecacci, 2021) — situations where no human actor can be meaningfully held to account for an outcome that the system produced.

**EU AI Act Article anchors by layer.** The Act (Regulation (EU) 2024/1689) does not organise its obligations by the seven-layer stack used here, but its high-risk system requirements can be mapped onto the layers, which makes compliance gaps easier to see. The mapping below is indicative, not exhaustive; obligations frequently cross layers, and general-purpose-AI (GPAI) provisions in Articles 53–55 cut across the model layer for all foundation models regardless of downstream use case.

| Layer | Primary EU AI Act anchors | What the article requires |
|-------|---------------------------|----------------------------|
| Sensing | Art. 10 (data and data governance); Art. 13 (information to deployers) | Training, validation and test datasets must be relevant, representative, and free of errors; deployers must be told what input data the system expects |
| Knowledge / Memory | Art. 12 (record-keeping / automatic logging); Art. 26(6) (deployer log retention) | High-risk systems must log events automatically; deployers must keep logs for at least six months |
| Model | Art. 15 (accuracy, robustness, cybersecurity); Arts. 53–55 (GPAI obligations: technical documentation, training-data summary, systemic-risk evaluation) | Model performance must be declared and stable under adversarial conditions; GPAI providers carry transparency and (for systemic-risk models) evaluation duties |
| Tool / Skill | Art. 9 (risk management system); Art. 50 (transparency for certain outputs — synthetic audio, image, video, text) | Tool-mediated actions must be assessed in a risk management lifecycle; outputs that interact with natural persons must be disclosed as AI-generated |
| Orchestration | Art. 11 (technical documentation describing system architecture); Art. 17 (quality management system) | The architecture, including agent decomposition and delegation chains, must be documented; providers must operate a quality management system covering it |
| Governance | Art. 14 (human oversight); Art. 22 (authorised representatives for third-country providers); Art. 26 (deployer obligations) | Humans must be able to understand, intervene in, and stop the system; non-EU providers must designate an EU representative; deployers carry operational duties |
| Interface | Art. 13 (transparency to deployers); Art. 50 (transparency to natural persons interacting with AI) | Users must be informed that they are interacting with an AI system unless this is obvious from context; deployers must receive usable instructions |

The Act's Article 14 "meaningful human oversight" requirement is the institutional counterpart of the architectural condition stated in §6 below: a system that cannot be understood, intervened in, and revised by a human principal cannot satisfy this article in substance, however many sign-off steps it imposes in form (cf. Santoni de Sio & van den Hoven, 2018; Draft P).

### 2.7 Human interface layer (Drafts G, M, H)

The top layer is the interface between the system and the humans it serves and is served by. Draft G frames hybrid intelligence as mutual augmentation; Draft M provides the taxonomies that distinguish tool-use, collaboration, and agency as distinct modes; Draft H examines human augmentation and co-evolution across generations.

**Function:** Translate between the system's operations and the human's intent, attention, expectations, and feedback. This is the layer at which the user experiences the system and at which the system experiences the user.

**Human position:** The human is, by definition, in this layer. The architectural question is not *whether* the human is present but *how*: as a supervisor (human-on-the-loop), as a collaborator (human-in-the-loop), as a subject the system acts upon, or as a co-author of new artefacts that re-enter the lower layers as training data.

**Primary failure mode:** Mode mismatch — the interface presents the system as a collaborator when it is actually behaving as a tool, or as a tool when it is actually behaving as an agent. This is the source of the misplaced trust documented in Draft G's appropriate-reliance literature (Bansal et al., 2021; Buçinca et al., 2021), and the design problem that Amershi et al.'s (2019) eighteen HCI guidelines for human-AI interaction were intended to make tractable — guidelines that pre-date the agentic shift and require extension for systems that take consequential actions on the user's behalf rather than only recommending them.

---

## §3 — What "Hybrid" Means at Each Layer

The word "hybrid" in hybrid intelligence is not a single relation. At each layer of the stack, the human and the machine combine in a different way, and a system that achieves productive hybridisation at one layer can still fail at another.

| Layer | What hybridisation means at this layer | Human role | Machine role |
|-------|----------------------------------------|------------|--------------|
| Sensing | Joint instrumentation of the world | Choose what to sense; supply own signals | Convert sensed states into representations |
| Knowledge | Joint curation and audit of memory | Authorise, verify, forget | Store, retrieve, summarise |
| Model | Joint training and evaluation | Supply feedback signal; benchmark | Distil patterns; predict |
| Tools | Joint authoring and authorisation | Write tools; grant permissions | Select; invoke; integrate results |
| Orchestration | Joint design of coordination | Set protocols; arbitrate disputes | Decompose; delegate; integrate |
| Governance | Joint accountability | Bear responsibility; enforce constraints | Operate within constraints; produce records |
| Interface | Joint sense-making | Express intent; interpret output | Express state; interpret intent |

The mode of hybridisation moves up the stack from *physical* (joint sensing) to *cognitive* (joint reasoning) to *normative* (joint accountability) to *interpersonal* (joint sense-making). Different organisations and different domains require different emphases. A surgical robotics system foregrounds the sensing-and-tool layers; a legal-research assistant foregrounds the knowledge and interface layers; a national-scale governance application (Draft Y on Singapore) foregrounds the governance layer.

What makes a system *hybrid* in the strong sense developed by Lutz, Newlands, and Jarrahi (2025) is that the human-machine relation is *mutual*: not just AI assistance to humans, but bidirectional augmentation across multiple layers simultaneously. A system that hybridises at one layer only is closer to what Jarrahi (2018) called *symbiosis* — productive but asymmetric. A system that hybridises across layers approaches the moving target of hybrid intelligence proper.

---

## §4 — The Commons Dependency Through the Stack

A central thread in this volume is the dependency of contemporary AI on the open knowledge commons described in Draft A and mapped in Draft S. The reference architecture above lets that dependency be traced layer by layer.

**Sensing layer:** Largely commons-independent. Sensors are physical devices; the data they produce is fresh. The exception is that *sensor models* (e.g., the calibration models that convert raw camera output to corrected images) are increasingly trained on commons-derived datasets, importing commons dependence into hardware that appears autonomous.

**Knowledge layer:** Deeply commons-dependent. The semantic memory of most production systems is built on retrieval indices derived from web crawls, Wikipedia, arXiv, Stack Overflow, and GitHub — the four pillars of Draft S. A system without the commons would be reduced to its proprietary corpus, which in most domains is too narrow to support general-purpose reasoning.

**Model layer:** The most commons-dependent layer of all. Paradigm I models (Draft V §2) are *distillations* of the commons — Brown et al. (2020) GPT-3 was trained on a five-source mix dominated by filtered Common Crawl, WebText2, Books1/2, and Wikipedia; subsequent models extend this base. Paradigm II models (self-play, Draft V §3) are in principle commons-independent, since they generate their own training signal — but in practice the *evaluation infrastructure* that decides what counts as a good outcome (formal verifiers, simulators, test suites) is itself commons-derived.

**Tool layer:** Significantly commons-dependent. The tool ecosystem is built on open source software — Python, Node.js, the Hugging Face transformers library, the LangChain and AutoGen frameworks. Most tool implementations are themselves open source. Closing the commons would not eliminate tools, but would dramatically slow their evolution and limit interoperability.

**Orchestration layer:** Moderately commons-dependent. Open frameworks (LangGraph, AutoGen, CrewAI) carry the bulk of orchestration patterns; closed alternatives exist but are less common. The coordination *patterns* themselves (hierarchical, peer-to-peer, market-based) are intellectual commons established in academic literature (Wooldridge, 2009; Sandholm, 1999) — they exist regardless of whether their implementations are open.

**Governance layer:** Commons-independent in operation but commons-relevant in legitimacy. Regulatory frameworks (EU AI Act, NIST RMF) operate on legal-institutional infrastructure rather than the digital commons. But the *legitimacy* of AI governance increasingly depends on the public's ability to inspect what models do — which depends on commons-dependent infrastructure for auditing, benchmarking, and red-teaming.

**Interface layer:** Moderately commons-dependent. Interface conventions (chat patterns, tool palettes, permission dialogues) are partially established in open research; the underlying frameworks (web standards, accessibility specifications) are commons artefacts.

The pattern is unmistakable: the deeper one goes into the technical heart of the stack — the model and knowledge layers — the more dependent the system is on the commons. Enclosure of the commons would not stop AI development, but it would re-distribute it: the layers that depend most heavily on the commons would consolidate around whoever owns the post-enclosure substitute. This is the political-economic core of Draft F's extraction-paradox argument, made architecturally precise.

---

## §5 — The 2026 Research Frontier

A reference architecture is useful only if it makes the unsolved problems visible. This section names the open problems of 2026, organised by layer, and indicates which other drafts in this volume address them.

**Sensing.** Active sensing — the design of sensor placements and sampling policies that maximise the *training value* of collected data, rather than its volume — remains underdeveloped (Draft AJ §3). Sim-to-real transfer, the ability to train in simulation and deploy in physical environments, is improving rapidly but remains a substantial source of deployment failure. The boundary between sensing and surveillance — when does instrumentation of human behaviour cross from useful signal to unaccountable tracking? — is unresolved at both technical and regulatory levels.

**Knowledge.** Three problems stand out. Catastrophic forgetting in continual learning (Draft AL §3) — how does a system add new knowledge without losing what it already knew? Provenance — Draft U argues that hybrid systems need to know not only *what* they remember but *where it came from* and *whether it has been retracted* (cf. CrossRef `update-to`). And the *unharvested commons* (Draft W) — the oral traditions, indigenous epistemologies, and non-WEIRD cultural knowledge that current training corpora systematically exclude.

**Model.** Calibration failure (Draft I) — current models are confidently wrong in ways that resist mitigation. The mechanistic understanding of *why* scaling works (Liu, Liu, & Gore, 2025 on superposition) is still an active research frontier. The relationship between model capability and human capability across domains (Draft AC) is being mapped empirically but lacks predictive theory.

**Tools.** Tool ecosystems are immature: discovery (which tool fits the current task?), versioning (what happens when a tool changes?), security (Draft E on prompt injection through tool outputs), and accountability (who is liable when a tool produces a harmful action?) are all open problems. The Anthropic settlement documented in Baggersgaard (2026) demonstrates that the legal-economic tooling around training data — itself a kind of meta-tool — is also unresolved.

**Orchestration.** Multi-agent systems exhibit failure modes that single-agent systems do not (Draft AK §4): cascading hallucination, instruction-following drift, sub-agent reward misalignment. Empirical evidence on whether multi-agent debate actually improves accuracy is mixed (Khan et al., 2024). Principal hierarchies — who authorises an agent to spawn sub-agents, and how the resulting delegation chains are audited — are essentially unsolved at scale.

**Governance.** The responsibility gap (Matthias, 2004) is the deepest open problem in the field. EU AI Act compliance requires meaningful human control (Santoni de Sio & van den Hoven, 2018) but the *operationalisation* of that requirement — what records suffice, what oversight intensity is required at each risk tier, how cross-border deployments are governed — is being established case by case. Draft AN on alignment, when written, will treat the technical underpinnings of these governance requirements.

**Interface.** Trust calibration (Draft G) — how do users learn when to trust the system and when not to? — is the central unsolved problem of HCI in the agentic era. Draft H's co-evolution argument suggests this problem is generational rather than session-level: users who grow up alongside agentic systems develop different baseline expectations and different failure-recovery behaviours.

**Cross-cutting.** Two problems touch every layer. *Robustness* — systems that work in benchmarks but fail under distribution shift, adversarial input, or resource pressure (Draft Z on frugal AI shows the resource dimension; Draft E shows the adversarial dimension). *Equity* — who benefits from hybrid intelligence and who bears its costs, addressed by Drafts F (commons extraction), W (unharvested commons), AF (annotation labour), and Y (national strategy).

---

## §6 — What a Mature Hybrid Agentic System Looks Like

The reference architecture allows a tentative answer to the question that opens this chapter: what does a mature hybrid agentic system look like?

A mature system is one in which:
1. **Sensing** is *deliberate* — instrumentation is designed against the task rather than collected opportunistically.
2. **Knowledge** is *grounded* — every claim the system makes can be traced to a source the user can inspect and audit, and every memory the system retains can be revised, retracted, or forgotten on demand.
3. **Models** are *calibrated* — the system knows what it does not know, and signals that uncertainty in a form the human can act on.
4. **Tools** are *authorised* — every action the system takes on the world is bounded by permissions whose principal is human and whose audit trail is verifiable.
5. **Orchestration** is *legible* — the multi-agent decomposition the system uses is visible to the human, and the principal chain of delegation is recorded.
6. **Governance** is *meaningful* — humans have control they can actually exercise, not merely formal control they cannot operationalise.
7. **The interface** is *honest* — the system represents itself to the user as what it actually is at any given moment (tool, collaborator, or agent), not as what is most flattering or marketable.

No deployed system in 2026 satisfies all seven conditions. The frontier coding agents that can implement an AlphaZero pipeline in three hours (Sherwood et al., 2026) score high on tool authorisation and orchestration legibility within their sandboxed environments and low on grounded knowledge and honest interface. National-scale deployments (Draft Y on Singapore) score high on governance and lower on sensing deliberateness. Production enterprise systems trade calibration for fluency, and orchestration legibility for product polish.

The architectural point is not that any single system will satisfy every condition; specialisation is rational and unavoidable. The point is that the *book of hybrid intelligence research* must contain chapters that address each of the seven, because a deployment that scores zero on any of them is not a hybrid intelligence system but a single-purpose tool with hybrid-intelligence marketing.

---

## §7 — The Commons-Dependent Future

The volume opened with the three-stage model: accumulation of the commons (Draft A), mining and refinement of the commons into models (Drafts V, S), augmentation and feedback through hybrid systems that re-deposit value into the commons (Drafts G, AK, AL). The reference architecture refines this model. Hybrid intelligence is not the third stage of a linear progression; it is a recursive system in which each layer of the stack depends on, contributes to, and is constrained by the commons in different ways.

Two trajectories are visible from 2026. In the first, the commons continues to grow — augmented by hybrid systems that produce verifiable, attributable, openly licensed contributions, governed by extensions of the open source institutional patterns documented in Drafts A and D. In this trajectory, the seven-layer stack becomes increasingly modular, increasingly auditable, and increasingly accountable; the architecture of hybrid intelligence converges with the architecture of public infrastructure.

In the second trajectory, the commons is enclosed. Training data is acquired through commercial deals (or, as Baggersgaard (2026) documents, retroactive settlements); proprietary tool ecosystems consolidate around vendor-specific protocols; national or corporate boundaries constrain the cross-border mobility of models, data, and skills. In this trajectory, the seven-layer stack still exists but each layer is owned. The hybridisation of human and machine intelligence proceeds, but inside enclosed environments whose terms of use are non-negotiable.

The choice between these trajectories is not technical. It is institutional. The thesis of this volume — that open source code and the broader open knowledge commons are the *fuel* for hybrid intelligence — implies a corollary: the institutions that govern that fuel determine the kind of hybrid intelligence society ends up with. The reference architecture is the map; the political economy of the commons (Draft F) is the territory.

---

## Cross-references

This chapter is integrative and references nearly every other draft in the volume. Primary cross-references by section:

- **§2.1 Sensing layer:** Draft AJ (sensing infrastructure), Draft AP (embodied HI when written)
- **§2.2 Knowledge layer:** Draft AL (memory architectures), Draft U (epistemic infrastructure), Draft I (epistemic limits), Draft W (unharvested commons), Draft X (provenance and detection)
- **§2.3 Model layer:** Draft V (paradigms), Draft AG (general intelligence), Draft Z (frugal AI), Draft AC (model vs. human performance)
- **§2.4 Tool layer:** Draft T (tool calling), Draft AH (theoretical agency), Draft AI (deployment failure modes), Draft E (structural vulnerabilities), Draft B (closed models)
- **§2.5 Orchestration layer:** Draft AK (multi-agent orchestration), Draft G (collaboration patterns), Draft M (taxonomies)
- **§2.6 Governance layer:** Draft P (governance and compliance), Draft AB (credit and blame), Draft AN (alignment, when written), Draft Y (Singapore), Draft AP (legal personality)
- **§2.7 Interface layer:** Draft G, Draft M, Draft H (human augmentation), Draft AA (outperformance psychology), Draft BA (student learning)
- **§4 Commons dependency:** Draft A (commons history), Draft S (open knowledge platforms), Draft F (extraction paradox), Draft K (openness layers)
- **§5 Research frontier:** all of the above plus Draft AF (annotation labour), Draft AS (technostress), Draft AU (environmental load), Draft AW (commercial datasets)

---

## Key Sources (pointer set; full APA in upstream drafts)

- **Lutz, C., Newlands, G., & Jarrahi, M. H. (2025).** Definition and conceptual frame for hybrid intelligence. *Cited in Drafts G, M.* `[J]`
- **Jarrahi, M. H. (2018).** *Business Horizons*, 61(4), 577–586. Human-AI symbiosis in organisational decision-making. *Cited in Draft G.* `[J]`
- **Russell, S., & Norvig, P. (2021).** *Artificial Intelligence: A Modern Approach* (4th ed.). Foundational agent definition. *Cited in Drafts AL, M.* `[J]`-tier monograph.
- **Bommasani, R., et al. (2021).** Foundation models report (Stanford CRFM). *Cited in Draft V.* `[R]`
- **Brown, T., et al. (2020).** GPT-3 paper. NeurIPS 2020. *Cited in Drafts V, S, with Table 2.2 corpus composition.* `[C]`
- **Silver, D., et al. (2018, 2021).** AlphaZero and the reward-is-enough hypothesis. *Cited in Draft V.* `[J]`
- **Wooldridge, M. (2009).** *An Introduction to MultiAgent Systems* (2nd ed.). *Cited in Draft AK.* `[J]`-tier monograph.
- **Lewis, P., et al. (2020).** Retrieval-Augmented Generation. NeurIPS 2020. *Cited in Drafts AL, T.* `[C]`
- **Park, J. S., et al. (2023).** Generative Agents. UIST 2023. *Cited in Drafts AL, AK.* `[C]`
- **Sherwood, J., Aybar, B., & Kaplan, B. (2026).** Frontier Coding Agents + AlphaZero. arXiv:2604.25067. *Cited per STEERING.md across Drafts AC, AK, V, G, T.* `[P]`
- **Liu, Y., Liu, Z., & Gore, J. (2025).** Superposition Yields Robust Neural Scaling. NeurIPS 2025. *Cited per STEERING.md in Drafts V, Z, AG, AD.* `[C]`
- **Matthias, A. (2004).** The responsibility gap. *Ethics and Information Technology*. *Cited in Draft P.* `[J]`
- **Santoni de Sio, F., & van den Hoven, J. (2018).** Meaningful human control. *Frontiers in Robotics and AI*. *Cited in Draft P.* `[J]`
- **Baggersgaard, C. (2026).** Anthropic settlement coverage. *Forskerforum.* *Cited per STEERING.md in Drafts C, F, P.* `[R]`
- **European Parliament and Council. (2024).** *Regulation (EU) 2024/1689 laying down harmonised rules on artificial intelligence (AI Act)*. OJ L, 2024/1689, 12 July 2024. *Cited for §2.6 Article anchor table; full reference in Drafts P, AP.* `[R]`
- **Bansal, G., Wu, T., Zhou, J., Fok, R., Nushi, B., Kamar, E., Ribeiro, M. T., & Weld, D. (2021).** Does the whole exceed its parts? The effect of AI explanations on complementary team performance. *CHI 2021.* *Cited in Drafts G, AK; added here for §2.7 interface-layer anchor.* `[C]`
- **Amershi, S., Weld, D., Vorvoreanu, M., Fourney, A., Nushi, B., Collier, P., Suh, J., & Horvitz, E. (2019).** Guidelines for human-AI interaction. *CHI 2019.* *Cited in Draft G; added here for §2.7 interface-layer anchor.* `[C]`
- **Kambhampati, S. (2024).** Can large language models reason and plan? *Annals of the New York Academy of Sciences, 1534*(1), 15–18. *Cited in Draft V; added here for §2.3 model-layer failure-mode anchor.* `[J]`

For full bibliographic detail and OpenAlex citation counts, see the Key Sources sections of the upstream drafts referenced above.
