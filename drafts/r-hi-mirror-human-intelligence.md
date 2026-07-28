# Draft R — What Hybrid Intelligence Teaches Us About Human Intelligence

**Version:** v0.3 (2026-05-12) / **Status:** VandenBroeck 2025 attribution flag resolved → Sun, Fengfei et al. (2025); §2.2 anchored to Sun et al.'s 20–60% overconfidence finding; cross-refs added to Drafts H (§1.1) and I (§2.2).
**Next:** Find empirical meta-cognition studies; consider §3 expansion on embodied cognition (Varela/Thompson/Rosch).

---

## Overview and Chapter Position

Building and studying artificial intelligence is one of the most productive mirrors humanity has ever held up to itself. When we try to formalise and replicate intelligence, we are forced to make explicit what we have hitherto taken for granted: what is a concept, what is understanding, what makes an answer *correct*, what is creativity *really*?

Hybrid intelligence — the interplay of humans and AI — is a particularly rich field of inquiry because it does not merely pose the philosophical questions abstractly but provides empirical data: we can observe what happens when human and artificial intelligence meet, complement, fail, and augment each other. The patterns in that encounter reveal something fundamental about both.

This draft is not primarily an empirical literature survey but a synthesising reflection: what does HI research *imply* about the nature of intelligence, about knowledge, and about creativity? It is the chapter's most philosophical element and functions as a framing conclusion to the more empirical drafts.

---

## Part 1: Intelligence Is Not Individual — It Never Was

**1.1 The Extended Mind and AI as New Extension**
Andy Clark & David Chalmers' *Extended Mind* thesis (1998) argued that cognition is not confined to the skull: notebooks, calculators, other people are parts of our cognitive system in a meaningful sense. That proposition was philosophically controversial in 1998.

HI makes it empirically unavoidable. When a physician diagnoses with AI assistance, it is not "the brain plus a tool" — it is an integrated cognitive system, where it is meaningless to try to locate the diagnosis either "in the doctor" or "in the AI". The degree of understanding, the type of error, and the character of the decision change fundamentally depending on the configuration.

The consequence: HI gives us empirical evidence that human intelligence *always was* distributed — we simply built more rudimentary extensions (pen, book, calculator). AI is a qualitatively new extension, but not a break from history. (For the historical and developmental dimensions of how humans are reshaped *by* their extensions — niche construction, generational re-skilling, dependency — see Draft H on human augmentation and co-evolution.)

**1.2 Intelligence as an Ecological Phenomenon**
James Gibson's affordance theory and Edwin Hutchins' *Cognition in the Wild* (1995) show that human cognition is adapted to and dependent on structured environments. Navigation is not an individual cognitive achievement — it is a cognition distributed across brain, map, compass, nautical charts, and crew.

Hippocampus research (Maguire 2000; Javadi 2017) shows that GPS use actually changes hippocampal representation of space — and conversely that London taxi drivers' hippocampi grow with the city's complexity. Intelligence shapes environments; environments shape intelligence. AI is the most potent environmental factor so far.

The analogy between human and AI memory systems is more than metaphor. Jia et al. (2026) survey memory mechanisms across large language and multimodal models, taxonomising them into *implicit memory* (knowledge encoded in model parameters), *explicit memory* (external storage and retrieval), and *agentic memory* (persistent structures in autonomous agents). This tripartite structure maps loosely onto hippocampal and neocortical memory systems in humans — procedural and semantic memory consolidated in weights; episodic and working memory externalised in retrieval; prospective memory encoded in agent state. The survey's central question — "how far are we from human memory?" — is precisely the question that HI research operationalises empirically: not as abstract philosophy but as a measurable design constraint. The gaps are instructive: AI implicit memory is static (no continual learning), explicit memory is human-cued (no autonomous consolidation), and agentic memory lacks the autobiographical integration that characterises human episodic memory.

**1.3 The Platonic Representation Hypothesis**
Huh et al. (2024) present evidence that different AI models converge toward the same internal representations of the world — regardless of architecture and training data. The hypothesis: there is a universal structure in the perceptual world that sufficiently capable systems necessarily converge toward.

If this holds, it has a radical implication for the theory of human cognition: human intelligence and AI intelligence are not fundamentally different modalities — they are two instances of the same convergence process toward the world's structures. This is one of the strongest arguments that we are studying *intelligence in general* — not two separate phenomena.

