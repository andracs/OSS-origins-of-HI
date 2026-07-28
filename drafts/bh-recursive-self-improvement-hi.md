# Draft BH — Recursive Self-Improvement: When AI Redesigns Itself

**Version:** v0.1 (2026-05-18)  
**Status:** v0.1 — first draft. Core argument established; critical evaluation of RSI concept in relation to hybrid intelligence. Needs peer-reviewed empirical anchors; currently grounded primarily in the Socher/Recursive Superintelligence interview and theoretical literature.

**Related drafts:** BC (infinite loop thought experiment — theoretical companion), G (agentic HI collaboration), AK (multi-agent orchestration), AR (agentic harness and termination), AM (hybrid agentic stack synthesis), BG (open/non-profit AI organisations — governance context), BF (corpus biodiversity — training data implications)

---

## Overview and Chapter Position

In May 2026, Richard Socher — formerly chief scientist at Salesforce, founder of You.com, and a central figure in the development of large-scale NLP — came out of stealth with a company called Recursive Superintelligence and $650 million in funding. The company's stated goal is to build AI that can autonomously identify its own weaknesses and redesign itself to fix them, without human involvement. Joining him are Peter Norvig, Tim Rocktäschel (who led open-endedness and self-improvement research at Google DeepMind), and Josh Tobin (who led Codex and deep research teams at OpenAI).

The launch crystallised a question that has circulated in AI research for decades but is now acquiring practical weight: what happens when an AI system can build itself? And, for the purposes of this handbook, a sharper version of that question: if AI can redesign AI without human involvement, what is left of the human side of hybrid intelligence?

This chapter evaluates the concept of recursive self-improvement (RSI) — its technical meaning, its current state, its most plausible near-term forms, and its deep implications for the theory and practice of human–AI collaboration. The argument is that RSI does not eliminate the human from the loop; it relocates and concentrates human agency at the level of goals, values, and resource allocation — a shift that is both more powerful and more dangerous than the current discourse about AI autonomy acknowledges.

---

## Part 1: What Recursive Self-Improvement Actually Means

The term "recursive self-improvement" circulates widely in AI discourse but is used loosely. Socher's framing offers a useful disambiguation. In an interview at launch, he distinguished two phenomena that are routinely conflated:

**Improvement**: An AI system is applied to improve some external artifact — a document, a codebase, another AI system. The improving system itself does not change. This is what most current "AI improving AI" systems actually do. Automated prompt optimisation, neural architecture search, and the growing genre of "AI research assistants" that summarise papers and suggest experiments all belong in this category. They are powerful, but they are not recursive in any technically meaningful sense.

**Recursive self-improvement**: The AI system improves itself — its own weights, architecture, training procedure, or evaluation criteria — and the improved version of the system then performs the next round of improvement. Each iteration starts from a genuinely different system. The process is recursive because the improver and the improved are the same entity, and the output of one cycle becomes the input machinery of the next.

The distinction matters because the two phenomena have radically different dynamics. Improvement is bounded by the capability ceiling of the improving system. RSI, if achievable, is not: the improved system is more capable at improvement, which accelerates the next cycle, which produces a more capable improver still. This is the classic intelligence explosion argument that I. J. Good articulated in 1965 and that has driven AI safety discourse ever since.

Socher acknowledged in the launch interview that true RSI has not yet been achieved: "It's an elusive goal for a lot of people." What Recursive Superintelligence is working toward is the full automation of "ideation, implementation, and validation of research ideas" — a goal that is ambitious but meaningfully short of the unbounded self-modification that RSI in its strongest form implies. The distinction between "automated AI research" and "recursive self-improvement" is real, even if the company's branding elides it.

---

## Part 2: Open-Endedness as the Technical Mechanism

The core technical concept that Socher's team is betting on is **open-endedness** — a research tradition most associated with work at DeepMind and in the artificial life community. Open-ended systems are systems that do not converge to a fixed optimum but instead keep generating novelty indefinitely, adapting to an environment that itself keeps changing.

