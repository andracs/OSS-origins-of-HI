# Draft BC — The Infinite Loop Thought Experiment: Will an LLM Ever Finish?

**Version:** v0.1 (2026-05-11)  
**Status:** v0.1 — first draft. Thought experiment structure established; theoretical grounding planted. Empirical depth thin — needs evidence from Reflexion, SWE-bench loop benchmarks, and agentic failure mode literature.

---

## Overview and Chapter Position

Here is a thought experiment. You give a large language model a task — write a paragraph, solve a problem, generate a plan. Instead of accepting the first output and moving on, you put it in a loop: the model generates an output, evaluates that output, decides whether it is good enough, and if not, tries again. You repeat this indefinitely.

The question is simple and strange: will it ever stop?

This thought experiment is not merely academic. It is the skeleton of every self-improving agentic system currently being built — from Reflexion to AutoGPT to the improvement crons that run across research pipelines. Any system that asks a model to revise its own work is implicitly running this loop. The question of whether and when the loop terminates is therefore a foundational question for agentic hybrid intelligence.

The draft connects to Draft AR (the agentic harness, which controls when loops terminate and on whose authority) and Draft I (LLM epistemic limits, which determine whether self-evaluation is reliable). It is positioned as a theoretical companion to the empirical chapter on agentic failure modes (Draft AI).

---

## Part 1: The Setup

The loop has four steps:

1. **Generate** — the model produces an output *O_n* in response to task *T*
2. **Evaluate** — the model assesses *O_n* against some criterion *C* (explicitly stated or implicit)
3. **Decide** — the model decides: *is O_n good enough?*
4. **Repeat or halt** — if yes, the loop terminates; if no, the model generates *O_{n+1}*

The question is whether this process converges — reaches a state where the model consistently decides its output is good enough — and if so, when and why.

Three variants of the experiment are worth distinguishing:

**Variant A — Deterministic loop (temperature = 0):** The model is run with greedy decoding. Given the same input, it produces the same output. The loop either immediately converges (the model evaluates its first attempt as sufficient) or enters a cycle — alternating between a small set of outputs and evaluations without ever halting.

**Variant B — Stochastic loop (temperature > 0):** The model is run with sampling. Each generation step introduces randomness. The loop cannot cycle deterministically — but it can wander without converging.

**Variant C — Loop with external feedback:** An external evaluator (automated test, human, or separate model) replaces the model's self-evaluation. The convergence properties change substantially — external feedback is not subject to the model's self-evaluation biases.

---

## Part 2: Theoretical Constraints

### 2.1 The halting problem shadow

Turing's halting problem (1936) establishes that there is no general algorithm that can determine, for an arbitrary program and input, whether the program will eventually halt. A loop running on an LLM is not a classical program — its transitions are probabilistic, not deterministic — but the halting problem's intuition extends: no general external observer can, by inspecting the loop's current state, guarantee it will terminate.

This is not merely a theoretical curiosity. It means that any practical agentic system that runs an LLM in a self-improvement loop must impose *external* termination conditions — a maximum iteration count, a timeout, a human interrupt — because the loop's own convergence cannot be guaranteed. The termination condition is not a convenience; it is a logical necessity.

### 2.2 Fixed points and why they are not guaranteed

A system converges to equilibrium when it reaches a **fixed point**: a state *s** such that applying the loop's transition function to *s** returns *s**. For continuous functions on compact spaces, Brouwer's fixed-point theorem guarantees at least one fixed point exists. But the theorem's conditions — continuity, compactness — do not straightforwardly apply to the space of LLM outputs.

More practically: even if a fixed point exists, the loop need not reach it. Gradient descent famously gets stuck in local minima; iterative revision can get stuck in local *quality* minima where each revision is different but no better. The model may cycle between two outputs of equivalent estimated quality, never converging to either.

### 2.3 The self-evaluation problem

The loop's convergence depends critically on the quality of step 3: the model's evaluation of its own output. If the evaluation is reliable — if the model correctly identifies when its output is good enough — convergence is possible. If the evaluation is unreliable, the loop's behaviour becomes erratic.