The convergence claim acquires mechanistic depth when read together with the *superposition* literature. Elhage et al. (2022) showed that neural networks routinely represent more features than they have dimensions, packing concepts into overlapping directions in activation space — a finding now extended by Liu, Liu & Gore (2025), whose NeurIPS 2025 result derives neural scaling laws directly from superposition geometry: loss decreases with model dimension because additional dimensions reduce interference between superposed feature vectors. Read together, Huh and Liu et al. suggest that what converges across architectures is not a discrete inventory of concepts but a *geometry* — a high-dimensional manifold whose structure is dictated by the statistics of the world the systems are trained on. The implication for cognitive science is significant: if biological neural systems also represent features in superposition (as a long tradition from sparse-coding theory suggests), then the structural similarity between biological and artificial cognition is not metaphorical but architectural — both are dimensionality-limited systems compressing a richer feature space into a manifold whose geometry is partially determined by the input distribution itself.

---

## Part 2: What AI Cannot Do — and What That Reveals

**2.1 Competence Without Understanding**
Daniel Dennett's distinction: AI demonstrates that *competence* and *understanding* can be separated. LLMs are competent at a wide range of linguistic and cognitive tasks — and yet there are strong reasons to doubt that they *understand* in the sense we normally mean by the word.

The question it raises: what *is* human understanding, if not merely a more sophisticated competence? Thomas Nagel's "What Is It Like to Be a Bat?" (1974) points to the phenomenal dimension of consciousness as what AI manifestly lacks. But Nagel's point is more radical: we have no access from the outside to verify what understanding is. HI makes this problem practical — we cannot fully trust AI, and part of the reason is that we do not know whether it *understands*, and we lack a clear concept of what we mean by that.

**2.2 Hallucination and the Human Sanity Check**
LLMs hallucinate: they produce convincingly incorrect claims without internal alarm (Rawte et al. 2023). Kadavath et al. (2022) show that models have partial but limited self-knowledge — larger models can estimate "P(True)" for their own answers reasonably well on multiple-choice tasks, but calibration breaks down on novel or open-ended problems. Ulmer et al. (2025) document a systematic *mind-confidence gap*. Sun, Li, Wang & Göette (2025) put empirical numbers on the phenomenon: on algorithmically constructed reasoning problems with known solutions, five frontier LLMs overestimated the probability of their own answers being correct by 20–60%, and — crucially — the overconfidence *intensified* as the underlying probability of being correct *decreased*. Humans show the same baseline bias, but not the same divergence at low confidence.

What this reveals about human cognition: we are *not* fundamentally better calibrated — humans hallucinate, are overconfident, and are poor at estimating their own competences (Dunning-Kruger). What *actually* distinguishes humans is not the absence of hallucination but access to meta-cognitive correction mechanisms: social feedback, experiential learning over time, consequences for real-world actions that create incentives for calibration. Well-designed HI systems replicate these correction mechanisms socially — they do not replace human meta-cognition; they amplify it. (For the inverse perspective — how the *structural* features of LLMs that cause hallucination shape what counts as an epistemic limit, and why retrieval and calibration patches are insufficient — see Draft I on LLM epistemic limits.)

**2.3 Symbol Grounding and the Foundation of Meaning**
LLMs operate over language without having the perceptual and action-based grounding (*Bodenständigkeit*) that language is typically thought to have for humans (Harnad 1990). A dog running is represented in the model as patterns in co-occurrence statistics — not as a remembered perceptual encounter with a dog.

And yet: LLMs are competent users of language. What does this reveal? Either that grounding is not necessary for linguistic competence — or that grounding is embedded *implicitly* in statistical structure (because language is co-produced by grounded users over generations). Mikolov et al.'s Word2Vec (2013) showed that geometric relations in word-vector spaces reflect semantic relations — king is to queen as man is to woman. Semantics is encoded in distributed statistical structure. What this says about human semantics is contested, but not trivial.

---

## Part 3: What HI Reveals About Knowledge

**3.1 Knowledge Is Never Purely Individual**
Training data is crystallised collective knowledge: the written thoughts, discoveries, failures, and insights of millions of people, compressed into model parameters. When an AI answers a question, it draws on an accumulated human knowledge base that would have been inaccessible to any single individual.

This is not new — books, libraries, and universities do the same. But AI compresses and makes accessible at a scale and with an integration that has no historical precedent. The consequence for epistemology: individual knowledge and collective knowledge are not two separate categories — individual cognitive capacity is always mediated by culturally accumulated knowledge. AI is simply the most efficient mediation mechanism so far.

**3.2 Tacit Knowledge and Its Limits**
Michael Polanyi's classical observation: "We know more than we can tell." Expert knowledge is partly non-verbalisable — the experienced surgeon, the skilled pianist, the intuitive researcher knows something they cannot articulate. HI reveals this boundary precisely: what AI *cannot* learn from text and code is the part of human knowledge that has never been formalised.