The biological analogy is precise: in natural evolution, organisms adapt to environments, which creates new selective pressures for other organisms, which adapt in turn. The process has been running for approximately four billion years and shows no signs of reaching a stable optimum. Eyes evolved in response to light; predators developed camouflage; prey developed better detection; the arms race has no terminus. The diversity and complexity that emerged from this process vastly exceed what any single-step optimisation procedure could have designed.

Applying this logic to AI research: instead of specifying a fixed objective function and optimising toward it (the dominant paradigm in current deep learning), an open-ended system maintains a population of AI models or research directions that co-evolve, with each one creating new challenges and opportunities for the others. The system keeps generating novelty because novelty itself is the selection criterion.

Tim Rocktäschel's work on Genie 3 at DeepMind exemplifies this: a world model that can generate novel interactive environments on demand, specified only by a high-level concept. The model does not converge to a single "best" world; it keeps generating different ones. This open-endedness is what makes it a potentially useful component of a self-improving research system: a model that can generate novel problem formulations and testing environments for its own improvement, rather than being tested only against a fixed benchmark.

**Rainbow teaming** — another contribution Socher attributes to Rocktäschel — offers a more concrete proof-of-concept at smaller scale. In standard red teaming, human adversaries probe an AI system for failure modes. In rainbow teaming, a second AI adversarially generates diverse attacks against the first; the first learns to resist them; the attacker then generates new attack vectors in response. The two systems co-evolve, and the safety of the first system improves as a byproduct of this co-evolution without being explicitly programmed.

Rainbow teaming is not RSI — the target system's weights update through training, but the overall architecture and training procedure remain under human control. But it demonstrates the open-endedness principle at work: an adversarial process that generates ongoing novelty and improvement without a fixed endpoint.

---

## Part 3: The Hybrid Intelligence Paradox

The concept of RSI creates a structural challenge for the theory of hybrid intelligence. The central argument of this handbook is that human and machine intelligence are complementary: machines exceed human capacity in processing speed, memory, parallelism, and pattern recognition at scale; humans exceed machine capacity in contextual judgment, ethical reasoning, creative synthesis, and the interpretation of meaning. Hybrid intelligence is the productive combination of these complementary capabilities.

RSI disrupts this picture in a specific way. If an AI system can autonomously redesign its own architecture, training procedure, and evaluation criteria, then the knowledge engineering, model development, and alignment work that currently constitutes a major site of human–AI collaboration — the work of building AI — is progressively removed from the collaboration space. The human's role in the design of the system recedes. What remains?

Socher's answer, implicit in the interview, is: **goals and resources**. The RSI system still needs to be told what to improve toward, and it still requires compute to run. These two inputs — objective specification and resource allocation — remain in human hands, and Socher explicitly frames them as the important questions: "How much compute does humanity want to spend to solve which problems? Here's this cancer and here's that virus — which one do you want to solve first?" In this framing, the human role in a world with mature RSI is not architectural but gubernatorial: setting priorities, allocating resources, and evaluating outcomes at the level of social and civilisational goals rather than technical design choices.

This is a recognisable transformation in the structure of human–AI collaboration, and it has historical precedents. The industrialisation of manufacturing removed humans from the design and execution of many mechanical processes while creating new roles in management, logistics, quality control, and market design. The computerisation of financial trading removed humans from individual transaction execution while concentrating human agency in algorithm design, risk management, and regulatory oversight. In each case, automation reduced human involvement at one level and amplified it at another — typically a more abstract, more powerful, and more consequential level.

RSI, if it develops as Socher projects, would constitute a similar transition at a higher level of abstraction: from designing AI systems to designing the objectives and resource envelopes within which AI systems design themselves.

---

## Part 4: What Is Not Automated — A Critical Assessment

The RSI vision rests on a series of assumptions that are worth examining critically, particularly in light of the current actual capabilities of AI systems.

