# Draft AY — Machine Learning in the Industrial Automation Sector: Adoption, Architecture, and the Operator in the Loop

**Version:** v0.5 (2026-05-13)
**Status:** v0.5 — two new §3 subsections added: §3.5 precision agriculture (anchored to Wolfert et al. 2017 *Agricultural Systems* and Liakos et al. 2018 *Sensors*) and §3.6 grid operations and renewable forecasting (anchored to Wang et al. 2019 *Energy Conversion and Management* and Alimi et al. 2020 *IEEE Access*). All four new sources verified clean via OpenAlex + CrossRef (no retractions). Cross-reference wiring in §7.2 extended to add Draft Z as a direct connection through the grid-operations / energy-footprint axis. Citation counts re-verified for Lee/Bagheri/Kao 2015 (4731 → 4743), Lei et al. 2018 (2329 → 2342), and Sambasivan et al. 2021 (644 → 650).
**Next:** Expand §3.4 robotics/flexible manufacturing into a fuller subsection; add logistics-and-warehouse-automation subsection; add geographic-asymmetry subsection (Germany / Japan / South Korea / China concentration vs. deployment elsewhere); wire OT/IT cybersecurity dimension to the itsecbog companion track.

---

## Overview and Chapter Position

Industrial automation is the oldest large-scale deployment domain for machine intelligence. Programmable logic controllers (PLCs) entered factories in the late 1960s; distributed control systems (DCS) followed in the 1970s; statistical process control predates digital computing entirely. Long before "machine learning" became a category for general-purpose foundation models, factories were already running closed-loop optimisation, anomaly detection, and predictive scheduling on dedicated industrial hardware. The ML revolution of the 2010s and the foundation-model boom of the 2020s did not arrive in an empty room — they entered a domain with established control theory, decades of operator practice, formal safety standards, and a regulatory infrastructure that long predated the data-driven paradigm.

This chapter examines the perspectives that the industrial automation sector brings to the broader hybrid intelligence picture. It is the empirical companion to Draft AJ (IoT sensing for hybrid training) and Draft AP (embodied hybrid intelligence): where AJ describes how industrial sensing infrastructure produces the data that trains AI systems and AP discusses agents acting in physical environments, this draft examines the more conservative middle ground — production lines, refineries, power plants, and warehouses where ML augments existing automation rather than replacing it.

The chapter argues three things. First, the industrial sector treats ML as an extension of existing control theory and statistical process management, not as a paradigm shift — and this framing has substantive consequences for how models are validated, deployed, and decommissioned. Second, the operator and the domain engineer remain structurally central in industrial ML deployments, not because the technology cannot replace them but because liability, safety certification, and tacit process knowledge make full automation economically and legally unattractive in most regulated environments. Third, the gap between ML capability demonstrated in research benchmarks and ML capability deployed in production industrial settings is wider than in consumer or enterprise software domains — and the reasons are structural, not merely technical.

---

## §1 — The Pre-ML Baseline: Industrial Automation Before the Data-Driven Era

### 1.1 Three layers of classical industrial automation

Industrial automation systems are conventionally described as a three-layer hierarchy. The bottom layer is field instrumentation: sensors (temperature, pressure, vibration, flow, optical) and actuators (valves, motors, heaters, robotic end-effectors). The middle layer is control: PLCs running deterministic ladder logic at millisecond cycle times, DCS coordinating continuous processes across hundreds of control loops, and SCADA (Supervisory Control and Data Acquisition) systems aggregating telemetry for human operators. The top layer is enterprise resource planning (ERP) and manufacturing execution systems (MES) that integrate production with business logistics.

This hierarchy — codified in the ANSI/ISA-95.00.01-2010 standard (IEC 62264-1 Mod), *Enterprise-Control System Integration — Part 1: Models and Terminology* — defines where data lives, who owns it, and which systems are subject to which safety regimes. ML deployments must locate themselves within this architecture, and the location chosen has profound implications for what the model is permitted to do, how it is validated, and how it interacts with safety-critical control loops.

### 1.2 The PID controller and its conceptual shadow

The proportional-integral-derivative (PID) controller, developed in the 1920s and formalised by Ziegler and Nichols (1942), remains the dominant control element in industrial automation today. Åström and Hägglund (2001) — drawing on extensive industry survey work — observe that PID and PI controllers account for the overwhelming majority of regulatory control in process industries, with industry surveys at the time placing the share above 95% of all control loops. PID is interpretable, locally tunable, fails predictably, and is supported by a century of engineering literature on stability analysis.

