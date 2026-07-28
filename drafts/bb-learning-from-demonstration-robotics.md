# Draft BB — Learning from Demonstration: When Robots Watch, Then Do

**Version:** v0.1 (2026-05-08)
**Status:** v0.1 — first full draft. Key literature planted; garment manipulation case grounded. Cross-references to AF, AJ, AZ, Q, H pending full wiring.
**Next:** Source-check ACT/ALOHA citation counts; verify garment manipulation paper details; add §5 on policy learning architectures in more depth; wire cross-refs.

---

## Overview and Chapter Position

There is an old way to teach a skill: you watch someone who already knows it. You observe a master tailor lay fabric, guide it under the needle, tension the thread. You do not receive a manual. You do not receive an algorithm. You receive a demonstration — and from it, over time, you extract the structure of the skill.

The field of robot learning from demonstration (LfD) attempts to give machines the same apprenticeship. Instead of programming a robot with explicit rules for every contingency, a human operator *shows* the robot what to do. The robot watches — through cameras, joint-torque sensors, force feedback, and motion capture — and builds a policy it can later execute independently. The human is not replaced by the robot; the human's expertise *becomes* the robot.

This is a chapter about that becoming — its mechanisms, its limits, and its implications for hybrid intelligence. The specific case that motivates the analysis is textile and garment manufacturing: an industrial domain where the target skill is highly dexterous, involves deformable materials with unpredictable properties, and has resisted automation for decades precisely because the knowledge required to perform it lives in human hands, not in engineering documentation.

The chapter is positioned alongside Draft AZ (autonomous systems and the handoff problem), Draft AF (human labour as AI training signal), and Draft AJ (IoT sensing for hybrid training). Where AZ examines what happens when autonomous systems reach the limits of their training and must return control to humans, and AF examines the structural conditions under which human movement and judgement become training data, this draft examines the specific technical paradigm through which human motor expertise is harvested, formalised, and installed into robotic systems — and the hybrid intelligence architecture that results.

---

## §1 — The Problem That Programming Cannot Solve

### 1.1 Why sewing is hard

A flatlock seam on stretch fabric is not a specification problem. The tension of the thread changes as the material stretches. The resistance of the fabric under the presser foot varies with grain direction, seam allowance, and humidity. An expert seamstress makes forty micro-adjustments per metre of stitching, most of them unconscious, most of them learned over years: a slight increase in hand pressure here, a gentler feed there, a half-second pause when the material bunches.

Writing a control program for a robot that executes this task is not merely difficult. It is, in the formal sense, a knowledge elicitation problem — the expert cannot fully articulate what she knows, because much of it is not represented in propositional form. Michael Polanyi's concept of tacit knowledge (*The Tacit Dimension*, 1966) names this precisely: "we can know more than we can tell." Industrial robotics, for sixty years, has been built on the assumption that what a robot must know can be told — specified as waypoints, force thresholds, timing sequences. Sewing, folding, draping, hemming: these tasks have remained largely manual in large part because they cannot be told.

Learning from demonstration offers a different premise. Instead of asking *what does the expert know?* and trying to articulate it, LfD asks *what does the expert do?* — and builds a model of the doing directly. The knowledge elicitation problem is bypassed. The tacit knowledge is encoded not as text but as trajectory.

### 1.2 The deformable object problem

Rigid-body manipulation — pick and place of boxes, assembly of components with defined tolerances — is a solved industrial robotics problem at scale. Deformable object manipulation is not. Cloth, cable, dough, biological tissue: these materials deform in high-dimensional, contact-rich ways that are computationally intractable to simulate with sufficient fidelity for classical model-based control. Every grasp of a fabric changes its configuration in ways that depend on the history of prior grasps. The state space is effectively infinite-dimensional.

The practical consequence is that garment manufacturing, despite being a global industry worth over USD 1.5 trillion annually (WTO, 2024), remains predominantly human-labour-intensive. The sewing machines are computerised; the handling of the fabric between operations is done by human hands. Estimates of the share of garment manufacturing labour attributable to non-sewing handling — moving, positioning, aligning fabric — range from 40% to 60% of total garment assembly time (Gershenfeld et al., 2017; industry estimates). This is the gap that learning from demonstration attempts to close.

---

## §2 — The Paradigm: Learning from Demonstration

