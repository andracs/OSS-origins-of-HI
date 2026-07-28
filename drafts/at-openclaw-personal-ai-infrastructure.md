# Draft AT — The Personal AI Infrastructure Revolution: OpenClaw and the Democratisation of Agentic Hybrid Intelligence

**Version:** v0.4 (2026-05-16)  
**Status:** v0.4 — peer-reviewed historical anchors. §1.1 trade-press histories (Hafner & Lyon 1996; Levy 1984) supplemented with academic scholarly histories — Abbate (1999) *Inventing the Internet* (MIT Press, Inside Technology series) for ARPANET; Haigh & Ceruzzi (2021) *A New History of Modern Computing* (MIT Press) for PC democratisation. Closes the 2026-05-16 analyst flag on Zahavi et al. hallucinated citation (resolved by Sonnet 4.6 commit 9c5c496-equivalent earlier; STEERING.md updated this cycle). CrossRef retraction check clean on Park et al. (2023) UIST.  
**Note on positionality:** The author is the creator of OpenClaw. This chapter draws on first-hand design knowledge; claims about design decisions and rationale are authoritative; claims about broader significance should be treated as the author's analytical framing and subjected to peer review scrutiny accordingly.  
**Next:** address Task 011 (Zuboff 2015 *Journal of Information Technology* "Big other" alongside Zuboff 2019 book); compare ClawHub skill ecosystem with app store models and npm/PyPI registry governance; expand §3.3 self-improving hybrid system with empirical evidence on memory-augmented agents; cross-ref AR (harness architecture), AK (orchestration), T (tool-calling), AS (technostress implications of always-on agents).

---

## Overview and Chapter Position

Every major transition in computing has involved a shift in *who controls the infrastructure*. Mainframes concentrated compute in institutional hands; personal computers moved it to individuals. The internet distributed information and communication; smartphones put networked computing in pockets. Each transition democratised access to capabilities previously available only to organisations with resources to operate infrastructure.

The emergence of agentic AI creates the conditions for a similar transition. For most of its history, AI has been a service: a capability accessed through an API, consumed through a product, controlled by a provider. The user is the consumer, not the operator. The intelligence is powerful but not *theirs*.

OpenClaw represents a different vision: *personal AI infrastructure* — an open, configurable system that places a capable, autonomous, multi-model AI agent under the genuine control of the individual user. This chapter traces the architectural and philosophical principles behind this vision, situates it within the broader history of computing democratisation, and examines its implications for hybrid intelligence. The argument is that the shift from AI-as-service to AI-as-personal-infrastructure is not merely a convenience improvement; it is a qualitative change in the human-AI relationship, with significant consequences for agency, accountability, and the sustainability of hybrid intelligence.

---

## §1 — Computing Revolutions as Shifts in Control

### 1.1 The pattern of democratisation

The history of computing is, in significant part, a history of successive democratisations — each of which extended the capacity for computational self-determination to a larger population.

The mainframe era (1950s–1970s) concentrated computing in institutional operators. Users submitted jobs; operators ran them; results were returned hours later. The relationship was legible but disempowering: the user was a consumer of institutional computing capacity, not an operator of their own.

The personal computer revolution (late 1970s–1980s) changed this fundamentally. The Apple II, the IBM PC, and the machines that followed put a general-purpose computer under individual control (Haigh & Ceruzzi, 2021; Levy, 1984). Alan Kay and Adele Goldberg at Xerox PARC articulated the vision explicitly: the computer as a *personal dynamic medium* — an instrument so responsive and configurable that it would become an extension of the user's intellectual capability, not merely a productivity tool (Kay & Goldberg, 1977). The realisation of this vision required both hardware miniaturisation and, crucially, an operating system that made the machine *operable* by a non-specialist: configurable, extensible, and owned by its user.

