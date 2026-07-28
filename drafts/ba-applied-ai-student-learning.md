# Draft BA — Applied AI and Student Learning: Personalization, Scaffolding, and the Transformation of Educational Practice

**Version:** v0.3 (2026-05-11)
**Status:** v0.3 — Koedinger & Corbett (2006) Cambridge Handbook chapter verified via CrossRef (DOI 10.1017/cbo9780511816833.006; pages 61–78; ISBN 9780521845540), pending-citation flag resolved. Mollick & Mollick (2023) confirmed with DOI 10.2139/ssrn.4475995 and SSRN URL. UNESCO (2023) generative AI guidance attributed to Miao, F., & Holmes, W. (named authors per UNESCO title page) with unesdoc ark identifier.
**Next:** Trace Yan 2023 and Liang 2023 to specific publications on AI writing feedback in education; verify Khanmigo deployment scale figures against a Khan Academy or peer-reviewed institutional source; obtain Chiu (2024) full PDF via institutional access.

---

## Overview and Chapter Position

Education is the domain where hybrid intelligence has the clearest and most directly measurable human benefit case. Every student learns differently; every teacher has limited time; and the gap between what one-on-one expert instruction produces and what the best mass-education systems deliver has been precisely quantified. Applied AI offers, for the first time, a technically plausible route to closing that gap at population scale — not by replacing teachers, but by extending the reach and granularity of instructional support in ways no purely human system can match.

This chapter examines how applied AI enables student learning, anchored in Chiu's (2024) thematic study of generative AI in higher education. It situates current AI-enabled learning tools within the longer history of adaptive and intelligent instructional systems, examines the specific capabilities that large language models and multimodal models add to that history, and analyses the risks — cognitive offloading, academic integrity erosion, equity amplification — that accompany those capabilities.

The chapter argues three things. First, the adoption of generative AI in education does not represent a break from prior instructional technology but an acceleration of a trajectory toward individualized adaptive instruction that began with early intelligent tutoring systems in the 1980s. Second, the distinctive contribution of LLM-based tutors is not superior content knowledge but superior conversational flexibility — the capacity to meet a learner where they are, in natural language, without requiring pre-specified curriculum paths. Third, the risks of AI in education are not primarily about capability but about the distribution of access, the displacement of metacognitive effort, and the structural challenge of assessing learning in an environment where AI can perform many assessed tasks better than the students being assessed.

This draft connects most directly to Draft H (human augmentation and co-evolution), Draft AC (model vs. human performance), Draft I (LLM epistemic limits), and Draft AF (human labour in AI training). It is distinct from those drafts in its focus on the pedagogical relationship — the specific context of a learner trying to acquire knowledge or skill — rather than on capability benchmarks, labour economics, or system architecture.

---

## §1 — The Baseline Problem: Bloom's 2-Sigma and the Mass-Education Trade-off

### 1.1 The 2-sigma finding

In a landmark 1984 paper, Benjamin Bloom reported that students receiving one-on-one tutoring from a knowledgeable human tutor performed approximately two standard deviations better on achievement tests than students receiving conventional classroom instruction — placing the average tutored student at the 98th percentile of the conventionally taught distribution (Bloom, 1984). This "2-sigma problem" — achieving tutoring-equivalent outcomes at mass scale — has been the organizing challenge for instructional technology research for four decades.

The magnitude of the finding reflects the core limitation of classroom instruction: a single teacher addresses 25–35 students simultaneously, cannot diagnose each student's current misconceptions in real time, cannot adapt pacing to individual learning curves, and cannot provide the immediate corrective feedback that prevents misconceptions from consolidating into stable errors. The tutored student gets all of these; the classroom student gets none of them routinely.

### 1.2 Prior attempts to scale personalised instruction

Before generative AI, the principal technological responses to Bloom's challenge were:

**Computer-Based Instruction (CBI, 1960s–1980s):** Branching programs that routed students to different content based on quiz responses. Adaptive only within a pre-specified decision tree; could not handle open-ended responses or novel misconceptions.

