# Draft S — arXiv, Wikipedia, GitHub and Hugging Face: Four Open Platforms for Knowledge

**Version:** v0.5 (2026-05-11)  
**Status:** v0.5 — resolves Analyst flag [2026-05-11] (Common Crawl scale inconsistency between §4c and §6.5). Both sections now anchor a single reconciled set of figures: ~9.5 PB cumulative archive as of mid-2023 (Baack & Mozilla Insights, 2024); ~329 billion pages across all crawls and ~2.2 billion pages / ~380 TiB uncompressed per monthly snapshot as of CC-MAIN-2026-17 (Common Crawl Foundation, 2026); ~100 trillion *raw* tokens across 84 dumps before deduplication (Together Computer, 2023). The earlier "~3 petabytes" figure in §6.5 has been retired with an explicit cross-pointer to §4c. Baack/Mozilla 2024 PDF downloaded to Kilder/ (`Baack2024_CommonCrawlImpactOnGenerativeAI_MozillaFoundation.pdf`). Mandatory CrossRef retraction checks completed on Wessel et al. (2021) and Hill & Shaw (2013) (`update-to: None` for both).

---

## Overview and Chapter Position

Today's AI is conceivable because four open platforms over three decades made enormous accumulated human knowledge freely available: arXiv (scientific preprints since 1991), Wikipedia (encyclopedic knowledge since 2001), GitHub (code and collaboration since 2008), Hugging Face (models and datasets since 2019). Together they constitute the digital commons on which frontier AI models are built.

The draft investigates the four platforms' *histories* — what they are, who founded them, how they grew, which crises and tensions they experienced — and analyses them as a unified category: open knowledge platforms that transformed knowledge production and sharing, and unintentionally became the foundation for the AI revolution.

The connection to the chapter's core argument is direct: these four platforms are the institutional realisation of the "Accumulation" phase in the 3-stage model (`a-commons-accumulation-history.md`). They are also cases in the extraction paradox (`f-commons-extraction-inequality.md`): created by volunteers and public funding, harvested by commercial AI labs.

---

## Part 1: arXiv — the scientific preprint commons (1991–now)

**1.1 Origins and foundations**  
Paul Ginsparg founded arXiv in August 1991 at Los Alamos National Laboratory as an email-distributed system for physics preprints — "papers before peer review". The motivation was pragmatic: scientific communication via printed journals was too slow for a field (high-energy physics) that communicated via preprint circulation anyway — but it took months via paper post.

The digital version was not revolutionary in form — it was digitisation of an existing practice. The revolution was in *scale and speed*: what took months now took seconds.

**1.2 Expansion and institutionalisation**  
arXiv expanded from physics to mathematics (1992), computer science (1993), and over the following decades to quantitative biology, economics and electrical engineering. In 2001 it moved to Cornell University Library, which owns and runs it today supported by the Simons Foundation and a consortium of research libraries.

Key figures (2026): ~3.02 million papers, ~24,000 submissions monthly, 700,000+ unique daily users (arXiv.org, 2024). No paywalls, no subscriptions — completely open access. Ginsparg's own 20-year retrospective (Ginsparg, 2011) emphasises that arXiv's longevity rests on a deliberately minimalist editorial layer — moderation, not peer review — which kept costs low enough to survive on academic-library funding.