This conceptual shadow matters for ML adoption. Industrial engineers evaluate ML systems against an implicit PID benchmark: can the model's behaviour be analysed for stability? Is its failure mode bounded? Can a domain engineer who has not read a deep learning textbook understand why the model output the value it did? When the answer to these questions is "no", ML faces an adoption barrier that has nothing to do with predictive accuracy.

### 1.3 Statistical process control and the statistical heritage

Shewhart's (1931) statistical process control framework — control charts, process capability indices (Cp, Cpk), and the assumption that a stable process produces variation within calculable bounds — established the data-analytic foundation of industrial quality. Six Sigma (Motorola, 1986; popularised by Welch at GE in the 1990s) extended this into management methodology. By the time the deep learning era arrived, factories had been running data-driven decision loops for nearly a century — but on tightly defined statistical models, with explicit assumptions about distribution, stationarity, and operator interpretation.

Modern ML enters this domain not as a new capability but as a more flexible function approximator competing with the established statistical toolkit. The competition is decided not on benchmark accuracy but on whether the ML system fits the validation, certification, and operator-trust workflows that already exist.

---

## §2 — The Data Infrastructure: Industry 4.0 and Cyber-Physical Systems

### 2.1 The Industry 4.0 framing

The term "Industry 4.0" was introduced by the German Federal Ministry of Education and Research at Hannover Messe 2011 and became the dominant strategic framing for industrial digitalisation across Europe and Asia by the mid-2010s, codified in the Kagermann, Wahlster & Helbig (2013) acatech final report *Recommendations for implementing the strategic initiative INDUSTRIE 4.0*. The framing identifies four prior industrial revolutions (steam, electricity, electronics/computing, and now cyber-physical integration) and positions the integration of physical production with networked computation as the fourth.

Lee, Bagheri & Kao (2015) provided one of the most cited architectural articulations: a 5C architecture (Connection, Conversion, Cyber, Cognition, Configuration) describing how raw sensor data is progressively transformed into actionable intelligence at successively higher levels of abstraction. This architecture is influential because it makes explicit where ML belongs in the stack — primarily in the "Cognition" layer, where patterns extracted from converted sensor data inform decisions — and where it does not (the connection and conversion layers, which remain the province of traditional industrial protocols and signal processing).

### 2.2 The Industrial Internet of Things

The Industrial Internet of Things (IIoT) is the consumer-facing IoT's larger, older sibling. Industrial sensor networks predate consumer IoT by decades; what changed in the 2010s was the integration of these networks with cloud platforms, the standardisation of protocols (OPC UA, MQTT for industrial use), and the cost reduction of edge compute that made it feasible to run inference close to the sensor.

Wang, Wan, Zhang, Li & Zhang (2016) and Zhong, Xu, Klotz & Newman (2017) surveyed the resulting "smart factory" architecture: dense sensor coverage, real-time telemetry aggregation, federated analytics, and feedback loops that shorten the time between observation and corrective action from hours (in classical SPC) to seconds. The data volumes are substantial — a single instrumented turbine produces gigabytes per day, a modern automotive assembly line produces terabytes — but the data is also highly structured, well-labelled (every sample carries equipment ID, timestamp, and sensor metadata), and produced under controlled conditions. This is a starkly different ML training environment from web-scraped text or user-generated images.

### 2.3 The brownfield problem

A critical asymmetry separates industrial ML deployment from greenfield consumer applications: most industrial sites are *brownfield* — installations whose equipment, control systems, and operator workflows were built decades before the ML era. The SCADA-systems literature documents that legacy installations in regulated sectors (chemicals, refining, power, water) routinely operate well past 15 years in service, with many sites still running PLCs that predate widespread internet connectivity (Pliatsios, Sarigiannidis, Lagkas & Sarigiannidis, 2020). Industrial control hardware is typically depreciated and replaced on 15–20-year cycles, against the 2–5-year refresh typical of IT equipment, and the resulting age asymmetry is the single largest practical obstacle to retrofit ML deployment.

