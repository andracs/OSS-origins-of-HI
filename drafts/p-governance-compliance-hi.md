# Draft P — Governance and Compliance for Hybrid Intelligence

**Version:** v0.3 (2026-05-11)  
**Status:** v0.3 — regulatory mapping and governance frameworks with sector-specific depth in §1.3 (NYC LL 144 implementation evidence) and a new §5 on audit and verification methodology. 2026-05-11 cycle: added empirical NYC LL 144 compliance findings (Wright et al., 2024; Groves et al., 2024); introduced three-layered LLM audit framework (Mökander et al., 2023) and assurance-audit framework (Lam et al., 2024); downloaded Santoni de Sio & van den Hoven (2018) PDF; refreshed OpenAlex citation counts on five anchors.

---

## Overview and Chapter Position

Hybrid intelligence creates a governance vacuum: existing regulation is designed for either *human* decision-making (accountability clearly placed) or *autonomous* AI (technical audit requirements). HI falls between: accountability is distributed between human actors and AI components in a way that fits no existing category.

This draft maps: (1) the regulatory frameworks relevant to HI, (2) the specific governance challenges HI raises, (3) organisational compliance mechanisms, and (4) what regulation has yet to address in order to make HI governance meaningful.

The draft connects directly to `m-agentic-ai-taxonomies.md` (autonomy levels as the regulatory pivot), `b-closed-models-risks.md` (closed infrastructure as a governance problem), `e-llm-structural-vulnerabilities.md` (security vulnerabilities as compliance requirements) and `d-open-source-organization.md` (organisational governance patterns).

---

## Part 1: The central regulatory frameworks

### 1.1 EU AI Act (2024) — risk categorisation

The EU AI Act is the first binding horizontal AI regulation and the most ambitious regulatory framework globally. It categorises AI systems in four risk levels:

| Risk level | Examples | Requirements |
|---|---|---|
| Unacceptable risk | Social scoring, subliminal manipulation | Prohibited |
| High risk | Critical infrastructure, education, employment, law enforcement, migration, medical | Conformity assessment, registration, transparency, human oversight |
| Limited risk | Chatbots, deepfakes | Disclosure obligations |
| Minimal risk | Spam filters, AI in games | No requirements |

**The HI problem in the AI Act:** The Act regulates AI *systems*, not HI *configurations*. A system classified as "high risk" is subject to requirements for "meaningful human oversight" — but what constitutes meaningful oversight is not operationally defined. A radiologist approving AI diagnoses in two seconds per image formally satisfies the requirement but is effectively HOOTL (Human-Out-Of-The-Loop).

**General-Purpose AI (GPAI) — the special case:**  
Foundation models (GPT-4, Claude, Llama) are treated under the GPAI provisions. Requirements for transparency documentation, copyright compliance and safety evaluation for systems with "systemic risk" (>10^25 FLOP). This directly affects HI systems built on GPAI components.

### 1.2 NIST AI Risk Management Framework (2023)

The NIST AI RMF is not binding regulation but a widely adopted framework, particularly in the USA and in public procurement. Structured around four core functions:

- **Govern**: establish policies, roles, accountability allocation
- **Map**: identify and classify AI risks in context
- **Measure**: assess and monitor risks quantitatively/qualitatively
- **Manage**: handle and reduce risks on an ongoing basis

For HI the *Map* function is particularly relevant: it requires explicitly identifying *who* in the system (human or AI) makes which decisions, and what risks follow from this distribution. The NIST RMF contains no specific guidelines for HI, but the framework is flexible enough to be applied.

### 1.3 Sector-specific regulation

**Medicine (FDA, MDR):**  
The FDA's *Software as a Medical Device* (SaMD) regulation and the EU's Medical Device Regulation (MDR) require clinical validation of AI components in diagnostic systems. But they regulate the AI component, not the HI system as a whole. A physician using an FDA-approved AI diagnostic tool is not subject to special regulation for the overall decision process.

**Finance (ESMA, SEC, BaFin):**  
Algorithmic trading and AI-assisted credit assessment are subject to sector-specific regulation (MiFID II in the EU; Dodd-Frank in the USA). Common requirements: auditability, "kill-switch" capability, stress testing. HI systems in finance are generally better regulated than in other sectors due to the maturity of sectoral regulation.

