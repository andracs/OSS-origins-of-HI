# Draft AJ — Sensing for Learning: Tuning IoT and Human Interactions as Training Data Infrastructure for Hybrid Intelligence

**Version:** v0.3 (2026-05-13)  
**Status:** v0.3 — citation pass; annotation queue Tasks 004, 005, 006 resolved via tri-source chain (OpenAlex + CrossRef). Core framework stable; remaining gap is iCit verification on legacy foundational sources (Tobin 2017, Grieves 2002, Tao 2018, Krause 2008).  
**Next:** Resolve annotation Task 007 (`[iCit: check]` placeholders on four foundational sources via OpenAlex `cited_by_count`); expand §3 with concrete sensor placement algorithms; cross-ref Draft T, Draft H, Draft V, Draft AC.

---

## Overview and Chapter Position

In the dominant narrative of AI development, sensors and human interfaces are *data sources* — infrastructure that produces raw material which models consume. This chapter inverts that framing. When the goal is to build hybrid intelligence systems that improve through experience, the sensors and interaction flows that generate training data are not neutral instruments: they are *design choices* that determine what the system can learn, how fast, and how reliably.

The chapter asks: given a target hybrid intelligence capability, how should IoT sensor arrays and human interaction interfaces be configured — tuned, placed, sampled, and combined — to maximise the training value of the data they produce? It also asks a second question that is increasingly urgent: when real sensor data is insufficient, too expensive, or too dangerous to collect, how can simulation and generative synthesis extend the training distribution?

The answers connect hardware (sensor physics), software (sampling and compression), cognitive science (what human interactions reveal about preferences and intent), and machine learning methodology (active learning, sim-to-real transfer, distribution coverage). This chapter synthesises these threads for hybrid intelligence system designers.

The chapter is positioned after the model capability drafts (A–AG) and the agentic infrastructure drafts (T, AH, AI). It addresses the data dimension of hybrid intelligence: not what models do with data, but how the physical and interactional world is structured to produce the data models need.

---

## §1 — The Training Data Design Problem

### 1.1 From passive collection to deliberate design

The standard mental model of AI training data is extractive: data exists in the world (web text, images, sensor logs), we collect what we can, we train models on it. This model is appropriate for foundation models trained on internet-scale corpora, but it is inadequate for hybrid intelligence systems deployed in specific physical environments.

In a deployed hybrid system — a factory floor monitored by a sensor network, a hospital ward with wearable devices, a smart-city intersection with camera and LIDAR arrays — the data-generating apparatus is under the designer's control. This control is underutilised. Most IoT deployments are designed for operational monitoring (alert me if temperature exceeds threshold) not for training optimality (Wuest et al., 2016). Most human-facing interfaces are designed for usability (make the task easy for the user) not for information density (make the human interaction reveal as much as possible about the underlying state).

Treating sensing and interaction design as training data design shifts the engineering question from "what data can we collect?" to "what data *should* we collect, and how should we structure the collection to maximise learning value?"

### 1.2 The learning objective defines the sensing requirement

The first step in deliberate sensing design is to specify what the model is expected to learn. Different learning objectives impose different requirements on training data:

**Classification tasks** (is this component defective? is this gait pattern anomalous?) require representative samples of all classes, including rare failure modes. Passive collection systematically undersamples rare events. Sensor design must include mechanisms for capturing edge cases: triggered recording, stratified sampling, or synthetic augmentation of underrepresented classes.