**Intelligent Tutoring Systems (ITS, 1980s–present):** Systems with explicit student models, domain knowledge representations, and tutoring strategies — capable of diagnosing misconceptions and selecting instructional moves dynamically. The Cognitive Tutor (Carnegie Learning) and ALEKS (McGraw-Hill) are commercial descendants. VanLehn's (2011) meta-analysis found that step-based ITS produced effect sizes approaching those of human tutoring (around 0.76 standard deviations) — substantial, and considerably closer to one-on-one human tutoring than earlier reviews had estimated.

**Massive Open Online Courses (MOOCs, 2012–present):** Scalable delivery of recorded lectures with automated quiz grading. Achieved scale (millions of students) but minimal personalisation; completion rates of 5–15% reflect the absence of adaptive support.

VanLehn's (2011) revised estimate left the gap to one-on-one human tutoring narrower than Bloom (1984) had implied — but the gap is still real, and outside the laboratory conditions of the underlying studies, deployed ITS systems rarely reach the 0.76 figure. The question generative AI raises is whether conversational models, which abandon the explicit student/domain models of classical ITS in favour of natural-language interaction, can extend ITS-class effectiveness to a wider range of subjects, learners, and instructional contexts than hand-authored systems ever reached.

---

## §2 — Chiu (2024) on Transforming Higher Education with Generative AI

### 2.1 Study design and themes

Chiu (2024) is a qualitative interview study of 51 students from three research-intensive universities, designed to identify how generative AI (GenAI) is reshaping the goals, pedagogy, and assessment of higher education from the learner's perspective. Chiu starts from an initial conceptual framework derived from a systematic literature review of opportunities and challenges of AI in education, then uses that framework to organise data collection and thematic analysis. The study reports three principal themes — broadly clustered around *learning outcomes*, *pedagogy*, and *assessment* — together with ten subthemes, each grounded in student accounts of how GenAI is changing their experience of higher education (Chiu, 2024).

The study's substantive claims, drawn from those themes, are direct enough to anchor a chapter. Future higher education, on Chiu's reading, must train students to be employable in a workforce that already uses GenAI; this entails *new learning outcomes* (skills in learning and teaching with GenAI alongside more general AI literacy), *new pedagogy* emphasising interdisciplinarity and maker-style learning, and *new assessment* weighted towards in-class and hands-on activities that GenAI cannot complete on the student's behalf. Chiu (2024) closes with six future research directions: (i) competence for the future workforce and self-assessment measures; (ii) AI literacy and competency measures; (iii) the relationships among new literacies; (iv) interdisciplinary teaching; (v) innovative pedagogies and their evaluation; and (vi) new assessment formats and their acceptance by students and institutions.

### 2.2 Positioning Chiu within the broader literature

Chiu (2024) sits within a cluster of 2023–2024 work that maps generative AI onto educational practice. Kasneci et al. (2023) survey opportunities and challenges of LLMs in education, identifying personalised feedback, writing assistance, and automated assessment as the principal opportunity areas while flagging hallucination, bias propagation, and academic integrity as the principal risk areas. Mollick and Mollick (2023) propose seven instructional design patterns for deliberate AI integration in higher education classrooms — AI as tutor, coach, mentor, teammate, tool, simulator, and student — each tied to a prompt template intended to make the design choices replicable. Miao and Holmes's (2023) guidance for UNESCO member states emphasises teacher mediation, age-appropriate use, and AI literacy as prerequisites for beneficial deployment.

Chiu's contribution relative to these neighbouring works is its student-perspective evidence base: where Kasneci et al. survey the literature and Mollick and Mollick propose design patterns, Chiu reports what learners themselves say about the outcomes, pedagogies, and assessments they expect higher education to provide in a GenAI-saturated environment. The three themes and six research directions in Chiu (2024) are therefore used in this chapter as a structuring lens for §3–§7 — with the proviso that Chiu's empirical base is undergraduate students at research-intensive universities, and the generalisations beyond that setting in §5 and §7 must be supported by evidence drawn from elsewhere.

---

## §3 — Intelligent Tutoring Systems: History, Architecture, and the LLM Transition

### 3.1 The architecture of classical ITS

A classical intelligent tutoring system has four components (Anderson, Corbett, Koedinger & Pelletier, 1995): (1) a *domain model* representing expert knowledge of the subject; (2) a *student model* tracking the learner's current knowledge state, including diagnosed misconceptions; (3) a *pedagogical module* selecting the next instructional move given the student model; and (4) a *communication interface* presenting content and receiving student responses. The architecture is principled and interpretable, but rigid: the domain model must be hand-authored, the student model can only represent states the designers anticipated, and the communication interface cannot handle the full range of natural-language interaction.