**Legal system:**  
AI risk-assessment tools (COMPAS and similar) are used in the USA for sentencing and parole decisions. Regulation is minimal and primarily procedural (disclosure requirements in some states). The EU AI Act will classify these as high-risk and require impact assessment.

**Employment:**  
AI in recruitment and performance assessment is under increasing regulatory focus. NYC Local Law 144, in force from July 2023, requires that *automated employment decision tools* (AEDTs) used in hiring or promotion within New York City be independently bias-audited annually for race and gender disparate impact, with the audit summary publicly posted and a transparency notice given to applicants. It is the first operational example of a jurisdiction-specific algorithmic compliance regime.

Early implementation evidence is sobering. Wright et al. (2024), in a study of 391 NYC employers conducted by 155 student investigators, found that only 18 employers posted an audit report and only 13 posted the required transparency notice. The authors term this "null compliance": because the law leaves the in-scope determination to the employer, a missing audit cannot be distinguished from a non-applicable system. Nearly all of the audits that were posted reported an impact ratio above the 0.8 four-fifths rule of thumb, raising further questions about audit independence. Groves et al. (2024), interviewing 17 auditors and practitioners working within the regime, identify four structural failures: vague statutory definitions of both "AEDT" and "independent auditor", a faulty transparency-driven theory of change, narrowing of the in-scope class by industry lobbying, and auditor difficulty obtaining access to vendor data. The implication for HI governance is direct: compliance regimes that rely on regulated parties to self-classify, with transparency as the only enforcement lever, fail to deter the behaviour they target — a pattern that the EU AI Act's deployer-provider obligations will need to anticipate.

### 1.4 Standardisation organisations

- **ISO/IEC 42001** (2023): AI management system standard — a certifiable framework for organisational AI governance
- **ISO/IEC 23053**: Framework for AI systems using machine learning
- **IEEE 7000 series**: Ethical design standards for autonomous systems
- **CEN/CENELEC**: European standardisation bodies developing harmonised standards under the AI Act

These standards are under-utilised in the HI context — they primarily address isolated AI systems.

---

## Part 2: HI-specific governance challenges

### 2.1 The accountability problem — *responsibility gaps*

When an HI system fails, it is unclear who bears accountability:
- The AI developer (fault in the model)?
- The system integrator (fault in the HI configuration)?
- The human operator (fault in the judgement of AI output)?
- The organisation (fault in governance design)?

Matthias's (2004) concept of the *responsibility gap* — originally formulated for learning automata — describes the phenomenon that no single actor bears full accountability for an autonomous system's actions, because the system's behaviour emerges from training rather than direct programming. Santoni de Sio & Mecacci (2021) extend the analysis to four distinct gap types in contemporary AI: culpability, moral, public, and active responsibility gaps. This is not merely a philosophical problem but a practical compliance problem: existing tort law and criminal-law accountability placement presupposes an identifiable responsible actor.

**The EU AI Act's answer:** The provider (*provider*) of the AI system bears primary accountability; the user (*deployer*) has secondary accountability. But this addresses the AI component, not the HI system — and in practice the provider and the deployer are often not identical actors.

### 2.2 Meaningful human oversight — operationalisation

"Meaningful human oversight" is central to the AI Act and NIST RMF, but operationally indefinable. What makes oversight meaningful?