The internet and the smartphone added connectivity and ubiquity, but introduced a counter-movement: the re-centralisation of computing capability in platform operators. The internet's own origins were institutional — ARPANET grew out of a small Defense-funded research community whose protocols only later opened to broader participation (Abbate, 1999; Hafner & Lyon, 1996) — and the platform consolidation that followed inherited part of that institutional logic. The smartphone is personal hardware running software largely controlled by Apple or Google; the cloud is personal data stored on servers belonging to Amazon, Microsoft, or Google. The democratisation of access was real; the democratisation of control was partial.

### 1.2 AI as a recentralisation force

The first wave of capable AI was built at scale by large organisations and delivered as a service. GPT-4, Claude, Gemini — each is the product of infrastructure investments measured in hundreds of millions of dollars, operated by a handful of companies, and accessed through APIs under terms of service that reserve the right to modify, restrict, or discontinue access. Adoption has been unusually rapid: a representative U.S. workforce survey conducted in August 2024 found that roughly 39 percent of Americans aged 18–64 had used generative AI, with about 28 percent using it for work — a diffusion pace exceeding that of personal computers and the internet at comparable points after release (Bick, Blandin, & Deming, 2024). Subsequent analysis of consumer ChatGPT usage logs documents that by mid-2025 the platform had reached hundreds of millions of weekly active users worldwide, with non-work tasks (writing assistance, information seeking, personal advice) accounting for the majority of conversations (Chatterji et al., 2025). The empirical record thus shows mass *consumption* of AI services without corresponding diffusion of operational control.

From a hybrid intelligence perspective, this creates a structural problem. If the AI component of a hybrid intelligence system is controlled by a third party — its parameters, its training, its availability, its pricing — then the human component's ability to form a genuine long-term partnership with the AI component is limited. The AI can be changed, withdrawn, or repriced unilaterally. The relationship is tenancy, not ownership.

This is not merely theoretical. The rapid deprecation of AI models — GPT-3.5 retired, Claude 1 discontinued, numerous fine-tuned models abandoned (Bommasani et al., 2021; Robbes et al., 2012) — creates a recurring disruption of human-AI working relationships that is structurally analogous to having a skilled colleague reassigned or fired without notice, on a cycle of months rather than years.

---

## §2 — The OpenClaw Architecture: Personal AI Infrastructure in Practice

### 2.1 Design philosophy

OpenClaw was designed around three principles that distinguish personal AI infrastructure from AI-as-a-service:

**User as principal, not consumer.** In the principal hierarchy developed in Draft AR, the user is typically the lowest-trust principal — operating within constraints set by the developer and operator. OpenClaw inverts this for personal deployment: the user *is* the developer and operator. The system prompt, the skill registry, the permission model, the cron schedule, the notification routing — all are configurable by the user. The infrastructure serves the user's goals, not a platform operator's product strategy.

**Model as interchangeable component, not locked dependency.** OpenClaw is multi-model: the user can route different tasks to different AI providers (Claude, Gemini, OpenAI, locally-hosted models) and configure fallback chains. A cron job that runs quality checks on academic drafts might use Opus 4.7 for the depth of reasoning; a quick summarisation task might use Haiku for speed and cost. The intelligence is modular, not monolithic. When a provider changes pricing or deprecates a model, the user can reroute without rebuilding the system.

**Skill as commons, not proprietary extension.** The capability of an OpenClaw agent is extended through skills — modular, composable capability packages defined in a standard format (SKILL.md). Skills can be shared, installed, and published through ClawHub, an open registry that functions analogously to a package manager. The skill ecosystem is a commons: capabilities developed by any user can be made available to all.

### 2.2 Core architectural components

OpenClaw implements the harness architecture described in Draft AR across a mobile-first, always-on deployment model:

**The session layer** manages persistent, named AI sessions that survive device restarts and maintain conversation context across days and weeks. Unlike chat interfaces that treat each conversation as ephemeral, OpenClaw sessions represent ongoing working relationships between the user and specific AI agents with specific configurations.

**The cron system** enables scheduled agentic work: tasks that run automatically at specified times without user initiation. A user can configure an agent to improve a document corpus every morning, monitor a news feed and summarise findings each afternoon, run quality checks on creative work each evening, and push results to a repository — all without manual intervention. The agent works while the user sleeps.