Brownfield deployment imposes constraints that benchmark ML rarely confronts. Sensor coverage is partial and non-uniform — some loops are heavily instrumented while critical ones are blind. Data historians may store only down-sampled or aggregated values, not raw signals. Network bandwidth at the operational technology (OT) layer is often constrained by deterministic-timing requirements that prohibit the bandwidth bursts associated with cloud upload. Adding ML to a brownfield site is therefore frequently not a software project but a sensor retrofit, network redesign, and operator-training programme combined.

---

## §3 — Application Domains

### 3.1 Predictive maintenance

Predictive maintenance is the most mature ML application in industrial settings and probably the only one with consistent positive return on investment across sectors. The premise is straightforward: sensor data (vibration, acoustic emission, temperature, current draw, lubricant condition) carries signatures of incipient component failure that precede catastrophic failure by hours to weeks. ML models trained on labelled fault histories can detect these signatures earlier than threshold-based alarms and with fewer false positives than purely statistical methods.

Lei, Li, Guo, Li, Yan & Lin (2018) provided a comprehensive review of machinery health prognostics methods, distinguishing data-driven approaches (neural networks, support vector machines, gaussian process regression) from physics-informed approaches that combine first-principles degradation models with data-driven residual modelling. The review's central finding — that hybrid approaches combining physical models with data-driven correction generally outperform purely data-driven approaches in low-data regimes typical of industrial deployment — has become a standard observation in industrial ML practice.

The economic case for predictive maintenance is well-established. The McKinsey (2017) *Smartening Up With Artificial Intelligence (AI) — What's in it for Germany and its Industrial Sector?* report estimates that AI-enhanced predictive maintenance can deliver up to 20% asset productivity gains, up to 20% downtime reduction, up to 25% inspection cost reduction, and up to 10% reduction in overall maintenance costs. (Larger figures often quoted in secondary consulting literature — 30–50% downtime reduction, 10–40% maintenance cost reduction — should be treated cautiously: they aggregate across heterogeneous case studies rather than reflecting a single audited deployment.) These figures are large enough that even moderately reliable models pay for the deployment cost. The hybrid intelligence dimension is significant: the ML system rarely makes the maintenance decision unilaterally; it raises an alert, the maintenance engineer evaluates the alert against operational context the model does not see (planned shutdowns, parts availability, crew schedules), and the human authorises or defers the intervention. This is a co-pilot pattern, not an autopilot pattern.

### 3.2 Quality control and visual defect detection

Computer vision for industrial quality control is the second-most-deployed industrial ML application, driven by the maturation of convolutional architectures during the 2012–2018 period and the subsequent transformer-based vision models. Defect detection on assembly lines — surface scratches on automotive panels, solder joint defects on PCBs, cosmetic flaws on consumer goods — is now routinely delegated to learned vision systems that outperform threshold-based machine vision and approach trained human inspectors on defined defect classes.

The regulatory dimension is consequential. In sectors with formal product certification (medical devices, aerospace, pharmaceuticals), the substitution of a learned classifier for a rule-based inspection system requires re-validation of the entire quality system under standards such as ISO 13485 (medical devices), AS9100 (aerospace), or 21 CFR Part 11 (FDA-regulated industries). The cost and timeline of re-validation often exceeds the cost of training the model itself and structurally favours the deployment of ML in less regulated parts of the production line — incoming material inspection, packaging — over safety-critical assembly steps.

### 3.3 Process optimisation in continuous industries

Continuous process industries (oil refining, petrochemicals, steel, pulp and paper, cement, power generation) have been deploying advanced process control (APC) since the 1980s. Model predictive control (MPC) — solving a constrained optimisation over a forward-looking horizon at each control step — became standard in refining by the late 1990s. ML enters this domain primarily through two channels: (a) as a learned plant model replacing or augmenting first-principles models inside MPC, and (b) as a soft sensor inferring unmeasured quality variables (product composition, conversion efficiency) from measured variables in real time.

The economic stakes are large: even single-percent improvements in product yield or energy efficiency at refinery scale translate to multi-million-dollar annual gains. The technical challenge, equally large, is that continuous process plants run far more often in *steady state* than in transient operation, meaning that the data available for training is dominated by narrow operating regimes and contains little information about the dynamics that matter most when something goes wrong. ML models in this domain frequently exhibit the brittleness pattern characteristic of out-of-distribution generalisation — strong performance during routine operation, unreliable performance during the upset conditions where good control matters most.

### 3.4 Robotics and flexible manufacturing