Santoni de Sio & van den Hoven (2018) provide the philosophical foundation for *meaningful human control* and propose two structural conditions: a "tracking" condition (the system's behaviour must respond to the relevant moral reasons of the controlling humans) and a "tracing" condition (system actions must be traceable to a specifically located human in the design and operation chain). Building on this, Cheruvu (2026) and Bensch et al. (2025) — both chapters in the *Springer Handbook of Human-Centered AI* — operationalise three practical criteria for HI deployments:
1. **Competence**: the human actor must have the capacity to assess AI output — not merely approve it formally
2. **Time**: there must be sufficient time for real assessment — not rubber-stamping
3. **Consequence**: the human actor's assessment must actually be able to change the system's behaviour

All three are underspecified in existing regulation. A medical system that requires a physician's signature on 200 AI diagnoses per hour formally satisfies the AI Act's oversight requirement.

### 2.3 Transparency and explainability

The AI Act requires transparency for high-risk systems: users must be informed that they are interacting with AI, and the system must provide explanations for decisions. But explainability in the HI context is more complex than for autonomous systems:

- Who should be explained what — the end user, the human operator, the regulator?
- An explanation of the AI component is not an explanation of the HI system's overall decision
- Post-hoc explanations (LIME, SHAP, TCAV) describe the model's behaviour, not its reasoning

Liesenfeld et al. (2024) on "openwashing" is relevant: just as openness claims can be misleading, transparency compliance can be superficial.

### 2.4 Watermarking and provenance

Rijsbosch et al. (2025) investigate watermark adoption under the AI Act. A requirement to watermark AI-generated content is meaningful for autonomous generative systems, but what applies in the HI context — where a human edits, comments and modifies AI output? Is the overall product "AI-generated"? Nemecek et al. (2026) on C2PA and watermarking partially addresses this via provenance certificates that track editorial history.

### 2.5 GPAI compliance downstream

Organisations building HI systems on top of foundation models (via API) partly inherit compliance obligations. GPAI providers' technical documentation and usage policies become de facto compliance boundaries for downstream HI systems. But this creates a dependency: HI organisations' compliance is partly determined by what frontier labs choose to disclose and allow.

---

## Part 3: Governance models for HI organisations

### 3.1 Internal AI governance — three levels

Effective HI governance requires structures at three organisational levels:

**Strategic level:**
- AI ethics policy and risk appetite
- Board/leadership anchoring (AI governance officer / Chief AI Officer)
- Third-party audit and independent assessment

**Tactical level:**
- Risk assessment for specific HI systems (cf. NIST RMF *Map*)
- Incident-response procedures for HI failures
- Vendor management (GPAI dependencies)

**Operational level:**
- User guidelines and competence development
- Monitoring and alerting (anomaly detection in HI output)
- Review protocols that ensure genuine oversight (not rubber-stamping)

### 3.2 Ait et al. (2025) — DSL for HI governance

The formal domain-specific language for governance specification provides a way to make HI governance *executable*: instead of prose text, governance rules can be expressed as machine-executable specifications. This is early research but points toward a future where compliance can be verified automatically.

### 3.3 Decentralised governance — ARGO and DAO models

JafariMeimandi et al. (2025) describes ARGO (Autonomy-Rights-Governance-Oversight) as a decentralised governance model for AI systems. Sharma et al. (2024) investigates DAO (Decentralised Autonomous Organisation) as a governance form — not specifically for HI but relevant as an alternative to hierarchical compliance.

The connection to `d-open-source-organization.md`: open source governance principles (meritocracy, fork rights, transparent decision processes) constitute an alternative governance model to formal regulatory compliance.

### 3.4 Jensen & Meckling (1976) — the principal-agent problem in HI

The classical principal-agent theory from financial economics is directly relevant to HI governance: the human actor (agent) acts on behalf of an organisation (principal), but now with AI as a third actor that is either a tool for the agent or an independent actor. The principal-agent problem doubles: the organisation must now manage *both* human behaviour *and* the AI system's behaviour.

---

## Part 4: What regulation does not address

**4.1 Systemic risks from broad HI adoption**  
Existing regulation handles individual systems. It does not address what happens when many HI systems operate simultaneously in the same domain — concentration risks, monoculture effects, systemic correlation (cf. `b-closed-models-risks.md`).

**4.2 Global jurisdiction gaps**  
The AI Act applies in the EU; the NIST RMF is voluntary in the USA; China has a different regulatory approach. HI systems operate across jurisdictions. There is no binding international framework — and the tech diplomacy needed to create one is in an embryonic phase (Hiroshima AI Process, Bletchley Park Declaration).

**4.3 Regulating HI over time**  
HI systems change continuously via RLHF, fine-tuning and use. A compliance approval is a snapshot, not an ongoing guarantee. Regulation that presupposes static systems is structurally unsuited to adaptive HI systems.

**4.4 Governance of governance**  
Who monitors the regulators? NIST and the EU AI Act are built on industry input. Foundation labs have strong incentives and resources to shape the standards they themselves must comply with — a classic capture problem (Stigler 1971).

---

## Part 5: Audit and verification methodology

Compliance is only as strong as the audit machinery behind it. The NYC LL 144 evidence in §1.3 shows what happens when audit methodology is left undefined: regulated parties classify themselves out of scope, auditors disagree on what they are auditing, and posted impact ratios cluster suspiciously close to the legal threshold. A meaningful HI governance regime requires an audit methodology that is structurally adequate to the system being audited.

### 5.1 The three-layered audit framework

Mökander, Schuett, Kirk and Floridi (2023) propose a three-layered audit blueprint that maps cleanly onto HI systems built on foundation-model substrate:

1. **Governance audits** — directed at the technology provider (the foundation lab). What policies, processes and red-teaming practices does the provider follow when designing and releasing the underlying model? Audit artefacts: model cards, system cards, safety evaluation reports, RLHF documentation.
2. **Model audits** — directed at the model itself after pre-training and before release. What are the model's capabilities, refusal patterns, bias profile, and known failure modes? Audit artefacts: capability evaluations on standardised benchmarks, adversarial probing reports, dual-use uplift assessments.
3. **Application audits** — directed at the HI application built on top of the model. What is the human-AI workflow, what decisions does the system support, and how is human oversight implemented in practice? Audit artefacts: workflow documentation, decision-distribution logs, oversight competence evidence.

The three layers are interdependent: an application audit cannot answer questions the model audit failed to ask, and a model audit cannot replace a governance audit of the upstream developer. The framework's value for HI is that it forces the audit boundary to follow the *responsibility distribution* established in §2.1 — provider, deployer, and the human in the loop each face audit scrutiny appropriate to their causal role.

### 5.2 Assurance audits for algorithmic systems

Lam et al. (2024), drawing on financial-audit and safety-case traditions, propose a complementary *assurance audit* framework. Where Mökander's three layers map *where* to look, Lam et al. map *what evidence is sufficient*: a defensible audit must specify a target claim (the system performs within stated bias thresholds), the criteria against which it will be evaluated, the evidence types collected (statistical tests, process documentation, interviews), and the assurance level the auditor can reasonably warrant. This is the methodology gap that Wright et al. (2024) identify in NYC LL 144 — the law does not specify any of these elements, so auditors converged on the minimum.

### 5.3 Audit failure modes specific to HI

Three failure modes deserve special attention in HI audits:

- **Layer confusion.** A governance audit of the foundation-model provider does not guarantee that the deployer's application is safe. A model audit does not guarantee that the human-AI workflow preserves the safety properties of the model in isolation. Auditors must be explicit about which layer they are warranting.
- **Snapshot fallacy.** HI systems change continuously via fine-tuning, prompt updates and human-feedback loops. An audit conducted at deployment time describes a system that no longer exists three months later. Continuous monitoring, not annual snapshots, is the structurally adequate response (cf. §4.3).
- **Oversight rubber-stamping.** As §2.2 noted, formal human oversight can be operationally vacuous. Application audits must measure not only that humans approve AI outputs but that they *can* — competence, time, consequence. Decision-distribution logs that show approval rates above 99% within seconds per decision are evidence of HOOTL deployment regardless of nominal oversight design.

The connection to `b-closed-models-risks.md`: governance and model audits depend on access that the provider may decline to grant. Where the model is closed, the deployer and any external auditor are confined to behavioural probing — a structurally weaker audit than internal inspection. This is one of the practical compliance costs of closed infrastructure.

---

## Open Questions

1. **Can "meaningful human oversight" be operationalised?** Is it possible to define quantifiable thresholds (min. time per decision, min. competence level, max. decisions per hour) that make the oversight concept legally usable?

2. **Who bears accountability for HI failures?** Should the EU adapt the Product Liability Directive for HI systems — and what is the right accountability allocation between AI provider, system integrator and human operator?

3. **Is sector-specific regulation better than horizontal?** The AI Act is horizontal (applies to all sectors); the FDA's SaMD regulation is sector-specific (medicine only). Which approach provides better governance of HI in practice?

4. **Regulation by design vs. regulation by compliance**: can governance requirements be integrated into HI systems' architecture (cf. Ait et al.'s DSL approach) rather than being handled as an external compliance layer?