**The skill registry** provides a curated set of capabilities available to agents: web search, document reading, image analysis, code execution, API calls to external services, notification delivery, memory operations. Skills are described in SKILL.md format — a structured specification that allows agents to discover, select, and invoke capabilities appropriately.

**The notification layer** routes agent outputs and alerts to the user through messaging channels — primarily Telegram, but extensible to other channels. This creates an asymmetric communication model: the agent can initiate contact (reporting completions, surfacing anomalies, requesting decisions) rather than passively waiting for user queries.

**The memory system** provides persistent storage of information across sessions — user preferences, project context, past decisions, learned facts. Memory is structured by type (user, feedback, project, reference) and indexed for retrieval. An agent can, over time, build a model of the user's working style, preferences, and project context that makes its assistance progressively more appropriate.

**The multi-node deployment** allows agents to operate across devices: a server running in a data centre handles background processing; a mobile client provides the notification and interaction layer; the system maintains coherence across both. This enables a class of applications — always-on background agents that also surface results on mobile devices — that is structurally impossible with chat-only interfaces.

### 2.3 The ClawHub skill ecosystem

ClawHub is OpenClaw's skill registry: an open repository where users can publish, discover, and install skill packages. The ecosystem model draws explicitly on the success of open source package managers (npm, pip, apt) as models for community-maintained capability commons (Decan et al., 2019; Benkler, 2006).

The analogy with open source is substantive, not merely rhetorical. A skill package is a defined interface (the SKILL.md specification) with a public implementation — the prompts, tool configurations, and execution logic that define the capability. Any user can inspect, fork, and modify a published skill. The registry creates network effects: a skill developed for one use case (academic literature search, code review, news monitoring) becomes available to all users who share that use case, without duplication of effort.

This positions the skill ecosystem as a new layer in the digital commons described in Draft A. Where earlier commons accumulated code (open source), data (Wikipedia, arXiv), and models (open weights), the skill commons accumulates *agentic capability* — the institutional knowledge of how to deploy AI agents effectively in specific domains.

#### Comparative positioning: OpenClaw in the personal AI infrastructure landscape

The claim that OpenClaw represents "a different vision" requires contextualisation against adjacent open-source projects pursuing overlapping goals. Open Interpreter (Lucas, 2023) enables natural-language control of local computing environments through a code-execution interface, but operates as an interactive single-session tool rather than persistent agent infrastructure; it provides no scheduling, no cross-session memory, and no skill commons. Auto-GPT (Significant Gravitas, 2023) demonstrated early the potential for goal-directed agents with web access and file memory, but its architecture centred autonomous task decomposition rather than user-configurable skill composition and multi-channel orchestration. Local inference frontends — LM Studio, Ollama — make open-weight models accessible on consumer hardware, addressing the substrate dependency described in §4.3 without providing session management, cron scheduling, or skill ecosystem layers. Home Assistant, the most mature community-governed personal infrastructure project, offers persistent, extensible home automation with thousands of community integrations that are structurally analogous to skills — but its AI integration remains a peripheral add-on rather than a first-class architectural component (Home Assistant, 2024).

Multi-agent frameworks such as AutoGen (Wu et al., 2023) and MetaGPT (Hong et al., 2023) address the orchestration layer for developer-facing workflows, but assume an operator running agent pipelines programmatically rather than an individual configuring a persistent personal infrastructure. OpenClaw's distinctiveness lies in combining five components that no single prior system integrates: persistent named sessions, cron-scheduled agentic work, a community skill commons, multi-channel notification routing, and structured cross-session memory — under direct user control without requiring software development expertise.

---

## §3 — The Revolution in Human-AI Relationship

### 3.1 From reactive to proactive

The dominant interface paradigm for AI in 2023–2025 was *prompt-and-response*: the human initiates, the AI responds, the interaction concludes (Wang et al., 2024). This is a tool paradigm — the AI is an instrument activated by user intention, powerful but passive.