This is an empirical hypothesis that can be tested: domains where human expertise is primarily tacit (craft, social intuition, bodily skill) should exhibit the weakest HI synergy, because AI's contribution is limited to what has been made explicit. Domains with strong formalised knowledge (medicine, law, code) should exhibit the strongest synergy. The empirical literature partly supports this (cf. `o-hi-ecosystems-studies.md`).

**3.3 The Knowledge Boundary as Identity Marker**
A more speculative observation: in a world where AI can produce competent output in most verbal and formal domains, the cognitive identity of the human contribution shifts toward what AI *cannot* do. Human expertise is redefined from "can answer correctly" to "knows when the answer is wrong", "can ask the question that is not being asked", "can navigate the normative complexity that is not in the dataset".

This is not a consolation prize — it is a substantive epistemological observation: human meta-cognition, normative judgement, and contextual sensitivity are not residuals after AI's automation, but fundamental forms of knowledge that presuppose human experience in the world.

---

## Part 4: What HI Reveals About Creativity

**4.1 Creativity as Recombination — and What Remains**
Boden's analysis (cf. `l-creativity-ai.md`): combinatorial creativity is what AI does best, and it constitutes a large part of human creativity. If AI can do it, it may not be the most interesting aspect of human creativity.

What apparently remains: *transformational* creativity — that which changes the rules by which creativity is assessed. Turing himself, Einstein, Beethoven. But is there evidence that transformational creativity is qualitatively different from exploratory creativity — or is it merely exploratory creativity that happens to strike a boundary?

HI casts new light: the human contributor in creative HI systems contributes *selection and evaluation* — what is good? What surprises? What is meaningful? These are normative, experience-based, and context-sensitive functions that presuppose a living subject with concrete interests and experiences. That is the part of creativity that cannot be reduced to statistical recombination.

**4.2 Intentionality and the Role of Randomness**
Human creativity involves intentionality — a direction, an effort toward something. But large parts of creative breakthrough are random: the unexpected meeting, the mistake that turns out to be productive, the association that arises without plan.

AI can produce surprising output — but the surprise is from the user's perspective, not the AI's. What does this reveal? Perhaps that creative surprise is *relational*: it is surprising to a subject with expectations. AI can generate inputs for human creative surprise — but cannot experience it. This may not be an incidental asymmetry but the core of what creativity is: an encounter between expectation and the unexpected, which requires a subject with expectations.

**4.3 AI as Generative Disruption**
Paradoxically: AI can *advance* human creativity by producing output that challenges, provokes, and surprises — even though AI itself is not creative in the subjective sense. A random generator can provide creative occasions for a human with an intentional project. What HI adds is *structured randomness* — output that is informed enough to be useful, but sufficiently unexpected to expand the human search space.

---

## Part 5: The Deeper Conclusion — The Mirror Points Both Ways

**5.1 AI as Operationalised Intelligence Theory**
Every AI architecture is an implicit theory of what intelligence is. The transformer is a theory that attention-based contextualisation of sequences is sufficient for cognition. Reinforcement learning is a theory that reward optimisation is sufficient for behaviour. Diffusion models are a theory that knowledge is a statistical manifold in high-dimensional space.

These theories are imprecise and incomplete — but they are explicit and falsifiable. What they reveal about human intelligence is that we have hitherto lacked precise, falsifiable theories of it. AI research compels cognitive science to sharpen its concepts.

**5.2 The Human Differential as an Empirical Question**
What are humans better at than AI? This is no longer a philosophical question but an empirical one. HI research continuously produces data: domains and task types where the human contribution is positive, negative, or neutral. This is a unique historical situation: for the first time we have a system that is cognitively competent enough to function as a control condition for human intelligence.

What we are learning, tentatively: humans are relatively better at contextual sensitivity, normative navigation, long-range causal understanding, social inference, and meta-cognition. AI is relatively better at breadth of pattern recognition, consistency under volume, and integration of formalised knowledge. This distribution is not accidental — it reflects what *can* be formalised and what cannot.

**5.3 Intelligence as a Relational Form**
The deepest conclusion: the study of HI points toward a relational conception of intelligence. Intelligence is not an individual attribute — either for humans or for AI — but a property that arises in the relation between a system and its environment, its tasks, its collaborators. An LLM is not intelligent; a radiologist is not intelligent; the HI system that combines them in a clinical context is intelligent to the degree that it produces clinically good knowledge.

This is not merely an academic point. It is a design principle: HI should not be designed as "an AI plus a human watchdog" but as an integrated cognitive system in which the components' properties are mutually configuring.

---

## Open Questions

1. **Is the Platonic representation hypothesis falsifiable?** Do all intelligent systems converge toward the same representations, or are there multiple stable attractors?