Industrial robotics has transformed from the rigid, blind, pre-programmed manipulators of the 1970s–1990s to learning-capable systems that can handle limited variability in part position, geometry, and material. The shift was enabled by three convergent advances: low-cost depth sensing (RGB-D cameras since the Kinect era), vision-language-action models that can be prompted with task descriptions rather than coded with explicit motion plans, and reinforcement learning from sim-to-real transfer pipelines that train policies in simulation and deploy them on physical hardware.

Collaborative robots ("cobots") — manipulators designed to operate safely alongside human workers without cages — represent a distinct deployment pattern central to the hybrid intelligence framing. Cobot deployments typically involve task division between human and machine at a finer granularity than classical robot cells: the human handles high-variability or judgement-heavy operations while the robot handles repetitive or ergonomically punishing operations on the same workpiece, in real time. This is the most explicitly hybrid form of industrial automation. The full treatment of embodied agency belongs in Draft AP; this section establishes only that flexible manufacturing is the domain where industrial automation and the broader agentic AI literature most directly intersect.

### 3.5 Precision agriculture

Precision agriculture is the industrial-ML domain that least resembles a factory and that nevertheless reproduces nearly the same deployment patterns. Field sensors (soil moisture probes, leaf chlorophyll meters, multispectral aerial imagery from satellites and UAVs) feed models that recommend variable-rate fertilisation and irrigation, predict yields, and detect plant disease. Wolfert, Ge, Verdouw & Bogaardt (2017) surveyed the data-pipeline architecture of "smart farming" and identified the same brownfield constraints documented in §2.3 — heterogeneous equipment, partial sensor coverage, intermittent connectivity in agricultural settings — combined with sector-specific issues such as seasonal data sparsity (a single growing season produces only one full label cycle), farmer concerns about vendor lock-in and data ownership, and the asymmetric value of false negatives (a missed disease outbreak can erase a season's yield while a false positive merely wastes inputs).

Liakos, Busato, Moshou, Pearson & Bochtis (2018) catalogued ML methods applied across crop management, livestock management, water management and soil management; their consistent finding that supervised learning dominates the deployed literature, and that deployment success correlates strongly with domain-expert involvement in dataset labelling and validation, echoes the tacit-knowledge pattern in §4.2. The hybrid intelligence reading is that precision agriculture is not "robot farming" but a co-pilot architecture in which the farmer retains agronomic and economic judgement while ML extends perceptual reach across larger areas and longer timescales than human inspection can cover.

### 3.6 Grid operations and renewable forecasting

Electric power systems are a particularly demanding industrial ML domain because the underlying physical system — transmission and distribution grids, heterogeneous generation portfolios, demand response — must be balanced in real time on millisecond-to-minute timescales to prevent cascading failures, while the increasing share of variable renewable generation has made short-horizon forecasting accuracy materially consequential for system economics and stability. Wang, Lei, Zhang, Zhou & Peng (2019) surveyed deep-learning approaches to renewable-energy forecasting across solar, wind, and hydropower; their review establishes that hybrid models combining numerical-weather-prediction outputs with learned residuals consistently outperform either physics-only or data-only approaches alone — a recurrence of the physics-informed-ML pattern already identified in §3.1's predictive-maintenance discussion.

Alimi, Ouahada & Abu-Mahfouz (2020) reviewed ML applications in power-system security and stability assessment and reach a conclusion that mirrors §5.2's certification gap: real-time control loops in safety-critical grid functions remain dominated by classical methods (model-based state estimation, security-constrained optimal power flow, model predictive control), while ML enters primarily in advisory roles — anomaly detection in PMU (phasor measurement unit) streams, condition monitoring for transformers and switchgear, and short-horizon load and renewable-generation forecasting that feed into the classical optimisation engines. The grid-operations case is also the cleanest empirical link between Draft AY and Draft Z (frugal AI / environmental footprint), since the optimisation target itself — minimising fuel use and curtailment while meeting demand — has direct energy and emissions consequences.

---

## §4 — The Hybrid Intelligence Picture: Where Humans Remain Central

### 4.1 The operator-in-the-loop is the default architecture

In nearly every industrial ML deployment outside narrowly bounded edge cases, a human operator or engineer retains authority over significant decisions. The model recommends; the human authorises. This is not vestigial caution — it is structurally enforced by liability allocation, certification requirements, and the practical observation that domain experts catch failure modes that the model's training distribution did not cover.

The pattern reverses the popular framing of ML as the decisive intelligence with humans in supervisory roles. In industrial settings the human remains the decision-maker on consequential actions; the ML system extends the operator's perceptual reach (across more sensors than a human can monitor) and pattern-recognition capacity (across longer histories than a human can recall), but does not substitute for the operator's judgement. This is hybrid intelligence in its most established form, predating the term itself by decades.

### 4.2 Tacit process knowledge as ML training input

Industrial processes contain enormous amounts of tacit knowledge — operator heuristics, equipment-specific quirks, historical incidents whose lessons are remembered by the on-shift crew but not formally documented. Successful industrial ML deployments treat this tacit knowledge as a training input, not a substitute target. The pattern is to embed domain experts in the data labelling and model evaluation loop, to allow operators to flag model outputs as anomalous (creating a continuous fine-tuning signal), and to architect deployments so that operator overrides are themselves recorded and inform future training.

This is the same loop that consumer-facing RLHF systems implement at scale, but with crucial differences: the human raters are domain experts (not crowdworkers); the feedback signal is high-stakes rather than preference-based; and the loop closes within a single facility rather than across millions of users. Draft AF (human labour in AI training) examines the labour dimension of the consumer pattern; the industrial pattern is structurally different and merits separate treatment.

### 4.3 Trust calibration and the alert-fatigue problem

Industrial ML systems frequently generate more alerts than operators can act on. A predictive maintenance system that flags 5% of machinery as "elevated risk" daily across a refinery produces hundreds of alerts per shift; if even 10% of those alerts represent false positives, operators learn to discount the system within weeks. The literature on alert fatigue — originating in clinical contexts but with patterns that translate directly to industrial alarm management (Cvach, 2012) — consistently shows that low-precision alarm systems degrade rather than improve safety outcomes.

The implication is that operator trust in industrial ML is a *calibration* problem, not a *capability* problem. A 99%-accurate model that floods the operator with false positives loses the operator; an 85%-accurate model that flags only the highest-confidence cases retains trust. Industrial ML deployment success therefore depends as much on the threshold engineering, alert routing, and confidence-presentation interface as on the underlying model. This connects to Draft I (LLM epistemic limits and calibration failure): the same calibration concerns that shape responsible LLM deployment have been studied for forty years in the industrial alarm-management literature.

---

## §5 — Adoption Barriers and Economic Friction

### 5.1 The data-quality bottleneck

The popular ML narrative emphasises algorithm and compute as the binding constraints. In industrial deployment, the binding constraint is almost always data quality: missing sensors, miscalibrated instruments, drifting baselines, undocumented changes to equipment that invalidate historical training data, and labelling regimes that capture outcomes but not contextual variables. Industrial ML practitioners commonly report that 60–80% of project effort is consumed by data acquisition, cleaning, and labelling — proportions consistent with the broader ML practitioner literature (Sambasivan et al., 2021).

### 5.2 Certification and the validation gap

Safety-critical industrial systems are governed by functional safety standards (IEC 61508 for general industrial systems, IEC 61511 for process industries, ISO 26262 for automotive, DO-178C for aviation software). These standards require demonstrable correctness analysis — tracing requirements through design through implementation through test — for any element implicated in safety functions. Conventional ML approaches sit uneasily within this framework. The research literature on ML certification — running under terms such as "safe ML", "explainable AI for safety", or "assurance cases for learned components" (Burton, Gauerhof & Heinzemann, 2017) — has produced principled approaches but no widely deployed certification path for general ML systems in safety-critical loops.

The practical effect is that ML in safety-critical industrial applications is typically deployed in advisory mode (informing operators) rather than in direct control loops. The few exceptions — primarily in non-life-safety domains such as energy efficiency optimisation or cosmetic quality control — illustrate the rule.

### 5.3 The economic friction of deployment

Industrial automation projects routinely cost 10–100× the apparent value of the underlying ML model itself once integration costs are accounted for: sensor retrofits, OT/IT integration work, operator training, change management, validation, and ongoing model monitoring. This economic friction is the proximate explanation for the visible adoption gap between published industrial ML research (which is large and growing) and deployed industrial ML (which lags well behind). Bertolini, Mezzogori, Neroni & Zammori (2021) surveyed the academic-industrial gap and identified deployment cost rather than algorithmic capability as the dominant explanation.

---

## §6 — Workforce Transformation

### 6.1 The substitution-versus-complementation question

The economic literature on automation and labour is voluminous and contested. Acemoglu and Restrepo (2020) estimated that the deployment of one additional industrial robot per thousand workers reduces US local-labour-market employment-to-population ratio by approximately 0.2 percentage points and wages by 0.42% (Acemoglu & Restrepo, 2020, *Journal of Political Economy* 128(6), pp. 2188–2244). The findings are widely cited as evidence that industrial automation has been net-substitutive for affected workers despite aggregate productivity gains.

The ML wave introduces a different substitution pattern. Where industrial robots primarily substituted for routine manual labour, ML in industrial settings primarily substitutes for routine cognitive labour (process monitoring, scheduling, quality inspection). Brynjolfsson, Rock and Syverson (2021) — in the *American Economic Journal: Macroeconomics* version of their earlier NBER working paper — argued that the workforce effects of ML would differ from prior automation waves precisely because the substituted tasks involve different occupational profiles, and that aggregate productivity statistics will lag the underlying capability gains until complementary intangible investments mature (the "productivity J-curve" pattern).

### 6.2 The reskilling question and the maintenance paradox

A consistent empirical finding in the industrial automation literature is that successful automation does not eliminate the human workforce but transforms it: factories with the highest automation intensity often employ as many or more technically skilled workers per unit output than less-automated competitors, but the skill profile shifts toward maintenance, calibration, programming, and exception handling (Frank, Dalenogare & Ayala, 2019). The "lights-out factory" remains rare in practice because the cost of human absence — when something goes wrong — exceeds the cost of human presence.

The implication for ML-augmented industrial workplaces is that workforce planning should anticipate not workforce reduction but workforce reskilling. The political-economy and equity dimensions of this transition belong to Draft F (commons extraction and inequality) and Draft AF (human labour in AI training); this draft establishes only the empirical baseline that the substitution-versus-complementation question is unresolved and likely heterogeneous across industries.

---

## §7 — Open Questions and Cross-Reference Wiring

### 7.1 What this draft does not yet cover

§3.5 and §3.6 (added in v0.5) now treat precision agriculture and grid operations / renewable forecasting respectively. A complete treatment of industrial ML perspectives would still extend to: logistics and warehouse automation as the most rapidly growing industrial ML deployment area in 2024–2026 (Amazon Robotics, Symbotic, AutoStore); the cybersecurity dimension of industrial ML (poisoned models, adversarial inputs to vision QC systems, OT/IT boundary attacks — partially covered in the itsecbog companion track); and the geographic asymmetry of industrial ML deployment (concentration in Germany, Japan, South Korea, China; underdeployment elsewhere). A fuller treatment of §3.4 robotics and flexible manufacturing also remains pending. These are flagged for the next expansion cycle.

### 7.2 Cross-references

This draft connects most directly to:
- **Draft AJ** (IoT sensing for hybrid training) — the data infrastructure described in §2 is the upstream of AJ's training pipelines; the agricultural sensor networks of §3.5 and the PMU streams of §3.6 are concrete instances of AJ's sensing-to-training pattern
- **Draft AP** (embodied hybrid intelligence) — the robotics discussion in §3.4 is the upstream of AP's full embodiment treatment
- **Draft N** (AI/ML ecosystem) — industrial ML is a distinct ecosystem with its own vendors (Siemens, ABB, Rockwell, Honeywell, Schneider) and its own research communities
- **Draft H** (human augmentation and co-evolution) — §4's operator-in-the-loop pattern is one of the longest-running examples of human-machine co-evolution
- **Draft AF** (human labour in AI training) — §6's workforce dimension shares structural features with AF's account of the AI labour layer
- **Draft AC** (model vs. human performance) — industrial ML provides decades of validation data on the model-vs-human comparison in well-defined task domains
- **Draft AB** (credit, blame, and responsibility gaps) — §5.2's certification discussion is a concrete instance of AB's accountability-allocation problem
- **Draft P** (governance and compliance) — functional safety standards are a mature governance regime that ML governance discussions can learn from rather than reinvent
- **Draft I** (LLM epistemic limits) — §4.3's alarm-fatigue/calibration discussion connects directly to I's calibration-failure analysis
- **Draft Z** (frugal AI / environmental footprint) — §3.6's grid-operations and renewable-forecasting use cases are also the cleanest empirical link between industrial ML and the energy-cost / emissions framing of Draft Z

---

## Key Sources

### Peer-reviewed journals and conferences

- Acemoglu, D., & Restrepo, P. (2020). Robots and jobs: Evidence from US labor markets. *Journal of Political Economy*, 128(6), 2188–2244. https://doi.org/10.1086/705716 [OA cit: 3324; CrossRef retraction check 2026-05-06: no update-to entry] [J]
- Alimi, O. A., Ouahada, K., & Abu-Mahfouz, A. M. (2020). A Review of Machine Learning Approaches to Power System Security and Stability. *IEEE Access*, 8, 113512–113531. https://doi.org/10.1109/access.2020.3003568 [OA cit: 357; CrossRef retraction check 2026-05-13: no update-to entry] [J]
- Åström, K. J., & Hägglund, T. (2001). The future of PID control. *Control Engineering Practice*, 9(11), 1163–1175. https://doi.org/10.1016/S0967-0661(01)00062-4 [OA cit: 1393; CrossRef retraction check 2026-05-06: no update-to entry] [J]
- Bertolini, M., Mezzogori, D., Neroni, M., & Zammori, F. (2021). Machine Learning for industrial applications: A comprehensive literature review. *Expert Systems with Applications*, 175, 114820. https://doi.org/10.1016/j.eswa.2021.114820 [OA cit: 524] [J]
- Brynjolfsson, E., Rock, D., & Syverson, C. (2021). The Productivity J-Curve: How Intangibles Complement General Purpose Technologies. *American Economic Journal: Macroeconomics*, 13(1), 333–372. https://doi.org/10.1257/mac.20180386 [OA cit: 531; CrossRef retraction check 2026-05-06: no update-to entry; published version of NBER WP 25148] [J]
- Burton, S., Gauerhof, L., & Heinzemann, C. (2017). Making the Case for Safety of Machine Learning in Highly Automated Driving. In *Computer Safety, Reliability, and Security — SAFECOMP 2017 Workshops*, Lecture Notes in Computer Science, Vol. 10489, pp. 5–16. Springer. https://doi.org/10.1007/978-3-319-66284-8_1 [OA cit: 129; CrossRef retraction check 2026-05-06: no update-to entry] [C]
- Cvach, M. (2012). Monitor alarm fatigue: An integrative review. *Biomedical Instrumentation & Technology*, 46(4), 268–277. https://doi.org/10.2345/0899-8205-46.4.268 [OA cit: 592; CrossRef retraction check 2026-05-06: no update-to entry; clinical-origin literature whose patterns translate to industrial alarm management] [J]
- Frank, A. G., Dalenogare, L. S., & Ayala, N. F. (2019). Industry 4.0 technologies: Implementation patterns in manufacturing companies. *International Journal of Production Economics*, 210, 15–26. https://doi.org/10.1016/j.ijpe.2019.01.004 [OA cit: 2684] [J]
- Lee, J., Bagheri, B., & Kao, H.-A. (2015). A Cyber-Physical Systems architecture for Industry 4.0-based manufacturing systems. *Manufacturing Letters*, 3, 18–23. https://doi.org/10.1016/j.mfglet.2014.12.001 [OA cit: 4743 (re-verified 2026-05-13); CrossRef retraction check 2026-05-06: no update-to entry] [J]
- Lei, Y., Li, N., Guo, L., Li, N., Yan, T., & Lin, J. (2018). Machinery health prognostics: A systematic review from data acquisition to RUL prediction. *Mechanical Systems and Signal Processing*, 104, 799–834. https://doi.org/10.1016/j.ymssp.2017.11.016 [OA cit: 2342 (re-verified 2026-05-13)] [J]
- Liakos, K. G., Busato, P., Moshou, D., Pearson, S., & Bochtis, D. (2018). Machine Learning in Agriculture: A Review. *Sensors*, 18(8), 2674. https://doi.org/10.3390/s18082674 [OA cit: 2913; CrossRef retraction check 2026-05-13: no update-to entry] [J]
- Pliatsios, D., Sarigiannidis, P., Lagkas, T., & Sarigiannidis, A. G. (2020). A Survey on SCADA Systems: Secure Protocols, Incidents, Threats and Tactics. *IEEE Communications Surveys & Tutorials*, 22(3), 1942–1976. https://doi.org/10.1109/COMST.2020.2987688 [OA cit: 296; CrossRef retraction check 2026-05-07: no update-to entry] [J]
- Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021). "Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI. *CHI 2021*. https://doi.org/10.1145/3411764.3445518 [OA cit: 650 (re-verified 2026-05-13)] [C]
- Wang, H., Lei, Z., Zhang, X., Zhou, B., & Peng, J. (2019). A review of deep learning for renewable energy forecasting. *Energy Conversion and Management*, 198, 111799. https://doi.org/10.1016/j.enconman.2019.111799 [OA cit: 1100; CrossRef retraction check 2026-05-13: no update-to entry] [J]
- Wang, S., Wan, J., Zhang, D., Li, D., & Zhang, C. (2016). Towards smart factory for industry 4.0: A self-organized multi-agent system with big data based feedback and coordination. *Computer Networks*, 101, 158–168. https://doi.org/10.1016/j.comnet.2015.12.017 [OA cit: 1371; CrossRef retraction check 2026-05-06: no update-to entry] [J]
- Wolfert, J., Ge, L., Verdouw, C. N., & Bogaardt, M.-J. (2017). Big Data in Smart Farming – A review. *Agricultural Systems*, 153, 69–80. https://doi.org/10.1016/j.agsy.2017.01.023 [OA cit: 2899; CrossRef retraction check 2026-05-13: no update-to entry] [J]
- Zhong, R. Y., Xu, X., Klotz, E., & Newman, S. T. (2017). Intelligent Manufacturing in the Context of Industry 4.0: A Review. *Engineering*, 3(5), 616–630. https://doi.org/10.1016/j.eng.2017.05.015 [OA cit: 2754; CrossRef retraction check 2026-05-06: no update-to entry] [J]