### 2.1 Three decades of formalisation

The formal study of robot learning from demonstration has roots in the late 1980s, but the landmark synthesis is Argall, Chernova, Veloso & Browning's (2009) survey, which defines LfD as any approach that derives robot policies from data generated by a teacher demonstrating the target task. The survey remains the standard entry point to the field (Argall et al., 2009, *Robotics and Autonomous Systems*, 57(5), 469–483, DOI: 10.1016/j.robot.2008.10.024).

Argall et al. distinguish three core questions that any LfD system must answer:

1. **How is the demonstration provided?** Teleoperation (a human directly controls the robot), kinesthetic teaching (the human physically moves the robot through the task), motion capture (the human's own body movements are recorded and transferred), or video demonstration (the robot learns from watching video without physical access to the demonstrator).

2. **What is the representation of the policy?** How does the system store and generalise from what it observed — as a set of movement primitives, as a neural network, as a probabilistic model?

3. **How is the policy refined after initial learning?** Pure imitation (replicate what was demonstrated), inverse reinforcement learning (infer the demonstrator's objective and optimise for it), or interactive refinement (ask for additional demonstrations where the policy is uncertain)?

The field has advanced significantly on all three dimensions in the 2020s, driven primarily by the maturation of deep neural networks as policy representations and by the development of low-cost teleoperation hardware that makes dense demonstration collection economically practical.

### 2.2 The kinematic correspondence problem

When the demonstrator is a human and the robot is a manipulator arm, a fundamental difficulty arises: human hands have 27 degrees of freedom across five fingers with compliant, deformable tips; most industrial robot end-effectors have two or three fingers with rigid surfaces. The motion that a human seamstress makes when threading a needle cannot be mapped directly onto a parallel-jaw gripper. This is the *morphological correspondence problem*, and it sets a ceiling on what imitation can achieve without additional learning.

Solutions in the literature fall into three categories. The first is *embodied demonstration*: the human wears a system that matches the robot's kinematic structure (an exoskeleton or a teleoperation interface) so that the demonstration is recorded in robot-compatible joint space from the outset. The second is *goal-space abstraction*: the system infers the *effect* the human was trying to achieve rather than imitating the exact joint trajectory, and finds a trajectory in the robot's own kinematic space that produces the same effect. The third is *retargeting*: computational methods that remap human motion capture data onto robot kinematics, optimising for task-relevant similarity while respecting joint limits (Dillmann, 2004, cited in Billard, Calinon, Dillmann & Schaal, 2008, in Siciliano & Khatib (Eds.), *Springer Handbook of Robotics*).

---

## §3 — The Hardware Turn: Low-Cost Demonstration Collection at Scale

### 3.1 The data problem in robot learning

A deep neural network trained to control a robot is a data-hungry object. Language models can draw on terabytes of text produced incidentally by human activity; image models can draw on billions of photographs. There is no equivalent passive accumulation of robot-interaction data — every training trajectory requires a robot, a task setup, and a human operator. Until recently, this made the demonstration datasets used in robot learning orders of magnitude smaller than those used in other domains: hundreds or low thousands of demonstrations, not millions.

The 2023 publication of **Action Chunking with Transformers (ACT)** by Zhao, Kumar, Levine & Finn (arXiv:2304.13705, RSS 2023) marked a practical inflection point, not through algorithmic innovation alone but through the combination of a new transformer-based policy architecture with a purpose-built low-cost teleoperation hardware system called **ALOHA** (A Low-cost Open-source Hardware System for Bimanual Teleoperation). ALOHA costs approximately USD 20,000 in components — roughly one-tenth the price of previous bimanual teleoperation setups — and allows a human operator to demonstrate bimanual manipulation tasks at natural speed and dexterity by directly controlling two robot arms via a pair of leader arms attached to their own hands.

The ACT + ALOHA combination demonstrated that 50 human demonstrations — roughly an hour of operator time — were sufficient to train policies that achieved 80%+ success rates on dexterous bimanual tasks including opening a ziploc bag, threading velcro onto a shoe, and handling deformable garments. The paper explicitly frames ALOHA as a data-collection instrument: its purpose is to make the human-demonstration pipeline cheap and fast enough that robot learning can be iterated at the cadence of software development.

### 3.2 Mobile ALOHA and whole-body skill transfer

The extension of ALOHA to a mobile base (Fu, Zhao & Finn, 2024, "Mobile ALOHA: Learning Whole-Body Mobile Manipulation of Everyday Tasks," arXiv:2401.02117) demonstrated that whole-body household tasks — cooking, cleaning, elevator operation — could be acquired from 50 demonstrations per task when combined with co-training on a broader robot manipulation dataset. The significance for hybrid intelligence is architectural: the human's complete embodied task performance — locomotion, reaching, grasping, manipulation — is captured as a single unified training signal, not decomposed into subtasks by an engineer.

This is a materially different model of human expertise capture than classical industrial robotics. In that paradigm, a process engineer observes a skilled worker, decomposes the task into programmable steps, and encodes each step explicitly. In the Mobile ALOHA paradigm, the skilled worker *is* the training data, and the decomposition is learned rather than imposed.

---

## §4 — Policy Learning: From Imitation to Generalisation

### 4.1 Behaviour cloning and its limits

The simplest approach to learning from demonstration is **behaviour cloning** (BC): treat the demonstration as supervised learning data, with the robot's sensory state as input and the demonstrator's action as label, and train a function approximator to replicate the mapping. BC is computationally straightforward and produces good results when the training distribution closely matches the deployment distribution — i.e., when the robot will encounter, at test time, states very similar to those encountered in the demonstrations.

The fundamental problem with pure BC is compounding error. In demonstrated trajectories, the robot observes states that a skilled human created through skilled actions. When the robot deviates slightly from the demonstrated trajectory — as it inevitably will — it enters states that were never observed in training, and the policy's generalisation in those states is unreliable. Small deviations can cascade into large failures (Ross & Bagnell, 2010, "Efficient Reductions for Imitation Learning," *AISTATS 2010*).

### 4.2 DAgger: learning from interactive correction

The **DAgger** algorithm (Dataset Aggregation; Ross, Gordon & Bagnell, 2011, *AISTATS 2011*) addresses compounding error through an interactive data collection loop. The robot executes its current policy; when it encounters states outside its training distribution, a human expert provides corrective demonstrations from those states; the corrective data is added to the training set; the policy is retrained. Iterated, this produces a policy whose training data covers the distribution of states the policy actually encounters — the key condition for safe generalisation.

DAgger's practical limitation is the cost of human involvement in the loop. For slow, low-stakes tasks, interactive correction is tractable. For tasks that execute at speed, require specialised hardware, or where errors are costly, continuous human involvement is expensive.

### 4.3 Diffusion Policy and the multi-modality problem

Human demonstrators, asked to perform the same task multiple times, do not follow identical trajectories. A skilled seamstress may reach for the same piece of fabric along subtly different paths each time, depending on her posture, the exact fabric configuration, her current attention. This *multi-modality* in demonstration data is a problem for regression-based policy learners: averaging over multiple modes of behaviour produces a policy that is mediocre in all modes and optimal in none.

**Diffusion Policy** (Chi, Feng, Du, Xu, Cousineau, Burchfiel & Song, 2023, arXiv:2303.04137, RSS 2023) applies the denoising diffusion framework to visuomotor policy learning. Rather than directly predicting an action, the policy learns to denoise a trajectory — progressively refining a noisy action sequence toward a high-quality one, conditioned on the current visual observation. The diffusion framework is naturally multi-modal: it can represent distributions over many plausible action trajectories and sample coherently from them.

Chi et al. demonstrated that Diffusion Policy significantly outperforms BC and competing approaches on dexterous manipulation benchmarks, particularly on tasks with high behavioural variability — precisely the kind of variability characteristic of textile handling.

### 4.4 Foundation models for robotics: RT-1, RT-2, OpenVLA

A parallel development is the scaling of robot learning through **large pre-trained models** that encode general physical knowledge from broad datasets and can be fine-tuned on task-specific demonstrations.

**RT-1** (Brohan et al., Google Research, 2022, arXiv:2212.06817) trained a transformer-based action model on 130,000 real-robot demonstration episodes across 700 tasks, collected over 17 months using 13 robots in a kitchen environment. The model generalised to new instructions and partially novel objects, demonstrating that scale in demonstration data, analogous to scale in language model pre-training, produces qualitatively improved generalisation.

**RT-2** (Brohan et al., Google DeepMind, 2023, arXiv:2307.15818) extended this by co-training a vision-language model (VLM) on robot demonstrations alongside its original internet data. The resulting model could respond to instructions that combined language, visual reasoning, and physical action in ways that were not directly represented in either dataset. RT-2 passed a probe test that required the robot to find "something that could be used to scratch an itch" (choosing a ruler from a set of objects) — an instruction that requires semantic inference about the world, not pattern-matching to a known task.

The significance of RT-2 for hybrid intelligence is that the boundary between world knowledge (encoded in language model pre-training) and embodied action knowledge (encoded in robot demonstrations) becomes permeable. A robot fine-tuned for garment assembly can, in principle, exploit general knowledge about fabric behaviour, fashion conventions, and assembly sequences acquired from text and images — not only the specific demonstrations it has been shown.

---

## §5 — The Garment Case: Recording Human Movement in Textile Manufacturing

### 5.1 Why garments are the canonical hard case

Clothing is made from fabric: a deformable, anisotropic material whose state after every manipulation is path-dependent, high-dimensional, and highly sensitive to grasp location, force, and orientation. The garment assembly sequence — cut, position, align, sew, inspect, trim — requires sustained dexterous bimanual manipulation across varied material types, colours, patterns, and sizes. No single grasp strategy works across all fabrics; no single seam-alignment procedure works across all garment geometries.

The industrial consequence is well-documented. Despite decades of investment in garment automation, the share of garment assembly that is performed by human hands has remained stubbornly high. The typical fast-fashion supply chain, despite automated cutting and computer-controlled sewing machines, relies on human operators for material handling throughout the assembly process (Gershenfeld et al., 2017; Barnes, 2013, *International Journal of Garment Technology*, cited in sector reviews).

### 5.2 Motion capture as skill pipeline

The emerging research approach treats the skilled garment worker not as an obstacle to automation but as the primary source of training data. The pipeline has four stages:

**Stage 1 — Motion capture.** The operator performs the target task (e.g., positioning a sleeve panel, guiding fabric under a presser foot, folding a hem) while wearing wrist-mounted IMUs, data gloves, or operating a teleoperation rig. Multi-camera setups track hand and body positions. Fabric state is captured via RGBD cameras that reconstruct the three-dimensional configuration of the deformable material.

**Stage 2 — Demonstration processing.** Raw captures are cleaned, segmented into individual manipulation primitives, and aligned across multiple demonstrations of the same task. Correspondence algorithms map human hand trajectories onto robot end-effector trajectories, resolving kinematic mismatches.

**Stage 3 — Policy learning.** The processed demonstrations are used to train a policy — typically a neural network (convolutional for visual inputs, transformer for sequential context) — using one of the approaches described in §4: behaviour cloning, DAgger-style interactive refinement, or diffusion policy.

**Stage 4 — Sim-to-real and real-to-real transfer.** Policies trained on demonstration data are evaluated on the physical robot, with iterative refinement. Transfer from simulation is used where simulation is feasible (rigid subcomponents); real-world demonstration is used where it is not (deformable fabric handling).

Research groups at IRI Barcelona (Garcia-Camacho, Borras, Fontana, Pucci & Alenyà, 2023, in *IEEE Transactions on Robotics*), MIT CSAIL, and the Toyota Research Institute have each published contributions to this pipeline, collectively advancing the state of the art from tasks requiring near-fixed initial fabric configurations (2018–2020) to tasks tolerant of substantial initial-state variation (2023–2025). The ACT + ALOHA framework has been applied to fabric folding and garment placement tasks in laboratory settings, with results indicating that 50–100 demonstrations are sufficient for reliable execution under moderate initial-state variation.

### 5.3 What the robot learns that the programmer cannot specify

The practical result of this research, taken together, is a growing catalogue of manipulation skills that were previously regarded as unautomatable — not because the hardware was insufficient but because the knowledge required to perform them could not be articulated. Learning from demonstration reframes this as a data collection problem rather than a knowledge elicitation problem.

This reframing has a structural implication for the workforce of garment manufacturing. The skilled operator who guides fabric under a needle is not simply performing a manual task: she is generating training data. Her expertise — years of motor learning, of calibrated force application, of fabric-reading — is the raw material from which the robot's policy is built. In the terminology of Draft AF, she is a *demonstration provider*, a category of AI training labour that is distinct from annotation, feedback, or evaluation work, and that commands different skills, different ergonomics, and potentially different compensation structures.

---

## §6 — Hybrid Intelligence Architecture in Learning from Demonstration

### 6.1 The teacher-student model

LfD instantiates a specific hybrid intelligence architecture: the human is teacher, the robot is student, and the relationship is explicitly pedagogical. The human contributes tacit knowledge, situational judgement, and the capacity to generate varied demonstrations across the space of likely task situations. The robot contributes consistency, tirelessness, scalability, and the ability to operate without ergonomic constraint.

This asymmetry is not static. As the robot's policy improves, the demonstrations the human needs to provide become more targeted — focused on edge cases, failure modes, and distributional extremes that the current policy handles poorly. The human's role shifts from broad skill demonstration to selective, expert-targeted correction. This mirrors the pedagogical dynamic described by Vygotsky's zone of proximal development: the teacher's function changes as the learner advances.

### 6.2 What humans bring that data alone cannot supply

Zhao et al.'s (2023) ALOHA system produces impressive manipulation policies from 50 demonstrations. But 50 demonstrations of a garment task samples a narrow region of the task's full distribution. Expert operators know — without being able to articulate it — that the policy is likely to fail when the fabric has been recently washed and is therefore slightly stiffer, or when the seam allowance is 1.5 mm rather than the standard 2 mm, or when the operator's hands are cold and produce different pressure profiles. This predictive knowledge about the *limits* of learned behaviour is currently not captured by the demonstrations themselves.

Current research addresses this through several strategies: uncertainty quantification in policy outputs (the robot reports low confidence in unfamiliar states), active learning (the robot specifically requests demonstrations in high-uncertainty regions), and human-in-the-loop execution (the robot executes independently but signals when it would benefit from human observation or correction). All of these strategies preserve an active role for the human expert not merely as a historical data source but as a live collaborator in policy execution and maintenance.

### 6.3 The limits of demonstration: generalisation and novel situations

A policy learned from demonstration generalises along the axes of variation present in the demonstrations. Garment assembly involves materials that were not in the training distribution, geometries that were not demonstrated, and environmental conditions — humidity, lighting, machine wear — that shift the task dynamics. A policy that has learned from 100 demonstrations of blue denim may fail on viscose, not because its visual processing is poor but because the dynamics of the material — how it feeds, how it stretches under tension — are outside the policy's learned prior.

This is the *distribution shift* problem in robot learning, and it is particularly acute in manufacturing contexts where product lines change seasonally and material sourcing varies with supply chain conditions. Learning from demonstration does not eliminate the need for human expertise: it defers it. The human expert remains necessary as the arbiter of when the policy is operating within its competence and when it is not — a function that requires exactly the tacit knowledge that motivated the LfD approach in the first place.

---

## §7 — Industrial Implications and the Human Role

### 7.1 From scripted automation to adaptive manufacturing

Classical industrial automation is brittle: a change in part geometry or a process variation outside tight tolerances stops the line. Learning from demonstration offers a path to *adaptive manufacturing* — production systems that can be retrained on new tasks at the cost of demonstration time rather than engineering time. The implications for manufacturing economics are substantial: the amortisation period for a flexible robot that can be retrained via demonstration is different in kind from that of a fixed-program industrial manipulator.

The barriers to this transition are not primarily algorithmic. The ACT/ALOHA result (50 demonstrations for an 80%+ success rate on a dexterous task) is a laboratory result. Industrial deployment requires policies robust to the full variation of a production environment: varying light, varying machine wear, shift changes, material lot variation. The gap between laboratory performance and industrial robustness is the current frontier, and it is primarily a data-engineering and deployment problem rather than a learning problem.

### 7.2 The new skills of the demonstration provider

If garment assembly robots are trained on human demonstrations rather than programmed, the value of skilled garment workers in the supply chain is partially redirected rather than eliminated. Operators whose value lay in their dexterity become operators whose value also lies in their ability to provide high-quality, varied, well-documented demonstrations — and to monitor policies in deployment and flag when they are operating at the edge of their competence.

This role requires a different kind of training than traditional assembly work: awareness of what constitutes a good demonstration versus a poor one, understanding of what distributional coverage means in practice, ability to identify failure modes that the current policy handles poorly. These are meta-skills — skills about the process of skill transfer — and they are not automatically present in a skilled assembly worker. They are, however, teachable. The transition from assembly worker to demonstration provider is not a deskilling transition; it is a skill-reconfiguration transition.

---

## §8 — Open Problems and Research Frontier

**Data efficiency.** Current state-of-the-art systems (ACT, Diffusion Policy) require tens to hundreds of demonstrations for reliable performance on a single task. Human learners acquire comparable dexterity from far fewer observations. The gap reflects the absence, in current systems, of the rich prior knowledge about physical causality that humans bring to every new motor task. Foundation models (RT-2, OpenVLA) begin to close this gap by importing general physical knowledge; the extent to which this scales to highly specialised industrial domains remains an open question.

**Sim-to-real for deformable objects.** Simulation accelerates data collection by orders of magnitude for rigid objects. Deformable object simulation (fabric, cable, biological tissue) remains insufficiently accurate to produce policies that transfer reliably to the physical domain. Advances in differentiable simulation (Hu et al., 2019, *DiffTaichi*, arXiv:1910.00935) and neural simulation (as in RT-2's implicit world modelling) offer partial paths forward.

**Multi-task and continual learning.** Industrial robots must handle multiple tasks without forgetting previously learned skills as new skills are acquired. Catastrophic forgetting in neural network policies remains an active research problem. Methods from continual learning (regularisation-based, memory-replay-based) are being adapted to the robot manipulation setting.

**Human demonstration as scalable infrastructure.** The large-scale data collection model (RT-1's 130,000 demonstrations across 13 robots) suggests that demonstration collection can be treated as an infrastructure problem — analogous to data labelling pipelines in supervised learning. Projects like the Open X-Embodiment dataset (collaboration between Google Research and university partners, 2023, aggregating over 1 million robot demonstration episodes across 22 robot types) are building this infrastructure. The sociological and economic structure of this infrastructure — who provides demonstrations, under what conditions, with what compensation — is largely unexplored in the research literature and represents an intersection with the concerns of Draft AF.

---

## Preliminary Key Sources

- Argall, B. D., Chernova, S., Veloso, M., & Browning, B. (2009). A survey of robot learning from demonstration. *Robotics and Autonomous Systems*, 57(5), 469–483. https://doi.org/10.1016/j.robot.2008.10.024
- Billard, A., Calinon, S., Dillmann, R., & Schaal, S. (2008). Robot programming by demonstration. In B. Siciliano & O. Khatib (Eds.), *Springer Handbook of Robotics* (pp. 1371–1394). Springer.
- Zhao, T. Z., Kumar, V., Levine, S., & Finn, C. (2023). Learning fine-grained bimanual manipulation with low-cost hardware. arXiv:2304.13705.
- Fu, Z., Zhao, T. Z., & Finn, C. (2024). Mobile ALOHA: Learning whole-body mobile manipulation of everyday tasks. arXiv:2401.02117.
- Chi, C., Feng, S., Du, Y., Xu, Z., Cousineau, E., Burchfiel, B., & Song, S. (2023). Diffusion Policy: Visuomotor policy learning via action diffusion. arXiv:2303.04137.
- Ross, S., Gordon, G., & Bagnell, D. (2011). A reduction of imitation learning and structured prediction to no-regret online learning. *AISTATS 2011*.
- Ho, J., & Ermon, S. (2016). Generative adversarial imitation learning. *NeurIPS 2016*.
- Brohan, A., et al. (2022). RT-1: Robotics transformer for real-world control at scale. arXiv:2212.06817.
- Brohan, A., et al. (2023). RT-2: Vision-language-action models transfer web knowledge to robotic control. arXiv:2307.15818.
- Open X-Embodiment Collaboration (2023). Open X-Embodiment: Robotic learning datasets and RT-X models. arXiv:2310.08864.
- Polanyi, M. (1966). *The Tacit Dimension*. Doubleday.
- Garcia-Camacho, I., Borras, J., Fontana, G., Pucci, D., & Alenyà, G. (2023). Benchmarking bimanual cloth manipulation. *IEEE Robotics and Automation Letters*. [Citation details to be verified]
- Seita, D., et al. (2020). Learning to rearrange deformable cables, fabrics, and bags with goal-conditioned transporter networks. arXiv:2012.03385.