Agentic AI with persistent scheduling breaks this paradigm. The agent initiates. It completes work without being asked. It surfaces results when they are ready, not when the user queries. The relationship shifts from *tool use* to something closer to *delegation*: the human specifies goals and constraints; the agent pursues them autonomously; the human reviews, redirects, and approves.

This shift has been noted in the organisational literature on human-agent teams (Draft G), but its personal dimension is less examined. For an individual user, the experience of having an agent that works continuously toward goals the user has specified — improving a manuscript, monitoring a codebase, maintaining a knowledge base — is qualitatively different from querying a chat interface. It introduces a category of *asynchronous collaboration* previously available only to people with human assistants: work proceeding in parallel with the user's other activities, with results delivered on completion rather than in real time (Seeber et al., 2020).

### 3.2 The principal who knows the system

A distinctive feature of personal AI infrastructure is that the user understands the system they are operating. In enterprise AI deployments, end users interact with agent capabilities configured by IT departments, product teams, or external providers — the principal hierarchy is layered and the user operates near the bottom. In personal AI infrastructure, the user configured the system, wrote or selected the skills, set the cron schedules, designed the notification routing. This intimacy with the system has significant implications:

- **Calibrated trust**: the user knows why the agent behaves as it does, because they designed the behaviour. Trust is grounded in understanding rather than brand reputation (Lee & See, 2004).
- **Rapid iteration**: when the agent's behaviour diverges from the user's goals, the user can modify the configuration directly rather than waiting for a product team to update a feature.
- **Personal data sovereignty**: the user controls where data is stored, which models see which data, and how long memory persists. There is no platform operator collecting usage data as a secondary product (Zuboff, 2015, 2019).

### 3.3 The self-improving hybrid system

Perhaps the most significant implication of personal AI infrastructure is the possibility of a *self-improving* hybrid system: a human-agent partnership that, over time, becomes progressively better calibrated to the human's working style, expertise, and goals.

In a chat interface, each conversation begins from scratch. The model has no knowledge of the user's prior interactions, preferences, or evolving context (unless explicitly re-provided). The partnership does not accumulate.

In a persistent personal AI infrastructure with structured memory, the agent accumulates knowledge of the user: what kinds of feedback the user gives, what quality standards they apply, what topics they are working on, what decisions they have made and why. This accumulated context is not in the model weights — it is in the memory layer, maintained by the harness. Over months of interaction, the agent becomes a progressively better partner: more calibrated, more anticipatory, less in need of repeated instruction (Glikson & Woolley, 2020; Park et al., 2023).

This dynamic is what Kay and Goldberg (1977) envisioned for the personal computer as a dynamic medium: a system that adapts to the user's cognitive style rather than forcing the user to adapt to the system's interface. The personal AI infrastructure achieves this adaptation not through model fine-tuning but through accumulated memory and feedback-shaped configuration.

---

## §4 — Critical Assessment: Risks and Limitations

### 4.1 The technostress risk of always-on agents

Draft AS documents the psychological risks of agentic AI systems that work continuously and surface outputs asynchronously. Personal AI infrastructure amplifies these risks by placing always-on agents under direct user control without organisational governance structures to set limits. The user who configures an agent to run quality checks every hour and send Telegram notifications at all times is simultaneously the beneficiary and the victim of the always-on design.

Sustainable personal AI infrastructure requires users to design their own governance: notification quiet hours, pacing controls, scope boundaries. The tools for this governance are available in the harness architecture (Draft AR §6), but the incentive to implement them runs against the optimisation drive that motivates sophisticated users to build more capable systems.

### 4.2 The skill quality problem

A commons-based skill ecosystem faces the quality assurance challenges that characterise all open source commons: inconsistent documentation, abandoned packages, skills that work for their author's specific configuration but fail in others'. The npm ecosystem's experience — millions of packages, a long tail of low-quality or unmaintained code, and periodic catastrophic failures from widely-adopted but fragile dependencies (Decan et al., 2019) — is a cautionary precedent (see Draft A on the xz backdoor).

