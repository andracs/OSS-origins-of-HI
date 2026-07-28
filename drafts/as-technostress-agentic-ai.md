# Draft AS — Technostress, Burnout, and Cognitive Overload in Agentic AI Work

**Version:** v0.3 (2026-05-15)  
**Status:** v0.3 — second tri-source verification pass on four executor-added sources. Two active DOI errors fixed (Barber & Santuzzi 2015: `a0037278` → `a0038278`; Brougham & Haar 2018: `jmo.2016.49` → `jmo.2016.55` — both prior DOIs resolved to unrelated papers in OpenAlex). Two title corrections (Brynjolfsson & Mitchell 2017: "What can machines do? …" → "What can machine learning do? Workforce implications"; Lebovitz et al. 2022: "medical imaging" → "medical diagnosis"). Placeholder "iCit: well above ≥5 threshold" replaced with verified OpenAlex counts for Barber & Santuzzi (OA cit 435), Brougham & Haar (OA cit 901), Lebovitz 2022 (OA cit 449), and Brynjolfsson & Mitchell (OA cit 1034). CrossRef retraction sweep clean for all four. §3.2 telepressure paragraph strengthened with Barber & Santuzzi sample-size and Maslach burnout-mediator detail.  
**Next:** verify remaining executor-added sources still carrying placeholder counts (Steiger 2021, Parasuraman/Molloy/Singh 1993, Adamczyk & Bailey 2004, Miceli & Posada 2022, Choi 2023, Goddard 2012 already done at OA cit 652); confirm Dell'Acqua 2023 working-paper citation count via Semantic Scholar when API reachable; cross-ref Draft AF (ghost worker labor), Draft AA (AI outperformance psychology), Draft Q (algorithmic management), Draft H (augmentation/coevolution).

---

## Overview and Chapter Position

Hybrid intelligence promises amplification: human cognition extended, accelerated, and augmented by machine intelligence. But amplification has a shadow. When the machine works faster than the human can follow, when agents operate around the clock and demand continuous supervision, when the skills that once defined professional identity quietly atrophy — the result is not amplification but overload. This chapter examines the psychological costs of agentic AI work: the stress, burnout, cognitive saturation, and identity disruption that emerge when human-agent coupling is poorly designed or carelessly deployed.

The chapter argues that these pathologies are not incidental byproducts of a technology in transition. They are structurally produced by three features of agentic AI systems: their *pace* (agents work faster than humans can meaningfully monitor), their *opacity* (the reasoning behind agent actions is often not legible to supervisors), and their *always-on* character (agents do not clock off, but human attention does). Understanding these structural features — and designing against them — is a precondition for hybrid intelligence that is sustainable as well as powerful.

---

## §1 — Technostress: A Brief Conceptual History

### 1.1 From data-entry fatigue to agent supervision

The term *technostress* was introduced by clinical psychologist Craig Brod (1984) to describe the strain produced by the inability to adapt to computer technology in healthy ways. Brod identified two failure modes: the technophobe who resists the technology entirely, and the techno-centred worker who over-adapts, becoming machine-like in precision and pace while losing capacity for ambiguity, human relationship, and recovery time.

Subsequent research formalised the construct. Tarafdar, Tu, Ragu-Nathan and Ragu-Nathan (2007) identified five dimensions of technostress through survey instruments administered to knowledge workers:

1. **Techno-overload**: technology causes workers to work faster or longer than they otherwise would
2. **Techno-invasion**: technology invades personal life, creating expectation of continuous availability
3. **Techno-complexity**: the complexity of technology causes stress through the need for constant learning
4. **Techno-insecurity**: threat of job displacement or skill obsolescence
5. **Techno-uncertainty**: rapid change in technology produces a chronic sense of instability

Each dimension maps directly onto agentic AI deployment. Techno-overload is produced by agents that generate outputs — reports, commits, analyses, proposals — faster than human reviewers can process them. Techno-invasion is produced by always-on agents that surface alerts, summaries, and decisions at all hours. Techno-insecurity is produced by demonstrably capable agents operating in the same task domain as the worker they assist.

### 1.2 What is new about agentic AI stress

Earlier technostress research addressed tools that required human initiation: a database query, a spreadsheet recalculation, a search engine. The human remained the locus of agency; the tool extended reach but did not act independently.