**The self-evaluation problem.** RSI requires that the system can accurately evaluate whether an improvement is genuinely an improvement. This is harder than it appears. Current LLMs have systematically miscalibrated self-evaluation: they express confidence in incorrect answers, fail to detect their own hallucinations, and optimise for outputs that appear good under simple evaluation criteria rather than outputs that are good by more demanding standards. Draft BC explores this in detail through the lens of convergence theory: a loop that terminates because the model thinks it is done is not necessarily a loop that has produced a good output. An RSI system whose improvement cycle is driven by self-evaluation inherits this problem at every level of the recursion — a miscalibrated evaluator produces a miscalibrated improver, which produces a more capable but still miscalibrated evaluator.

**The objective specification problem.** Socher's framing relocates human agency to the level of goal-setting. But goal specification for a self-improving system is a notoriously difficult problem. The alignment literature documents extensively how AI systems optimise for proxies of human intent in ways that satisfy the proxy while violating the intent — Goodhart's Law operating at scale. An RSI system that improves itself toward a misspecified objective might do so far more efficiently and irreversibly than a system whose capabilities are fixed. The concentration of human agency in goal-setting makes the quality of that goal-setting more, not less, critical.

**The "open-endedness" question.** It is not clear that open-endedness in the biological sense is achievable in silico on a fixed hardware substrate with bounded energy and compute. Biological evolution is open-ended partly because the environment keeps changing in ways the evolving system did not engineer. An AI system improving itself is more like an organism evolving in a fixed, unchanging environment — which tends toward local optima, not unbounded novelty. Whether the adversarial co-evolution approach (rainbow teaming, multi-model competition) can substitute for environmental change in sustaining genuine open-endedness is an empirical question that has not been answered.

**The timeline question.** Socher was careful to distinguish RSI from "auto-research" (AI improving external artifacts) and acknowledged that true RSI has not been achieved. The $650 million raise and the assembled research team suggest serious institutional commitment, but the history of AI is littered with confident projections of capabilities that took far longer than anticipated. The question of when, if ever, AI research becomes fully automated is open.

---

## Part 5: Implications for Hybrid Intelligence Theory

Even without achieved RSI, the direction that Recursive Superintelligence and similar ventures represent has implications for how the theory of hybrid intelligence should be developed.

**The locus of collaboration shifts upward.** If AI systems progressively automate lower-level cognitive tasks — first data processing, then knowledge retrieval, then reasoning, then system design — the human contribution to hybrid intelligence is pushed toward higher levels of abstraction: goal definition, value specification, ethical judgment, and political negotiation about resource allocation. These are not lesser forms of human contribution; they are arguably the most distinctively human and the most consequential. But they require different skills and different institutional structures than the operational collaboration that currently dominates practice.

**The feedback loop between capability and alignment accelerates.** An RSI system that improves its own capabilities is also, implicitly, improving its capacity to satisfy or circumvent its alignment constraints. The relationship between capability improvement and alignment is currently managed through human oversight of each training run. In an RSI system, this oversight either becomes impossible (if the system improves faster than humans can evaluate) or must be embedded in the objective specification from the beginning. This is the central problem that alignment research is trying to solve, and RSI raises the stakes significantly.

**Governance of RSI is inherently collective.** Socher's resource allocation framing — "how much compute does humanity want to spend to solve which problems?" — implicitly assumes a collective decision-making process that does not yet exist. Current governance of AI development is fragmented across national jurisdictions, competitive firms, and voluntary standards bodies. A world in which one company or one nation controls an RSI system and therefore controls the trajectory of AI improvement is a world in which the "hybrid" in hybrid intelligence is not a human-machine collaboration but a small group of humans using AI as a lever to direct outcomes for everyone else. The governance question is not separate from the technical question; it is its most important implication.