### Institutional and standards sources

- ANSI/ISA-95.00.01-2010 (IEC 62264-1 Mod). *Enterprise-Control System Integration — Part 1: Models and Terminology*. International Society of Automation. (Edition verified 2026-05-07; superseded in 2025 by ANSI/ISA-95.00.01-2025 — the 2010 edition was the operative reference for the deployment patterns described in §1.) [R]
- IEC 61508 (2010). *Functional Safety of Electrical/Electronic/Programmable Electronic Safety-Related Systems*. International Electrotechnical Commission. [R]
- IEC 61511 (2016). *Functional Safety — Safety Instrumented Systems for the Process Industry Sector*. International Electrotechnical Commission. [R]
- ISO 26262 (2018). *Road vehicles — Functional safety*. International Organization for Standardization. [R]
- Kagermann, H., Wahlster, W., & Helbig, J. (Eds.) (2013). *Securing the future of German manufacturing industry — Recommendations for implementing the strategic initiative INDUSTRIE 4.0: Final report of the Industrie 4.0 Working Group*. April 2013, 84 pp. acatech — National Academy of Science and Engineering. (PDF verified 2026-05-07; saved to Kilder/Kagermann2013_Industrie4.0_acatech.pdf) [R]

### Foundational / historical

- Shewhart, W. A. (1931). *Economic Control of Quality of Manufactured Product*. D. Van Nostrand Company. [Foundational; no modern verification needed] [Book]
- Ziegler, J. G., & Nichols, N. B. (1942). Optimum settings for automatic controllers. *Transactions of the ASME*, 64, 759–768. [Foundational; no modern verification needed] [J]

### Industry / consulting reports

- McKinsey & Company (2017). *Smartening up with Artificial Intelligence (AI) — What's in it for Germany and its Industrial Sector?* Digital McKinsey, April 2017. (PDF verified 2026-05-07; saved to Kilder/McKinsey2017_SmarteningUpAI_Germany.pdf. Predictive-maintenance figures used in §3.1 are taken directly from §3.2.1 of the report.) [R]

### Tools and platforms (industrial automation reference)

- Siemens MindSphere — industrial IoT platform
- GE Predix — industrial analytics platform (status of GE's strategic position to be verified)
- PTC ThingWorx — industrial IoT and AR platform
- AVEVA (formerly Wonderware/OSIsoft) PI System — industrial historian, dominant in process industries
- Rockwell FactoryTalk — manufacturing automation platform
- ABB Ability — industrial digital platform

(These are reference points for the industrial-ecosystem dimension of §2 and §5; not citations.)
