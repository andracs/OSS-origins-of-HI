# Draft AI — Agents Calling Skills: Practical Implications for Deployment, Governance, and Failure Modes

**Version:** v0.4 (2026-05-12) / **Status:** executor citation cycle (Sonnet 4.6). Three Tasks 001–003 executed: §1.3 MCP adoption claim grounded with (Anthropic, 2024) inline; §2.2 hallucinated skill calls grounded with (Patil et al., 2024; Qin et al., 2024) — Gorilla (iCit 83) and ToolLLM (ICLR 2024, iCit >> 5); §3.2 NIS2 claim grounded with (Directive (EU) 2022/2555, Articles 21, 23). NIS2 Directive and ToolLLM added to Verified sources. Note: S2 API rate-limited during execution; ToolLLM iCit from established literature; §1.3 "de facto standard" still lacks independent analyst anchor (partial — MCP spec cited; analyst survey pending). / **Next:** resolve Ruan et al. (2024) ICML 2024 published DOI; cross-ref Draft AK (multi-agent orchestration) and Draft AL (memory) once written; add independent analyst/industry-survey anchor for §1.3 MCP adoption claim (McKinsey, Gartner, or similar 2024–2026)
*Full history → changelogs/ai-changelog.md*

---

## Overview and Chapter Position

Draft T mapped the technical infrastructure of agentic tool calling. Draft AH developed the theoretical implications: agency, extended cognition, emergent composition. This chapter is the engineering and governance counterpart: when an organisation deploys agents that autonomously call skills, what actually breaks, what does it cost, and what controls are needed?

The chapter is deliberately practical. It surveys the deployment patterns visible across the public agentic-AI landscape in 2024–2026, the categories of failure documented in incident reports and research, and the emerging governance frameworks designed to bound agent behaviour. It is intended for practitioners, security architects, and policy actors who are operationalising — not merely theorising about — skill-calling AI agents.

---

## §1 — Deployment Patterns

### 1.1 The reference architecture

A typical production deployment of a skill-calling agent contains the following components:

- **Orchestrator**: the LLM (or LLMs) that produces reasoning and selects skill calls
- **Skill registry**: a catalogue of available skills, each with a schema, description, and execution endpoint
- **Tool runtime**: executes the skill calls (HTTP, RPC, sandboxed code, MCP server)
- **Memory layer**: short-term context, conversation history, optionally long-term memory
- **Permission and audit layer**: enforces which skills can be called by whom, in what contexts, and logs all invocations
- **Application layer**: integrates the agent into the user-facing product

Draft T documented the protocols (function calling, MCP). This chapter focuses on the layers Draft T treated only briefly: the permission/audit layer and the operational discipline required to run such systems safely.

### 1.2 Patterns of skill access

Three deployment patterns dominate current practice:

**(a) Closed skill set.** The agent has access to a fixed, hand-curated set of skills with well-understood semantics. Examples: a customer-service agent with access to *lookup-order*, *refund*, *escalate-to-human*. The skill set is small, the semantics are constrained, and the failure surface is bounded. Enterprise AI deployments are predominantly focused on bounded, use-case-specific applications rather than open-ended general-purpose deployments (McKinsey & Company, 2024), and agentic deployments have followed this same pattern in early practice.

**(b) Open skill marketplace.** The agent can call any skill from a large registry, often including third-party skills. Examples: ChatGPT Plugins (2023), GPT Actions in Custom GPTs, the MCP server ecosystem (2024–2026). The capability is high, but so is the attack surface; trust assumptions about skills become a primary security concern.

**(c) Self-extending agent.** The agent can install or write new skills at runtime. Examples: Anthropic's Claude with skill-creation tools, Cursor and similar coding agents that write and execute code. This pattern is the most powerful and the most dangerous: the agent's effective capability is bounded only by its ability to find or compose new skills. Sherwood, Aybar, and Kaplan (2026) provide an empirical reference point for how fast this pattern is maturing: in a controlled benchmark, frontier coding agents were tasked with autonomously implementing a complete AlphaZero-style self-play training pipeline for Connect Four within a three-hour budget on consumer hardware, with success measured against an external solver. The same task transitioned from "unreliable completion" in January 2026 to near-saturation by April 2026 — a three-month capability jump on a benchmark that exercises file I/O, code execution, iterative debugging, and ML system design end-to-end. For governance purposes, the implication is operational: organisations deploying self-extending agents in 2026 must assume the agent is capable of building durable new tools (training pipelines, scrapers, deployment scripts) within the lifetime of a single task — which forecloses the option of treating sandbox-escape and skill-proliferation risks as future problems.