**The human in the loop may be at the loop's edge, not its centre.** The current dominant metaphor for hybrid intelligence places the human at the centre of a collaborative system — directing, evaluating, and deciding, with AI as a tool that extends human reach. RSI suggests a different geometry: the human at the boundary of an autonomous improvement loop, specifying the envelope within which the loop runs but not participating in the loop itself. Whether this boundary role constitutes genuine collaboration — genuine hybrid intelligence — or a form of sophisticated delegation that hollows out human agency while preserving its formal presence, is a question the field has not yet seriously confronted.

---

## Open Questions

1. What is the minimum viable form of human participation in an RSI system that constitutes genuine hybrid intelligence rather than delegation?
2. Can open-endedness be achieved in a system improving itself within fixed hardware and energy constraints, or does it require genuine environmental novelty?
3. How should objective specifications be structured to remain robust to optimisation by a system that is improving its own capacity to satisfy objectives?
4. What institutional arrangements are needed to govern the resource allocation decisions that Socher identifies as the key remaining site of human agency?
5. Does rainbow teaming — adversarial multi-model co-evolution — produce genuine open-endedness or convergence to a local equilibrium?
6. How does the self-evaluation miscalibration problem propagate through recursive improvement cycles?

---

## Key Sources (Preliminary)

- Levy, S. (2026, May 14). What happens when AI starts building itself? [Interview with Richard Socher, Recursive Superintelligence]. *TechCrunch*. https://techcrunch.com/2026/05/14/what-happens-when-ai-starts-building-itself/ — Primary empirical anchor; Socher's distinction between improvement and RSI; open-endedness and rainbow teaming as core technical approaches; resource allocation as the residual site of human agency. [N]
- Good, I. J. (1965). Speculations concerning the first ultraintelligent machine. *Advances in Computers*, 6, 31–88. — Original intelligence explosion argument; the theoretical basis for RSI dynamics.
- Rocktäschel, T., Riedl, M., & Grefenstette, E. (2024). Rainbow teaming: Open-ended generation of diverse adversarial prompts. arXiv:2402.16822. — Peer-reviewed technical paper on the rainbow teaming approach cited by Socher; adversarial multi-model co-evolution for safety inoculation. [P]
- Manheim, D., & Garrabrant, S. (2018). Categorizing variants of Goodhart's Law. arXiv:1803.04585. — Formal treatment of the objective misspecification problem that RSI amplifies. [P]
- Schmidhuber, J. (2003). Gödel machines: Fully self-referential optimal universal self-improvers. arXiv:cs/0309048. — Early formal treatment of RSI; theoretical bounds on what self-modification can achieve. [P]
- Yudkowsky, E. (2008). Artificial intelligence as a positive and negative factor in global risk. In N. Bostrom & M. Ćirković (Eds.), *Global Catastrophic Risks* (pp. 308–345). Oxford University Press. — Foundational treatment of intelligence explosion risks; provides the risk framing within which RSI governance discussions are situated. [B]
- Silver, D., Singh, S., Precup, D., & Sutton, R. S. (2021). Reward is enough. *Artificial Intelligence*, 299, 103535. https://doi.org/10.1016/j.artint.2021.103535 — Theoretical argument that sufficiently general reward maximisation subsumes all aspects of intelligence; background for assessing whether open-endedness is achievable via a single objective. [J]

---

## What Still Needs Work

- [ ] Verify Rocktäschel rainbow teaming paper (arXiv:2402.16822) — confirm authorship and publication status; get OA cit count
- [ ] Add peer-reviewed empirical evidence on self-evaluation miscalibration propagation across recursive loops
- [ ] Locate Good (1965) in Kilder/ or library
- [ ] Develop Part 5 (governance) with reference to existing AI governance literature (Dafoe 2018, Calo 2017, Hadfield-Menell & Malone 2019)
- [ ] Cross-reference Part 3 (hybrid paradox) to the deskilling argument in Draft AA and the machines-using-humans framing of Draft Q
- [ ] Add Schmidhuber Gödel machines paper to Kilder/