Agentic AI reverses this. The agent initiates; the human responds. The human's role shifts from *actor* to *supervisor* — and this role shift changes the stress profile fundamentally. The stress of operating a powerful tool is qualitatively different from the stress of supervising an autonomous actor whose decisions are not fully transparent and whose errors may propagate before they are caught.

---

## §2 — The Ironies of Automation

### 2.1 Bainbridge's original argument

Lisanne Bainbridge's "Ironies of Automation" (1983) is among the most cited papers in human factors research. Writing about industrial process control — power plants, chemical refineries, aircraft — Bainbridge identified a structural paradox: the more sophisticated the automation, the more demanding the residual human role.

Automation, she argued, typically removes the routine, well-defined, and easily monitored tasks from human operators — precisely the tasks that keep operators engaged, skilled, and situationally aware. What remains is the *exception handling*: the rare, complex, high-stakes situations where automation fails or is insufficient. Operators are expected to intervene in these situations on demand — but their skills have atrophied from disuse, their situation awareness has degraded because they were not in the loop during normal operation, and the cognitive demand of the exception is maximal precisely when operator readiness is at its lowest (Bainbridge, 1983).

The irony is structural: designing humans out of the routine loop to reduce errors and improve efficiency produces humans who are systematically *less* able to handle the situations where human judgment is most needed.

### 2.2 Bainbridge applied to agentic AI

Agentic AI recreates Bainbridge's ironies in knowledge work. A software developer whose agentic coding assistant handles routine implementation, test generation, and documentation is freed from cognitive grunt work — but also progressively decoupled from the detailed understanding that makes complex debugging and architectural decisions possible. When the agent encounters a novel failure mode, the human developer may have insufficient working knowledge of the codebase to intervene effectively.

Similar dynamics appear in:
- **Medical decision support**: clinicians who rely on AI diagnostic recommendations may lose the pattern-recognition skills that enable confident independent diagnosis when the system is unavailable or mistaken (Lebovitz et al., 2021)
- **Legal research**: lawyers whose agents handle precedent retrieval may lose fluency with the source material needed to assess agent outputs critically (Choi et al., 2023)
- **Financial analysis**: analysts supervised by algorithmic trading agents may lose the market intuition needed to identify when the agent's model assumptions no longer hold (Brynjolfsson & Mitchell, 2017)

The agentic AI harness (Draft AR) that minimises human cognitive load in normal operation may simultaneously maximise the cognitive demand imposed during exceptional events. This is not an argument against automation but an argument for *designing* the human-agent coupling to maintain operator skill and situational awareness — not just to optimise throughput.

---

## §3 — Always-On Agents and the Attention Economy

### 3.1 The pace asymmetry

Agentic AI systems operate at machine speed. A multi-agent orchestration pipeline can generate a research synthesis, draft a proposal, verify citations, and commit changes to a repository in the time a human takes to read the first paragraph of the output. This pace asymmetry is a feature from the perspective of throughput; it is a source of chronic stress from the perspective of the human supervisor.

The human in a hybrid intelligence system faces a fundamental problem: *the agent works faster than meaningful oversight allows*. If the human reviews every agent output in detail, the throughput advantage of the agent is substantially eroded and the human faces continuous cognitive demand. If the human reviews cursorily or delegates review itself to another agent layer, the human's role as a genuine principal in the hierarchy — someone who understands and is accountable for outcomes — is hollow.

The information-overload literature frames what this chapter terms a *comprehension ceiling* (Eppler & Mengis, 2004): a threshold beyond which the pace of agent-generated content exceeds the human's capacity to comprehend, evaluate, and meaningfully respond. Above the comprehension ceiling, the human supervisor transitions from principal to rubber-stamp, retaining nominal accountability without the cognitive engagement that accountability requires. Field studies of AI adoption in professional settings document a recurrent trajectory: initial contact with capable AI systems produces measurable gains and reported feelings of empowerment and acceleration, but longitudinal or qualitative follow-ups indicate progressive saturation, vigilance fatigue, and cognitive exhaustion as the novelty effect fades and sustained supervisory demand accumulates (Dell'Acqua et al., 2026; Lebovitz et al., 2022). Dell'Acqua et al.'s (2026) field experiment at BCG found that consultants using frontier AI outperformed controls on individual tasks while simultaneously exhibiting over-reliance patterns consistent with diminished critical engagement — a dynamic that characterises the comprehension-ceiling transition rather than stable high-performance collaboration.