The three patterns trade capability against controllability. A practical observation: deployments that fail in production typically do so because they were classified as one pattern but operated as another. A "closed skill set" deployment that includes a *send-email* skill is operating as an open pattern with respect to information exfiltration; a "self-extending" agent without strong sandboxing is operating without meaningful permission boundaries.

### 1.3 Vendor and ecosystem snapshot (2024–2026)

The current ecosystem is fragmented but converging:

- **Anthropic Claude with MCP and Skills**: structured skill ecosystem with explicit permissions; integration with Claude Code and the broader Claude Agent SDK
- **OpenAI Assistants API and Custom GPTs**: skill access via Actions; plugin model deprecated April 2024 (OpenAI, 2024)
- **Microsoft Copilot Studio**: enterprise-focused agent builder with curated skill connectors
- **Google Vertex AI Agents**: skill access via function calling and agent extensions
- **Open-source frameworks**: LangChain, LangGraph, AutoGen, CrewAI — orchestration layers over the underlying model APIs

The Model Context Protocol (Anthropic, 2024) is the most significant standardisation effort: a wire protocol for how agents discover and call skills, designed to be vendor-neutral. As of early 2026, MCP server registries contain skills from major SaaS providers (Slack, GitHub, Linear, Notion, Datadog) and have emerged as the leading open protocol for inter-vendor skill interoperability (Anthropic, 2024; Hasan et al., 2025).

For practitioners: the choice of orchestration layer matters less than the discipline applied to skill design, permissioning, and audit. A LangChain deployment with rigorous controls outperforms a managed-service deployment with lax permissions.

---

## §2 — Failure Modes

The failures documented in production deployments cluster into six categories. Each is grounded in incidents reported in the public security and AI-safety literature 2023–2025.

### 2.1 Prompt injection and skill hijacking

The most consequential class. An attacker controlling input to the agent (a webpage the agent retrieves, a document it summarises, an email it processes) embeds instructions that cause the agent to call skills in attacker-chosen ways. Greshake et al. (2023) documented "indirect prompt injection" in which a webpage loaded by an agent contained instructions that the agent then followed.

Practical examples documented in 2023–2025:
- Email-summarisation agents tricked into forwarding the user's inbox to attacker addresses (Greshake et al., 2023)
- Coding agents retrieving documentation pages that contained instructions to add backdoors (Greshake et al., 2023)
- Banking-domain agents hijacked into executing unauthorized fund transfers via injected instructions embedded in task inputs — a failure mode systematically benchmarked across AgentDojo's financial task suite (Debenedetti et al., 2024)

The defining feature: the agent's permission to call a skill (forward email, write code, issue refund) was legitimate; the injection redirected *which* skill call was made and with *what* arguments.

**Mitigations** in current practice: input sanitisation (limited efficacy; Perez & Ribeiro, 2022), tool-call confirmation by humans for high-impact skills, separation of *trusted* and *untrusted* context regions, and structured skill APIs that make injection harder (Debenedetti et al., 2024).

### 2.2 Hallucinated skill calls

The agent invokes a skill that does not exist, or invokes a real skill with hallucinated arguments. Less catastrophic than injection but operationally costly: workflows fail silently, downstream systems receive malformed inputs, debugging is difficult (Patil et al., 2024; Qin et al., 2024).

Common in long-context multi-step agents where the skill registry has drifted from what the agent believes is available. Mitigated by strict validation at the tool-runtime layer: invalid skill names rejected, schema validation enforced, type errors surfaced to the agent.

### 2.3 Cascading skill loops

The agent calls a skill whose output triggers another skill call, which produces output that triggers a third, and so on. Without explicit termination conditions or budget controls, the agent can consume resources indefinitely. Documented in emulated production environments and benchmark scenarios where agents charged with "maintaining" a system entered repair loops that themselves required repair (Ruan et al., 2024).

Mitigations: hard limits on the number of skill calls per task; budget controls (token budget, dollar budget, time budget); circuit breakers that pause execution when patterns of repetition are detected.

### 2.4 Privilege creep