The Cognitive Tutor for algebra (Koedinger & Corbett, 2006) is the best-studied commercial ITS, with randomised controlled trial evidence of significant learning gains over textbook instruction. Its student model tracks mastery of approximately 100 algebra "knowledge components" and adjusts problem difficulty accordingly. Its ceiling is also instructive: it cannot explain *why* a step is wrong in natural language; it can only indicate that it is wrong and return the student to a worked example.

### 3.2 LLMs as a new tutoring architecture

Large language models do not have the explicit domain model, student model, or pedagogical module of classical ITS. They have, instead, a vast implicit encoding of domain knowledge (whatever appeared in training data), the capacity to generate explanations in natural language at multiple levels of abstraction, and the ability to respond to open-ended student utterances without pre-specified response paths. The trade-off relative to classical ITS is precise: LLMs gain flexibility and naturalness at the cost of inspectability and guaranteed correctness.

The educational implications of this trade-off are significant. An LLM-based tutor can, for the first time, handle a student who says "I don't understand why you have to flip the inequality sign when you multiply by a negative number" and produce a correct, appropriately pitched explanation — something no prior automated system could do reliably. The same LLM can, on a bad forward pass, produce a confident but mathematically incorrect explanation of the same point — something no classical ITS would do, because its feedback was generated from a hand-authored domain model. The hallucination risk in educational AI is not merely about factual accuracy but about teaching incorrect procedures with the authority of a fluent explanation.

### 3.3 Khanmigo and the deployment frontier

Khan Academy's Khanmigo — a GPT-4-based tutoring assistant integrated into the Khan Academy platform — is among the most widely deployed LLM tutoring systems as of 2026 (deployment scale figures pending verification against a Khan Academy or peer-reviewed institutional source). It is designed around a Socratic constraint: the system is prompted to answer students' questions with guiding questions rather than direct answers, preserving the need for student cognitive effort. This design choice operationalises a specific theory of learning — that the act of retrieving and constructing an answer consolidates learning more effectively than receiving the answer — and is consistent with Chi and Wylie's (2014) ICAP framework, which ranks interactive engagement above passive reception for learning outcomes.

---

## §4 — Generative AI as a Learning Scaffold

### 4.1 What scaffolding means in instructional theory

Scaffolding — a concept originating in Wood, Bruner and Ross's (1976) extension of Vygotsky's zone of proximal development — refers to temporary instructional support that enables a learner to accomplish tasks they could not accomplish alone, with the support progressively withdrawn as the learner's competence develops. The metaphor is architectural: scaffolding is erected to enable construction and removed when the structure stands independently.

AI-based scaffolding has an architectural irony: it is infinitely patient and infinitely available, which means the temporal pressure for withdrawal — the natural progression from assisted to independent performance — is absent unless deliberately engineered. A student who always has an AI scaffold available may never develop the capacity for unscaffolded performance, not because the scaffold failed but because it succeeded too completely.

### 4.2 Writing assistance and the composition learning problem

Writing is the domain where generative AI scaffolding has had the greatest and most contested impact in education. LLMs can draft, revise, critique, and explain written texts in natural language with a fluency that exceeds most student writers. The pedagogical question is whether engaging with these capabilities constitutes learning to write or substituting for writing.

The evidence is preliminary but directional. Early classroom studies of AI writing assistants suggest that students who receive AI feedback on drafts often produce higher-quality final submissions than those who do not, but that the learning transfer — whether students write better on unassisted tasks after AI-assisted practice — depends critically on how the AI feedback is structured. Feedback that explains *why* a passage is weak and *what kind of revision* would address it appears to produce more transfer than feedback that rewrites the passage directly. (Specific peer-reviewed citations for these classroom studies are pending — see Source-acquisition note below.)

### 4.3 Adaptive feedback and formative assessment

Formative assessment — the use of assessment to guide ongoing instruction, as distinct from summative assessment that certifies achievement — is the context where AI-generated feedback has the clearest theoretical rationale. A student who submits a programming assignment at midnight and receives specific, line-level feedback on their misconceptions in seconds is better positioned to correct and resubmit before the next class than a student who must wait for a teaching assistant to grade and return work three days later. The time compression of the feedback loop is the primary mechanism through which AI formative assessment improves learning.