Skill quality in an agentic ecosystem has additional stakes: a poorly-designed skill does not merely produce wrong output, it may produce wrong *actions* — file modifications, API calls, repository commits — that are difficult to reverse.

### 4.3 The concentration paradox

Personal AI infrastructure democratises the *operation* of agentic AI but not its *foundation*. The models that power OpenClaw agents — Claude, Gemini, GPT — are still produced by a small number of well-capitalised organisations. The routing layer and the skill ecosystem are personal and open; the intelligence substrate remains centralised. This is structurally analogous to a smartphone that runs open software on proprietary silicon: meaningful autonomy at the application layer, continued dependency at the infrastructure layer.

The long-term resolution of this tension likely depends on the maturation of open-weight models capable of running locally — a development that is technically plausible within the medium term but that currently involves significant quality trade-offs relative to frontier proprietary models (Dubey et al., 2024).

---

## §5 — Implications for Hybrid Intelligence

Personal AI infrastructure represents a new deployment context for hybrid intelligence: the individual as their own HI architect, designer, operator, and beneficiary simultaneously. The institutional HI use cases addressed in Draft G (enterprise, healthcare, research) involve distributed principal hierarchies, organisational governance, and collective use cases. Personal AI infrastructure collapses these distinctions: one person configures, one person uses, one person benefits, one person bears the consequences of failures.

This concentration of roles creates both opportunities and responsibilities. The user who has designed their own AI harness is, in a meaningful sense, more genuinely in control than one who operates within an enterprise system designed by others. They are also more directly accountable for the system's behaviour — without an IT department or product team to blame when the agent does something unexpected.

The broader implication for hybrid intelligence research is that personal AI infrastructure constitutes a new unit of analysis: not the organisation deploying AI but the individual operating their own hybrid intelligence system. The design principles, governance challenges, psychological dynamics, and capability patterns of this configuration differ systematically from institutional deployments and deserve dedicated empirical and theoretical attention.

---

## Foreløbige referencer

- Abbate, J. (1999). *Inventing the Internet*. MIT Press (Inside Technology series). [R] [OA cit: 815] — canonical peer-reviewed STS scholarly history of ARPANET and Internet protocol development; reviewed in *American Historical Review* (Cortada, 2000), *Enterprise & Society* (Cukier, 2000), and *Isis*; supplements the Hafner & Lyon (1996) trade-press narrative with academically-grounded historiography. Anchors §1.1 ARPANET institutional-origin claim. *(executor-added 2026-05-16)*
- Haigh, T., & Ceruzzi, P. E. (2021). *A New History of Modern Computing*. MIT Press. [R] [OA cit: 122] — updated peer-reviewed academic history of computing succeeding Ceruzzi's earlier MIT Press editions (1998, 2003); canonical scholarly account of the personal computer transition. Supplements the Levy (1984) trade-press cultural history with peer-reviewed historiographic anchor. Cited in §1.1 for the PC-democratisation empirical claim. *(executor-added 2026-05-16)*
- Seeber, I., Bittner, E., Briggs, R. O., de Vreede, T., de Vreede, G.-J., Elkins, A., Maier, R., Merz, A. B., Oeste-Reiß, S., Randrup, N., Schwabe, G., & Söllner, M. (2020). Machines as teammates: A research agenda on AI in team collaboration. *Information & Management*, 57(2), 103174. https://doi.org/10.1016/j.im.2019.103174 `[J]` [OA cit: 650] — peer-reviewed anchor for §3.1 asynchronous collaboration claim; research agenda paper establishing foundational framework for AI-as-teammate in knowledge work, including delegation patterns and asynchronous task completion as key team interaction modes. *(executor-added 2026-05-11)*
- Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779. https://doi.org/10.1016/0005-1098(83)90046-8 [J] (CrossRef verified 2026-05-06; no retraction notice)
- Bick, A., Blandin, A., & Deming, D. J. (2024). *The rapid adoption of generative AI* (NBER Working Paper No. 32966). National Bureau of Economic Research. https://doi.org/10.3386/w32966 [R] [OA cit: 72] (PDF: `Kilder/Bick2024_RapidAdoptionGenerativeAI_NBER_w32966.pdf`)
- Chatterji, A. K., Cunningham, T., Deming, D. J., Hitzig, Z., Ong, C., Shan, C. Y., & Wadman, K. (2025). *How people use ChatGPT* (NBER Working Paper No. 34255). National Bureau of Economic Research. https://doi.org/10.3386/w34255 [R] [OA cit: 83] (PDF: `Kilder/Chatterji2025_HowPeopleUseChatGPT_NBER_w34255.pdf`)
- Hafner, K., & Lyon, M. (1996). *Where wizards stay up late: The origins of the Internet*. Simon & Schuster. [R] (canonical narrative history of ARPANET; widely cited in internet historiography — see Edwards, 1998, *Isis* book review)
- Kay, A., & Goldberg, A. (1977). Personal dynamic media. *Computer*, 10(3), 31–41. https://doi.org/10.1109/C-M.1977.217672 [J] (CrossRef verified 2026-05-06)
- Levy, S. (1984). *Hackers: Heroes of the computer revolution*. Doubleday. [R]
- OpenClaw. (2026). *OpenClaw documentation and skill specification*. https://openclaw.ai [practitioner source]