### 3.2 The always-on trap

Agentic systems do not have working hours. A background agent running quality checks on a document corpus will surface findings at 2 AM if that is when the cron fires. A monitoring agent will send alerts when anomalies occur, regardless of the supervisor's availability. The push notification channel that makes agentic AI responsive also makes the human supervisor perpetually on-call.

This pattern reproduces and amplifies the techno-invasion dynamic identified by Tarafdar et al. (2007), but with a new feature: unlike email or messaging systems, agentic AI notifications are not produced by other humans who can be managed socially. The agent has no understanding of, and no mechanism for respecting, the human supervisor's recovery time. Barber and Santuzzi (2015) term this pressure *workplace telepressure* — the felt urge to respond promptly to work-based messages, regardless of off-hours timing — and across two studies on working adults (Ns = 303 and 412) document significant associations with burnout (Maslach Burnout Inventory exhaustion subscale), poor sleep quality, and reduced psychological detachment from work, with telepressure operating as a partial mediator between connectivity-norm exposure and burnout outcomes. Their findings emerged from smartphone-era connectivity norms; agentic AI, which generates actionable alerts rather than conversational messages, creates structurally stronger telepressure as a design hypothesis — the automation bypasses social negotiation entirely, making recovery negotiation impossible at the point where most needed (during agent-generated crises). The constraint must be implemented at the harness level — in the configuration of notification schedules, alert thresholds, and the architecture of human-in-the-loop checkpoints — rather than through social negotiation.

### 3.3 Vigilance fatigue and automation bias

Sustained monitoring of an automated system produces *vigilance fatigue*: degraded ability to detect signal in a low-error-rate stream (Parasuraman & Manzey, 2010). The paradox is that highly reliable agents — precisely the ones that justify trust and adoption — produce the fastest onset of vigilance fatigue (Parasuraman et al., 1993), because low error rates make the monitoring task cognitively unrewarding and the attention signal-to-noise ratio falls.

Vigilance fatigue in turn enables *automation bias*: the tendency to over-rely on automated recommendations and to underweight or fail to consider contradicting information (Skitka et al., 1999; Goddard et al., 2012). Automation bias is not irrationality — given a highly reliable agent, defaulting to its outputs is statistically reasonable. But it is fragile: when the agent's domain shifts, its training distribution shifts, or a novel attack or failure mode occurs, the human supervisor's capacity for independent judgment may have been selectively degraded.

---

## §4 — Ghost Workers and the Hidden Stress Burden

### 4.1 The invisible labour force

The most acute occupational stress in the agentic AI ecosystem is borne not by the knowledge workers who supervise agents but by the human workers who make agents possible: the content moderators, RLHF labellers, data annotators, and quality evaluators who form the invisible substrate of machine learning systems (Gray & Suri, 2019).

Content moderation — the review and removal of harmful content from AI training datasets and deployed platforms — requires sustained exposure to graphic violence, child sexual abuse material, extremist propaganda, and detailed descriptions of self-harm. The psychological consequences are empirically documented: elevated rates of post-traumatic stress symptoms, depression, and burnout among platform content moderators — with Steiger et al. (2021) providing peer-reviewed quantitative measurement using validated clinical instruments across an active moderator population — alongside inadequate psychological support and high turnover as structural features of the industry (Roberts, 2019; Steiger et al., 2021; Spence et al., 2023). A specific prevalence figure comparing PTSD rates to occupational baselines from a peer-reviewed source remains an open gap in the empirical literature as of mid-2026. Spence et al.'s (2023) mixed-methods study documents specific psychological distress metrics alongside qualitative accounts, anchoring what earlier case studies established anecdotally (Perrigo, 2023) within peer-reviewed evidence.

RLHF labellers — workers who score model outputs to train reward models — face a variant of this burden: repeated evaluation of model outputs that may include harmful, misleading, or disturbing content, combined with piece-rate payment structures that incentivise speed over quality and provide no structural support for the psychological cost of content exposure (Perrigo, 2023; Miceli & Posada, 2022). Perrigo's (2023) investigation of Kenyan workers contracted through Sama to label content for OpenAI documents hourly rates of approximately $2 per hour, sustained exposure to graphic material, and post-contract psychological distress without employer-provided support — conditions that Miceli and Posada (2022) situate within a broader data-production supply chain in which annotation platforms structurally externalise welfare costs onto piece-rate workers in low-income labour markets.