The empirical literature on LLM self-evaluation is not encouraging. Kadavath et al. (2022) show that LLMs are systematically miscalibrated in their confidence estimates. Research on sycophancy (Perez et al., 2022; Sharma et al., 2023) shows that models have a bias toward validating their own outputs — particularly when the evaluation criterion is vague. An LLM evaluating its own creative writing may converge rapidly not because the output is good but because the model cannot clearly distinguish better from worse.

The inverse failure also occurs: models in some settings exhibit **revision compulsion** — a tendency to keep revising even when outputs are already high quality, because the revision action is itself rewarded by training. The loop runs, but convergence is repelled rather than attracted.

### 2.4 Goodhart's Law in the loop

When the model's satisfaction criterion is an imperfect proxy for actual task quality — which it almost always is — the loop optimises the proxy, not the task. This is Goodhart's Law (*any measure used as a target ceases to be a good measure*) applied to iterative AI self-improvement.

A model asked to "make this paragraph more persuasive" may converge on text that scores highly on surface markers of persuasiveness (confident assertions, rhetorical questions, vivid vocabulary) while becoming less factually accurate. It has found a fixed point — but the fixed point is in the proxy space, not the task space.

---

## Part 3: Empirical Evidence

### 3.1 Reflexion: convergence in well-defined domains

Shinn et al.'s Reflexion framework (2023) is the most systematic empirical study of iterative LLM self-improvement. Reflexion augments a language agent with a verbal self-reflection mechanism: after each failed attempt at a task, the model generates a textual critique of what went wrong and stores it in an episodic memory. The next attempt can consult this critique.

On well-defined programming tasks (HumanEval, MBPP), Reflexion converges within a small number of iterations — typically fewer than five — and achieves meaningful performance gains over non-iterative baselines. The convergence is reliable because the evaluation function is external and objective: the code either passes automated tests or it does not. When the evaluation criterion is unambiguous, the loop works.

On open-ended tasks — writing, reasoning, planning — the gains are smaller and the convergence is less reliable. The evaluation criterion is no longer binary, and the model's self-assessment introduces noise.

### 3.2 Compounding error and divergence

The inverse of convergence is **divergence**: the loop produces outputs that get progressively worse. This is documented in the multi-step hallucination literature (Rawte et al., 2023; cited in Draft I): in long agentic loops, small errors compound across steps, each revision incorporating and amplifying the errors of the previous one. A model asked to iteratively improve a factual summary may introduce confabulations in early revisions that are then reinforced and elaborated in later ones.

Divergence is more likely when: (1) the task involves factual claims that the model cannot verify, (2) the revision prompt encourages elaboration rather than correction, (3) the loop runs for many iterations without external grounding.

### 3.3 Plateau and pseudo-convergence

A third empirical pattern is the **plateau**: the loop runs, each revision is different, but meaningful quality improvement stops after a small number of iterations. The model continues revising — because its self-evaluation does not recognise the plateau — but the revisions are lateral rather than improving. This is pseudo-convergence: the loop appears to be working but has ceased to produce value.

The plateau is difficult to detect from inside the loop. It requires an external observer with an independent quality measure to identify that iteration has ceased to be productive.

---

## Part 4: What This Means for Agentic Design

### 4.1 External termination is not optional

The thought experiment's answer is: an LLM in a pure self-evaluation loop has no guaranteed termination. External stopping conditions — maximum iterations, timeouts, external evaluators, human checkpoints — are not engineering conveniences but logical requirements. Any agentic system that omits them is running an ungrounded loop.

### 4.2 The evaluation function determines everything

The quality of the loop's behaviour is almost entirely determined by the quality of the evaluation function. An external, objective evaluator (automated tests, formal verification, human expert review) produces reliable convergence. A model's self-evaluation is a noisy proxy that may converge to the wrong fixed point or fail to converge at all. This suggests a design principle: **separate the generator from the evaluator**. The ARIS framework's cross-model adversarial review (Yang et al., 2026, cited in Draft AK) instantiates this — an executor model generates, a reviewer from a different model family evaluates.

### 4.3 The satisficing alternative

Herbert Simon's concept of **satisficing** — accepting the first solution that meets a threshold rather than optimising indefinitely — is directly applicable. A loop with a satisficing criterion (halt when output meets minimum standard *C*, not when it is optimal) converges faster and more reliably than an optimising loop. This is how most well-designed agentic systems actually work in production: they define done as *good enough*, not *best possible*.