Automated code grading is the most mature domain: tools such as Gradescope (now part of Turnitin) and GitHub Copilot's educational variants use a combination of test-case execution and LLM-generated feedback. The challenge for domains without executable ground truth — essay writing, mathematical proof, historical argument — is that AI feedback quality depends on the LLM's calibrated uncertainty, a property that connects directly to Draft I's analysis of LLM epistemic limits.

---

## §5 — Personalized Learning at Scale

### 5.1 From adaptive sequencing to adaptive explanation

Classical adaptive learning systems personalized *what content* was presented next based on student performance. Generative AI personalizes *how content is explained* — selecting analogies, adjusting vocabulary, providing more or fewer intermediate steps based on conversational inference about the student's current state. This is a qualitatively different form of personalisation: adaptive explanation rather than adaptive sequencing.

The distinction matters because the most common barrier to learning is not encountering the wrong content at the wrong time but encountering an explanation that does not connect with the student's existing conceptual framework. A student who understands fractions but not negative numbers needs an explanation of negative fractions that builds from fractions; a student who understands temperature as negative but not fractions needs the opposite bridge. No pre-authored curriculum path handles all starting points; a conversational system that can probe the student's prior understanding and tailor the explanation accordingly can.

### 5.2 Language and access

Mass adoption of LLM-based educational tools in English has a significant equity implication: they are substantially less capable in lower-resource languages, where training data is thinner and quality of instruction correspondingly weaker. A student learning mathematics in Swahili, Yoruba, or Tagalog through an LLM receives lower-quality instruction than a student learning in English, French, or Mandarin — reproducing, in AI form, the resource asymmetries of the pre-AI educational world. This is the connection to Draft W (the unharvested commons and WEIRD bias in AI training data): the same linguistic bias in training corpora that produces lower-quality LLM outputs in low-resource languages produces lower-quality AI tutors for students who speak those languages.

---

## §6 — Metacognition and the Cognitive-Offloading Risk

### 6.1 What metacognition is and why it matters

Metacognition — the learner's capacity to monitor and regulate their own cognitive processes — is among the strongest predictors of long-term academic achievement (Zimmerman, 2002; Hattie, 2009). A metacognitively skilled learner notices when they do not understand something, selects strategies to address the gap, and monitors whether the strategy is working. These are learnable skills, but they require that the learner experience the state of not-understanding without immediately having it resolved.

An always-available AI tutor that resolves every moment of confusion may prevent metacognitive skill development by eliminating the productive struggle that develops it. This is the cognitive-offloading risk: students who use AI assistance intensively may become dependent on it not only for content knowledge but for the monitoring and regulation functions that characterise skilled learners.

### 6.2 The academic integrity dimension

Generative AI's capacity to produce examination-quality written work, solved problem sets, and code on demand has destabilised the primary mechanisms by which educational institutions measure individual learning. Traditional essays, take-home assignments, and even some in-class tests can now be completed by AI systems whose outputs automated detection tools cannot reliably distinguish from human writing — Sadasivan et al. (2023) show, both empirically and via an impossibility argument, that as language models approach human text distribution the false-positive/false-negative trade-off facing any detector becomes essentially that of a coin flip, and that paraphrasing or recursive perturbation defeats most existing detectors.

The institutional response is bifurcated: some institutions are prohibiting AI use on assessments; others are redesigning assessments to presuppose AI access and assess higher-order capabilities (synthesis, critique, application to novel problems) that are harder to delegate entirely to AI. The second response is theoretically more robust — it aligns assessment with what students actually need to be able to do in AI-saturated professional environments — but requires substantial curriculum redesign and a rethinking of what educational certification means.

---

## §7 — Equity Dimensions

### 7.1 The access paradox

AI tutoring tools could, in principle, deliver one-on-one instruction quality to students who currently have no access to human tutors — students in under-resourced schools, in rural areas, in low-income households. This would be a radical democratisation of educational quality. The practical reality is more constrained: the best AI tutoring tools require high-quality internet connectivity, modern devices, and sufficient AI literacy to use them effectively. These prerequisites are correlated with the socioeconomic advantages that already predict educational outcomes, which means that AI tutoring tools will reach advantaged students first and most reliably.