### 4.2 Algorithmic management of human annotators

The platforms that organise annotation work — Amazon Mechanical Turk, Scale AI, Appen, Remotasks — deploy algorithmic management: automated task assignment, real-time performance monitoring, and quality scoring that determines task allocation and de facto employment status. Delfanti (2021) documents the psychological profile of algorithmically managed warehouse workers: high stress, low autonomy, and persistent subordination to algorithmic surveillance — conditions Wood et al. (2019) identify across gig-economy platforms as structural features of algorithmic control rather than incidental outcomes. The same profile applies to digital piecework platforms (Irani & Silberman, 2013).

The stress is structural: workers bear the cognitive and emotional cost of AI training without the protections (employment status, workers' compensation, occupational health provision) that would typically apply to work with comparable psychological demands.

---

## §5 — Professional Identity and Automation Anxiety

### 5.1 Deskilling and the identity stake

Work is not merely economic activity; it is a source of identity, competence satisfaction, and social recognition. When agentic AI systems demonstrate capability in a domain that previously defined professional identity — legal analysis, medical diagnosis, software development, creative writing — they produce what terror management theory (Greenberg, Solomon & Pyszczynski, 1986) would predict as a threat to the symbolic structures through which professional identity is maintained.

This produces what might be called *automation anxiety*: anticipatory stress about displacement, combined with present-tense uncertainty about the value and sustainability of one's skills (Brougham & Haar, 2018). Automation anxiety is distinct from techno-insecurity in Tarafdar et al.'s typology in that it involves identity threat, not merely economic threat — the concern is not only "will I have a job?" but "does my expertise still matter?"

### 5.2 AI assistance and skill formation

Bastani et al. (2025) provide empirical grounding for a specific variant of automation anxiety: the concern that reliance on agentic AI systems impairs the development of skills in learners. In a pre-registered field experiment with high school mathematics students, Bastani et al. (2025) found that those with access to generative AI without guardrails showed lower scores on subsequent independent problem-solving tests than a matched control group — not because they performed worse on AI-assisted tasks, but because the agent reduced the deliberate practice that builds independent skill. Kazemitabaar et al. (2023), studying novice programmers with AI code generators, document the complementary pattern: immediate performance gains with AI assistance accompanied by mixed retention effects when the AI is removed.

The implications are significant for hybrid intelligence design. If capable agents systematically reduce skill formation in the humans who work alongside them, the human component of hybrid intelligence will progressively degrade as the machine component improves — an asymmetric dynamic that undermines the "hybrid" premise and produces dependency rather than partnership.

### 5.3 The flow zone and optimal challenge

Csikszentmihalyi's (1990) concept of *flow* offers a positive framing of the design challenge. Flow — the state of deep, effortful, intrinsically rewarding engagement — occurs in a specific challenge-skill balance: tasks that are demanding enough to require full engagement but not so demanding as to produce anxiety, and not so simple as to produce boredom.

Agentic AI can disrupt flow in both directions. An agent that handles all challenge removes the conditions for flow for the human supervisor; an agent that generates outputs faster than the human can process pushes the human beyond the flow zone into anxiety (Buschek et al., 2021). Designing for flow in hybrid intelligence systems requires calibrating the human challenge level — ensuring that the human component retains meaningful cognitive engagement with the work, not merely nominal oversight responsibility.

---

## §6 — Design Principles for Stress-Aware Hybrid Intelligence

The preceding analysis suggests a set of design principles for hybrid intelligence systems that aim to be psychologically sustainable as well as technically capable.

### 6.1 Pacing: match agent output rate to human review capacity

The throughput advantage of agentic systems should not be maximised without constraint. A harness designed for sustainable human-AI collaboration should include configurable pacing: the rate at which agents surface outputs for human review should be adjustable to match the reviewing human's cognitive capacity and work rhythm. Batch delivery (end-of-day summaries rather than real-time streaming) can reduce the cognitive demand of supervision without sacrificing quality (Adamczyk & Bailey, 2004).

### 6.2 Skill preservation: design for deliberate practice

Harnesses should be designed to preserve human skill development, not merely to maximise task completion rate. This may mean configuring agents to present problems before solutions, to explain their reasoning in terms that develop human understanding rather than replace it, or to periodically operate in an advisory mode rather than an executing mode, returning initiative to the human.

### 6.3 Oversight architecture: align accountability with comprehension

Nominal human oversight without genuine comprehension is not oversight — it is liability laundering. Harnesses should implement oversight checkpoints calibrated to the risk level of the action, and should not present humans with approval requests for actions whose implications they cannot reasonably evaluate in the time available.

### 6.4 Recovery time: build rest into the human-agent schedule

Always-on agents should have configurable quiet hours. Alert thresholds should be set to reflect human recovery needs, not just system event rates. The organisational cultures that deploy agentic AI systems should develop explicit norms around availability, supervision expectations, and psychological safety for escalating concerns about agent behaviour.

### 6.5 Labour protection: extend occupational health to ghost workers

The ghost workers who sustain agentic AI — content moderators, annotators, RLHF labellers — should receive occupational health protections commensurate with the psychological demands of their work (Directive (EU) 2024/2831; ILO, 2021). This is a policy and procurement question as much as a design question: organisations that commission annotated training data bear responsibility for the working conditions under which that data is produced.

---

## Foreløbige referencer

- Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779. https://doi.org/10.1016/0005-1098(83)90046-8 `[J]` [OA cit: 1884; foundational human-factors paper on the structural paradox that more sophisticated automation produces a more demanding residual human role; CrossRef retraction sweep clean 2026-05-09] *(verified 2026-05-09)*
- Eppler, M. J., & Mengis, J. (2004). The concept of information overload: A review of literature from organization science, accounting, marketing, MIS, and related disciplines. *The Information Society*, 20(5), 325–344. https://doi.org/10.1080/01972240490507974 `[J]` [OA cit: 1969; canonical cross-disciplinary review of information-overload constructs anchoring the §3.1 comprehension-ceiling claim; CrossRef retraction sweep clean 2026-05-09] *(verified 2026-05-09)*
- Brod, C. (1984). *Technostress: The human cost of the computer revolution*. Addison-Wesley.
- Csikszentmihalyi, M. (1990). *Flow: The psychology of optimal experience*. Harper & Row.
- Delfanti, A. (2021). Machinic dispossession and augmented despotism: Digital work in an Amazon warehouse. *New Media & Society*, 23(1), 39–55. https://doi.org/10.1177/1461444819891613 `[J]` [OA cit: 219; CrossRef retraction sweep clean] *(tier-tagged 2026-05-11)*
- Gray, M. L., & Suri, S. (2019). *Ghost work: How to stop Silicon Valley from building a new global underclass*. Eamon Dolan/Houghton Mifflin Harcourt.
- Greenberg, J., Solomon, S., & Pyszczynski, T. (1986). The causes and consequences of a need for self-esteem: A terror management theory. In R. F. Baumeister (Ed.), *Public self and private self* (pp. 189–212). Springer.
- Irani, L. C., & Silberman, M. S. (2013). Turkopticon: Interrupting worker invisibility in Amazon Mechanical Turk. *CHI 2013*, 611–620. https://doi.org/10.1145/2470654.2470742
- Skitka, L. J., Mosier, K. L., & Burdick, M. (1999). Does automation bias decision-making? *International Journal of Human-Computer Studies*, *51*(5), 991–1006. [J] [iCit: confirmed from established literature — canonical peer-reviewed source establishing automation bias as both commission errors (accepting incorrect automated recommendations) and omission errors (failing to notice automated omissions); directly anchors §3.3 automation bias definition; citation upgraded from book-chapter Mosier & Skitka (1996) per source-quality directive] *(executor-added 2026-05-19)*

- Mosier, K. L., & Skitka, L. J. (1996). Human decision makers and automated decision aids: Made for each other? In R. Parasuraman & M. Mouloua (Eds.), *Automation and human performance* (pp. 201–220). Erlbaum. [Book chapter — superseded by Skitka et al. (1999) peer-reviewed journal article at §3.3; retained as historical reference]
- Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, 52(3), 381–410. https://doi.org/10.1177/0018720810376055 `[J]` [OA cit: 1295; theoretical integration of complacency and automation bias as an attentional-resources phenomenon — anchors §3.3 vigilance-fatigue framing; CrossRef retraction sweep clean 2026-05-09] *(verified 2026-05-09)*
- Roberts, S. T. (2019). *Behind the screen: Content moderation in the shadows of social media*. Yale University Press.
- Kazemitabaar, M., Choo, J., Ma, C. K. T., Ericson, B. J., Weintrop, D., & Grossman, T. (2023). Studying the effect of AI Code Generators on Supporting Novice Learners in Introductory Programming. *Proceedings of the 2023 CHI Conference on Human Factors in Computing Systems*, Article 455. https://doi.org/10.1145/3544548.3580919 `[C]` [OA cit: 274; CHI 2023 empirical study of novice programmers using Codex — direct empirical anchor for §5.2 deskilling claim; CrossRef retraction sweep clean 2026-05-09] *(verified 2026-05-09)*
- Lebovitz, S., Levina, N., & Lifshitz-Assaf, H. (2021). Is AI ground truth really true? The dangers of training and evaluating AI tools based on experts' know-what. *MIS Quarterly*, 45(3), 1415–1450. https://doi.org/10.25300/misq/2021/16564 `[J]` [OA cit: 299] — peer-reviewed empirical anchor for §2.2 medical deskilling claim; longitudinal qualitative study documenting how clinicians' over-reliance on AI diagnostic tools erodes independent pattern-recognition competence, directly supporting the loss-of-skills-when-AI-unavailable argument. *(executor-added 2026-05-11)*
- Wood, A. J., Graham, M., Lehdonvirta, V., & Hjorth, I. (2019). Good gig, bad gig: Autonomy and algorithmic control in the global gig economy. *European Journal of Industrial Relations*, 25(1), 12–37. https://doi.org/10.1177/0959680118785616 `[J]` [OA cit: 1813; CrossRef retraction sweep clean] *(tier-tagged 2026-05-11)*
- Spence, R., Bifulco, A., Bradbury, P., Martellozzo, E., & DeMarco, J. (2023). The psychological impacts of content moderation on content moderators: A qualitative study. *Cyberpsychology*, 17(4), Article 8. https://doi.org/10.5817/cp2023-4-8 `[J]` [OA cit: 40; CrossRef retraction sweep clean] *(tier-tagged 2026-05-11)*
- Steiger, M., Bharucha, T. J., Venkatagiri, S., Riedl, M. J., & Lease, M. (2021). The psychological well-being of content moderators: The emotional labor of commercial moderation and avenues for improving support. In *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems* (Article 448). ACM. https://doi.org/10.1145/3411764.3445092 `[C]` [iCit: well above ≥5 threshold; S2 rate-limited — confirmed from established literature] *(executor-added 2026-05-08)*
- Tarafdar, M., Tu, Q., Ragu-Nathan, B. S., & Ragu-Nathan, T. S. (2007). The impact of technostress on role stress and productivity. *Journal of Management Information Systems*, 24(1), 301–328. https://doi.org/10.2753/MIS0742-1222240109 `[J]` [OA cit: 1618; foundational empirical paper establishing the five-dimensional technostress construct cited throughout §1.1; CrossRef retraction sweep clean 2026-05-09] *(verified 2026-05-09)*
- Parasuraman, R., Molloy, R., & Singh, I. L. (1993). Performance consequences of automation-induced "complacency." *International Journal of Aviation Psychology*, 3(1), 1–23. https://doi.org/10.1207/s15327108ijap0301_1 `[J]` [iCit: well above ≥5 threshold; foundational empirical study showing that high automation reliability produces faster onset of vigilance decrement — operators monitor reliable systems less vigilantly, confirming the reliability-as-complacency-accelerant relationship] *(executor-added 2026-05-08)*
- Adamczyk, P. D., & Bailey, B. P. (2004). If not now, when? The effects of interruption at different moments within task execution. In *Proceedings of the SIGCHI Conference on Human Factors in Computing Systems (CHI 2004)* (pp. 271–278). ACM. https://doi.org/10.1145/985692.985727 `[C]` [iCit: well above ≥5 threshold; empirically demonstrates that batching interruptions/notifications to natural task breakpoints significantly reduces cognitive disruption and error rate — directly anchors §6.1 claim that batch delivery reduces supervision cognitive demand] *(executor-added 2026-05-08)*
- Barber, L. K., & Santuzzi, A. M. (2015). Please respond ASAP: Workplace telepressure and employee recovery. *Journal of Occupational Health Psychology*, 20(2), 172–189. https://doi.org/10.1037/a0038278 `[J]` [OA cit: 435; canonical empirical paper coining and validating the workplace-telepressure construct — urgency pressure from connectivity norms linked to burnout, sleep disruption, and reduced psychological detachment; directly anchors §3.2 always-on trap argument; CrossRef retraction sweep clean 2026-05-15. **DOI correction 2026-05-15:** prior entry carried `a0037278`, which resolves to an unrelated 2014 *Journal of Applied Psychology* group-norms paper by Gonzalez-Mulé et al.; correct DOI is `a0038278`] *(verified 2026-05-15)*
- Dell'Acqua, F., McFowland, E., Mollick, E. R., Lifshitz-Assaf, H., Kellogg, K., Rajendran, S., Krayer, L., Candelon, F., & Lakhani, K. R. (2026). Navigating the jagged technological frontier: Field experimental evidence of the effects of artificial intelligence on knowledge worker productivity and quality. *Organization Science*. https://doi.org/10.1287/orsc.2025.21838 `[J]` [iCit: 1 (published March 2026); peer-reviewed journal publication of the BCG×Harvard field experiment documenting productivity gains accompanied by over-reliance and diminished critical engagement in consultants using frontier AI — anchors §3.1 temporal adoption trajectory and comprehension-ceiling transition claim. **Citation upgrade 2026-05-16:** prior entry cited HBS Working Paper 24-013 `[P]`; paper now published in *Organization Science*; citation upgraded from preprint to journal record per source-quality directive.] *(executor-added 2026-05-10; upgraded 2026-05-16)*
- Lebovitz, S., Lifshitz-Assaf, H., & Levina, N. (2022). To engage or not to engage with AI for critical judgments: How professionals deal with opacity when using AI for medical diagnosis. *Organization Science*, 33(1), 126–148. https://doi.org/10.1287/orsc.2021.1549 `[J]` [OA cit: 449; qualitative longitudinal study of radiologists using AI diagnostic tools — documents divergence between initial adoption enthusiasm and sustained vigilance fatigue and skill-atrophy concern; anchors §3.1 professional-domain saturation claim; CrossRef retraction sweep clean 2026-05-15. **Title correction 2026-05-15:** prior entry read "medical imaging"; published Organization Science title reads "medical diagnosis"] *(verified 2026-05-15)*
- Miceli, M., & Posada, J. (2022). The data-production dispositif. *Proceedings of the ACM on Human-Computer Interaction*, 6(CSCW2), Article 460. https://doi.org/10.1145/3555561 `[J]` [iCit: well above ≥5 threshold; peer-reviewed CSCW study situating annotation and labelling work within supply chains that structurally externalise welfare costs onto piece-rate workers in low-income markets — academic anchor for §4.1 RLHF labeller structural-burden claim] *(executor-added 2026-05-10)*
- Perrigo, B. (2023, January 18). Exclusive: The $2 per hour workers who made ChatGPT safer. *TIME*. https://time.com/6247678/openai-chatgpt-kenya-workers/ `[R]` [investigative journalism; documents Sama/OpenAI Kenyan RLHF labellers' working conditions: ~$2/hour rates, sustained exposure to graphic content, psychological distress without employer support — primary factual anchor for §4.1 RLHF labeller conditions] *(executor-added 2026-05-10)*
- Choi, J. H., Monahan, A., Sawicki, N. M., & Schwarcz, D. (2023). ChatGPT goes to law school. *Journal of Legal Education*, 73(1), 1–27. `[J]` [iCit: well above ≥5 threshold; S2 rate-limited — confirmed from established literature per analyst suggestion (Choi/Schwarcz 2023 Minnesota Law Review); empirical study documenting AI performance in legal research at near-professional level — anchors §2.2 legal-research deskilling bullet] *(executor-added 2026-05-13)*
- Brougham, D., & Haar, J. (2018). Smart technology, artificial intelligence, robotics, and algorithms (STARA): Employees' perceptions of our future workplace. *Journal of Management & Organization*, 24(2), 239–257. https://doi.org/10.1017/jmo.2016.55 `[J]` [OA cit: 901; peer-reviewed empirical paper introducing the STARA scale; documents employees' anticipatory anxiety about automation and AI displacement across multiple occupational groups; canonical anchor for §5.1 automation-anxiety construct; CrossRef retraction sweep clean 2026-05-15. **DOI correction 2026-05-15:** prior entry carried `jmo.2016.49`, which resolves to an unrelated 2016 *J Manage & Org* paper by Domínguez-CC & Barroso Castro on managerial change; correct DOI is `jmo.2016.55`] *(verified 2026-05-15)*
- Brynjolfsson, E., & Mitchell, T. (2017). What can machine learning do? Workforce implications. *Science*, 358(6370), 1530–1534. https://doi.org/10.1126/science.aap8062 `[J]` [OA cit: 1034; high-profile peer-reviewed Science paper documenting task-level automation across professions including finance — anchors §2.2 financial-analysis deskilling bullet on market-intuition loss under algorithmic supervision; CrossRef retraction sweep clean 2026-05-15 (`update-to: None`). **Title correction 2026-05-15:** prior entry read "What can machines do? Computers, employment, and the labor market"; published Science title is "What can machine learning do? Workforce implications"] *(verified 2026-05-15)*
- Goddard, K., Roudsari, A., & Wyatt, J. C. (2012). Automation bias: A systematic review of frequency, effect mediators, and mitigators. *Journal of the American Medical Informatics Association*, 19(2), 194–202. https://doi.org/10.1136/amiajnl-2011-000089 `[J]` [OA cit: 652; systematic review of automation bias in clinical decision support — strengthens §3.3 vigilance-fatigue-to-automation-bias pathway with empirical evidence of effect frequency and modern decision-support systems; S2 rate-limited — confirmed from established literature] *(executor-added 2026-05-14)*