### 4.4 Iteration count as a governance parameter

The maximum number of iterations a loop may run before requiring human review is a governance parameter, not merely a technical setting. It determines how much autonomous revision an agent may perform without oversight. Under the Parasuraman et al. (2000) autonomy taxonomy (cited in Draft M), a loop with no iteration limit operates at autonomy level 9 or 10; a loop with a low limit operates at level 5–6. Setting iteration limits is therefore an act of governance, not engineering.

---

## Open Questions

1. **Is there a task class where LLM self-evaluation loops are reliably convergent?** The evidence suggests well-defined tasks with binary evaluation criteria (code passing tests, formal proofs) approach this. What is the general characterisation?

2. **Does model scale affect convergence?** Larger models may have better self-evaluation calibration, producing faster and more reliable convergence. Or they may have more revision compulsion, producing longer loops. Empirical comparison across model families is lacking.

3. **What happens in multi-model loops?** When generator and evaluator are different models — or different model sizes — convergence properties change. The cross-model adversarial design of ARIS suggests faster convergence and higher terminal quality. Is this general?

4. **The philosophical question:** A loop that converges to a fixed point produces an output that the model evaluates as finished. But the model's evaluation is fallible. Is a "finished" output from an unreliable evaluator meaningfully different from an unfinished one? What does *done* mean for a stochastic system?

---

## Key Sources (Preliminary)

- Turing, A. M. (1936). On computable numbers, with an application to the Entscheidungsproblem. *Proceedings of the London Mathematical Society*, 2(42), 230–265.
- Shinn, N., Cassano, F., Labash, A., Gopinath, A., Narasimhan, K., & Yao, S. (2023). Reflexion: Language agents with verbal reinforcement learning. arXiv:2303.11366. PDF in Kilder. **[P]**
- Kadavath, S., Conerly, T., Askell, A., Henighan, T., Drain, D., Perez, E., Schiefer, N., Das, S., Grosse, R., Fort, S., Ganguli, D., Lovitt, L., Treutlein, B., Kernion, J., Li, T., Jones, E., Landau, A., Clark, J., Petrov, B., … Clark, J. (2022). Language models (mostly) know what they know. arXiv:2207.05221. PDF in Kilder. **[P]**
- Simon, H. A. (1955). A behavioral model of rational choice. *Quarterly Journal of Economics*, 69(1), 99–118. https://doi.org/10.2307/1884852
- Rawte, V., Sheth, A., & Das, A. (2023). A survey of hallucination in large foundation models. arXiv:2309.05922. PDF in Kilder. **[P]**
- Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A*, 30(3), 286–297. https://doi.org/10.1109/3468.844354 **[J]**
- Yang, R., Li, Y., & Li, S. (2026). ARIS: Autonomous research via adversarial multi-agent collaboration. arXiv:2605.03042. **[P]**
- Levy, S. (2026, May 14). What happens when AI starts building itself? [Interview with Richard Socher, Recursive Superintelligence]. *TechCrunch*. https://techcrunch.com/2026/05/14/what-happens-when-ai-starts-building-itself/ — Socher distinguishes "improvement" (AI improving external artifacts) from true recursive self-improvement (AI autonomously redesigning its own architecture and training process); introduces open-endedness and rainbow teaming (adversarial multi-model co-evolution for safety inoculation) as the core technical approach; directly anchors Part 4 discussion of multi-model loops and the question of when/whether self-improvement converges. Also primary source for Draft BH. **[N]**

---

## What Still Needs Work

- Add empirical data from SWE-bench and similar agentic benchmarks on iteration-to-convergence distributions
- Explore the formal connection to fixed-point theory more rigorously (Banach fixed-point theorem for contractive mappings as a potential positive convergence result)
- Add the Goodhart's Law literature more formally (Manheim & Garrabrant, 2018, arXiv:1803.04585)
- Cross-reference to Draft AS (technostress) — infinite loops without termination conditions are a direct cause of runaway compute cost and human oversight fatigue
- Explore the philosophical question in Part 4.4 more carefully: what does task completion mean for a stochastic system with imperfect self-evaluation?