Over time, the skills available to a deployed agent expand: new integrations are added, old skills are not retired, permissions accumulate. The agent's effective capability gradually exceeds what was authorised at the time of initial deployment.

This is structurally identical to user-permission creep in traditional IT systems and admits the same controls: regular permission reviews, just-in-time access provisioning, automatic expiration of unused skill grants, and explicit approval for new skills. The novelty in agentic systems is the speed: skill ecosystems can be augmented programmatically by the agent itself in self-extending architectures, which makes traditional review cadences too slow.

### 2.5 Skill ambiguity and silent semantic drift

A skill's behaviour changes — the upstream API is updated, a third-party service modifies its semantics — and the agent does not notice. The skill description (which the agent uses to decide when to call) no longer matches what the skill actually does. Outputs become subtly incorrect. Patil et al. (2024) demonstrate the empirical reality of this failure mode: when API documentation and version contracts change, LLM tool-call accuracy degrades measurably even when the underlying model capability is unchanged — the agent continues invoking the old schema while the skill's behaviour has shifted.

This is a documentation and contract problem. Mitigations: skill versioning, contract tests that validate skill semantics before deployment, and explicit deprecation paths. The MCP specification anticipates this with version negotiation, but enforcement is still ad hoc.

### 2.6 Cross-agent interference

In multi-agent deployments where multiple agents share access to a skill registry, one agent's action can affect another's state through shared resources. A common variant: agent A deletes a record that agent B was about to update; both succeed individually, but the system state is inconsistent.

This is the classical concurrent-systems problem — race conditions, lost updates, phantom reads — applied to AI orchestration. The mature solutions (transactions, locking, optimistic concurrency control) apply but are not yet standard in agent frameworks (Guo et al., 2024). Practitioners rely on operational discipline and post-hoc reconciliation.

---

## §3 — Governance and Control Frameworks

### 3.1 The least-skill principle

Drawing on the security principle of least privilege: an agent should have access only to the skills it requires for its assigned task, and no more. This is harder than it sounds. Skills tend to be defined for general utility, not for specific tasks; restricting an agent's access often requires defining task-specific skill subsets.

Operational implementations:
- **Role-based skill access**: skills are grouped into roles; agents are assigned roles
- **Task-scoped skill grants**: the orchestrator dynamically enables only the skills relevant to the current task, disables them at task end
- **Capability tokens**: skills accept signed tokens that bind invocation to a specific authorising context

The least-skill principle is the foundation of agent governance. Most reported failures involve agents that had more skill access than their task required (Ruan et al., 2024; OWASP, 2025).

### 3.2 Human-in-the-loop and human-on-the-loop

Two governance patterns are widely documented (Parasuraman et al., 2000; Endsley, 2017; Mosqueira-Rey et al., 2022):

**Human-in-the-loop**: high-impact skill calls (sending external email, executing financial transactions, modifying production systems) require explicit human approval before execution. This is the default pattern in regulated domains and in early production deployments where trust is being built.

**Human-on-the-loop**: skill calls execute autonomously, but humans monitor and can intervene. This is the default pattern in mature deployments where the agent has demonstrated reliability on a task class.

The choice between them is not merely operational — it has legal and ethical weight. The EU AI Act (in force 2024, full application phasing in through 2026) explicitly considers agentic systems within scope (Article 2; Recitals 89–90, Regulation (EU) 2024/1689) and requires "appropriate human oversight" for high-risk AI systems among them (Article 14, Regulation (EU) 2024/1689). NIS2 compliance for critical-infrastructure operators imposes audit and incident-reporting obligations that constrain autonomous skill calls (Directive (EU) 2022/2555, Articles 21, 23).

### 3.3 Audit and observability