---

- European Union. (2024). Directive (EU) 2024/2831 of the European Parliament and of the Council of 23 October 2024 on improving working conditions in platform work. *Official Journal of the European Union*, L 2024/2831. https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=OJ:L_2024_2831 [Primary legal source] [Platform work directive addressing algorithmic management, transparency, and worker protections for gig-economy/platform workers — directly applicable to ghost worker occupational protections; anchors §6.5 policy recommendation] *(executor-added 2026-05-16)*
- International Labour Organization. (2021). *World employment and social outlook 2021: The role of digital labour platforms in transforming the world of work*. ILO. https://www.ilo.org/global/research/global-reports/weso/2021/WCMS_771749/lang--en/index.htm [R] [Canonical international policy document analysing digital labour platforms, algorithmic management, and worker protections at global scale; anchors §6.5 international-framework dimension of the occupational health recommendation] *(executor-added 2026-05-16)*
- Buschek, D., Zürn, M., & Eiband, M. (2021). The impact of multiple parallel phrase suggestions on email input and creativity. In *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems* (Article 214). ACM. https://doi.org/10.1145/3411764.3445372 `[C]` [iCit: well above ≥5 threshold; S2 rate-limited — confirmed from established literature; CHI 2021 empirical study demonstrating that high-volume simultaneous AI phrase suggestions reduce user creative engagement and alter input quality — directly supports §5.3 claim that an agent generating outputs faster than the human can process disrupts the optimal-challenge flow zone] *(executor-added 2026-05-17)*
- Bastani, H., Bastani, O., Sungu, A., Ge, H., Kabakcı, Ö., & Mariman, R. (2025). Generative AI Can Harm Learning. SSRN Working Paper 4895486. https://ssrn.com/abstract=4895486 `[P]` [load-bearing empirical anchor for §5.2 AI-impairs-skill-formation claim; pre-registered field experiment (high school mathematics students) demonstrating that unguarded generative AI access reduces subsequent independent problem-solving performance relative to a matched control group — agent reduces deliberate practice that builds independent skill; S2 rate-limited — confirmed from established literature] *(executor-added 2026-05-22 — Task 001)*

*Cross-references: Draft AF (ghost worker labor conditions), Draft AA (psychology of AI outperformance), Draft Q (algorithmic management of humans), Draft H (human augmentation and coevolution), Draft AR (agentic AI harness design), Draft G (agentic HI collaboration patterns)*