5. **Openwashing in compliance**: just as open-source claims can be misleading (Liesenfeld 2024), compliance claims ("AI Act-compliant") can mask real governance deficiencies. What are the effective verification mechanisms?

---

## Sources (Anchors)

Status tags: `[J]` peer-reviewed journal · `[C]` peer-reviewed conference · `[P]` preprint · `[R]` technical/institutional report. Citation metric: `[OA cit: N]` from OpenAlex (latest refresh 2026-05-11).

**Already in Kilder:**
- `[R]` NIST (2023). *AI Risk Management Framework 1.0* (NIST AI 100-1). ✓
- `[C]` Ait, A. et al. (2025). DSL for Human-Agent Governance. *ASE 2025*. ✓
- `[J]` Cheruvu, R. (2026). Human-in/on-the-Loop Design for Human Controllability. In W. Xu (ed.), *Handbook of Human-Centered Artificial Intelligence*. Springer. https://doi.org/10.1007/978-981-97-8440-0_75-1 ✓
- `[J]` Bensch, L., Bensch, O., Nilsson, T., et al. (2025). Human-in/on-the-Loop AI: Enabling Human Controllability and Decision-Making in Spaceflight. In W. Xu (ed.), *Handbook of Human-Centered Artificial Intelligence*. Springer. https://doi.org/10.1007/978-981-97-8440-0_40-1 ✓
- `[P]` JafariMeimandi, M. et al. (2025). An Adaptive Responsible AI Governance Framework for Decentralized Organizations. arXiv:2510.03368. [OA cit: 0]
- `[C]` Liesenfeld, A. et al. (2024). Rethinking open source generative AI: open washing and the EU AI Act. *FAccT 2024*. https://doi.org/10.1145/3630106.3659005 [OA cit: 49] ✓
- `[R]` Bommasani, R. et al. (2024). The Foundation Model Transparency Index. CRFM/Stanford. ✓
- `[R]` Wan, K. et al. (2025). The Foundation Model Transparency Index v1.1. ✓
- `[P]` Rijsbosch, R. et al. (2025). Adoption of Watermarking for Generative AI Systems in Practice and Implications under the new EU AI Act. arXiv:2503.18156. [OA cit: 0]
- `[P]` Nemecek, A. et al. (2026). Authenticated Contradictions from Desynchronized Provenance and Watermarking. arXiv:2603.02378. [OA cit: 0]
- `[P]` Sharma, T. et al. (2024). Blockchain Governance: An Empirical Analysis of User Engagement on DAOs. arXiv:2407.10945. [OA cit: 1]
- `[J]` Jensen, M. C. & Meckling, W. H. (1976). Theory of the firm: Managerial behavior, agency costs and ownership structure. *Journal of Financial Economics, 3*(4), 305–360. ✓
- `[P]` Gabriel, I. (2020). Artificial intelligence, values, and alignment. arXiv:2001.09768 (later published *Minds and Machines* 2020). ✓
- `[P]` Kapoor, S. et al. (2024). On the societal impact of open foundation models. arXiv:2403.07918. ✓
- `[R]` Solaiman, I. (2023). The gradient of generative AI release: Methods and considerations. ✓
- `[P]` Lindstrom, A. D. et al. (2025). AI Alignment through RLHF? Contradictions and Limitations. arXiv:2406.18346. [OA cit: 2]
- `[J]` Floridi, L. et al. (2018). AI4People — An Ethical Framework for a Good AI Society. *Minds and Machines, 28,* 689–707. https://doi.org/10.1007/s11023-018-9482-5 [OA cit: 3259] ✓ *(refresh 2026-05-11)*
- `[J]` Santoni de Sio, F. & Mecacci, G. (2021). Four Responsibility Gaps with Artificial Intelligence: Why they Matter and How to Address them. *Philosophy & Technology, 34,* 1057–1084. https://doi.org/10.1007/s13347-021-00450-x [OA cit: 364] ✓ *(refresh 2026-05-11)*
- `[J]` **Santoni de Sio, F. & van den Hoven, J. (2018).** Meaningful Human Control over Autonomous Systems: A Philosophical Account. *Frontiers in Robotics and AI, 5,* 15. https://doi.org/10.3389/frobt.2018.00015 [OA cit: 441] ✓ *(downloaded 2026-05-11)*
- `[J]` **Mökander, J., Schuett, J., Kirk, H. R. & Floridi, L. (2023).** Auditing large language models: a three-layered approach. *AI and Ethics.* https://doi.org/10.1007/s43681-023-00289-2 [OA cit: 183] ✓ *(downloaded 2026-05-11; primary anchor for §5.1)*
- `[C]` **Groves, L., Metcalf, J., Kennedy, A., Vecchione, B. & Strait, A. (2024).** Auditing Work: Exploring the New York City algorithmic bias audit regime. *FAccT '24.* https://doi.org/10.1145/3630106.3658959 [OA cit: 35] ✓ *(arXiv:2402.08101 downloaded 2026-05-11; §1.3 and §5.2 anchor)*