The equity trajectory of AI in education therefore depends on deliberate policy intervention: subsidised device and connectivity access, teacher training that is concentrated in under-resourced schools, and localisation of tools into the languages actually spoken by disadvantaged populations. Without these interventions, AI tutoring tools will likely amplify rather than reduce existing educational inequalities in the near term.

### 7.2 The teacher-displacement question

Policy discussions of AI in education sometimes frame the prospect of AI tutors as a teacher-replacement scenario, with economic consequences for the teaching workforce. The framing is largely incorrect for the near-to-medium term. The tasks AI tutors perform well — adaptive explanation of curriculum content, formative feedback on drafts and solutions — are a subset of the teacher's role. The tasks teachers perform that AI does not — noticing that a student is distressed rather than confused, managing classroom dynamics, building the relationships that motivate students who are alienated from academic culture, making curriculum decisions that reflect community values — are not being automated in any currently deployed system.

The more accurate framing is that AI tutors are a force multiplier for teachers: extending their reach to the moments (evening, weekend, independent study) when they cannot be present, and providing data on student misconceptions that informs what the teacher addresses in class time. This is hybrid intelligence in the educational domain — not replacement of the teacher but extension of the teacher's perceptual and instructional reach.

---

## §8 — Open Questions and Cross-Reference Wiring

### 8.1 Gaps for v0.2 expansion

A complete treatment would extend to: the specific evidence base for LLM tutoring systems (RCTs are only beginning to emerge and will be the primary source of credible effect-size estimates by 2026–2027); the implications for higher education specifically, where Chiu (2024) is most directly applicable; AI in professional training and workplace learning; the neuroscience of learning as a basis for evaluating AI pedagogical design; and the assessment-design literature on what higher-order tasks are most resistant to full AI delegation.

### 8.2 Cross-reference wiring

- **Draft H** (human augmentation and co-evolution) — AI-enhanced student learning is one of the earliest-onset and most widely experienced forms of human cognitive augmentation; the long-run co-evolutionary question (does AI assistance change how human cognition develops?) is H's contribution
- **Draft AC** (model vs. human performance) — the tutoring domain offers unusually clean empirical comparisons: Bloom's 2-sigma human-tutor benchmark vs. ITS effect sizes vs. emerging LLM-tutor RCT evidence
- **Draft I** (LLM epistemic limits) — §3.2's hallucination risk in educational contexts and §4.3's calibrated feedback quality are direct instantiations of I's calibration-failure analysis in a high-stakes domain
- **Draft AF** (human labour in AI training) — the data labelling and RLHF labour that shapes LLM tutoring quality includes a significant component of educational-content annotation; the labour conditions of those workers connect to the quality of the instruction students receive
- **Draft W** (unharvested commons and WEIRD bias) — §5.2's language access analysis is W's WEIRD-bias argument applied to the educational domain
- **Draft P** (governance and compliance) — §6.2's academic integrity crisis is a governance challenge that universities, exam boards, and accreditation bodies are actively navigating; the governance lag relative to the technology pace is a case study for P's analysis
- **Draft R** (HI as mirror of human intelligence) — the pedagogical design of AI tutors embeds theories of how humans learn; the choices made (Socratic questioning in Khanmigo, ICAP-aligned feedback) reflect specific theories of mind instantiated in technology
- **Draft AB** (credit, blame, and responsibility) — when an AI tutor produces a confident but incorrect explanation that a student learns and reproduces on an exam, attribution of the error is non-trivial; the responsibility gap in educational AI is largely unaddressed

---

## Key Sources

### Peer-reviewed (verified 2026-05-05; retraction-free per CrossRef)