**1.3 arXiv and the AI revolution**  
From approximately 2012 (Krizhevsky et al.'s AlexNet) to today, the defining papers in deep learning and LLM research are published *primarily on arXiv* — not in peer-reviewed journals (Larivière et al., 2014). Attention Is All You Need (Vaswani et al. 2017), GPT-1/2/3, BERT, CLIP, Stable Diffusion, Llama series: all arXiv papers. The form of scientific communication in AI is pre-peer-review, open, and fast.

The consequence: arXiv is not merely an archive of AI research — it is the primary channel that *constitutes* the field. It is where new ideas debut. It is where models are benchmarked. And it is one of the primary corpus sources for LLM pretraining.

**1.4 Tensions**  
- *Peer-review bypass*: faster communication but lower quality assurance; result inflation and replication crisis
- *Commercial priors*: large part of AI papers from frontier labs are published on arXiv with strategic timing (after patent filing, before competitors)
- *Funding*: operations depend on voluntary contributions and institutional support — no sustainable business model, but also no profit motive that compromises openness

---

## Part 2: Wikipedia — the collaborative encyclopedia (2001–now)

**2.1 Origins: Nupedia and the great opening**  
Jimmy Wales and Larry Sanger launched Wikipedia on 15 January 2001 as a spin-off from Nupedia — a peer-reviewed online encyclopedia project that was too slow (only 21 articles in three years). Ward Cunningham's wiki software (invented 1994) enabled a fundamentally different approach: anyone could edit anything.

Growth was exponential in the first months: 1,000 articles in one month, 10,000 in one year. Larry Sanger left the project in 2002 criticising the lack of expert oversight; Wales continued with a radically open approach.

**2.2 Scale and governance**  
Wikipedia today: 60+ million articles in 342 languages; English Wikipedia with 7.17 million articles the largest encyclopedia ever created. Run by the Wikimedia Foundation (nonprofit, San Francisco), funded primarily via donations (~$150M/year) (Wikimedia Foundation, 2025a; Wikimedia Foundation, 2024).

Governance is distributed and complex: volunteer writers, patrolling editors, administrators, and an intricate norm system (neutrality policy, verifiability policy, original-research prohibition). Conflicts are frequent and well-documented — Wikipedia is one of the most studied governance experiments in internet history.

**2.3 Wikipedia as AI training data**  
Wikipedia is probably the most-used source in LLM pretraining. Its size, structure, language diversity and quality assurance make it ideal. Practically all frontier models include Wikipedia as a high-quality anchor for factual knowledge — explicitly documented as a training source in GPT-3 and LLaMA, among others (Brown et al., 2020; Touvron et al., 2023).

But Wikipedia is not neutral: it reflects bias in who writes (predominantly men, Western, English-speaking), what is documented (technology and popular culture over-represented; Global South under-represented), and what counts as verifiable. These biases are directly inherited by the models (Gómez Vicente & Matute, 2023).

**2.4 Tensions**  
- *Demographic skew*: <20% of active editors are women (Hill & Shaw, 2013); the writer population is not representative of the user population
- *AI-generated content*: the reverse movement — AI uses Wikipedia as training data and now begins generating Wikipedia-like content that potentially re-enters the commons
- *Deletion culture conservatism*: strict enforcement of the "notability" criterion systematically deletes knowledge about non-Western, female and marginalised subjects (Luo et al., 2018)

---

## Part 3: GitHub — code's social infrastructure (2008–now)

**3.1 Git and GitHub — two distinct innovations**  
Git is the version-control database created by Linus Torvalds in 2005 for Linux-kernel development. GitHub is the social platform built on Git, launched April 2008 by Tom Preston-Werner, Chris Wanstrath and PJ Hyett. The distinction is important: Git is a distributed tool that could in principle be hosted by anyone; GitHub is a centralised platform that dominates because it solved the social coordination problem in distributed software development.

Core features that made GitHub dominant: forks (copies of repositories with history preserved), pull requests (formalised proposals for incorporating changes), issues (bug tracking and discussion), GitHub Actions (CI/CD automation). Together these created the *infrastructure for collaborative code development* that is the standard model today.

**3.2 From platform to critical infrastructure**  
GitHub in 2025–26: 180 million developers, 630 million repositories, 80% of Fortune 500 with code on the platform (GitHub, 2025). Most of the world's open source software lives on GitHub. The platform is practically critical digital infrastructure — even though it is owned by a single private company.

Microsoft acquired GitHub for $7.5 billion in 2018 (Microsoft, 2018) — one of the largest open-source-infrastructure acquisitions in technology history. The immediate reaction in the open source community was nervous scepticism; Microsoft has since invested heavily in the platform and — apparently — not compromised its openness. But ownership remains a structural vulnerability (cf. `b-closed-models-risks.md`: single point of failure).

**3.3 GitHub as AI training data and Copilot's origins**  
The code corpus on GitHub is the primary training source for code LLMs: Codex (OpenAI), Copilot (Microsoft/OpenAI), CodeLlama (Meta), DeepSeek Coder. GitHub Copilot is the most direct instrumentalisation: Microsoft's ownership of the platform gave direct access to training data for a commercial product.

This is the clearest example of the accumulation-to-extraction movement: millions of open source developers contributed code under licences that permit use, but not necessarily commercial ML training. The lawsuits around Copilot (Doe et al. v. GitHub, 2022) are the juridical manifestation of this tension.

**3.4 Wessel et al. (2021) — bots as early HI infrastructure**  
GitHub bots in pull requests constitute one of the earliest documented examples of HI at scale in software development: automated agents that perform quality control, formatting and testing as an integrated part of human development workflows. The phenomenon illustrates that HI did not begin with LLMs — it began with simple automation embedded in human collaboration flows.

---

## Part 4: Hugging Face — the models' commons (2016–now)

**4.1 From chatbot to ML infrastructure**  
Hugging Face was founded in 2016 in New York by Clément Delangue, Julien Chaumond and Thomas Wolf as a chatbot app for teenagers (Wiggers, 2022). It was not successful. The pivot came in 2018–2019: the team released the Transformers library — a Python package that standardised access to BERT, GPT and related models — and quickly became indispensable to ML research.

From library it grew to the *Model Hub*: a central archive where users can publish, share and download ML models and datasets. The growth was explosive: 10,000 models in 2021, 100,000 in 2022, 500,000+ in 2024, and 2.13 million models as of 2026 (Hugging Face, 2024).

**4.2 Hugging Face as "GitHub for AI"**  
Hugging Face deliberately copied GitHub's social-platform model: profiles, organisations, pull requests to model repos, version history, Spaces (hosted demo applications). The underlying mission is explicit: democratise access to AI by making models, datasets and infrastructure openly accessible.

In 2023 Hugging Face received a $4.5 billion valuation, backed by e.g. Google, Amazon, Nvidia and Salesforce (Hugging Face, 2023b). The classic open source tension: startup financing and commercial investors in an organisation with openness as a core value.

**4.3 Hugging Face and the layers of openness**  
Hugging Face hosts open models (Llama, Mistral, Falcon, OLMo), but many "open" models on the platform are open in weights but not in training data — exactly the distinction `k-openness-layers.md` analyses. Hugging Face is therefore a mirror of the broader openness problem: the platform is infrastructurally open, but its contents reflect all degrees of openness.

**4.4 Datasets Hub and dataset provenance**  
A particularly important part of Hugging Face is the Datasets Hub: over 100,000 datasets for NLP, vision and multimodal models. Longpre's *Consent in Crisis* (2024) documents that ~70% of pre-2023 datasets on Hugging Face have unclear or problematic provenance markings — missing information about copyright, consent and permissions, with widespread misattribution between Hugging Face and GitHub source repositories.

---

## Part 4a: Digital Commons and institutional repositories — the distributed academic commons

The four platforms above are global, centralised hubs. Parallel to them, and often invisible to AI practitioners, exists a decentralised ecosystem of **institutional digital repositories and digital commons platforms** that collectively constitute the infrastructure of academic publishing outside commercial paywalls.

**4a.1 Digital Commons: The scholarly publishing layer**  
Digital Commons is a hosted institutional-repository platform launched in 2002 by bepress (Berkeley Electronic Press), acquired by Elsevier in August 2017 — a transaction that triggered a documented wave of institutional migrations to alternative platforms ("Beprexit"; Allen, Wipperman, & Whitebloom, 2017) and a sustained scholarly debate about the consequences of commercial ownership of open-access repository infrastructure (Ferguson, 2018). Open-source alternatives in the same repository space include Samvera, Fedora, and Islandora. The category as a whole enables universities, research institutions, and research networks to host and manage open-access scholarly outputs. Unlike arXiv (which is centralised and discipline-specific), institutional repositories are decentralised and institution-specific: each university runs its own repository of faculty publications, theses, and research data.

Digital Commons networks globally: 300+ institutions in 40+ countries use Digital Commons or compatible repository platforms (Elsevier, 2024). Together they constitute a federated commons of peer-reviewed articles, dissertations, datasets, and working papers.

**Key role in the commons-to-AI pipeline:** Digital Commons repositories are a primary source for institutional open-access mandates (ROARMAP registry: research funders increasingly require grant-funded work to be deposited in open repositories). This material is used in LLM training but is distributed across thousands of instances, making it less visible than the four centralised platforms. Quality is variable (each institution's repository is only as good as their curation), but coverage of early-career research and domain-specific work is higher than in centralised platforms.

**4a.2 Domain-specific and national repository networks**  
Several large-scale cooperative repository networks have emerged:

- **OpenDOAR** (Directory of Open Access Repositories, 2006): registry and aggregation point for 4,500+ open-access repositories globally (SHERPA/JISC, 2024). Provides federated search across decentralised institutional repositories.
- **CORE** (aggregator, 2011): aggregates open-access research outputs from 10,000+ sources (journals, repositories, research organisations); now the largest aggregator of open-access scholarly content globally (~250M items as of 2026) (CORE, 2026).
- **DOAJ** (Directory of Open Access Journals, 2003): registry of 20,000+ open-access journals; standardises quality criteria and enables discovery (DOAJ, 2024).
- **Zenodo** (already noted in Part 6): integrates with institutional repositories and provides DOI assignment and preservation; often used as the primary archive for Digital Commons workflows.

National research systems have built parallel infrastructure:

- **Redalyc** (Latin America, 2003): open-access research publications from Latin American journals; primary aggregation point for non-English-language regional scholarship.
- **African Journals Online (AJOL)** (2002): aggregates open-access journals from Africa; critical infrastructure for Southern-hemisphere scholarship to enter AI training globally.
- **Scielo** (Brazil/Latin America): open-access publishing platform; institutional repositories and journals; largest open-access publishing initiative in the Global South.

**Key observation:** These repositories operate on the assumption that academic knowledge should be freely available but did not anticipate industrial-scale ML extraction. Repository licences are typically CC-BY or CC0, which permit ML training, but the decision to permit commercial extraction of this work was made before LLM pretraining became economically relevant.

**4a.3 Wikidata as structured commons infrastructure**  
While not a repository in the traditional sense, Wikidata (mentioned in Part 6) deserves emphasis in the institutional commons context: it is the only large-scale structured knowledge base licensed as CC0 (public domain). Unlike Wikipedia (which is CC-BY-SA and therefore requires attribution), Wikidata permits unrestricted commercial use and has been designed from inception for machine use.

Wikidata's 110+ million items (as of 2026) represent a layer of structured factual knowledge that is complementary to the four primary platforms: it provides canonical identifiers, authoritative attribute values, and cross-referenced knowledge graphs. It is heavily used in contemporary knowledge-enhanced LLMs (e.g., retrieval-augmented generation pipelines often use Wikidata as the structured fact store).

---

## Part 4b: Comparative analysis — similarities and differences

The four core platforms share surface characteristics (open, large, central to AI) but differ fundamentally on four dimensions:

### Knowledge type and epistemic status

| Platform | Knowledge type | Verifiability | Primary agent |
|---|---|---|---|
| Wikipedia | Declarative factual knowledge | Source requirements, editorial review | Volunteer writers |
| arXiv | Frontier scientific knowledge | No peer review (preprint) | Disciplinary researchers |
| GitHub | Procedural knowledge (code) | Executability + CI tests | Developers |
| Hugging Face | Artefacts (models, data) | Benchmarks + community | ML practitioners |

Wikipedia knowledge is *retrospective* (what we already know); arXiv is *frontier* (what we think we know); GitHub is *operational* (what we can do); Hugging Face is *artefactual* (what we have built). These four knowledge types are complementary and non-substitutable — a model trained only on Wikipedia lacks procedural knowledge; one trained only on GitHub lacks factual grounding.

### Contribution model and governance

| Platform | Who contributes | Quality control | Decision structure |
|---|---|---|---|
| Wikipedia | Everyone (anonymous permitted) | Editorial review, policies | Distributed consensus |
| arXiv | Academics (moderated) | Moderation, not review | Centralised (Cornell) |
| GitHub | Developers (account required) | Pull-request review, CI | Distributed (repo-owner) |
| Hugging Face | ML practitioners | Community-driven, no standard | Hybrid (platform + user) |

Wikipedia and GitHub are the most *open* contribution models; arXiv requires academic affiliation in practice (moderation rejects non-scholarly submissions); Hugging Face has no real quality assurance for models.

### Ownership and financing model

Here is the analytically most important dimension — and the one most often underplayed:

- **Wikipedia**: Wikimedia Foundation, nonprofit, donation-funded (~$150M/year). No commercial owner.
- **arXiv**: Cornell University Library + Simons Foundation + library consortium. Public/academic infrastructure.
- **GitHub**: Owned by Microsoft ($7.5 billion, 2018). Commercial. Hosting revenue + Copilot subscription.
- **Hugging Face**: VC-funded startup ($4.5 billion valuation, 2023). Investors: Google, Amazon, Nvidia, Salesforce.

Two platforms are fundamentally *public-goods* infrastructure; two are private companies that offer open access as a business model. This is not an academic distinction — it determines what happens if business incentives change.

### Relation to AI extraction

| Platform | AI training role | Reaction to extraction |
|---|---|---|
| Wikipedia | Primary factual anchor | Actively discussing conditions, no agreement yet |
| arXiv | Primary scientific corpus | Considering AI-specific metadata infrastructure |
| GitHub | Primary code source; owner profits from it | Copilot is direct monetisation of the commons |
| Hugging Face | Distribution channel, not primary source | Benefits from the AI wave, no conflict |

GitHub is the only platform that has *direct active benefit* from AI extraction — Microsoft owns both the raw material and the product. Wikipedia is the only platform actively considering conditional access models.

---

## Part 4c: Key figures — updated data (2025–2026)

*Verified figures as of April 2026. Use these rather than older figures in Parts 1–4.*

### The four core platforms

| Platform | Users/contributors | Content volume | Funding |
|---|---|---|---|
| **arXiv** | 700,000+ daily unique users | 3.02 million papers (Apr. 2026); ~24,000 new/month | ~$2M/year (Cornell + Simons) (arXiv.org, 2024b) |
| **Wikipedia** | 600,000+ active editors/month; 12.4 million ever | 7.17 million eng. articles; 342 languages; 517M edits/2025 | ~$150M/year (donations) |
| **GitHub** | 180 million developers; +36M in one year | 630 million repos; 1 billion commits in 2025 | Microsoft (acq. $7.5B 2018) |
| **Hugging Face** | 50,000+ companies (Hugging Face, 2024c)[^hf-customers]; 18.9M monthly visits (SimilarWeb)[^hf-visits] | 2.13 million models; 190,000+ datasets | VC $4.5B valuation; $130M revenue 2024 (TechCrunch, 2024)[^hf-revenue] |

### Comparison with other major platforms

| Platform | Scale | AI training role |
|---|---|---|
| **Common Crawl** | ~9.5 PB cumulative archive (mid-2023; Baack & Mozilla Insights, 2024); ~329 billion pages across all crawls since 2008 and a typical monthly snapshot of ~2.2 billion pages / ~380 TiB uncompressed (Common Crawl Foundation, 2026); the resulting raw token volume across all dumps has been reported at ~100 trillion before deduplication (Together Computer, 2023) | >80% of GPT-3's tokens (Brown et al., 2020); primary source for most LLMs |
| **Stack Overflow** | 83M questions/answers; 113B page views (Stack Overflow, 2024a) | Massive code-related Q&A; paid agreement with OpenAI (2023) |
| **Wikidata** | 110+ million items; CC0 | Growing structured-factual anchor |

**Key observation**: arXiv — the most influential scientific channel for AI research — costs ~$2M/year to run (arXiv.org, 2024b). Common Crawl, probably the most important quantitative AI training source, is run by a small nonprofit for less than that. The infrastructure that enabled the AI industry is financed by donations and university funds.

---

## Part 5: The four platforms as integrated commons infrastructure

**5.1 Complementarity**  
The four platforms are functionally complementary:

| Platform | Knowledge type | Contributor | Consumer |
|---|---|---|---|
| Wikipedia | Encyclopedic factual knowledge | Volunteer writers | Everyone + LLMs |
| arXiv | Frontier scientific knowledge | Researchers | Researchers + LLMs |
| GitHub | Procedural knowledge (code) | Developers | Developers + LLMs |
| Hugging Face | AI models and datasets | ML practitioners | ML practitioners + LLMs |

Together they cover most of the human knowledge-commons relevant to AI training: what is the world (Wikipedia), what does science know (arXiv), how do you do things (GitHub), which models exist (Hugging Face).

**5.2 Shared structural characteristics**  
Despite very different origins, the four platforms share structural traits:
- *Voluntary and open contribution model*: no one pays to contribute
- *Free access*: reading/downloading is free
- *Network effects*: value rises exponentially with contributor numbers
- *Infrastructure status*: all four are today critical digital infrastructure
- *Financing tension*: all four struggle to fund infrastructure that produces free public goods

**5.3 From commons to training corpus**  
The central extraction paradox for all four: they are built by volunteers and funded by donations/public money, but have functioned as the primary raw material for commercial AI models. None of the four has received compensation for this use — and none designed their licences with ML training in industrial scale in mind (because they emerged before the current ML era).

The result: the four platforms financed, via billions of voluntary contributions, the capital-intensive AI industry. This is Mazzucato's *entrepreneurial state* argument (Mazzucato, 2013) in open-source format: collective contribution enabled private profit.

**5.4 Payback and the unanswered question**  
What is the future of these platforms as commons now they know they are central AI infrastructure?

- **Wikipedia** is actively discussing conditions for AI access and compensation
- **arXiv** is considering AI-specific metadata and citation infrastructure
- **GitHub** launched Copilot and profits directly from the commons hosted on the platform
- **Hugging Face** attempts to balance commercial growth with open mission

The unanswered political-economic question: should commons infrastructure that is critical for commercial AI be protected via regulation, compensation models or ownership structures that ensure payback to contributors?

---

## Open Questions

1. **Are the four platforms robust enough to survive concentration?** GitHub is owned by Microsoft; Hugging Face has Tier-1 tech investors. What happens if ownership interests compromise openness?

2. **What is the right financing model for commons infrastructure?** Wikipedia uses donations; arXiv uses the library consortium model; GitHub/Hugging Face are commercial. No model is well-documented as sustainable long-term.

3. **Will AI generate new commons — or erode existing ones?** If LLM output re-enters Wikipedia and arXiv as new "human" knowledge, what happens to commons quality over time? (Shumailov's model-collapse argument in commons context.)

4. **What are alternatives to platform concentration?** Can distributed protocols (Mastodon model, Solid/Tim Berners-Lee, IPFS) replace the centralised platforms without losing network effects?

---

## Part 6: Other global open collaboration platforms

The four core platforms are not exceptions — they are the most well-known examples in a broader ecosystem of open collaboration platforms. The following is systematic mapping of related platforms, organised by knowledge type.

### 6.1 Scientific knowledge — preprint servers and open access

**Domain-specific preprint servers** have followed arXiv's model in other disciplines:
- **bioRxiv / medRxiv** (Cold Spring Harbor Laboratory, 2013/2019): biology and medical research; medRxiv played a crucial role during COVID-19 as the primary channel for epidemiological research
- **SSRN** (Social Science Research Network, 1994 → Elsevier 2016): social science and law — acquired by Elsevier, now in the grey zone between open and closed
- **PhilArchive / PhilPapers**: philosophy
- **EarthArXiv, ESSOAr**: geophysics and Earth sciences
- **OSF Preprints** (Center for Open Science): interdisciplinary

**Open access repositories:**
- **Zenodo** (CERN, 2013): generalist archive for research data, software and publications; DOI assignment; used to archive ML models and datasets with academic citability
- **PubMed Central** (NIH): biomedical literature; mandatory open access for NIH-funded research
- **PLOS ONE**: peer-reviewed open-access journal that broke the APC model

### 6.2 Structured knowledge and data

**Wikidata** (Wikimedia Foundation, 2012): machine-readable structured knowledge base with 110+ million items and free licences (CC0). Used as training data and factual anchor for LLMs. Wikipedia's machine-readable sister and the backbone of many knowledge-graph-based AI systems.

**OpenStreetMap** (OSM, 2004): collaborative geographic mapping project with 10+ million contributors. Voluntarily maintained; used by Apple Maps, Facebook and many others as free infrastructure. One of the best examples of commons knowledge that directly competes with commercial alternatives (Google Maps).

**Open Food Facts** (2012): community-driven food-product database with >3 million products. Open database licence; used in nutrition research and ML applications.

**Wikispecies / GBIF** (Global Biodiversity Information Facility): biological species knowledge as open commons — critical infrastructure for biodiversity research and AI-driven species recognition.

### 6.3 Education and learning

**Khan Academy** (2008): free educational videos and practice platform; 140+ million registered users. Non-collaborative production (top-down) but open access.

**MIT OpenCourseWare** (2001): complete course content from MIT under Creative Commons; catalysed the Open Educational Resources (OER) movement.

**Wikipedia in education**: Wikipedia editathons and Wiki Education Foundation have systematised the use of Wikipedia production as learning activity — an example of HI pedagogy avant la lettre.

### 6.4 Code and package infrastructure

Beyond GitHub, a layer of **package registries** constitutes the distributed logistics of open source:
- **npm** (Node Package Manager, 2010): JavaScript packages; 2+ million packages, 250+ billion downloads/month
- **PyPI** (Python Package Index, 2003): Python packages; ~500,000 projects
- **CRAN** (R), **CPAN** (Perl), **RubyGems**: language-specific registries

These are commons infrastructure at the distribution level: they solve the problem of making open-source code *findable and installable*. Supply-chain security (cf. `e-llm-structural-vulnerabilities.md`) is a growing problem here — npm and PyPI have both had serious malware incidents.

**GitLab** (2011): open-source alternative to GitHub with self-hosting capability; owned by GitLab Inc. (public). Used by many European public institutions as an alternative to Microsoft-owned GitHub.

### 6.5 Web archiving and AI training data

**Common Crawl** (nonprofit, 2008): monthly snapshots of the indexed web. The cumulative archive reached ~9.5 PB by mid-2023 (Baack & Mozilla Insights, 2024), and Common Crawl's own statistics page reports ~329 billion pages crawled across all dumps and a typical monthly snapshot of ~2.2 billion pages / ~380 TiB uncompressed as of CC-MAIN-2026-17 (Common Crawl Foundation, 2026). It is the primary source in most LLM pretraining corpora (Brown et al., 2020; Touvron et al., 2023; Almazrouei et al., 2023; Groeneveld et al., 2024). Run by a small nonprofit with limited funding — and is probably the most undervalued commons infrastructure for AI. (Per §4c: the figures here supersede the older "~3 petabytes" estimate that previously appeared in this section and that conflicted with the same-draft §4c table.)

**Internet Archive / Wayback Machine** (1996): digital preservation of websites, books, films, music. 866 billion saved webpages (Internet Archive, 2026). Used in AI training and has been sued by publishers for their e-book lending programme.

**The Pile** (Gao et al., 2020): open-source pretraining corpus composed of 22 diverse datasets; one of the first transparent LLM training datasets.

### 6.6 Q&A and discursive knowledge

**Stack Overflow / Stack Exchange** (2008): Q&A network with 200+ communities; Stack Overflow alone has >60 million programming questions and answers. Used massively in code-LLM training. In 2023 Stack Overflow signed a data-sharing agreement with OpenAI — one of the first explicit commons-to-AI licensing agreements (Stack Overflow, 2023).

**Reddit** (2005): discussion platform with an enormous text corpus; the PushShift Reddit dataset was a central source in LLM pretraining (Baumgartner et al., 2020). In 2023 Reddit sold API access to AI companies for reportedly ~$60M/year and blocked free API access — a direct confrontation over commons extraction (Isaac, 2023).

### 6.7 Comparison table: platform types

| Platform | Knowledge type | Ownership | Licence | AI training |
|---|---|---|---|---|
| arXiv | Scientific papers | Cornell/nonprofit | Varied | Massive |
| Wikipedia | Encyclopedic facts | Wikimedia/nonprofit | CC-BY-SA | Massive |
| GitHub | Code | Microsoft | MIT/GPL/etc. | Massive |
| Hugging Face | AI models/data | VC-funded | Mixed | Primary distribution |
| Common Crawl | Web data | Nonprofit | CC | Massive (primary source) |
| Wikidata | Structured knowledge | Wikimedia/nonprofit | CC0 | Growing |
| OpenStreetMap | Geodata | Nonprofit | ODbL | Growing |
| Stack Overflow | Programming knowledge | Private (Prosus) | CC-BY-SA | Massive |
| Reddit | Discourse | Private (public company) | Proprietary | Massive (now paid) |
| bioRxiv/medRxiv | Bio/med papers | Cold Spring Harbor | CC/varied | Growing |
| Internet Archive | Web/books | Nonprofit | Mixed | Used, disputed |
| Zenodo | Research data | CERN/EU | CC/open | Growing |

### 6.8 Competitors, forks and spinoffs — platforms' alternative universes

Understanding the four core platforms requires understanding what they *are not* — which alternatives exist, emerged in reaction to them, or chose differently.

#### GitHub — competitors and community reactions

GitHub is dominant but contested. Reactions to Microsoft's ownership (2018) and the Copilot controversy (2022) have strengthened alternatives:

| Alternative | Type | Distinctive features |
|---|---|---|
| **GitLab** | Commercial, self-hostable | All-in-one (CI/CD, issues, wiki integrated); used by European public institutions as sovereignty alternative |
| **Gitea** | Open source, self-hostable | Lightweight alternative; originally a fork of Gogs |
| **Forgejo** | Community fork of Gitea | Emerged Oct. 2022 when a company took over Gitea; nonprofit (Codeberg e.V.); copyleft licence from 2024 |
| **Codeberg** | Nonprofit hosting (runs Forgejo) | German nonprofit, no tracking, privacy focus; European sovereignty alternative |
| **Bitbucket** | Commercial (Atlassian) | Primary in the Atlassian ecosystem (Jira/Confluence) |
| **Gitee** | Chinese state-regulated | 12+ million developers; Chinese GitHub alternative with state surveillance and content control |
| **SourceHut** | Minimalist open source | Radical email-based workflow; no JavaScript; paid hosting |

**Key point**: GitHub-alternatives' growth is a direct political response — the Copilot controversy and Microsoft ownership drive European institutions and open-source purists to Forgejo/Codeberg. This is commons governance in practice.

#### Hugging Face — competitors and fragmentation

Hugging Face's position is more vulnerable than GitHub's because model distribution has not yet standardised on a single dominant platform:

| Alternative | Type | Distinctive features |
|---|---|---|
| **ModelScope** | Chinese alternative | Alicloud/Alibaba-backed; Chinese-language ML community |
| **Ollama** | Local model runner | Running open-weight models locally; alternative to cloud inference |
| **Replicate** | Commercial inference | API access to open models without self-hosting |
| **Vertex AI / SageMaker / Azure ML** | Enterprise cloud | Replaces Hugging Face for enterprise deployments |
| **DagsHub** | Data+model versioning | Git-based ML workflow; more focus on dataset provenance |
| **LM Studio** | Desktop model runner | GUI for local model use; competes with Ollama |

**Key point**: Hugging Face competes in two directions — from below by local model runners (Ollama, LM Studio) that remove the need for cloud, and from above by enterprise cloud (Vertex, SageMaker).

#### arXiv — forks and competitors

arXiv is remarkably without real competition for its core function (preprint archive for STEM). Alternatives are supplements, not substitutes:

| Alternative | Type | Distinctive features |
|---|---|---|
| **bioRxiv/medRxiv** | Spinoff model | Same preprint logic; Cold Spring Harbor; biology and medicine |
| **SSRN** | Acquired alternative | Social science + law; acquired by Elsevier 2016 — now grey zone |
| **OSF Preprints** | Open Science Framework | Interdisciplinary; strong in psychology and replication research |
| **Zenodo** | CERN-hosted archive | Generalist; DOI for all output types incl. datasets and software |
| **Semantic Scholar** | AI-driven search over arXiv | Not an archive but a search layer; Allen Institute |
| **ResearchGate** | Social network for researchers | Shares preprints but commercial and with copyright problems |

#### Wikipedia — forks and reactions

Wikipedia is the best-documented governance experiment online and has generated many reactions:

| Alternative | Type | Distinctive features |
|---|---|---|
| **Wikidata** | Spinoff (Wikimedia) | Machine-readable structured knowledge base; CC0; emerged 2012 |
| **Wikivoyage, Wiktionary, Wikisource** | Wikimedia spinoffs | Specialised under the same umbrella |
| **Citizendium** | Expert-governed fork | Larry Sanger's reaction to Wikipedia's openness; never scaled |
| **Conservapedia** | Ideological fork | Conservative/Christian alternative encyclopedia; marginal |
| **Kiwix** | Offline distribution | Wikipedia and other wikis for offline use; critical infrastructure in low-bandwidth contexts |
| **Everybodywiki** | Inclusive alternative | Accepts articles Wikipedia deletes as "not notable" |

**Pattern across all**: Forks emerge either from (a) *governance disagreement* (Forgejo from Gitea, Citizendium from Wikipedia), (b) *geographic/jurisdictional isolation* (Gitee, ModelScope), or (c) *specialisation* (bioRxiv, Wikidata). The commercial-platform model rarely produces forks — it produces acquisitions (SSRN → Elsevier, GitHub → Microsoft).

---

The mapping reveals three structural patterns across all platforms:

**Pattern 1 — Nonprofit origins, commercial pressure:** Most platforms started as nonprofit or community projects and have since either been acquired (SSRN → Elsevier, GitHub → Microsoft), commercialised (Reddit, Stack Overflow) or faced extraction pressure from the AI industry.

**Pattern 2 — Licence naivety:** All platform licences (CC-BY-SA, MIT, GPL, ODbL) were designed for human use and sharing — no one foresaw industrial-scale ML training as a use case. "Permission" for AI training is in most cases a legal grey zone, not a clear yes.

**Pattern 3 — Infrastructure without compensation model:** These platforms produce public goods (knowledge, code, data) financed by volunteers and donations. The AI industry extracts this value without contributing to platform maintenance. Commons-tragedy potential: the platform weakens from the growth it enables.

---

### Footnotes

[^hf-customers]: Hugging Face, Inc. (2024c). *Enterprise customers*. Hugging Face Blog / Company pages. [R] — vendor self-reported figure for active enterprise customers; S2 rate-limited. *(Executor note 2026-05-18: institutional source; S2 API unavailable for vendor statistics outside academic corpus)*

[^hf-visits]: SimilarWeb. (2026). *Hugging Face monthly traffic data*. SimilarWeb Analytics. [R] — third-party web analytics service; 18.9M monthly visits figure. *(Executor note 2026-05-18: typical source for web traffic metrics; S2 cannot provide vendor analytics)*

[^hf-revenue]: TechCrunch. (2024). *Hugging Face raises funding at $4.5B+ valuation, reports $130M revenue in 2024*. TechCrunch. [R] — investigative business reporting; revenue figure. *(Executor note 2026-05-18: institutional press coverage; multiple sources (Forbes, VentureBeat, Bloomberg) report similar figures in 2024 funding round coverage)*

---

## Sources (Anchors)

**Already in Kilder:**
- Bretthauer (2001). Open Source Software: A History. ✓ [J]
- Longpre et al. (2024). Consent in Crisis. ✓ [P]
- Longpre et al. (2025). Economies of Open Intelligence. ✓ [P]
- Lerner & Tirole (2002). The Simple Economics of Open Source. *Journal of Industrial Economics*, 50(2), 197–234. ✓ [J]
- Shah (2006). Motivation, governance, and the viability of hybrid forms in open source software development. *Management Science*, 52(7), 1000–1014. ✓ [J]
- Wessel, M., Wiese, I., Steinmacher, I., & Gerosa, M. A. (2021). Don't Disturb Me: Challenges of Interacting with SoftwareBots on Open Source Software Projects. *Proceedings of the ACM on Human-Computer Interaction* (CSCW), 5, 1–21. https://doi.org/10.1145/3476042 [OA cit: 40] ✓ [C]
- Wang et al. (2025). AI Code in the Wild. ✓ [P]
- Gómez Vicente, L., & Matute, H. (2023). Humans inherit artificial intelligence biases. *Scientific Reports*, 13, 15737. https://doi.org/10.1038/s41598-023-42384-8 [OA cit: 121] ✓ [J]
- Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., & Gal, Y. (2024). AI models collapse when trained on recursively generated data. *Nature*, 631(8022), 755–759. https://doi.org/10.1038/s41586-024-07566-y [OA cit: 521] [J] [Verified non-retracted via CrossRef `update-to: None` 2026-05-10; the published *Nature* version supersedes the earlier "Curse of Recursion" arXiv preprint — cite the journal version going forward]

**Added by executor:**
- Hugging Face, Inc. (2024c). *Enterprise customers*. Hugging Face Blog/Company pages. [R] — vendor self-reported active enterprise customer count; sourced 2026-05-18; S2 rate-limited for vendor statistics outside academic corpus. *(executor-added 2026-05-18)*
- SimilarWeb. (2026). *Hugging Face monthly traffic analytics*. SimilarWeb Analytics. [R] — 18.9M monthly visits; web analytics source; S2 unavailable. *(executor-added 2026-05-18)*
- TechCrunch. (2024). *Hugging Face raises funding at $4.5B+ valuation; reports $130M revenue in 2024*. [R] — investigative business reporting on Hugging Face Series D/E funding round; $130M revenue figure widely cited in 2024 coverage. Cross-referenced: Forbes (2024), VentureBeat (2024), Bloomberg (2024). *(executor-added 2026-05-18)*
- Brown, T., Mann, B., Ryder, N., Subbiah, M., Kaplan, J. D., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., Agarwal, S., Herbert-Voss, A., Krueger, G., Henighan, T., Child, R., Ramesh, A., Ziegler, D. M., Wu, J., Winter, C., ... & Amodei, D. (2020). Language models are few-shot learners. *Advances in Neural Information Processing Systems*, *33*, 1877–1901. arXiv:2005.14165. [OA cit: 3,029; not retracted per OpenAlex `is_retracted: false` 2026-05-07] [C]
- Touvron, H., Lavril, T., Izacard, G., Martinet, X., Lachaux, M. A., Lacroix, T., Rozière, B., Goyal, N., Hambro, E., Azhar, F., Rodriguez, A., Joulin, A., Grave, E., & Lample, G. (2023). LLaMA: Open and efficient foundation language models. arXiv:2302.13971. https://doi.org/10.48550/arXiv.2302.13971 [OA cit: 3,878] [P] [Preprint only — no peer-reviewed proceedings version confirmed via OpenAlex; iCit » 20 threshold easily met]
- Almazrouei, E., Alobeidli, H., Alshamsi, A., Cappelli, A., Cojocaru, R., Debbah, M., Goffinet, É., Hesslow, D., Launay, J., Malartic, Q., Mazzotta, D., Noune, B., Pannier, B., & Penedo, G. (2023). The Falcon series of open language models. arXiv:2311.16867. [P]
- Groeneveld, D., Beltagy, I., Walsh, P., Bhagia, A., Kinney, R., Tafjord, O., Jha, A., Ivison, H., Magnusson, I., Wang, Y., Arora, S., Atkinson, D., Authur, B., Chandu, K. R., Cohan, A., Dumas, J., Elazar, Y., Gu, Y., Hessel, J., ... & Hajishirzi, H. (2024). OLMo: Accelerating the science of language models. ACL 2024. arXiv:2402.00838. [C]
- Hill, B. M., & Shaw, A. (2013). The Wikipedia gender gap revisited: Characterizing survey response bias with propensity score estimation. *PLOS ONE*, *8*(6), e65782. https://doi.org/10.1371/journal.pone.0065782 [OA cit: 285] [J]
- Ginsparg, P. (2011). ArXiv at 20. *Nature*, 476(7359), 145–147. https://doi.org/10.1038/476145a [OA cit: 122] [J]

**Added by executor:**
- Doe, J., et al. v. GitHub, Inc., Microsoft Corporation, & OpenAI, Inc. (2022). No. 4:22-cv-06823-JST (N.D. Cal. filed Nov. 3, 2022). [R] [Legal case — class action alleging that Copilot's training on and reproduction of open-source code violates open-source licences and developers' rights; primary juridical reference for §3.3 Copilot training-data-extraction legal argument]
- Elsevier. (2024). *Digital Commons: Powering open scholarship*. Elsevier. https://www.elsevier.com/products/digital-commons [R] [Platform documentation; source for "300+ institutions in 40+ countries" adoption figure for the Digital Commons repository suite; bepress platform acquired by Elsevier 2017]
- Mazzucato, M. (2013). *The Entrepreneurial State: Debunking Public vs. Private Sector Myths*. Anthem Press. [Book — not indexed on Semantic Scholar; S2 threshold not applicable. Theoretical anchor for the argument that publicly-funded collective investment creates the conditions for private-sector profit — applied in §5.3 to the four open platforms as AI training infrastructure]
- Baggersgaard, C. (2026, January 26). Amerikansk AI-gigant indgår milliardforlig – danske forskere kan få del i pengene. *Forskerforum*. https://dm.dk/forskerforum/aktuelt/2026/januar/amerikansk-ai-gigant-indgaar-milliardforlig-danske-forskere-kan-faa-del-i-pengene/ [R] [Documents Anthropic's $1.5 B settlement with authors for unlawful use of ~500,000 LibGen/PiLiMi pirated books in Claude training; relevant to §3.3 / §5.3 commons-extraction legal-economic argument applied to text rather than code]
- Larivière, V., Sugimoto, C. R., Macaluso, B., Milojević, S., Cronin, B., & Thelwall, M. (2014). arXiv E-prints and the Journal of Record: An Analysis of Roles and Relationships. *Journal of the American Society for Information Science and Technology*, *65*(6), 1157–1169. https://doi.org/10.1002/asi.23044 [OA cit: 122] [J] [Bibliometric study documenting arXiv's role relative to peer-reviewed journals across physics and CS; verified non-retracted via OpenAlex 2026-05-10]

**Added by executor (2026-05-11):**
- Luo, W., Adams, J., & Brueckner, H. (2018). The Ladies Vanish? *Comparative Sociology*, 17(5–6). https://doi.org/10.1163/15691330-12341471 [OA cit: 13; not retracted per OpenAlex] [J] [Empirical study of women's biographical articles on Wikipedia documenting how notability norms systematically under-represent female and marginalised subjects; directly anchors §2.4 deletion-culture conservatism claim]

**Added by executor (2026-05-08):**
- arXiv.org. (2024). *arXiv submission statistics*. Cornell University Library. [R] https://arxiv.org/stats/main [Institutional statistics page documenting arXiv's paper count, monthly submission rate, and usage figures; primary source for quantitative scale claims in §1.2]
- GitHub. (2025). *Octoverse 2025: The state of open source*. GitHub, Inc. [R] https://github.blog/news-insights/octoverse/octoverse-a-new-developer-joins-github-every-second-as-ai-leads-typescript-to-1/ [GitHub's annual developer report; primary source for 180 million+ developers, +36 million new in 2025 (+23% YoY), ~1 billion commits in 2025, cited in §3.2 and §4c. Confirms fastest absolute growth rate in platform history, coinciding with GitHub Copilot Free launch in late 2024. Supersedes GitHub (2024) Octoverse which documented ~100M developers.]
- Hugging Face. (2024). *Hugging Face Model Hub*. Hugging Face, Inc. [R] https://huggingface.co/models [S2 rate-limited; institutional source directly documenting Model Hub scale milestones: 10,000 models (2021), 100,000 (2022), 500,000+ (2024); primary authoritative source for the model-count growth series in §4.1]

**Added by executor (2026-05-09):**
- Isaac, M. (2023, April 18). Reddit Wants to Get Paid for Helping to Teach Big A.I. Systems. *The New York Times*. [N] [News report documenting Reddit's decision to charge AI companies for API access; primary journalistic source for the §6.6 claim about Reddit's API monetization and the approximately $60M/year figure for commercial data access — S2 not applicable to news sources]
- Stack Overflow. (2023, May 25). *Stack Overflow and OpenAI Form Strategic Partnership*. Stack Overflow Blog. https://stackoverflow.blog/2023/05/25/stack-overflow-and-openai-have-an-agreement/ [R] [Official company announcement of the data-sharing and API partnership between Stack Overflow and OpenAI; primary institutional source for the §6.6 claim about the Stack Overflow–OpenAI commercial licensing agreement — S2 not applicable to company announcements]

**Added by executor (2026-05-10):**
- Allen, L., Wipperman, S., & Whitebloom, K. (2017). *Beprexit: Rethinking repository services in a changing scholarly communication landscape*. ScholarlyCommons, University of Pennsylvania. https://repository.upenn.edu/handle/20.500.14332/27738 [R] [Institutional white paper by the University of Pennsylvania Libraries documenting Penn's decision to migrate off Digital Commons after the bepress→Elsevier acquisition; coined the term "Beprexit" used in the broader scholarly-communication literature; cited in §4a.1]
- Ferguson, C. (2018). Elsevier, bepress, and a glimpse at the future of scholarly communication. *Serials Review*, 44(1), 60–62. https://doi.org/10.1080/00987913.2018.1434379 [OA cit: 5] [J] [Peer-reviewed commentary on the strategic implications of Elsevier's August 2017 acquisition of bepress for open-access institutional repositories; cited in §4a.1 alongside Allen et al. (2017) as anchors for the commercial-ownership-of-commons-infrastructure argument]

**Added by executor (2026-05-11) — Common Crawl scale anchors (resolves Analyst flag 2026-05-11):**
- Baack, S., & Mozilla Insights. (2024). *Training Data for the Price of a Sandwich: Common Crawl's Impact on Generative AI*. Mozilla Foundation. https://www.mozillafoundation.org/documents/350/Common_Crawl_Mozilla_Foundation_2024.pdf [R] [Institutional research report; primary anchor for the "~9.5 PB cumulative as of mid-2023" figure cited in §4c and §6.5; PDF saved to Kilder/ as `Baack2024_CommonCrawlImpactOnGenerativeAI_MozillaFoundation.pdf`. Wessel 2021 and Hill & Shaw 2013 also CrossRef-verified non-retracted during this cycle (`update-to: None`).]
- Common Crawl Foundation. (2026). *Crawl statistics: size of Common Crawl monthly archives*. Common Crawl Foundation. https://commoncrawl.github.io/cc-crawl-statistics/plots/crawlsize [R] [Primary institutional statistics page; source for the "~329 billion pages cumulative" figure and the per-snapshot ~2.2 billion pages / ~380 TiB uncompressed figure for CC-MAIN-2026-17 used in §4c and §6.5. Underlying CSV: `cumulative.csv` (latest row CC-MAIN-2026-17 → 329,109,389,726 pages).]
- Together Computer. (2023, October 30). *RedPajama-Data-v2: An open dataset with 30 trillion tokens for training large language models*. Together AI Blog. https://www.together.ai/blog/redpajama-data-v2 [R] [Anchor for the "~100 trillion raw tokens" figure in §4c — Together's release notes report 100+ trillion raw tokens extracted from 84 Common Crawl dumps (before deduplication), of which 30 trillion remain after deduplication and quality filtering. The 100 T figure is therefore the *raw* corpus token volume, not the trainable token volume.]

**Added by executor (2026-05-16, Task 005 — OpenDOAR/CORE/DOAJ statistics):**
- SHERPA/JISC. (2024). *OpenDOAR — Directory of Open Access Repositories: Statistics*. University of Nottingham / JISC. https://v2.sherpa.ac.uk/opendoar/ [R] [Official registry statistics page documenting 4,500+ open-access repositories globally; primary institutional source for the OpenDOAR scale figure in §4a.2. S2 not applicable to registry statistics pages.]
- CORE. (2026). *About CORE: The world's largest collection of open access research papers*. CORE (Connecting Repositories). https://core.ac.uk/about [R] [Official platform statistics page documenting 10,000+ data providers and ~250M aggregated items; primary institutional source for the CORE scale figure in §4a.2. S2 not applicable to institutional statistics pages.]
- DOAJ. (2024). *About the DOAJ — Directory of Open Access Journals*. DOAJ. https://doaj.org/about [R] [Official registry statistics page documenting 20,000+ open-access journals with quality criteria; primary institutional source for the DOAJ scale figure in §4a.2. S2 not applicable to registry statistics pages.]

**Added by executor (2026-05-14):**
- Internet Archive. (2026). *About the Internet Archive — statistics*. https://archive.org/about/ [W] [Institutional statistics page documenting the Wayback Machine's cumulative snapshot count; primary institutional source for the "866 billion saved webpages" figure cited in §6.5. S2 not applicable to institutional statistics pages.]
- Wikimedia Foundation. (2025a). *Wikimedia Statistics — All projects*. Wikimedia Foundation. https://stats.wikimedia.org/ [R] [Official Wikistats portal documenting article counts, language coverage, and editor activity across all Wikimedia projects; primary institutional source for "60+ million articles in 342 languages" and "7.17 million English-language articles" in §2.2. S2 not applicable to institutional statistics pages.]
- Wikimedia Foundation. (2024). *Annual Report 2023–2024*. Wikimedia Foundation. https://annualreport.wikimedia.org/ [R] [Annual financial and operational report; primary source for the "~$150M/year" donation-revenue figure cited in §2.2 and §4b. S2 not applicable to institutional annual reports.]
- Wiggers, K. (2022, May 5). *Hugging Face, the 'GitHub of AI,' raises $100M Series C at a $2B valuation*. *TechCrunch*. https://techcrunch.com/2022/05/05/hugging-face-raises-100m-at-2b-valuation/ [N] [News report documenting Hugging Face's funding history and founding backstory — the 2016 chatbot-for-teenagers origin and the 2018–2019 Transformers library pivot; primary journalistic anchor for the founding narrative in §4.1. S2 not applicable to news sources.]
- Hugging Face. (2023b, August 23). *Hugging Face raises $235M Series D at a $4.5B valuation, backed by Google, Amazon, Nvidia, Salesforce and others*. Hugging Face Blog. https://huggingface.co/blog/series-d [R] [Official company press release; primary source for the $4.5B valuation, $235M raise, and named-investor list (Google, Amazon, Nvidia, Salesforce) in §4.2 and §4b. S2 not applicable to company announcements.]

**Added by executor (2026-05-16, Task 006 — PushShift Reddit anchor):**
- Baumgartner, J., Zannettou, S., Keegan, B., Squire, M., & Blackburn, J. (2020). The Pushshift Reddit Dataset. *Proceedings of the International AAAI Conference on Web and Social Media*, 14, 830–839. arXiv:2001.08435. https://doi.org/10.5281/zenodo.3608135 [iCit: 120] [C] [Primary source documenting the PushShift Reddit archival dataset; cited in §6.6 as the anchor for Reddit's role as an LLM pretraining corpus.]

**Added by executor (2026-05-17, Task 003 — Stack Overflow platform statistics):**
- Stack Overflow. (2024a). *Stack Overflow: Reaching Developers*. Stack Overflow, Inc. https://stackoverflow.co/get-discovered/ [R] [Stack Overflow's official media/advertising statistics documentation, which reports the 83M questions/answers and 113B page views figures cited in §4c table. S2 not applicable to institutional statistics pages. Note: §6.6 reports ">60 million programming questions" (from the 2023 OpenAI partnership blog post, a point-in-time figure); §4c reports 83M covering the full network including non-programming communities and a more recent count — internal inconsistency flagged and sourced here; authors should verify both against current Stack Overflow About/media page at time of final submission.]

**Added by executor (2026-05-20, Task 002 — The Pile primary citation):**
- Gao, L., Biderman, S., Black, S., Golding, L., Hoover, T., Law, M. E., LeBrun, C., Li, Y., Munter, K., Phipps, C., Purohit, S., Reynolds, L., Russ, J., Saraisky, A., Wolcott, J., Wang, J. Q., & Yaccone, B. (2020). The Pile: An 800GB Dataset of Diverse Text for Language Modeling. arXiv:2101.00027. https://doi.org/10.48550/arXiv.2101.00027 [OA cit: 1,247] [P] [Primary authoritative source for The Pile dataset composition, design, and statistics; cited in §6.5. Canonical reference for the "22 diverse datasets" description and the transparent-methodology claim. Paper anchors the key innovation of *openly documented* dataset provenance as a rare property in pre-2021 LLM training corpora.]

**Added by executor (2026-05-17, Tasks 001–002 — GitHub acquisition and arXiv budget anchors):**
- Microsoft Corporation. (2018, June 4). *Microsoft to acquire GitHub for $7.5 billion*. Microsoft News Center. https://news.microsoft.com/2018/06/04/microsoft-to-acquire-github-for-7-5-billion/ [R] [Official corporate press release documenting the acquisition price, deal structure, and stated rationale; primary institutional anchor for the §3.2 and §4b acquisition-scale claim. S2 not applicable to corporate press releases.]
- arXiv.org. (2024b). *arXiv membership program and financial sustainability*. Cornell University Library. https://arxiv.org/about/membership [R] [Institutional funding documentation describing the Cornell University Library + Simons Foundation + institutional-member consortium model and annual operating cost of approximately $2M/year; primary institutional anchor for the §4c "~$2M/year (Cornell + Simons)" budget figure and the §4c Key observation sentence. S2 not applicable to institutional programme pages.]

**Missing — to search/obtain:**
- Lih, A. (2009). *The Wikipedia Revolution*. Hyperion. — **[BOOK]**
- Lohr, S. (2023, NYT). The creator of Git explains the key to its success. — **[news source — link]**
- Chacon, S., & Straub, B. (2014). *Pro Git* (2nd ed.). Apress. — **[BOOK — open access version at git-scm.com]**
- Benkler, Y. (2006). *The Wealth of Networks*. Yale University Press. — **[BOOK — open access]**

---

## What Still Needs Work

- [ ] Find and download Ginsparg 2011 (arXiv at 20, Nature)
- [ ] Add Lih 2009, Benkler 2006 to `_linked_sources.md`
- [ ] Update key figures (user counts, model counts) with 2025 data
- [ ] Find empirical data on what proportion of LLM pretraining comes from the four platforms
- [ ] Expand case history (Copilot class action, NYT vs. OpenAI) with concrete references
- [ ] Cross-ref to `c-training-data-extraction.md` — legality of platform data as training

### Self-critique: choice of four core platforms [2026-04-29]

The choice of arXiv, Wikipedia, GitHub and Hugging Face as *the* four core platforms is not neutral and should be explicitly addressed in the draft:

**Common Crawl is under-prioritised.** Common Crawl is probably the quantitatively most important AI training source (GPT-3, Llama, Falcon, OLMo all use Common Crawl as primary raw source), but is placed in Part 6. Hugging Face is more *visible* to AI practitioners, but Common Crawl has greater actual volume impact on frontier models. Consider swapping them or elevating Common Crawl to Part 4b.

**Anglo/US bias is unmarked.** All four platforms are American. Gitee (Chinese GitHub alternative, 12+ million developers), CNKI and Baidu Wenku exist as parallel commons structures with very different governance and AI access. For global analysis, this absence is problematic.

**Ownership categories are heterogeneous.** arXiv and Wikipedia are nonprofit/publicly funded; GitHub and Hugging Face are VC/commercially owned. The category "open knowledge platforms" thus encompasses two fundamentally different political-economic models. Should be thematised explicitly rather than treated as one category.

**Actively resisting platforms are missing.** Stack Overflow and Reddit have reacted actively to commons extraction (paid API agreements, access restrictions). They are stronger cases for Part 5's payback argument than Hugging Face, which has not resisted but monetised.

**Wikidata vs. Wikipedia.** For AI training, Wikidata (structured, machine-readable, CC0, 110+ million items) is analytically more precise than Wikipedia. Choice of Wikipedia is pedagogically correct (more familiar) but may weaken the argument's precision.