**Cited but not in Kilder (paywalled or no PDF mirror available):**
- `[J]` Matthias, A. (2004). The responsibility gap: Ascribing responsibility for the actions of learning automata. *Ethics and Information Technology, 6,* 175–183. https://doi.org/10.1007/s10676-004-3422-1 [OA cit: 918] *(refresh 2026-05-11)* — *paywalled; cited as the originating responsibility-gap source*
- `[C]` **Wright, L., Muenster, R. M., Vecchione, B., Qu, T., Cai, P. & Smith, A. (2024).** Null Compliance: NYC Local Law 144 and the challenges of algorithm accountability. *FAccT '24.* https://doi.org/10.1145/3630106.3658998 [OA cit: 27] — *ACM proceedings only; PDF mirror not located 2026-05-11; primary anchor for §1.3 NYC LL 144 null-compliance finding*
- `[C]` **Lam, K. T., Lange, B., Blili-Hamelin, B., Davidovic, J., Brown, S. & Hasan, A. (2024).** A Framework for Assurance Audits of Algorithmic Systems. *FAccT '24.* https://doi.org/10.1145/3630106.3658957 [OA cit: 25] — *ACM proceedings only; primary anchor for §5.2 assurance-audit methodology*
- `[R]` EU AI Act — Regulation (EU) 2024/1689. — official EUR-Lex text; linked as web reference
- `[J]` Stigler, G. J. (1971). The theory of economic regulation. *Bell Journal of Economics and Management Science, 2*(1), 3–21. — JSTOR-paywalled; cite as classical regulatory-capture reference
- `[R]` FDA (2021). Artificial Intelligence/Machine Learning (AI/ML)-Based Software as a Medical Device (SaMD) Action Plan.
- `[P]` Doshi-Velez, F. & Kim, B. (2017). Towards a rigorous science of interpretable machine learning. arXiv:1702.08608. ✓ *(in Kilder)*