2. **What is the neural and computational basis of meta-cognition?** If humans are better at knowing what they do not know, what is the precise mechanism — and can it be replicated?

3. **Is transformational creativity a quantitative or qualitative difference from exploratory creativity?** Empirical investigation: can we identify historical breakthroughs that *cannot* be reconstructed as exploratory creativity in a retrospectively defined space?

4. **What happens to human identity when AI surpasses us at most things?** Psychological and sociological research on this mirror effect is in its early stages.

5. **Can HI research inform a new cognitive science?** A cognitive science that explicitly takes distributed, relational, historically anchored intelligence as its starting point — rather than the isolated individual as baseline?

---

## Sources (Anchors)

**Already in Kilder:**
- Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7–19. [J] [OA cit: 5005] ✓
- Nagel, T. (1974). What is it like to be a bat? *The Philosophical Review*, 83(4), 435–450. [J] ✓
- Maguire, E. A., et al. (2000). Navigation-related structural change in the hippocampi of taxi drivers. *PNAS*, 97(8), 4398–4403. [J] [OA cit: 3204] ✓ (CrossRef: no retraction)
- Javadi, A.-H., et al. (2017). Hippocampal and prefrontal processing of network topology to simulate the future. *Nature Communications*, 8, 14652. [J] [OA cit: 214] ✓
- Mikolov, T., et al. (2013). Efficient estimation of word representations in vector space. arXiv:1301.3781. [P] [OA cit: 18 110] ✓ (foundational; iCit far above [P] threshold)
- Huh, M., et al. (2024). The Platonic representation hypothesis. arXiv:2405.07987. [P] [OA cit: 25] ✓ (ICML 2024 — upgrade to [C] when OpenAlex venue updates)
- Elhage, N., et al. (2022). Toy models of superposition. arXiv:2209.10652. [P] [OA cit: 41] ✓
- Liu, Y., Liu, Z., & Gore, J. (2025). Superposition yields robust neural scaling. NeurIPS 2025. arXiv:2505.10465. [C] [OA cit: 0 — too new] ✓
- Kadavath, S., et al. (2022). Language models (mostly) know what they know. arXiv:2207.05221. [P] [OA cit: 161] ✓
- Rawte, V., et al. (2023). A survey of hallucination in large foundation models. arXiv:2309.05922. [P] [OA cit: 96] ✓
- Ulmer, D., et al. (2025). Mind the confidence gap: Overconfidence, calibration, and distractor effects in large language models. arXiv:2502.11028. [P] [OA cit: 1] ✓
- Sun, F., Li, N., Wang, K., & Göette, L. (2025). Large language models are overconfident and amplify human bias. arXiv:2505.02151. [P] [OA cit: 5] ✓ (attribution corrected from prior "VandenBroeck" misattribution; first-author verified via OpenAlex DOI lookup 2026-05-12; PDF in Kilder/ as `Sun2025_LLMsOverconfidentAmplifyBias_arXiv2505.02151.pdf`)
- Silver, D., & Sutton, R. (2025). The era of experience. [R] ✓
- Kuhn, L., et al. (2023). Semantic uncertainty: Linguistic invariances for uncertainty estimation in natural language generation. ICLR 2023. arXiv:2302.09664. [C] [OA cit: 49] ✓
- Jia, Z., et al. (2026). The AI hippocampus: How far are we from human memory? arXiv:2601.09113. [P] [OA cit: 0 — too new] ✓

**Missing — to search/obtain:**
- Hutchins, E. (1995). *Cognition in the Wild*. MIT Press. — **[BOOK]**
- Polanyi, M. (1966). *The Tacit Dimension*. Doubleday. — **[BOOK]**
- Dennett, D. (1991). *Consciousness Explained*. Little, Brown. — **[BOOK]**
- Harnad, S. (1990). The symbol grounding problem. *Physica D.* — **[check access]**
- Gibson, J. J. (1979). *The Ecological Approach to Visual Perception*. Houghton Mifflin. — **[BOOK]**
- Boden, M. A. (2004). *The Creative Mind.* — **[BOOK — also cited in Draft L]**

---

## What Still Needs Work

- [ ] Add all BOOK references to library wishlist
- [ ] Find Harnad 1990 (symbol grounding) — check if accessible
- [ ] Find empirical studies on meta-cognition as human differential
- [ ] Consider section on *embodied cognition* (Varela, Thompson, Rosch) — the body as cognitive foundation AI lacks
- [ ] Re-verify Liu, Liu & Gore (2025) NeurIPS 2025 venue once OpenAlex indexes the proceedings (currently still listed as preprint)