- Anderson, J. R., Corbett, A. T., Koedinger, K. R., & Pelletier, R. (1995). Cognitive tutors: Lessons learned. *Journal of the Learning Sciences*, 4(2), 167–207. https://doi.org/10.1207/s15327809jls0402_2 [OA cit: 1895] [J]
- Bloom, B. S. (1984). The 2 sigma problem: The search for methods of group instruction as effective as one-to-one tutoring. *Educational Researcher*, 13(6), 4–16. https://doi.org/10.3102/0013189x013006004 [OA cit: 2397] [J]
- Chi, M. T. H., & Wylie, R. (2014). The ICAP framework: Linking cognitive engagement to active learning outcomes. *Educational Psychologist*, 49(4), 219–243. https://doi.org/10.1080/00461520.2014.965823 [OA cit: 2487] [J]
- Chiu, T. K. F. (2024). Future research recommendations for transforming higher education with generative AI. *Computers and Education: Artificial Intelligence*, 6, 100197. https://doi.org/10.1016/j.caeai.2023.100197 [OA cit: 356] [J] — qualitative interview study, 51 students at three research-intensive universities; three themes / 10 subthemes; six future research directions. PDF not obtained (Elsevier paywall on direct PDF endpoint); section 2 in this draft is grounded in the published abstract via OpenAlex `abstract_inverted_index`, retrieved 2026-05-05.
- Kasneci, E., Seßler, K., Küchemann, S., Bannert, M., Dementieva, D., Fischer, F., … Kasneci, G. (2023). ChatGPT for good? On opportunities and challenges of large language models for education. *Learning and Individual Differences*, 103, 102274. https://doi.org/10.1016/j.lindif.2023.102274 [OA cit: 4598] [J]
- VanLehn, K. (2011). The relative effectiveness of human tutoring, intelligent tutoring systems, and other tutoring systems. *Educational Psychologist*, 46(4), 197–221. https://doi.org/10.1080/00461520.2011.611369 [OA cit: 1869] [J] — DOI corrected from earlier draft entry (10.1080/00461520.2011.558 was incomplete/incorrect).
- Wood, D., Bruner, J. S., & Ross, G. (1976). The role of tutoring in problem solving. *Journal of Child Psychology and Psychiatry*, 17(2), 89–100. https://doi.org/10.1111/j.1469-7610.1976.tb00381.x [OA cit: 8181] [J]
- Zimmerman, B. J. (2002). Becoming a self-regulated learner: An overview. *Theory Into Practice*, 41(2), 64–70. https://doi.org/10.1207/s15430421tip4102_2 [OA cit: 6192] [J]

### Preprint

- Sadasivan, V. S., Kumar, A., Balasubramanian, S., Wang, W., & Feizi, S. (2023). Can AI-generated text be reliably detected? arXiv:2303.11156. https://doi.org/10.48550/arXiv.2303.11156 [OA cit: 149] [P] — iCit > 20 threshold met; no peer-reviewed equivalent confirmed, retain as [P].

### Institutional / book

- Hattie, J. (2009). *Visible Learning: A Synthesis of Over 800 Meta-Analyses Relating to Achievement*. Routledge. ISBN 978-0-415-47618-8. [Book — citation count not retrieved via DOI route; high in the field]
- Koedinger, K. R., & Corbett, A. (2006). Cognitive tutors: Technology bringing learning sciences to the classroom. In R. K. Sawyer (Ed.), *The Cambridge Handbook of the Learning Sciences* (pp. 61–78). Cambridge University Press. https://doi.org/10.1017/cbo9780511816833.006 [Book chapter; ISBN 9780521845540 / 9780521607773; verified via CrossRef 2026-05-11]
- Miao, F., & Holmes, W. (2023). *Guidance for generative AI in education and research*. UNESCO Publishing. https://unesdoc.unesco.org/ark:/48223/pf0000386693 [R — UNESCO institutional guidance; English-language identifier pf0000386693_eng]
- Mollick, E., & Mollick, L. (2023). Assigning AI: Seven approaches for students, with prompts. *SSRN Electronic Journal*. https://doi.org/10.2139/ssrn.4475995 [OA cit: 173] [P]

### Pending traceback (not yet cited inline)

- Yan, L., et al. (2023). [AI writing feedback in education — specific study pending traceback]
- Liang, et al. (2023). [AI writing assistant classroom study — specific study pending verification]

### Source-acquisition note

Chiu (2024) PDF could not be obtained on 2026-05-05: the Elsevier `pdfft` endpoint returned an HTML interstitial rather than the PDF. The published abstract retrieved via OpenAlex is sufficient for the §2 characterisation; obtaining the full PDF (e.g. via institutional access or a Sci-Hub mirror per the project's source-acquisition policy) remains a follow-up before any direct quotation from Chiu is included.