**Retraction check 2026-05-11** (CrossRef `update-to`): clean for Floridi 2018, Santoni de Sio & Mecacci 2021, Santoni de Sio & van den Hoven 2018, Matthias 2004, Liesenfeld 2024, Mökander 2023, Groves 2024, Wright 2024.

---

## What Still Needs Work

- Acquire Matthias 2004 PDF (currently paywalled at Springer) — try institutional access
- Acquire Wright et al. 2024 *Null Compliance* PDF (ACM proceedings only; arXiv mirror not located 2026-05-11 — retry with different search terms)
- Acquire Lam et al. 2024 *Assurance Audits* PDF (ACM proceedings only — retry)
- Acquire EU AI Act 2024/1689 official PDF (EUR-Lex direct download was empty — try mirror)
- Expand sector-specific regulation: finance — MiFID II RTS 6 algorithmic-trading kill-switch and pre-trade-control detail
- Find more recent case law or EU AI Act implementation guidance (2025–2026)
- Connect to `e-llm-structural-vulnerabilities.md` — prompt injection as compliance problem (NIST AI RMF)
- Reconsider whether `[P]` sources with OA cit < 5 (JafariMeimandi 2025, Rijsbosch 2025, Nemecek 2026, Sharma 2024) should remain primary anchors or be supplemented with peer-reviewed alternatives once available