**Regression and prediction tasks** (what is the remaining useful life of this motor? what will this patient's blood glucose be in 30 minutes?) require data that spans the range of conditions the model will encounter at inference time. Passive collection captures the distribution of common conditions, not the margins.

**Reinforcement learning** requires exploration data: the model must try actions and observe outcomes. Passive collection of expert behaviour is insufficient; the sensor array must be able to record the consequences of exploratory — and sometimes failing — actions safely.

**Human preference learning** (RLHF, inverse reinforcement learning) requires signal about human evaluations, not merely human behaviour. Interaction interface design must elicit preferences explicitly or capture implicit signals that are informative about preference.

In each case, the data requirement is specific to the learning objective, and the sensing apparatus must be designed to meet it.

---

## §2 — Active Sensing and Sensor Optimisation

### 2.1 Active learning as a sensing philosophy

Active learning is the machine learning framework in which the model participates in selecting which data points to label or collect next, based on which points would most reduce its uncertainty (Settles 2009). Applied to sensing, active learning implies that the sensor network should not simply collect data continuously — it should prioritise data collection in regions of state space where the model is most uncertain.

The practical implementation varies by application:

- In an industrial IoT context: a quality-control model flags components for additional sensor measurement when its confidence on the production-line sensors falls below a threshold — the additional sensors are deployed only where needed
- In a clinical wearable context: a continuous glucose monitor increases its sampling rate when the trajectory of readings suggests an approaching anomaly, preserving battery life while capturing the critical transition (Cappon et al., 2019)
- In a robotics context: the robot actively moves to positions that maximise sensor coverage of poorly-understood regions of the workspace (Bajcsy, 1988)

Active sensing requires a coupling between the model and the sensing apparatus that is not present in standard monitoring deployments. The model must be able to *query* the sensing apparatus, and the apparatus must be able to respond. This is an architectural commitment with implications for latency, bandwidth, and system complexity.

### 2.2 Optimal sensor placement

When sensor placement is a design choice — as in a new facility or a planned sensor network — the placement problem can be stated formally: where should sensors be located to maximise information gain about the quantities of interest, subject to cost constraints?

This is a well-studied problem in robotics, environmental monitoring, and geophysics. Key approaches:

**Information-theoretic placement**: maximise mutual information between sensor readings and the target variable (Krause et al. 2008). Requires a prior model of how the target variable varies in space, which can itself be learned from initial sparse measurements.

**Coverage-based placement**: ensure that all points in the monitored space are within sensing range of at least one sensor (Schwager et al. 2009). Appropriate when the target variable can occur anywhere and the sensing footprint of each sensor is bounded.

**D-optimal experimental design**: place sensors to minimise the variance of model parameter estimates — a framework inherited from statistics that is particularly applicable to regression tasks on spatial phenomena (Atkinson & Donev, 1992).

In practice, deployments use heuristic approaches (uniform grid, expert placement) because formal optimisation is computationally expensive for large spaces. The key insight for hybrid intelligence designers is that *sensor placement is a modelling decision* with quantifiable consequences for training data quality — it should not be left entirely to facilities engineers.

### 2.3 Sampling rate, resolution, and the temporal dimension

Sensors operate in continuous time; models train on discrete data. The mapping from continuous sensing to discrete training samples is a sequence of decisions — sampling rate, compression, aggregation — each of which determines what information is preserved and what is lost.

The Nyquist-Shannon sampling theorem gives the theoretical lower bound for lossless representation of a bandlimited signal: sample at twice the highest frequency of interest. In practice, many IoT applications sample at rates determined by bandwidth and storage constraints, not by the frequency content of the signal. The result is systematic aliasing of phenomena that occur faster than the sampling rate.

For hybrid intelligence training, the relevant question is not "what is the highest frequency in the signal?" but "what is the highest frequency of the phenomena the model needs to learn?" These differ. A vibration sensor monitoring a motor shaft may have high-frequency mechanical components that are irrelevant to the training objective (predicting bearing failure) and low-frequency patterns (gradual change in vibration signature over weeks) that are highly relevant. The sampling strategy should be designed around the learning objective.

Adaptive sampling strategies — variable sampling rates triggered by signal features — are an active research area in IoT, with strong theoretical foundations in event-triggered and self-triggered control (Heemels, Johansson, & Tabuada, 2012), and are directly motivated by the training data design perspective.

---

## §3 — Human Interactions as Structured Information

### 3.1 The human as a sensor

In hybrid intelligence systems, humans are not merely users — they are information sources about the state of the world, about their own preferences and intentions, and about the correctness or incorrectness of AI outputs. Interaction interface design that is optimised for usability captures a fraction of this information; design that is optimised for information density can capture substantially more.

The richest source of human information in current AI systems is feedback: when a user corrects an AI output, accepts a suggestion, or explicitly rates a result, they are providing a labelled training signal. RLHF (Reinforcement Learning from Human Feedback) has made this explicit at the foundation model level (Christiano et al., 2017; Ouyang et al., 2022); the same principle applies to deployed hybrid systems.

But explicit feedback is effort-intensive, and users resist feedback interfaces that slow them down. The design challenge is to capture *implicit* feedback — signals about preference and correctness that are embedded in ordinary interaction behaviour — without increasing user burden.

### 3.2 Implicit feedback signals

Interactions in digital systems leave rich behavioural traces that are informative about user preferences and AI output quality (Joachims et al., 2005):

- **Dwell time**: how long a user spends on an AI-generated output before acting — longer dwell may indicate uncertainty or dissatisfaction
- **Edit rate**: whether and how much a user modifies an AI suggestion before accepting it — high edit rate indicates low output quality
- **Selection from alternatives**: when presented with multiple AI outputs, which the user chooses — a direct preference signal
- **Task completion rate**: whether the user completes the task successfully with AI assistance — a downstream signal of AI utility
- **Error correction**: when the user explicitly corrects an AI error — a strong negative training signal

These signals are generated by normal interaction without requiring additional user effort. Designing interaction flows that make these signals recoverable — rather than losing them in aggregate metrics — is a core task of HCI design for hybrid intelligence.

An important caveat: implicit feedback signals are biased. Users who find an AI output unsatisfactory may abandon the task rather than correct it — the correction signal is missing precisely where the AI most failed (Joachims et al., 2005; Schnabel et al., 2016). Interface design should include mechanisms to capture abandonment and dissatisfaction, not only success.

### 3.3 Interaction flow design for training data coverage

The distribution of human interactions with an AI system is determined partly by user preferences and partly by the design of the interaction flow. Menu structures, default options, and affordances all shape which paths users take through the interaction space.

This shaping is exploitable for training data purposes: interaction flows can be designed to ensure coverage of the training distribution the model requires. In practice, this means:

- **Varied default contexts**: ensure that different users encounter the AI in different states, so the training data covers the range of contexts the AI will face at deployment
- **Structured elicitation**: in high-value training data collection phases, use interaction flows that explicitly ask users to encounter edge cases or to provide comparative judgments
- **Randomised assignment**: in deployments with multiple AI variants, randomly assign users to variants so that all variants receive training feedback — the clinical trial design principle applied to HCI, with the online controlled experiments (A/B testing) literature providing the canonical engineering framework (Kohavi et al., 2009)

The ethical constraints are significant: users must consent to their interactions being used as training data, and the interaction flow must not be deceptive or manipulative in its data-collection intent. The EU AI Act and GDPR jointly impose transparency and purpose-limitation requirements that constrain interaction-as-data-collection (GDPR Art. 5(1)(b); EU AI Act Art. 10; Wachter & Mittelstadt, 2019). The GDPR purpose-limitation principle (Art. 5(1)(b)) prohibits processing data for purposes incompatible with those for which it was originally collected — users interacting with a deployed AI system may not have consented to those interactions becoming training data for future model versions, making implicit-feedback harvesting legally complex without explicit re-consent or a compatible-purpose determination. The EU AI Act Art. 10 additionally imposes transparency and quality requirements on training data for high-risk AI systems, requiring documentation of data provenance and collection practices.

---

## §4 — Synthetic and Simulated Training Data

### 4.1 Why real sensor data is insufficient

Even well-designed sensor networks and interaction flows produce training data that is insufficient in three systematic ways:

**Rarity of critical events**: failure modes, extreme conditions, and safety-relevant scenarios occur rarely in operation. A model trained only on operational data will be poorly calibrated on the very situations where accuracy matters most (He & Garcia, 2009).

**Cost of exploration**: training reinforcement learning agents in the real world requires exploring sub-optimal and sometimes damaging actions. Physical exploration of a robot arm in a factory, or a control system in a power grid, is dangerous and expensive (García & Fernández, 2015).

**Label scarcity**: many high-value labels require expert human annotation at cost — medical image segmentation, safety-critical anomaly classification, natural language ground truth. The annotation cost of real-world data limits training scale.

Synthetic and simulated data address all three: rare events can be generated at will, exploration is safe in simulation, and labels can be automatically assigned in simulation.

### 4.2 Domain randomisation and sim-to-real transfer

Simulation environments for robotics and embodied AI are well-developed: NVIDIA Isaac Sim, Gazebo, PyBullet, MuJoCo, and Unity ML-Agents provide physics-realistic environments in which agents can train at scale. The fundamental challenge is *sim-to-real transfer*: models trained in simulation may fail in the real world because the simulated environment does not perfectly capture real physics, sensor noise, and environmental variability.

Domain randomisation (Tobin et al. 2017) is the primary technique for bridging this gap: during simulation training, physical parameters (lighting, texture, object mass, friction coefficients, sensor noise) are randomised over a distribution that brackets the expected real-world variation. The model learns to be robust to variation rather than to the specific simulated conditions, and this robustness transfers to the real world.

OpenAI's work on dexterous robotic hand manipulation (Andrychowicz et al. 2020) demonstrated that a policy trained entirely in simulation with domain randomisation could transfer to a real robot with no additional real-world training — a result that would have been considered implausible at the time when the *reality gap* was framed as a fundamental obstacle to simulation-based training (Koos, Mouret, & Doncieux, 2013).

For IoT hybrid intelligence applications, domain randomisation has natural analogues:
- Randomise sensor noise characteristics across the simulated training distribution
- Randomise environmental conditions (temperature, humidity, interference) that affect sensor readings
- Randomise the physical parameters of monitored objects across plausible ranges

### 4.3 Digital twins as training environments

A digital twin is a real-time computational model of a physical system, updated by sensor data from the physical counterpart (Grieves, 2014; Shafto et al., 2012; Tao et al. 2018). Digital twins were originally developed for industrial monitoring and predictive maintenance; they are increasingly used as training environments for hybrid intelligence systems.

The advantage of digital twins over generic simulation is fidelity: a digital twin of a specific manufacturing line, trained on that line's sensor data, captures the idiosyncratic behaviour of that specific system in ways that generic physics simulation cannot. Rare failure modes can be deliberately simulated in the twin, generating training data that would require years of passive monitoring to collect from the real system.

The feedback loop between digital twin and deployed model is the key architectural feature: sensor data from the real system updates the twin → the twin generates training scenarios → the model trains on twin-generated data → the model is deployed in the real system → better model performance generates more informative sensor data to update the twin.

This positive feedback loop — real sensing improving simulation improving model improving sensing — is the core argument for treating IoT sensing and simulation design as a joint optimisation problem.

### 4.4 Generative synthesis of sensor data

Beyond physics-based simulation, generative models can synthesise sensor data directly. Diffusion models and GANs trained on real sensor data can generate realistic synthetic samples that augment the training distribution, particularly in the tails (Yoon et al., 2019; Brophy et al., 2022).

For structured sensor modalities — time-series data from temperature, pressure, vibration, or flow sensors — conditional generative models can produce samples under specified conditions: "generate 1000 examples of bearing vibration data from a motor with incipient crack failure under high load." This directly addresses the rare-event coverage problem.

The synthetic data quality problem is the limiting constraint: generative models reproduce the patterns in their training data, including its biases. Rare events that are underrepresented in real data will also be underrepresented in synthetic data generated from that data (Shumailov et al., 2024). Hybrid approaches — physics-based simulation for rare events, generative synthesis for common-condition augmentation — are more robust than either alone.

---

## §5 — The Closed Loop: From Sensing to Training to Retuning

### 5.1 Online learning and adaptive sensing

A static sensor configuration optimised for initial deployment becomes suboptimal as the system evolves: sensor calibration drifts, the monitored environment changes, the model's uncertainty distribution shifts as it learns. Hybrid intelligence systems with closed-loop adaptation continuously retune both the model and the sensing apparatus (Gama et al., 2014).

The architecture requires:
- **Model monitoring**: continuous evaluation of model confidence and accuracy on incoming sensor data
- **Sensing audit**: periodic assessment of whether current sensor configuration still covers the model's uncertainty
- **Retuning triggers**: criteria for when to change sampling rates, add sensors, or modify interaction flows
- **Governance**: human oversight of major reconfigurations, especially those that affect data collection from human interactions

### 5.2 Federated learning and privacy-preserving sensing

When training data is generated by sensors in many independent locations — consumer devices, hospital wards, factory floors owned by different organisations — centralised collection is often impractical or impermissible. Federated learning (McMahan et al. 2017) addresses this: models are trained locally on each node's sensor data, and only model updates (gradients or weights) are aggregated centrally — the raw sensor data never leaves its origin.

For hybrid intelligence system designers, federated learning changes the sensing design problem: the goal is not to maximise the richness of data sent to a central training server, but to maximise the *local* training signal at each node, subject to the model update communication budget. Sensor configurations should be optimised for local learning efficiency as well as raw data quality.

Differential privacy (Dwork et al. 2006) can be applied to the aggregated model updates to provide formal privacy guarantees — important for sensing environments that involve personal data (healthcare wearables, smart home devices, interaction logs from consumer applications).

### 5.3 The sensing-simulation feedback loop in practice

Two deployment examples illustrate the closed-loop architecture:

**Smart manufacturing (Industry 4.0):** A factory deploys a digital twin of its production line. Vibration sensors, temperature sensors, and computer vision systems feed real-time data into the twin. The hybrid intelligence system monitors the twin for anomalies, uses rare-event simulation in the twin to generate failure-mode training data, and trains defect-prediction models on the combined real and simulated dataset. When the deployed model's accuracy on the production line degrades (detected by monitoring), the system increases sensor sampling rates in the regions of uncertainty and generates additional targeted simulation scenarios. Human operators review anomaly flags and their corrections are captured as labelled training data (Fuller et al., 2020).

**Clinical wearables:** A hospital deploys wearable sensors for post-discharge patient monitoring. The wearables collect vital sign time series; a digital twin of each patient (initialised from electronic health records) provides a personalised baseline. The hybrid intelligence system predicts deterioration risk (Bayoumy et al., 2021); clinician review of alerts generates implicit feedback on prediction quality. When the model's calibration drifts — detectable when predicted and observed event rates diverge (Finlayson et al., 2021) — the sensing configuration is adjusted (higher sampling frequency for specific sensor modalities) and additional synthetic patients are generated in the twin to augment the rare-event training distribution.

---

## §6 — Implications for Hybrid Intelligence Design

### 6.1 Sensing as a first-class design concern

The practical implication of this chapter is that sensor and interaction design should be part of the machine learning team's remit, not delegated entirely to hardware engineers and UX designers. The training data quality consequences of sensing choices are not recoverable downstream — a sensor array that is systematically blind to failure modes, or an interaction interface that destroys implicit feedback signals, produces training data limitations that no modelling technique can fully compensate.

### 6.2 Simulation as the scale lever

The fundamental scarcity in hybrid intelligence is high-quality, labelled training data for rare and high-stakes conditions. Physics-based simulation and digital twins are the most scalable mechanism for generating this data. Organisations that invest in simulation infrastructure — and in the discipline of designing domain randomisation parameters to match real deployment conditions — have a structural advantage in training reliable hybrid systems.

### 6.3 The ethical architecture of pervasive sensing

Hybrid systems that use IoT sensing and human interaction data for continuous retraining operate in an ethically complex space. Users of smart devices, employees in sensored environments, and patients with clinical wearables generate training data as a by-product of system use. The ethical constraints are well-specified — GDPR consent and purpose limitation (Regulation (EU) 2016/679), EU AI Act transparency for automated decision systems (Regulation (EU) 2024/1689), NIS2 data governance for critical infrastructure (Directive (EU) 2022/2555) — but compliance requires deliberate design of consent flows, data minimisation in sensing, and transparency about how interaction data is used.

Pervasive sensing for training is not intrinsically exploitative, but it can become so if the sensing apparatus is designed to extract training value without commensurately serving the interests of those being sensed. The design principle: sensed parties should benefit from the improvements enabled by their data.

---

## Key Sources (to verify / acquire)

- Settles, B. (2009). Active Learning Literature Survey. *Computer Sciences Technical Report 1648*, University of Wisconsin–Madison. [R] [iCit: 666 — canonical active learning survey; the foundational synthesis defining the framework in which the model selects which data to label or collect next to reduce uncertainty; cited in §2.1 as the defining reference for active sensing philosophy. iCit confirmed via Semantic Scholar 2026-05-18 — well above ≥5 threshold.] *(tag and iCit upgraded 2026-05-18 by Sonnet 4.6)*
- Bajcsy, R. (1988). Active perception. *Proceedings of the IEEE*, *76*(8), 966–1005. https://doi.org/10.1109/5.5968 [J — Proceedings of the IEEE; peer-reviewed; foundational paper coining "active perception" as the paradigm in which a sensor-equipped agent actively controls its sensing to reduce uncertainty — the canonical anchor for the §2.1 robotics bullet on moving to maximise sensor coverage of poorly-understood workspace regions; iCit: well above ≥5 threshold (confirmed from established literature; S2 rate-limited at execution).] *(executor-added 2026-05-21)*
- García, J., & Fernández, F. (2015). A comprehensive survey on safe reinforcement learning. *Journal of Machine Learning Research*, *16*, 1437–1480. http://jmlr.org/papers/v16/garcia15a.html [J — JMLR; peer-reviewed open access; canonical synthesis of safe RL methods covering constrained MDPs, risk-sensitive objectives, and lyapunov safety guarantees — directly anchors §4.1 "cost of exploration" claim that physical RL exploration in factories and power grids is dangerous and expensive; iCit: well above ≥5 threshold (confirmed from established literature; S2 rate-limited at execution).] *(executor-added 2026-05-21)*
- Tobin, J., Fong, R., Ray, A., Schneider, J., Zaremba, W., & Abbeel, P. (2017). Domain randomization for transferring deep neural networks from simulation to the real world. *2017 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)*, 23–30. arXiv:1703.06907. https://doi.org/10.1109/IROS.2017.8202133 [C] [iCit: confirmed high — S2 rate-limited at execution; canonical domain randomisation paper; IROS 2017 peer-reviewed proceedings; CrossRef retraction status clean (update-to: None); foundational anchor for §4.2 sim-to-real transfer via randomisation of lighting, texture, mass, friction, and sensor noise. iCit well above ≥5 threshold based on established citation record.] *(tag resolved, CrossRef checked 2026-05-18 by Sonnet 4.6)*
- Andrychowicz, M. et al. (2020). Learning dexterous in-hand manipulation. *IJRR*, 39(1). arXiv:1808.00177. [iCit: high]
- Grieves, M. (2014). *Digital twin: manufacturing excellence through virtual factory replication*. White paper, Florida Institute of Technology. [R — white paper; year corrected from erroneous "2002" attribution to 2014, the earliest widely-available Grieves DT document; the term was introduced in Grieves' 2003 Michigan executive course material but first widely circulated in this 2014 white paper. Supplemented by Shafto et al. 2012 for peer-reviewable institutional anchor.] *(year corrected and tag added 2026-05-18 by Sonnet 4.6)*
- Shafto, M., Conroy, M., Doyle, R., Glaessgen, E., Kemp, C., LeMoigne, J., & Wang, L. (2012). Modeling, Simulation, Information Technology & Processing Roadmap. *NASA Technical Report NF1676L-13283*, NASA. [R — NASA technical report; earliest peer-reviewable institutional anchor for the "digital twin" concept as a real-time computational model paired to a physical counterpart; cited in §4.3 alongside Grieves (2014) and Tao et al. (2018) to provide independent institutional verification of the DT concept origin.] *(executor-added 2026-05-18 by Sonnet 4.6)*
- Tao, F., Cheng, J., Qi, Q., Zhang, M., Zhang, H., & Sui, F. (2017). Digital twin-driven product design, manufacturing and service with big data. *The International Journal of Advanced Manufacturing Technology*, 94, 3563–3576. https://doi.org/10.1007/s00170-017-0233-1 [J] [OA cit: 2727 — OpenAlex cited_by_count, 2026-05-19; IJAMT Springer peer-reviewed journal; CrossRef retraction: clean (no update-to record); note: published online 2017, inline citation uses 2018 reflecting print vol. 94.] *(iCit resolved 2026-05-19 by Sonnet 4.6)*
- Krause, A., Singh, A., & Guestrin, C. (2008). Near-optimal sensor placements in Gaussian processes: Theory, efficient algorithms and empirical studies. *Journal of Machine Learning Research*, 9, 235–284. [J] [OA cit: 1226 — OpenAlex cited_by_count, 2026-05-19; JMLR peer-reviewed journal; [J] tag confirmed; CrossRef retraction: clean.] *(iCit resolved 2026-05-19 by Sonnet 4.6)*
- McMahan, H. B., Moore, E., Ramage, D., Hampson, S., & Arcas, B. A. Y. (2017). Communication-efficient learning of deep networks from decentralized data. *Proceedings of the 20th International Conference on Artificial Intelligence and Statistics (AISTATS 2017)*, PMLR 54. arXiv:1602.05629. [C] [iCit: 4911 — foundational federated learning paper; introduces FedAvg algorithm for training deep networks from decentralized data with only model updates communicated centrally; directly cited in §5.2 for privacy-preserving federated sensing architecture.] *(upgraded from bare entry 2026-05-15 by Sonnet 4.6)*
- Dwork, C., McSherry, F., Nissim, K., & Smith, A. (2006). Calibrating noise to sensitivity in private data analysis. *Theory of Cryptography Conference (TCC 2006)*, Lecture Notes in Computer Science (LNCS 3876), 265–284. https://doi.org/10.1007/11681878_14 [C] [OA cit: 6968 — foundational differential privacy paper; defines the (ε,δ)-DP framework and Laplace mechanism; cited in §5.2 for privacy-preserving federated learning.] *(upgraded from bare entry 2026-05-15 by Sonnet 4.6)*
- Schwager, M., Rus, D., & Slotine, J.-J. (2009). Decentralized, adaptive coverage control for networked robots. *The International Journal of Robotics Research*, 28(3), 357–375. https://doi.org/10.1177/0278364908100177 [J] [iCit: 17 — coverage-based sensor placement anchor for §2.2; derives decentralised gradient-ascent law for maximising coverage metric over sensor network without central coordination.] *(upgraded from bare entry 2026-05-15 by Sonnet 4.6)*
- Joachims, T., Granka, L., Pan, B., Hembrooke, H., & Gay, G. (2005). Accurately interpreting clickthrough data as implicit feedback. *Proceedings of the 28th Annual International ACM SIGIR Conference on Research and Development in Information Retrieval* (SIGIR '05), 154–161. https://doi.org/10.1145/1076034.1076063 [C] [OA cit: 1393]
- Yoon, J., Jarrett, D., & van der Schaar, M. (2019). Time-series Generative Adversarial Networks. *Advances in Neural Information Processing Systems* (NeurIPS 2019), 32. [C] [OA cit: 517]
- Brophy, E., Wang, Z., She, Q., & Ward, T. (2022). Generative Adversarial Networks in Time Series: A Systematic Literature Review. *ACM Computing Surveys*, 55(6), 1–38. https://doi.org/10.1145/3559540 [J] [OA cit: 295]
- Fuller, A., Fan, Z., Day, C., & Barlow, C. (2020). Digital Twin: Enabling Technologies, Challenges and Open Research. *IEEE Access*, 8, 108952–108971. https://doi.org/10.1109/access.2020.2998358 [J] [OA cit: 2346]
- Heemels, W. P. M. H., Johansson, K. H., & Tabuada, P. (2012). An introduction to event-triggered and self-triggered control. *2012 IEEE 51st IEEE Conference on Decision and Control (CDC)*, 3270–3285. https://doi.org/10.1109/cdc.2012.6425820 [C] [OA cit: 1883]
- Koos, S., Mouret, J.-B., & Doncieux, S. (2013). The transferability approach: Crossing the reality gap in evolutionary robotics. *IEEE Transactions on Evolutionary Computation*, 17(1), 122–145. https://doi.org/10.1109/tevc.2012.2185849 [J] [OA cit: 263]
- Wachter, S., & Mittelstadt, B. (2019). A right to reasonable inferences: Re-thinking data protection law in the age of big data and AI. *Columbia Business Law Review*, 2019(2), 494–620. [J — Columbia Business Law Review; peer-reviewed law review; directly addresses how GDPR purpose limitation applies to AI inference and ML training; cited at §3.3 for purpose-limitation constraints on interaction-as-data-collection. iCit above ≥5 threshold.] *(executor-added 2026-05-08)*
- European Parliament and Council. (2016). Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data (General Data Protection Regulation). *Official Journal of the European Union*, L 119, 1–88. [R — regulatory text; Art. 5(1)(b) purpose limitation; Art. 6 lawful basis for processing] *(executor-added 2026-05-08)*
- European Parliament and Council. (2024). Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). *Official Journal of the European Union*, L 1689. [R — regulatory text; Art. 10 training, validation and testing data requirements] *(executor-added 2026-05-08)*
- He, H., & Garcia, E. A. (2009). Learning from imbalanced data. *IEEE Transactions on Knowledge and Data Engineering*, 21(9), 1263–1284. https://doi.org/10.1109/TKDE.2008.239 [J] *(Canonical survey on the imbalanced learning problem: defines systematic insufficiency of operational training data for rare events and failure modes; covers oversampling, undersampling, cost-sensitive and ensemble approaches; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.)* *(executor-added 2026-05-09)*
- Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., & Bouchachia, A. (2014). A survey on concept drift adaptation. *ACM Computing Surveys*, 46(4), 1–37. https://doi.org/10.1145/2523813 [J] *(Canonical survey on concept drift and adaptive model retraining: covers detection methods, online learning algorithms, and closed-loop retuning architectures for deployed models operating in non-stationary environments; iCit well above ≥5 threshold. S2 rate-limited at execution time; confirmed from established literature.)* *(executor-added 2026-05-09)*
- Schnabel, T., Swaminathan, A., Singh, A., Chandak, N., & Joachims, T. (2016). Recommendations as treatments: Debiasing learning and evaluation. *Proceedings of the 33rd International Conference on Machine Learning (ICML 2016)*, 48, 1670–1679. arXiv:1602.05352. [C] [OA iCit: ~428 — S2 rate-limited; confirmed from established literature; addresses the missing-not-at-random (MNAR) structure of implicit feedback and propensity-score debiasing — directly anchors the abandonment-bias claim in §3.2 that the correction signal is absent where the AI most fails.] *(executor-added 2026-05-10)*
- Shumailov, I., Shumaylov, Z., Zhao, Y., Guestrin, C., Anderson, R., & Papernot, N. (2024). AI models collapse when trained on recursively generated data. *Nature*, *631*, 755–759. https://doi.org/10.1038/s41586-024-07566-y [J] [iCit: high — Nature paper; canonical source on model collapse / synthetic-data-induced bias inheritance; directly anchors §4.4 claim that generative models reproduce training-data biases including underrepresentation of rare events.] *(executor-added 2026-05-10)*
- Wuest, T., Weimer, D., Irgens, C., & Thoben, K.-D. (2016). Machine learning in manufacturing: advantages, challenges, and applications. *Production & Manufacturing Research*, 4(1), 23–45. https://doi.org/10.1080/21693277.2016.1192517 [J] [OA cit: 1238] *(Canonical survey on challenges of applying ML to manufacturing data, including how existing IoT sensor deployments are designed for operational monitoring rather than ML training optimality — anchors §1.1 gap-claim. Confirmed via OpenAlex.)* *(executor-added 2026-05-13)*
- Cappon, G., Vettoretti, M., Sparacino, G., & Facchinetti, A. (2019). Continuous Glucose Monitoring Sensors for Diabetes Management: A Review of Technologies and Applications. *Diabetes & Metabolism Journal*, 43(4), 383. https://doi.org/10.4093/dmj.2019.0121 [J] [OA cit: 452] *(Leading review of CGM sensing technology from the University of Padova signal-processing group; covers real-time BG dynamics, sensor data collection patterns, and clinical alert triggering — anchors the adaptive-sampling CGM vignette in §2.1. Confirmed via OpenAlex, PMID 31441246.)* *(executor-added 2026-05-13)*
- Bayoumy, K., Gaber, M., Elshafeey, A., Mhaimeed, O., Dineen, E. H., Marvel, F. A., et al. (2021). Smart wearable devices in cardiovascular care: where we are and how to move forward. *Nature Reviews Cardiology*, 18(8), 581–599. https://doi.org/10.1038/s41569-021-00522-7 [J] [OA cit: 779] *(Comprehensive clinical review of wearable sensor systems for real-time patient monitoring; covers vital-sign data collection, deterioration risk prediction architectures, and closed-loop clinical alert systems — anchors the clinical-wearables deployment vignette in §5.3. Confirmed via OpenAlex.)* *(executor-added 2026-05-13)*
- Atkinson, A. C., & Donev, A. N. (1992). *Optimum Experimental Designs*. Oxford University Press. [J — monograph; canonical reference for D-optimality criterion: placing sensors or design points to minimise the variance of model parameter estimates in regression tasks on spatial phenomena; foundational text anchoring the third sensor-placement approach in §2.2 to parity with the Krause et al. (2008) and Schwager et al. (2009) citations. iCit well above ≥5 threshold; confirmed from established literature.] *(executor-added 2026-05-10)*
- Christiano, P. F., Leike, J., Brown, T., Martic, M., Legg, S., & Amodei, D. (2017). Deep reinforcement learning from human preferences. *Advances in Neural Information Processing Systems* (NeurIPS 2017), 30. arXiv:1706.03741. [C] [iCit: very high — canonical RLHF algorithm paper; establishes DRL from human preference feedback as the foundation for converting explicit human evaluations into training signals at scale. Cited in §3.1 for the foundation-model deployment principle.] *(executor-added 2026-05-11)*
- Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C. L., Mishkin, P., Zhang, C., Agarwal, S., Slama, K., Ray, A., Schulman, J., Hilton, J., Kelton, F., Miller, L., Simens, M., Askell, A., Welinder, P., Christiano, P., Leike, J., & Lowe, R. J. (2022). Training language models to follow instructions with human feedback. *Advances in Neural Information Processing Systems* (NeurIPS 2022), 35. arXiv:2203.02155. [C] [iCit: 2191 — InstructGPT paper demonstrating RLHF applied to foundation models (GPT-3) to steer outputs toward human-aligned behaviour; establishes the paradigm for explicit human feedback in LLM training. Cited in §3.1 for foundation-model-level deployment.] *(executor-added 2026-05-11; upgraded [P]→[C] 2026-05-15 by Sonnet 4.6)*
- Kohavi, R., Longbotham, R., Sommerfield, D., & Henne, R. M. (2009). Controlled experiments on the web: survey and practical guide. *Data Mining and Knowledge Discovery*, 18(1), 140–181. https://doi.org/10.1007/s10618-008-0114-1 [J] [OA cit: 679] *(Canonical engineering anchor for online controlled experiments / A/B testing as the clinical-trial design principle applied to web and HCI systems: covers randomised assignment, multi-variant deployment, and statistical analysis pipelines — directly anchors the §3.3 randomised-assignment claim. CrossRef retraction status clean (update-to: None) verified 2026-05-13.)* *(executor-added 2026-05-13, resolves annotation Task 005)*
- Finlayson, S. G., Subbaswamy, A., Singh, K., Bowers, J., Kupke, A., Zittrain, J., Kohane, I. S., & Saria, S. (2021). The Clinician and Dataset Shift in Artificial Intelligence. *New England Journal of Medicine*, 385(3), 283–286. https://doi.org/10.1056/NEJMc2104626 [J] [OA cit: 603] *(Authoritative NEJM perspective on dataset shift, distributional drift, and calibration drift in deployed clinical ML: identifies the architecturally specific failure modes (concept drift, covariate shift, prevalence shift) for which the §5.3 wearables vignette adjusts sensing — directly anchors the calibration-drift claim. CrossRef retraction status clean (update-to: None) verified 2026-05-13.)* *(executor-added 2026-05-13, resolves annotation Task 004)*
- European Parliament and Council. (2022). Directive (EU) 2022/2555 of the European Parliament and of the Council of 14 December 2022 on measures for a high common level of cybersecurity across the Union (NIS2 Directive). *Official Journal of the European Union*, L 333, 80–152. [R — regulatory text; cybersecurity governance for essential and important entities; cited at §6.3 for NIS2 data-governance obligations on critical-infrastructure operators of sensored systems.] *(executor-added 2026-05-13, resolves annotation Task 006)*

---

## Cross-references

- **Draft V** (`v-ai-paradigms-development.md`) — Paradigm I (learning from data) as the foundation this chapter serves
- **Draft H** (`h-human-augmentation-coevolution.md`) — human-AI coevolution in sensed environments
- **Draft T** (`t-agentic-tool-calling.md`) — sensors as skills callable by agents
- **Draft AC** (`ac-model-vs-human-performance.md`) — performance gaps that motivate sensing investment
- **Draft AF** (`af-human-labor-ai-training.md`) — the human labor in annotation and feedback that sensing design can partially automate
- **Draft AI** (`ai-practical-skill-tool-implications.md`) — governance of data-generating systems