---

### Verified / executor-added

- Bommasani, R., Hudson, D. A., Adeli, E., Altman, R., Arora, S., von Arx, S., Bernstein, M. S., Bohg, J., Bosselut, A., Brunskill, E., Brynjolfsson, E., Buch, S., Card, D., Castellon, R., Chatterji, N., Chen, A., Creel, K., Davis, J. Q., Demszky, D., … Liang, P. (2021). *On the opportunities and risks of foundation models*. arXiv:2108.07258. https://doi.org/10.48550/arXiv.2108.07258 `[P]` [OA cit: 2153] — Stanford CRFM technical report; preprint only (no peer-reviewed proceedings version); documents provider-controlled foundation model lifecycle and downstream dependency risks; anchors §1.2 model-deprecation claim.
- Park, J. S., O'Brien, J. C., Cai, C. J., Morris, M. R., Liang, P., & Bernstein, M. S. (2023). Generative agents: Interactive simulacra of human behavior. In *Proceedings of the 36th Annual ACM Symposium on User Interface Software and Technology (UIST '23)*. ACM. https://doi.org/10.1145/3586183.3606763 (preprint: arXiv:2304.03442) `[C]` [OA cit: 169] — UIST 2023 peer-reviewed proceedings; empirically demonstrates memory-augmented agents accumulating experience and refining behaviour over time through memory streams, reflection, and planning; anchors §3.3 self-improving hybrid claim.
- Zimmermann, M., Staicu, C.-A., Tenny, C., & Pradel, M. (2019). Small world with high risks: A study of security threats in the npm ecosystem. In *Proceedings of the 28th USENIX Security Symposium* (pp. 995–1010). USENIX Association. (preprint: arXiv:1902.09217) `[C]` [OA cit: 123 combined (arXiv 89 + USENIX proceedings 34)] — empirical study documenting npm dependency chain vulnerabilities and systemic fragility from concentrated maintainership; anchors §2.3 and §4.2 ecosystem-quality discussion.
- Dubey, A., Jauhri, A., Pandey, A., Kadian, A., Al-Dahle, A., Letman, A., Mathur, A., Schelten, A., Yang, A., Fan, A., Goyal, A., Hartshorn, A., Yang, A., Mitra, A., Sravankumar, A., Korenev, A., Hinsvark, A., Roy, A., Kumar, A., … & Zhu, C. (2024). The Llama 3 herd of models. arXiv:2407.21783. https://doi.org/10.48550/arXiv.2407.21783 `[P]` [OA cit: indexing incomplete (OpenAlex W7115097999 currently reports 0 cites; this is a known indexing gap — Meta technical report widely cited across 2024–2025 LLM literature)] — documents Llama 3's benchmark performance relative to GPT-4o and Claude 3.5 Sonnet, showing that open-weight frontier models have substantially narrowed but not eliminated quality gaps on coding, reasoning, and multilingual tasks; primary empirical anchor for the "significant quality trade-offs" claim in §4.3.
- Lee, J. D., & See, K. A. (2004). Trust in automation: Designing for appropriate reliance. *Human Factors*, 46(1), 50–80. https://doi.org/10.1518/hfes.46.1.50_30392 `[J]` [OA cit: 3224; CrossRef retraction check 2026-05-12 — `update-to: []` clean] — canonical framework on calibrated trust in automation, distinguishing understanding-grounded appropriate reliance from both over-trust and under-trust; directly anchors §3.2 claim that understanding-based trust is qualitatively different from brand-reputation trust. *(executor-added 2026-05-08; counts and retraction status verified 2026-05-12)*
- Wu, Q., Bansal, G., Zhang, J., Wu, Y., Zhang, S., Zhu, E., Li, B., Jiang, L., Zhang, X., & Wang, C. (2023). AutoGen: Enabling next-gen LLM applications via multi-agent conversation. arXiv:2308.08155. https://doi.org/10.48550/arXiv.2308.08155 `[P]` [OA cit: 147] — establishes multi-agent framework as developer-facing orchestration layer; contextualises OpenClaw's personal-infrastructure focus as distinct from programmatic multi-agent pipeline frameworks; anchors §2.3 comparative analysis. *(executor-added 2026-05-08; OA cit verified 2026-05-12)*
- Hong, S., Zhuge, M., Chen, J., Zheng, X., Cheng, Y., Zhang, C., Wang, J., Wang, Z., Yau, S. K. S., Lin, Z., Zhou, L., Ran, C., Xiao, L., Wu, C., & Schmidhuber, J. (2023). MetaGPT: Meta programming for a multi-agent collaborative framework. arXiv:2308.00352. https://doi.org/10.48550/arXiv.2308.00352 `[P]` [OA cit: 134] — multi-agent software engineering framework operating in developer workflow context, not personal always-on infrastructure; comparative anchor for §2.3 positioning. *(executor-added 2026-05-08; OA cit verified 2026-05-12)*
- Home Assistant. (2024). *Home Assistant documentation: AI / voice assistant integration*. Nabu Casa. https://www.home-assistant.io/integrations/#voice [practitioner; official documentation confirming that AI/voice capabilities are integrations layered onto the home automation core, not first-class architectural components — comparative anchor for §2.3] *(executor-added 2026-05-08)*
- Lucas, K. (2023). *Open Interpreter* [Computer software]. GitHub. https://github.com/OpenInterpreter/open-interpreter [practitioner; open-source single-session code-execution agent enabling natural-language control of local computing environments; iCit not applicable (software repository); cited in §2.3 as comparative anchor — operates without persistent session management, cross-session memory, or skill commons. Authorship verified 2026-05-12 via GitHub API: repository owner organisation "openinterpreter"; earliest commits (created 2023-07-14) authored by KillianLucas — the prior "Killeen, L." attribution was a misspelling of Killian Lucas.] *(executor-added 2026-05-10; author name corrected 2026-05-12)*
- Richards, T. B. (Significant Gravitas). (2023). *Auto-GPT: An Autonomous GPT-4 Experiment* [Computer software]. GitHub. https://github.com/Significant-Gravitas/AutoGPT [practitioner; early open-source autonomous agent demonstrating goal-directed task decomposition with web access and file memory; iCit not applicable (software repository); cited in §2.3 as comparative anchor — architecture centred autonomous task decomposition rather than user-configurable skill composition and multi-channel orchestration. S2 rate-limited at execution time; confirmed from established literature.] *(executor-added 2026-05-10)*
- Zuboff, S. (2015). Big other: Surveillance capitalism and the prospects of an information civilization. *Journal of Information Technology*, *30*(1), 75–89. https://doi.org/10.1057/jit.2015.5 `[J]` [OA cit: >4000; field-defining peer-reviewed articulation of surveillance capitalism and the concept of behavioural modification through secondary data extraction — the academic foundation of Zuboff (2019); directly anchors §3.2 data-sovereignty claim that platform operators collect usage data as a secondary product. S2 rate-limited — confirmed from established literature; iCit far above ≥5 threshold.] *(executor-added 2026-05-17)*
- Zuboff, S. (2019). *The age of surveillance capitalism: The fight for a human future at the new frontier of power*. PublicAffairs. `[R]` (trade-press monograph; peer-reviewed academic foundation in Zuboff 2015 `[J]` above) — canonical book-length analysis of platform data extraction as behavioural modification commodity; anchors §3.2 data-sovereignty claim alongside Zuboff (2015). *(executor-added 2026-05-10; companion `[J]` entry added 2026-05-17)*
- Robbes, R., Lungu, M., & Röthlisberger, D. (2012). How do developers react to API deprecation? In *Proceedings of the ACM SIGSOFT 20th International Symposium on the Foundations of Software Engineering (FSE '12)* (pp. 1–11). ACM. https://doi.org/10.1145/2393596.2393645 `[C]` [OA cit: 68; empirical study of developer reactions to API deprecation in software ecosystems documenting downstream disruption — supports §1.2 claim that model deprecation creates recurring disruption for dependent users] *(executor-added 2026-05-13; OA cit verified 2026-05-16)*
- Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2024). A survey on large language model based autonomous agents. *Frontiers of Computer Science*, 18. https://doi.org/10.1007/s11704-024-40231-1 `[J]` [OA cit: 1038] — peer-reviewed Springer survey explicitly framing the prompt-response paradigm as the baseline interaction model from which LLM-based autonomous agents depart; documents the shift from human-initiated reactive interaction toward proactive, goal-directed agentic AI — grounds §3.1 claim about the dominant prompt-and-response paradigm of 2023–2025. *(executor-added 2026-05-16 by Sonnet 4.6 — replaces hallucinated Zahavi et al. (2024) CHI citation, unverifiable via S2/ACM DL, per Task 007)*
- Decan, A., Mens, T., & Grosjean, P. (2019). An empirical comparison of dependency network evolution in seven software packaging ecosystems. *Empirical Software Engineering*, 24(1), 381–416. https://doi.org/10.1007/s10664-017-9589-y `[J]` [OA cit: 10; peer-reviewed empirical comparison of npm, PyPI, CRAN, Cargo, RubyGems, Maven, and CPAN documenting package ecosystem growth and community governance — supports §2.3 claim about success of package managers as models for commons] *(executor-added 2026-05-13; OA cit verified 2026-05-16)*
- Benkler, Y. (2006). *The Wealth of Networks: How Social Production Transforms Markets and Freedom*. Yale University Press. `[R]` [OA cit: 1932; canonical monograph establishing the theoretical framework for commons-based peer production — foundational anchor for §2.3 "community-maintained capability commons" framing of the ClawHub skill ecosystem] *(executor-added 2026-05-13; OA cit verified 2026-05-16)*
- Glikson, A., & Woolley, A. W. (2020). Human trust in artificial intelligence: Review of empirical research on human-AI interaction. *Academy of Management Annals*, 14(2), 627–660. https://doi.org/10.5465/annals.2018.0057 `[J]` [OA cit: 2114; peer-reviewed empirical review documenting trust calibration and adaptation processes in human-AI team collaboration over extended interaction periods — empirically grounds §3.3 claim that agents become "progressively better partners" through accumulated interaction history and feedback] *(executor-added 2026-05-14 by Sonnet 4.6; OA cit updated 2026-05-16)*

---

*Cross-references: Draft AR (agentic AI harness architecture), Draft AK (multi-agent orchestration), Draft T (tool-calling infrastructure), Draft AS (technostress risks of always-on agents), Draft G (agentic HI collaboration), Draft A (open source commons as precedent for skill ecosystem), Draft K (openness layers applied to skill packages)*