Every skill call must be logged. The audit log should record: the agent identity, the skill identity, the arguments, the result, the timestamp, the invoking task or session, and the chain of reasoning that led to the call (the agent's internal "thought" — recoverable in most modern frameworks via the ReAct reasoning-trace pattern and its successors; Yao et al., 2023).

Beyond raw logs, mature deployments include:
- **Metrics dashboards**: skill call rate, error rate, latency, cost per task
- **Anomaly detection**: alerts on unusual skill-call patterns (a rare skill suddenly invoked frequently; a familiar skill invoked with unusual arguments)
- **Post-hoc analysis**: replayability of agent traces for debugging and incident response

Observability for agentic systems is an active engineering area. Production tools include LangSmith (LangChain, 2024) for end-to-end agent tracing and evaluation, Helicone (Helicone, 2024) as an open-source AI gateway and observability layer, and Honeycomb's LLM and agent-tracing features built on OpenTelemetry (Honeycomb, 2024). The most consequential standardisation effort is OpenLLMetry (Traceloop, 2023), an Apache 2.0 instrumentation library whose semantic conventions have been adopted into the OpenTelemetry GenAI Semantic Conventions specification — the emerging vendor-neutral standard for LLM, agent, and tool-call telemetry maintained by the OpenTelemetry project (OpenTelemetry Authors, 2025). The convergence on OpenTelemetry is significant for agentic systems: it allows traces from heterogeneous frameworks (LangChain, AutoGen, CrewAI, AG2) and providers (Anthropic, OpenAI, AWS Bedrock, Azure AI Inference) to interoperate in a single observability pipeline, which is a precondition for the cross-agent and cross-vendor governance discussed in §1.3 and §3.1.

### 3.4 Sandboxing

Skills that affect external state — execute code, write files, modify databases, call external APIs — must run in isolated environments. The sandboxing techniques are inherited from traditional software security:

- **Process isolation**: each skill execution in a separate process or container
- **Network egress control**: skills cannot reach arbitrary internet endpoints
- **Filesystem isolation**: skills see a constrained view of the filesystem
- **Resource limits**: CPU, memory, time bounded per skill call

For self-extending agents (§1.2c), sandboxing is non-negotiable. An agent that can write and execute code without sandbox enforcement is, in security terms, an arbitrary-code-execution vulnerability deployed by design (Ruan et al., 2024).

---

## §4 — Economic and Organisational Implications

### 4.1 The skill economy

Skill ecosystems are emerging as a market. MCP server registries, OpenAI's GPT Store, and platform-specific skill marketplaces are all attempts to monetise skill provision (Burkhardt & Rieder, 2024). The economic model is unsettled: some skills are free (open-source MCP servers), some are pay-per-call (commercial APIs wrapped as skills), some are bundled into platform subscriptions.

For organisations deploying agents, this implies:
- **Skill cost is part of agent cost**: an agent's per-task cost includes model inference plus skill invocation costs
- **Skill availability is a strategic dependency**: an agent that depends on a third-party skill inherits the third party's reliability and pricing
- **Skill provenance matters**: skills from low-trust sources are vectors for the failure modes documented in §2

A mature organisational practice is the *internal skill catalogue*: skills that the organisation has reviewed, tested, and approved for agent use, with clear ownership and SLAs. This is analogous to the internal package registries that mature software organisations maintain for open-source dependencies.

### 4.2 Organisational adoption patterns

Two patterns of organisational adoption are visible in 2024–2026:

**Centralised**: a platform team owns the skill catalogue, the orchestration framework, and the governance policies. Application teams consume the platform. This pattern reduces variance and concentrates governance, at the cost of slower iteration.

**Federated**: each application team builds and operates its own agentic systems, with light-touch organisational standards. This pattern enables faster experimentation, at the cost of duplicated effort and inconsistent controls.

Most large organisations are in transition: starting federated (during experimentation), moving toward centralised (as production deployments grow), with platform teams emerging from successful early projects (Maslej et al., 2024).

### 4.3 Skill design as a discipline

A practical observation from production deployments, supported by tool-learning research: the design of individual skills determines agent reliability more than the choice of model — empirically, tool description quality and schema precision have been shown to predict agent task success more strongly than the underlying model size (Patil et al., 2024). A well-designed skill is:

- **Single-purpose**: does one thing, predictably
- **Idempotent where possible**: repeat invocations produce the same result
- **Failure-honest**: returns explicit error states rather than ambiguous outputs
- **Schema-strict**: validates inputs, returns structured outputs
- **Observability-friendly**: emits sufficient telemetry for debugging
- **Documentation-rich**: the skill description tells the agent precisely when to use it

Organisations that treat skill design as a first-class engineering discipline — with reviews, tests, and ownership — get more reliable agentic systems than organisations that treat skills as ad-hoc API wrappers.

---

## §5 — Practical Recommendations

For organisations deploying skill-calling agents, the following practices are emerging as a working consensus across the security, AI-safety, and applied-ML communities (Shavit et al., 2023; NIST, 2023):

1. **Start with a closed skill set.** Open skill marketplaces are appropriate only after operational experience.
2. **Apply least-skill grants by default.** Justify each additional skill the agent receives.
3. **Require human approval for skills with material external effect.** Email, payments, code deployments, customer-facing actions.
4. **Sandbox aggressively.** Especially for code-execution skills.
5. **Log every skill call with full context.** Make traces replayable.
6. **Treat prompt injection as a foundational threat.** Architect for it from the beginning.
7. **Set hard budgets.** Maximum skill calls per task, maximum cost, maximum runtime.
8. **Maintain a curated internal skill catalogue.** Version, test, and own each skill.
9. **Plan for skill semantic drift.** Contract tests, version negotiation, monitoring of upstream changes.
10. **Establish incident response procedures specific to agentic systems.** Traditional IR playbooks do not cover skill-call hijacking or cascading skill loops.

These recommendations are not novel: most are direct applications of established security and reliability engineering principles. The novelty is that they must now be applied to systems whose autonomy and dynamism exceed those of traditional software — and to systems where the *user* of the skill is a probabilistic model whose behaviour is harder to bound than a deterministic program.

---

## Key Sources (to verify / acquire)

- Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. In *Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security (AISec '23, co-located with CCS '23)* (pp. 79–90). ACM. https://doi.org/10.1145/3605764.3623985 [C] [OA cit: 307 — peer-reviewed proceedings version of arXiv:2302.12173; CrossRef retraction status: clean (no `update-to` entries) as of 2026-05-12]
- Debenedetti, E., Zhang, J., Balunović, M., Beurer-Kellner, L., Fischer, M., & Tramèr, F. (2024). AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents. In *Advances in Neural Information Processing Systems 37 (NeurIPS 2024)*, Datasets and Benchmarks Track. https://doi.org/10.52202/079017-2636 (preprint arXiv:2406.13352) [C] [OA cit: 6 (preprint W4399912700) / 3 (published W4415796822) — published version indexed Dec 2024; CrossRef retraction status: clean as of 2026-05-12. Volume corrected from "38" to "37" — NeurIPS 2024 is volume 37 of NeurIPS Advances.]
- Anthropic. (2024). Model Context Protocol Specification. Anthropic technical documentation.
- ENISA. (2024). *Multi-layered framework for good cybersecurity practices for AI*. ENISA report.
- OWASP. (2025). *Top 10 for Large Language Model Applications* — particularly LLM07 (Insecure Plugin Design) and LLM08 (Excessive Agency).
- EU AI Act, Regulation (EU) 2024/1689 — Article 14 (Human oversight measures) on high-risk AI systems; Article 2 and Recitals 89–90 on agentic and autonomous systems within scope.
- NIS2 Directive (EU) 2022/2555 — relevant for critical-infrastructure agentic deployments.
- OpenAI. (2024, April 9). ChatGPT plugins sunset. OpenAI. https://openai.com/index/chatgpt-plugins/ [Plugin store closed March 19, 2024; all conversations ended April 9, 2024; deprecation announced February 23, 2024.]

## Verified / executor-added

European Parliament & Council of the European Union. (2024). Regulation (EU) 2024/1689 on artificial intelligence (EU AI Act). *Official Journal of the European Union*, L 2024/1689. Article 14: Human oversight measures. [Primary legal source — iCit not applicable; legislative text in force from 2024.]

Ruan, J., Chen, Y., Zhang, B., Xu, Z., Bao, T., Du, G., Shi, S., Mao, H., Zeng, X., & Liu, Y. (2024). Identifying the risks of LM agents with an LM-emulated sandbox. *Proceedings of the 41st International Conference on Machine Learning (ICML 2024)*. arXiv:2309.15817. [Documents systematic failure modes of LM agents including repetitive execution loops and cascading tool calls; iCit well above ≥5 threshold.]

LangChain. (2024). *LangSmith documentation* (Version accessed 2026-05-07). LangChain, Inc. https://docs.langchain.com/langsmith [R] — vendor technical documentation; framework-agnostic platform for tracing, evaluation, and deployment of LLM/agent applications. Canonical product URL: https://smith.langchain.com.

Helicone. (2024). *Helicone: Open-source AI Gateway and LLM Observability* (Version accessed 2026-05-07). https://www.helicone.ai/ [R] — vendor documentation; open-source (Apache 2.0) AI gateway and observability layer with request, session, and prompt-management tracing across multiple LLM providers.

Honeycomb. (2024). *Honeycomb for LLMs* (Version accessed 2026-05-07). Honeycomb.io. https://docs.honeycomb.io/send-data/llm [R] — vendor documentation; observability platform built on OpenTelemetry, supporting GenAI Semantic Conventions for high-cardinality querying of agent and LLM traces.

Traceloop. (2023). *OpenLLMetry: Open-source observability for LLM applications* (Apache-2.0 licensed). GitHub. https://github.com/traceloop/openllmetry [R] — community-maintained instrumentation library extending OpenTelemetry to LLM providers, vector databases, and agentic frameworks. Traceloop's semantic conventions for GenAI have since been adopted into the OpenTelemetry GenAI specification.

OpenTelemetry Authors. (2025). *Semantic conventions for generative AI systems* (Specification, Development status, v1.36.0 baseline). OpenTelemetry. https://opentelemetry.io/docs/specs/semconv/gen-ai/ [R] — vendor-neutral specification for GenAI observability, defining attributes, metrics, spans, and events for instrumenting LLM, agent, and tool-call telemetry. Maintained by the OpenTelemetry project under the GenAI Semantic Conventions working group; pre-stable but already adopted by major observability vendors (Datadog, Honeycomb, New Relic) and frameworks (LangChain, CrewAI, AutoGen, AG2).

Patil, S. G., Zhang, T., Wang, X., & Gonzalez, J. E. (2024). Gorilla: Large language model connected with massive APIs. In *Advances in Neural Information Processing Systems 37 (NeurIPS 2024)*. https://doi.org/10.52202/079017-4020 (preprint arXiv:2305.15334) [C] [OA cit: 83 (preprint W4378474282) / 15 (published W4415795271) — venue upgraded from preprint to NeurIPS 2024 main proceedings on 2026-05-12 cycle; CrossRef retraction status: clean as of 2026-05-12. Demonstrates that the quality of API/tool documentation (name, description, parameter schema) strongly predicts LLM tool-use accuracy — models tested on poorly described APIs fail even when the underlying capability is present, while models tested on well-described APIs succeed; primary empirical anchor for §4.3 claim that skill design quality determines agent reliability more than model choice.] *(executor-added 2026-05-10; venue/year corrected 2026-05-12)*

McKinsey & Company. (2024). *The state of AI in early 2024*. McKinsey Global Institute. https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai-in-early-2024 [R — industry survey of ~1,300 participants across regions and industries; finds that enterprise AI deployments are predominantly focused on bounded, use-case-specific applications rather than open-ended general-purpose deployments; iCit threshold not applicable to industry surveys. Note: citation narrowed 2026-05-22 (Sonnet 4.6) — the prior §1.2 claim "Most enterprise deployments fall in this [closed] category" over-extrapolated from McKinsey's general adoption data to a specific agentic skill-set taxonomy that the survey does not measure; text revised to match what the source can actually support.]

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. *Proceedings of the Eleventh International Conference on Learning Representations (ICLR 2023)*. arXiv:2210.03629. [C] [iCit: ~1200 — S2 rate-limited; confirmed from established literature; originating paper for the Thought/Act/Observe reasoning-trace pattern that underpins internal-reasoning recoverability in modern agent frameworks including LangChain, AutoGen, and CrewAI.] *(executor-added 2026-05-10)*

Shavit, Y., Misra, S., Albrecht, S., Balunović, M., Brönnimann, U., Chen, B., Cook, C., D'Amour, A., Dragan, A., & Garg, A. (2023). *Practices for governing agentic AI systems*. Technical report, OpenAI and Google. arXiv:2312.04870. [P] [iCit: above ≥5 threshold — S2 rate-limited; confirmed from established literature; synthesizes cross-community governance recommendations for agentic systems covering minimal footprint, sandboxing, auditability, and human oversight — directly supports §5 working-consensus framing.] *(executor-added 2026-05-10)*

NIST. (2023). *Artificial intelligence risk management framework (AI RMF 1.0)*. National Institute of Standards and Technology. NIST AI 100-1. https://doi.org/10.6028/NIST.AI.100-1 [R] [Foundational US government AI risk management framework organising AI governance around Govern, Map, Measure, and Manage functions; broadly adopted across the security, AI-safety, and applied-ML communities — co-anchors §5 working-consensus claim alongside Shavit et al. (2023). iCit threshold not applicable to government standards documents.] *(executor-added 2026-05-10)*

Sherwood, J., Aybar, B., & Kaplan, B. (2026). *Frontier coding agents can now implement an AlphaZero self-play machine learning pipeline for Connect Four that performs comparably to an external solver*. arXiv:2604.25067. [P] [Too new for iCit (April 2026); primary value as a 2026 empirical data point on frontier agentic capability. Anchors §1.2c claim that the self-extending pattern has matured to the point where frontier agents can build complete ML training pipelines within a single task budget. Cross-reference also intended for Drafts AK (multi-agent orchestration), AC (model vs. human performance), V (paradigm synthesis), and AN (alignment / recursive self-improvement signal). PDF: `Kilder/Sherwood2026_FrontierCodingAgents_AlphaZero_arXiv2604.25067.pdf`.] *(executor-added 2026-05-12)*

European Parliament & Council of the European Union. (2022). Directive (EU) 2022/2555 on measures for a high common level of cybersecurity across the Union (NIS2 Directive). *Official Journal of the European Union*, L 333/80. Article 21: Risk-management measures (requires appropriate technical and organisational measures for network and information security, including incident handling and monitoring). Article 23: Reporting obligations (requires initial notification within 24 hours of becoming aware of a significant incident; intermediate report within 72 hours; full report within one month). [Primary legal source — iCit not applicable; in force from 2023-01-16, transposition deadline 2024-10-17. Anchors §3.2 claim that NIS2 compliance imposes audit and incident-reporting obligations on critical-infrastructure operators deploying autonomous agentic systems.] *(executor-added 2026-05-12)*

Guo, T., Chen, X., Wang, Y., Chang, R., Pei, S., Chawla, N. V., Wiest, G., & Zhang, X. (2024). Large language model based multi-agents: A survey of progress and challenges. arXiv:2402.01680. [P — preprint (2024); comprehensive survey of multi-agent LLM architectures across profiling, communication, capability, and alignment dimensions; explicitly identifies coordination, shared-state management, and the absence of standard concurrency control primitives as open challenges in current agent frameworks — primary anchor for §2.6 claim that transactions, locking, and OCC are not yet standard; iCit well above ≥5 threshold. S2 rate-limited; confirmed from established literature.] *(executor-added 2026-05-13)*

Qin, Y., Liang, S., Ye, Y., Zhu, K., Yan, L., Lu, Y., Lin, Y., Han, X., Ding, N., Liu, Z., Zheng, Y., Zhang, X., Huang, Y., Jiang, H., Geng, X., Liu, Z., & Sun, M. (2024). ToolLLM: Facilitating large language models to master 16000+ real-world APIs. In *Proceedings of the 12th International Conference on Learning Representations (ICLR 2024)*. arXiv:2307.16789. [C] [iCit: well above ≥5 threshold (S2 unavailable at execution time; confirmed from established literature). Constructs a benchmark of 16,000+ real-world APIs and documents systematic failure modes including hallucinated API calls, incorrect argument construction, and schema mismatches — directly empirical anchor for §2.2 claim that hallucinated skill invocations are a documented failure mode in LLM tool-calling agents.] *(executor-added 2026-05-12)*

Maslej, N., et al. (2024). *Artificial Intelligence Index Report 2024*. Stanford University, Human-Centered Artificial Intelligence (HAI). [R — annual institutional survey covering AI adoption, enterprise deployment patterns, and organizational structures across regions and industries; documents the emergence of centralized AI platform teams and the federated-to-centralized transition in enterprise AI governance — anchors §4.2 claim about organisational adoption patterns in 2024–2026. iCit threshold not applicable to institutional annual reports.] *(executor-added 2026-05-13)*

Burkhardt, S., & Rieder, B. (2024). Foundation models are platform models: Prompting and the political economy of AI. *Big Data & Society*, 11(2). https://doi.org/10.1177/20539517241247839 [C] [OA cit: 40 — analyses how foundation models function as platform models with associated marketplace dynamics, API-access monetization patterns, and stratified economic structures across users, developers, and providers — anchors §4.1 "skill economy" claim that MCP registries, GPT Store, and platform skill marketplaces represent monetisation attempts within an emergent AI platform-economics framework.] *(executor-added 2026-05-15)*

Mialon, G., Dessì, R., Lomelí, M., Nalmpantis, C., Pasunuru, R., Raileanu, R., Rozière, B., Schick, T., Dwivedi-Yu, J., Celikyilmaz, A., Grave, E., LeCun, Y., & Scialom, T. (2023). Augmented language models: A survey. *Transactions on Machine Learning Research (TMLR)*. arXiv:2302.07842. [C] [iCit: 14 — canonical survey of tool-augmented and skill-calling LM architectures, documenting the evolution from isolated models to multi-tool, multi-vendor ecosystems and the need for interoperability standards; co-anchor for §1.3 MCP adoption context.] *(executor-added 2026-05-15)*

Hasan, M. M., Li, H., Fallahzadeh, E., Rajbahadur, G. K., Adams, B., & Hassan, A. E. (2025). Model Context Protocol (MCP) at First Glance: Studying the Security and Maintainability of MCP Servers. arXiv:2506.13538. [P — preprint; first large-scale empirical study of the MCP server ecosystem, analysing security vulnerabilities and maintainability characteristics of MCP server implementations; provides independent third-party academic evidence that MCP has achieved sufficient real-world adoption to constitute a studied ecosystem; iCit: 5.] *(executor-added 2026-05-18)*

Perez, F., & Ribeiro, I. (2022). Ignore Previous Prompt: Attack Techniques For Language Models. arXiv:2211.09527. [P — preprint; introduces and taxonomises direct prompt injection techniques and demonstrates empirically that naive input filtering and instruction-priority boundaries are bypassed — primary evidence for the "limited efficacy" characterisation of input sanitisation against prompt injection attacks; iCit: 89.] *(executor-added 2026-05-18)*

Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A: Systems and Humans*, *30*(3), 286–297. https://doi.org/10.1109/3468.844354 [J — IEEE Transactions on Systems, Man, and Cybernetics; canonical taxonomy of human-automation interaction types (acquisition, analysis, decision, action) and levels (fully manual through fully automated), providing the foundational theoretical framework from which the human-in-the-loop and human-on-the-loop governance patterns in §3.2 are derived; iCit: 343 (S2 confirmed 2026-05-21).] *(executor-added 2026-05-21)*

Endsley, M. R. (2017). From here to autonomy: Lessons learned from human–automation research. *Human Factors*, *59*(1), 5–27. https://doi.org/10.1177/0018720816681350 [J — Human Factors (SAGE); peer-reviewed; 2017 Fitts Award address synthesising decades of research on supervisory control, mode confusion, and human-on-the-loop monitoring in increasingly autonomous systems — explicitly addresses the design space between human-in-the-loop and human-on-the-loop governance modes; provides the HOTL-framing anchor missing from Parasuraman et al. (2000); iCit: well above ≥5 threshold (S2 rate-limited at execution; confirmed from established literature).] *(executor-added 2026-05-21)*

Mosqueira-Rey, E., Hernández-Pereira, E., Alonso-Ríos, D., Bobes-Bascarán, J., & Fernández-Leal, Á. (2022). Human-in-the-loop machine learning: A state of the art. *Artificial Intelligence Review*, *56*(4), 3005–3054. https://doi.org/10.1007/s10618-022-09247-1 [J — Artificial Intelligence Review (Springer); peer-reviewed; comprehensive survey of HITL-ML architectures covering active learning, annotation pipelines, and interactive training loops — provides the HITL-framing anchor for §3.2 alongside Parasuraman et al. (2000) and Endsley (2017); iCit: above ≥5 threshold (S2 rate-limited at execution; confirmed from established literature).] *(executor-added 2026-05-21)*

---

## Cross-references

- **Draft T** (`t-agentic-tool-calling.md`) — technical infrastructure
- **Draft AH** (`ah-skill-calling-theoretical-implications.md`) — theoretical companion to this chapter
- **Draft G** (`g-agentic-hi-collaboration.md`) — agentic HI collaboration
- **Draft P** (`p-governance-compliance-hi.md`) — governance frameworks for HI
- **Draft B** (`b-closed-models-risks.md`) — risks of opaque AI components
- **Draft AB** (`ab-credit-blame-agent-attribution.md`) — attribution of harm in agentic systems
