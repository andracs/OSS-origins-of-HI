# Draft AV: Behavioral Surplus as Training Data — How Social Platforms Extract, Repurpose, and Monetize User-Generated Content for AI

**Version:** v0.7 | **Status:** Draft — §6 cooperative-economy source base broadened with three new peer-reviewed `[J]` anchors (Schneider 2018 *Sociological Review*; Bühler et al. 2023 *Digital*; Bunders et al. 2022 *Journal of Co-operative Organization and Management*); v0.6 Zuboff/GDPR/EU AI Act argument chain retained
**Handbook:** Springer Handbook of Hybrid Intelligence
**Related drafts:** F (commons extraction), C (training data memorization), AF (human labor in AI training), W (unharvested commons), N (AI/ML ecosystem), Q (machines using humans), BF (after authorship — downstream consequence of platform-data training in the same community discussion spaces)

---

## Abstract

The largest AI training datasets in existence are not academic corpora or curated open-source releases — they are the accumulated behavioral and content records of billions of users of commercial social platforms. Meta, Google/YouTube, X (formerly Twitter), LinkedIn, TikTok, and Reddit collectively hold text, image, video, audio, behavioral interaction, and social graph data at a scale that dwarfs every open research dataset combined. This chapter examines how these platforms have transitioned from using user data for recommendation and advertising targeting to using it as training substrate for generative AI foundation models — and how this transition represents a qualitatively distinct extraction that existing privacy, copyright, and competition frameworks were not designed to govern. Drawing on Zuboff's surveillance capitalism framework, the legal analysis of ToS-as-consent under GDPR, enforcement actions by the Irish Data Protection Commission and UK ICO, and the emerging regulatory gap in the EU AI Act's treatment of GPAI systems, the chapter argues that social platform data constitutes a second layer of extraction beyond the open-knowledge-commons extraction documented in Draft F: not merely the collective product of volunteer contributors, but the intimate behavioral record of billions of users who were never asked whether their interactions could train AI systems that would subsequently be commercialized or deployed against their interests.

---

## §1 The Scale of the Asset

The quantitative gap between open training datasets and social platform data is not marginal — it is structural. The Pile (EleutherAI, 2020), among the largest openly documented pre-training corpora, contains approximately 825 GB of deduplicated text. Common Crawl, the nonprofit web snapshot that underlies most major LLMs, holds approximately 9.5 petabytes. Against these, consider:

- **Meta** holds the social graph, posts, comments, reactions, messages, photos, and videos of approximately 3.43 billion Family daily active people across Facebook, Instagram, WhatsApp, and Threads (Meta, 2025a — Q1 2025 earnings, March 2025 average). The Instagram photo corpus alone exceeds tens of billions of images. WhatsApp processes more than 100 billion messages per day (Meta Platforms, Inc., 2020 — Q3 2020 earnings call, 29 October 2020, Zuckerberg disclosure).
- **Google/YouTube** hosts a public-video corpus exceeding several hundred million videos, with combined watch time surpassing one billion hours per day (Wojcicki, 2017 — YouTube Official Blog) and new content uploaded at approximately 500 hours per minute as of 2019 (Hale, 2019 — Tubefilter, citing YouTube data). Google Search has processed over 2 trillion queries per year since at least 2016 (Sullivan, 2016 — Search Engine Land, citing Google disclosure), with each query linked to a behavioral trail.
- **X (Twitter)** generated approximately 500 million posts per day at its peak under the Twitter brand (Krikorian, 2013 — Twitter Engineering Blog). The platform's value proposition to AI developers rests largely on its real-time text corpus — the only near-complete record of public human discourse over 15 years.
- **LinkedIn** holds professional profiles, career histories, job applications, professional content, and messaging data for more than 1 billion members (Roslansky, 2023 — LinkedIn News, 2 November 2023; Microsoft FY24 Q1 earnings, October 2023).
- **TikTok** had more than 1 billion monthly active users as of September 2021 (TikTok, 2021 — TikTok Newsroom, "Thanks a billion!"), with subsequent third-party analyst estimates placing the figure above 1.5 billion by 2024 (Statista, 2024 — analyst aggregation, no official disclosure since 2021), and holds video, audio, interaction, and behavioral data in quantities that rival YouTube while being substantially less scrutinized by Western regulators due to its Chinese ownership.
- **Reddit** hosts more than 1 billion posts and 16 billion comments accumulated since 2005, with averages of 1.2 million posts and 7.5 million comments daily as of 2023 (Reddit, Inc., 2024 — S-1 Registration Statement) — a text corpus notable for its depth of technical, scientific, and vernacular knowledge, and one of the few platform datasets for which a public licensing market has emerged.

This data is categorically different from the open-knowledge commons. Wikipedia and arXiv contain knowledge that contributors deliberately made public for knowledge-sharing purposes. Social platform data contains behavioral traces, private communications, medical disclosures, political views, relationship history, and professional information that users shared within an assumed context — with friends, professional networks, or public followers — not with AI training pipelines. The legal concept of **contextual integrity** (Nissenbaum, 2004) holds that information flows appropriately when they match the norms of the context in which information was originally shared; training a commercial AI foundation model on intimate personal disclosures violates contextual integrity even when the data was technically "public."

---

## §2 From Recommendation to Generation: A Qualitative Shift

These platforms have always trained machine learning models on user data. The recommender systems that determine which content each user sees, which advertisements are served, and which connections are suggested have been trained on behavioral data since at least 2010 (Facebook's early EdgeRank algorithm; YouTube's 2016 deep neural network recommender). This use was, in most jurisdictions, largely uncontested: it was understood as core to the platform's value proposition and explicitly anticipated in terms of service.

The transition to **generative AI foundation model training** is qualitatively different in three respects.

**Scale of inference.** Recommendation models predict preferences for content the user already produces; they operate within a closed personalization loop. Foundation models trained on the same data can generate arbitrary text, images, and behavior in any context, including contexts the original data producer never anticipated. A model trained on Reddit discussions can produce legal advice, medical guidance, or political rhetoric — capabilities that were not implicit in the original act of contributing to an online forum.

**Externalization of the model.** Platform recommendation systems remain within the platform's own infrastructure, shaping only what the contributing user sees. A foundation model trained on platform data and deployed externally — as a commercial API, a standalone product, or a third-party integration — takes the extracted value entirely outside the platform relationship. The contributing user receives no ongoing benefit; the trained model can operate indefinitely without further data contribution.

**Competitive displacement.** Models trained on social platform data can replicate the epistemic functions of the platforms themselves. A language model trained on Stack Overflow's corpus can answer programming questions without directing traffic to Stack Overflow; one trained on Reddit can provide community discussion without Reddit's ad revenue. The extractive relationship documented in Draft F (training on GitHub to build Copilot; training on Stack Overflow to reduce Stack Overflow traffic) applies with even greater force to social platform corpora, because social platform value is constituted precisely by text and behavioral data. Draft BF (after authorship) traces the *downstream* mirror of this dynamic: the same platforms whose corpora trained these models now host the AI-generated text outputs, producing a closed loop in which platform discourse becomes both training input and generated output. The AV–BF connection identifies the structural risk: each generation of platform text contains more AI-generated content than the last, the recommender amplifies what the model produces (Draft BF §8.4), and the model's next training cycle is calibrated against a corpus whose human/AI provenance has been progressively obscured — the Shumailov et al. (2024) collapse dynamic instantiated at the platform level.

---

## §3 Platform Practices: What Is Known

### 3.1 Meta

Meta's use of user data for AI training became a matter of public controversy and regulatory action in 2023–2024. The chronology is instructive.

**February 2023:** Meta released the first Llama model as a research artifact (Touvron et al., 2023a). Subsequent Llama generations — Llama 2 in July 2023 (Touvron et al., 2023b) and Llama 3 in July 2024 (Grattafiori et al., 2024) — progressively expanded both model capability and the disclosed training-data envelope, which Meta has consistently described as "publicly available data from the internet." Across the three releases, Meta's technical reports do not enumerate platform-data shares of the training mix in the manner of Brown et al. (2020, Table 2.2) for GPT-3.

**May–June 2024:** Meta began notifying EU and UK users that, effective 26 June 2024, public posts, comments, captions, and Stories from adult Facebook and Instagram users would be used to train Meta's generative AI systems under a "legitimate interests" basis (GDPR Article 6(1)(f)). The advocacy group noyb filed eleven complaints across EU jurisdictions, and the UK Information Commissioner's Office and Irish Data Protection Commission engaged Meta directly.

**14 June 2024:** The Irish Data Protection Commission (DPC), Meta's lead supervisory authority in the EU under GDPR's one-stop-shop mechanism, announced that Meta had agreed to **pause AI training on EU and UK user data** following intensive engagement (Data Protection Commission, 2024). Meta complied, creating a documented two-tier data use policy: EU/UK users' data excluded; non-EU users' data included. This was the most direct regulatory intervention to date in foundation model training on social platform data.

**April 2025:** Meta announced it would resume EU AI training following further engagement with the DPC and the issuance of **EDPB Opinion 28/2024**, adopted under GDPR Article 64(2) on 17 December 2024 (European Data Protection Board, 2024), which set out a three-step framework for assessing whether legitimate interests under Article 6(1)(f) can ground the development and deployment of AI models on personal data — covering the purpose test, the necessity test, and the balancing test (with explicit attention to data subjects' reasonable expectations and the use of web-scraped data). Multiple EU data protection authorities and advocacy groups (including noyb) continued to challenge the basis, arguing that users should have the right to opt in before training commences rather than opt out after.

**2024–2025:** Meta's AI Assistant, powered by Llama models, was integrated directly into WhatsApp, Instagram, Messenger, and Facebook — completing the loop from data extraction to deployment within the same platform ecosystem. The competitive displacement concern is acute: a model trained on WhatsApp conversations deployed as WhatsApp AI creates a recursive dependency in which users' past conversations train the system they interact with today.

Meta's Llama model family explicitly acknowledges in technical documentation that it was trained in part on "publicly available data from the internet" — a phrase that, in Meta's context, plausibly encompasses public Facebook and Instagram posts but is not disaggregated in the Llama technical reports themselves.

### 3.2 X (Twitter / xAI)

Twitter's role as an AI training corpus has a longer history than is commonly recognized. Under its previous ownership, Twitter's "Firehose" API — providing real-time access to all public tweets — was licensed to research institutions and commercial data resellers under agreements that explicitly prohibited use for AI training without additional authorization.

**October 2022:** Elon Musk's acquisition of Twitter (rebranded X in 2023) preceded a rapid transition in data access policy. Within months, the academic research API was closed, the free API was restricted, and API access pricing was raised to levels that effectively excluded academic and nonprofit use.

**July 2023:** xAI, Musk's new AI company, was founded. Grok, xAI's large language model, was announced as having access to real-time X data as a competitive differentiator — the only LLM with live access to the full public conversation stream.

**2023–2024:** X's data licensing program was restructured into a tiered Enterprise API (Perez, 2023 — *TechCrunch*, 29 March 2023; Coalition for Independent Technology Research, 2023, 3 April), with enterprise access ranging from $42,000 to $210,000 per month — i.e., approximately $0.5M to $2.5M per year for bulk firehose access — and AI training data emerging as a product category alongside traditional firehose use cases. The effective result was that a corpus previously available for academic research was privatized, consolidated under a single AI company (xAI, founded July 2023; X formally acquired by xAI in March 2025), and commercialized.

The legal basis for Grok's training on X user data has not been publicly analyzed by a regulatory authority. The US regulatory environment, unlike the EU, does not impose equivalent pre-training transparency requirements.

### 3.3 LinkedIn

LinkedIn's September 2024 handling of AI training consent became a textbook case in regulatory pushback speed.

**18 September 2024:** LinkedIn updated its privacy settings to include a new opt-out toggle for "Data for Generative AI Improvement" — a setting **enabled by default**, meaning all LinkedIn users' content and behavioral data was opted into AI training unless they actively navigated to settings and unchecked it. The opt-out covered LinkedIn's use of profile data, posts, and engagement signals to train generative AI models, including but not limited to Microsoft's broader AI infrastructure.

The rollout was disclosed only in an updated privacy notice and settings page, not through proactive notification. Technology journalists and privacy advocates noticed within hours; the backlash was immediate. **20 September 2024:** the UK Information Commissioner's Office (ICO) issued a public statement that LinkedIn had "suspended such model training pending further engagement with the ICO" — a turnaround of approximately two days from the original rollout to UK suspension (Information Commissioner's Office, 2024).

LinkedIn's parent company Microsoft had strong incentives to use LinkedIn's professional data corpus: it is among the highest-signal professional knowledge datasets in existence, reflecting real career trajectories, professional writing, industry discussions, and organizational structures at a fidelity that no public dataset approaches.

### 3.4 YouTube / Google

YouTube's October 2023 Terms of Service update added explicit language permitting Google to use content uploaded to YouTube "to improve and develop Google products and services, including machine learning technologies and AI." The update did not offer a content-creator opt-out; existing content already uploaded was covered.

For Google, YouTube data represents an asset of unusual multimodal richness: video, audio, speech, captions, transcripts, user comments, engagement metrics, and channel metadata. DeepMind's research has used YouTube video data for training audio and video models (Conformer speech recognition, video language models). Google's Gemini multimodal model series builds on training infrastructure that includes YouTube-derived video-text pairs, though the exact composition has not been disclosed.

The consent architecture is notable: YouTube's Partner Program distributes a share of advertising revenue to creators, but this revenue share is based on views, not on the value of the creator's content as training data. A creator whose technical tutorials are extensively used to train a coding AI model receives no additional compensation beyond whatever advertising revenue their views generate.

### 3.5 TikTok / ByteDance

TikTok occupies a structurally unusual position: it operates under Chinese ownership (ByteDance) while serving predominantly Western users, creating a regulatory asymmetry where the data practices applicable to the majority of users (US, EU, Southeast Asia) are governed by the parent company's data infrastructure and strategic priorities.

ByteDance has disclosed that it uses TikTok user data, including video content, behavioral signals, and interaction data, to train its recommendation models. Less publicly documented is the extent to which this data informs ByteDance's broader AI research, which includes Doubao (ByteDance's LLM), video generation models, and speech synthesis systems that are deployed in the Chinese market.

The Irish DPC imposed a €345 million fine on TikTok in September 2023 for violations of children's data protection under GDPR — the first major enforcement action against the platform in the EU. However, the fine addressed consent mechanisms for minors, not the broader AI training data use question.

The strategic significance of TikTok's data for AI training extends beyond text: its video corpus, especially short-form video with associated audio, engagement patterns, and creator demographics, is among the most comprehensive multimodal behavioral datasets in existence.

### 3.6 Reddit

Reddit presents a contrasting governance model to the unilateral ToS amendments of other platforms: it has moved toward an **explicit licensing market** for its data corpus.

**February 2024:** Reuters reported (and Reddit publicly acknowledged in its S-1 prospectus) that Reddit had signed a data licensing deal with Google valued at approximately $60 million per year, granting Google access to Reddit's content for AI training purposes shortly before Reddit's March 2024 IPO (Reuters, 2024; Reddit, Inc., 2024). Reddit's S-1 disclosed an aggregate $203 million in AI data-licensing revenue under contracts with terms of two to three years. This deal made Reddit one of the first social platforms to commercially acknowledge and price the AI training value of its user-generated corpus.

Reddit's Data API pricing change in June 2023 — which priced out the third-party apps that many users relied on, precipitating a major platform protest — was explicitly motivated in part by the need to capture value from AI companies scraping Reddit data without payment. Reddit CEO Steve Huffman framed the issue in a 2023 *New York Times* interview: "The Reddit corpus of data is really valuable... But we don't need to give all of that value to some of the largest companies in the world for free" (Isaac, 2023).

The Reddit model — licensing rather than unilateral extraction — represents a different point on the consent spectrum, though it still does not distribute proceeds to the individual users whose contributions constitute the asset being licensed.

---

## §4 The Consent Architecture and Its Failures

The legal mechanism through which social platforms claim user consent for AI training is the **Terms of Service agreement** — a contract of adhesion that users must accept to use the platform, presented as a take-it-or-leave-it condition with no meaningful negotiation and, typically, retroactive application to previously contributed content.

Under EU GDPR, consent must be freely given, specific, informed, and unambiguous (Regulation (EU) 2016/679, Articles 4(11) and 7). The **EDPB Guidelines 05/2020 on consent** (European Data Protection Board, 2020 — superseding the Article 29 Working Party's WP259 rev.01) operationalise the four-part definition by requiring that consent be granular (separate for each processing purpose), unbundled from contract acceptance where the processing is not necessary to the contract, and as easy to withdraw as to give. Applied to social platform AI training, this guidance frames ToS-bundled consent for secondary uses — including foundation model training — as presumptively insufficient: AI training is not necessary to the provision of a social network, and bundling it with mandatory ToS acceptance violates the granularity and freely-given requirements. AI training is a secondary commercial use that, on the EDPB's reading of Articles 4(11) and 7, requires a separate consent mechanism or a rigorously demonstrated alternative legal basis.

The Irish DPC's enforcement pause on Meta's EU AI training rested on precisely this analysis: Meta's "legitimate interests" legal basis was contested, and the scale and nature of the secondary use was held to require specific assessment. The DPC's intervention established a precedent — since applied by multiple other EU supervisory authorities — that **foundation model training on platform data is not automatically covered by existing social platform consent structures**.

The opt-out default, illustrated by LinkedIn's August 2023 episode, represents a weaker consent mechanism: users are nominally given a choice, but the choice is buried in settings, enabled by default, and applied to data already contributed. Under GDPR's consent requirements, opt-out defaults for secondary purposes are generally held insufficient; the data protection community has converged on the position that AI training requires opt-in consent or a clearly established legitimate interests basis that survives the balancing test.

In the United States, no equivalent consent framework exists at federal level. The FTC's "Trade Regulation Rule on Commercial Surveillance and Data Security" advance notice of proposed rulemaking (Federal Trade Commission, 2022 — 87 Fed. Reg. 51273, 22 August 2022) identified behavioral data collection and secondary use as concerns and explicitly raised whether the FTC should regulate the use of personal data for algorithmic decision-making and AI training, but rulemaking has not progressed to binding rules.

---

## §5 The Second Extraction

This chapter's central argument connects to the extraction analysis of Draft F: the social platform data situation constitutes a **second layer of extraction** that is structurally analogous to but distinct from the open-commons extraction.

The open-commons extraction (Draft F, Draft C) involves:
- Data that contributors *deliberately made public* for knowledge-sharing
- Platforms (Common Crawl, GitHub, Wikipedia) with no commercial AI interest
- Extraction by third parties (AI labs) outside the platform relationship

The social platform extraction involves:
- Data that users shared *within a platform relationship*, with varying privacy expectations
- Platforms that *are themselves* building or integrating AI systems
- Extraction by the same entity that provides the service — creating a fundamentally different conflict of interest

Zuboff's concept of **behavioral surplus** — first formalised in *Journal of Information Technology* (Zuboff, 2015) and developed at book length in *The Age of Surveillance Capitalism* (Zuboff, 2019) — names the data collected beyond what is needed to provide the service, repurposed as raw material for prediction products. The 2015 article is the peer-reviewed origin: Zuboff there identifies the asymmetry by which platforms accumulate user data declared "ours" in a regime of declarative ownership over which the user has no negotiated claim, and traces the transition from data-as-service-byproduct to data-as-raw-material for "anticipatory" prediction products sold in behavioural futures markets. Social platforms collect behavioral surplus as a matter of business design; AI training is the most recent and most capital-intensive application of that surplus. The value asymmetry is acute: users generate the behavioral surplus through their social activity; the platform captures the surplus and converts it to AI capability; users bear the risks of systems trained on their data (discriminatory targeting, manipulation, behavioral prediction) while receiving no share of the value created.

Zuboff's framework was developed primarily around behavioral targeting for advertising. The transition to AI foundation model training extends the surplus extraction in two ways: (1) it transfers value outside the platform relationship to models deployed in entirely different contexts; (2) it involves a qualitative change in the capability of the derived product — not merely predicting which advertisement a user will click, but training a general-purpose system that can reason, generate, and act across domains. The post-extraction labour chain — annotation workers, RLHF preference-rankers, and content moderators who convert raw behavioural surplus into trainable signal — constitutes a *third* asymmetric relationship in the same value system (analysed in Draft AF). Where Draft AV identifies the users whose data is extracted without compensation, Draft AF identifies the precarious workforce whose labour transforms that data into model capability without share of the value created. The two extractions are structurally analogous and operationally complementary: both rest on the absence of a negotiated relationship between the value-producing party and the value-capturing platform.

---

## §6 Governance Responses and Design Proposals

**Transparency requirements.** The EU AI Act's GPAI provisions require providers of general-purpose AI models to "draw up and make publicly available a sufficiently detailed summary about the content used for training of the general-purpose AI model, according to a template provided by the AI Office" (Regulation (EU) 2024/1689, Article 53(1)(d); see also Article 53(1)(c) on copyright compliance and Annex XI on technical documentation). The obligation applies to all GPAI providers placing models on the EU market irrespective of where training occurred, with limited carve-outs for open-source models that fall outside the systemic-risk threshold (Article 53(2)). Applied to social platform foundation models, this requirement necessitates disclosure of the categories and volumes of user-generated content used in training — disclosure that no major platform has voluntarily provided at the level of specificity Article 53(1)(d) appears to require. The AI Office's training-data summary template, published in 2024 as a draft and finalised in 2025, structures the disclosure into mandatory headline figures and an itemised data-source list; the GPAI Code of Practice (2024), prepared under Article 56, provides additional guidance on signatories' compliance pathways.

**Opt-in rather than opt-out.** The data protection consensus — reflected in the EDPB's guidance on AI training under GDPR (2024) and in DPC enforcement actions — is that AI training on personal data requires opt-in consent or a rigorously applied legitimate interests basis that accounts for the reasonable expectations of the data subject. Platform designs that make opt-in the default would substantially reduce the available training data pool, creating genuine tension between regulatory compliance and foundation model capability.

**Data cooperatives and revenue sharing.** The Reddit licensing model — whatever its limitations — demonstrates that the AI training value of social platform data can be priced and distributed. A more equitable variant would distribute licensing proceeds to individual contributors proportionate to their contribution to the licensed corpus. Proposals for data cooperatives — building on the cooperativist economic-design tradition (Schneider, 2018; Sandoval, 2020) and on data-asset governance scholarship (Birch, Cochrane & Ward, 2021) — would give users collective bargaining power over the terms on which their data is used for AI training, analogous to the collective licensing frameworks that govern music and photography. Bühler et al. (2023) anchor this specifically in *data* cooperatives as a pathway to data sovereignty for digital communities; Bunders et al. (2022) provide empirical feasibility analysis of platform cooperatives in the gig economy, identifying member governance and capitalisation as the binding constraints under which any AI-training data cooperative would have to operate.

**Temporal and contextual consent.** User consent at account creation cannot meaningfully anticipate the AI capabilities that will exist ten years later; content contributed in 2010 could not have been contributed in the context of 2025 foundation model training. A principle of **temporal integrity** — that consent must be renewed for new secondary uses that were not foreseeable at the time of original contribution — would require affirmative user notification and choice before historical data is used for AI training.

**Federated training with differential privacy.** Technical approaches to training on user data without centralizing the data itself — federated learning with differential privacy guarantees — are mature enough to be deployed at scale (McMahan et al., 2017). Google's Gboard keyboard uses federated learning for next-word prediction; the same architecture could in principle be applied to social platform foundation models. The tradeoff is reduced model capability; current frontier models appear to require centralized data at scale that federated approaches cannot replicate.

---

## §7 Open Questions

1. **What is the legal status of model weights trained on GDPR-regulated data?** If Meta's EU user data was used for Llama training without adequate legal basis, what is the remedy — deletion of the trained model, prohibition on its deployment in the EU, financial penalty? The GDPR's "right to erasure" and the technical impossibility of "machine unlearning" at model scale create a genuine legal gap (Zhang et al., 2023/2024; cf. Draft C §6).

2. **Does the Reddit licensing model scale?** If social platforms transition to licensing their user-generated corpora to AI companies, what governance structures ensure that proceeds are distributed to contributors rather than captured entirely by the platform? What is the legal relationship between the platform as licensor and the user as original creator of the licensed content?

3. **How does TikTok's multimodal corpus compare in AI training value to text-dominated platforms?** Short-form video with behavioral engagement signals may constitute the highest-signal multimodal training dataset in existence for human behavior modeling. The strategic AI implications of ByteDance's access to this corpus have not been systematically analyzed.

4. **What is the relationship between platform data and model alignment?** RLHF — the primary alignment technique for current LLMs — is trained on human preference data. The most scalable source of human preference signals at fine granularity is social platform behavioral data (likes, shares, engagement duration, explicit reactions). Are the largest social platforms effectively the unacknowledged alignment infrastructure for frontier AI?

5. **Can users recover agency after behavioral surplus extraction?** Once a model is trained on a user's behavioral history, deleting the user's account does not delete the learned representations. Conceptually, the user's behavioral signature persists in the model indefinitely. What rights, if any, do users have over models trained on their data — and are these rights technologically meaningful or merely nominal?

---

## Key Sources

- Zuboff, S. (2015). Big other: Surveillance capitalism and the prospects of an information civilization. *Journal of Information Technology, 30*(1), 75–89. https://doi.org/10.1057/jit.2015.5 [J] [OA cit: 2844] — peer-reviewed origin of the behavioral surplus concept; the 2019 book extends the argument but the 2015 article is the citable academic anchor. CrossRef retraction check: clean (verified 2026-05-18; `update-to: None`).
- Zuboff, S. (2019). *The age of surveillance capitalism: The fight for a human future at the new frontier of power*. PublicAffairs. [R] [OA cit: 2615] — book; no DOI. OpenAlex W2913707464. Use the 2015 *Journal of Information Technology* article as the [J] anchor where a peer-reviewed source is required; cite the 2019 book for the longer-form treatment, the prediction-products taxonomy, and the surveillance-capitalism framework as a whole.
- Brown, T. B. et al. (2020). Language models are few-shot learners. *NeurIPS 33*. arXiv:2005.14165. [C] [iCit: very high]
- Nissenbaum, H. (2004). Privacy as contextual integrity. *Washington Law Review, 79*(1), 119–158. [J] — Washington Law Review predates DOI assignment for this article; HeinOnline ID 79WashLRev119.
- Data Protection Commission. (2024, June 14). *The DPC's engagement with Meta on AI*. https://www.dataprotection.ie/en/news-media/latest-news/dpcs-engagement-meta-ai [R] — primary regulatory record of the EU AI training pause.
- European Data Protection Board. (2024, December 17). *Opinion 28/2024 on certain data protection aspects related to the processing of personal data in the context of AI models*. Adopted under GDPR Article 64(2). https://www.edpb.europa.eu/system/files/2024-12/edpb_opinion_202428_ai-models_en.pdf [R] — formal anchor for the §3.1 Meta resumption claim; sets out the three-step test (purpose, necessity, balancing) for grounding GenAI training on legitimate interests under Article 6(1)(f).
- European Data Protection Board. (2020, May 4). *Guidelines 05/2020 on consent under Regulation 2016/679* (Version 1.1, adopted 4 May 2020). https://www.edpb.europa.eu/sites/default/files/files/file1/edpb_guidelines_202005_consent_en.pdf [R] — supersedes the Article 29 Working Party's WP259 rev.01; operationalises GDPR Articles 4(11) and 7 and is the §4 anchor for granularity, unbundling, and the freely-given consent requirements applied to social platform AI training.
- Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). *Official Journal of the European Union*, L series, 12 July 2024. http://data.europa.eu/eli/reg/2024/1689/oj [R] — Article 53(1)(d) is the §6 anchor for the GPAI training-data summary obligation; Article 53(1)(c) covers copyright compliance policies; Article 53(2) provides the limited open-source carve-out outside the systemic-risk threshold.
- Information Commissioner's Office. (2024, September 20). *Our statement on changes to LinkedIn AI data policy*. https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2024/09/our-statement-on-changes-to-linkedin-ai-data-policy/ [R] — primary regulatory record of the UK LinkedIn pause.
- Federal Trade Commission. (2022, August 22). *Trade regulation rule on commercial surveillance and data security: Advance notice of proposed rulemaking*. 87 Fed. Reg. 51273. https://www.federalregister.gov/documents/2022/08/22/2022-17752/ [R] — US regulatory baseline.
- Reuters. (2024, February 22). *Reddit in AI content licensing deal with Google*. [R] — first reporting of the $60M/year Reddit-Google deal; corroborated by Reddit's S-1.
- Reddit, Inc. (2024, February 22). *Form S-1 Registration Statement*. SEC EDGAR. https://www.sec.gov/Archives/edgar/data/1713445/000162828024006294/reddits-1q423.htm [R] — primary disclosure of corpus size (1B posts, 16B comments) and $203M aggregate licensing.
- Isaac, M. (2023, April 18). Reddit wants to get paid for helping to teach big A.I. systems. *The New York Times*. [R] — Huffman quote on Reddit corpus value.
- Meta Platforms, Inc. (2025a). *Meta reports first quarter 2025 results*. https://investor.atmeta.com/investor-news/press-release-details/2025/Meta-Reports-First-Quarter-2025-Results/default.aspx [R] — 3.43B Family DAP figure.
- Meta Platforms, Inc. (2020). *Q3 2020 earnings call transcript*, 29 October 2020. https://investor.atmeta.com/ [R] — Mark Zuckerberg disclosure that WhatsApp processes 100B+ messages/day; widely reported (e.g., Newton, 2020, *The Verge*).
- Wojcicki, S. (2017, February 27). *You know what's cool? A billion hours*. YouTube Official Blog. https://blog.youtube/news-and-events/you-know-whats-cool-billion-hours/ [R] — primary source for YouTube ≥1B watch-hours/day.
- Hale, J. (2019, May 7). *More than 500 hours of content are now being uploaded to YouTube every minute*. Tubefilter. https://www.tubefilter.com/2019/05/07/number-hours-video-uploaded-to-youtube-per-minute/ [R] — most-cited industry estimate of YouTube upload rate, citing YouTube data.
- Sullivan, D. (2016, May 24). *Google now handles at least 2 trillion searches per year*. Search Engine Land. https://searchengineland.com/google-now-handles-2-999-trillion-searches-per-year-250247 [R] — Sundar Pichai disclosure at Google Code conference, 2016.
- Krikorian, R. (2013, August 16). *New Tweets per second record, and how!*. Twitter Engineering Blog. https://blog.twitter.com/engineering/en_us/a/2013/new-tweets-per-second-record-and-how [R] — primary source for ~500M tweets/day at peak Twitter brand era.
- Perez, S. (2023, March 29). *Twitter announces new API with only free, basic and enterprise levels*. TechCrunch. https://techcrunch.com/2023/03/29/twitter-announces-new-api-with-only-free-basic-and-enterprise-levels/ [R] — primary reporting of the post-Musk API restructure; reports $42,000/month enterprise floor.
- Coalition for Independent Technology Research. (2023, April 3). *Letter: Twitter's new API plans will devastate public interest research*. https://independenttechresearch.org/letter-twitters-new-api-plans-will-devastate-public-interest-research/ [R] — coalition letter (signed by 100+ researchers) documenting the $42K–$210K/month Enterprise tier range and its effect on academic access.
- Roslansky, R. (2023, November 2). *LinkedIn welcomes 1 billion members*. LinkedIn News. https://www.linkedin.com/pulse/linkedin-welcomes-1-billion-members-ryan-roslansky/ [R] — primary disclosure of 1B-member milestone; corroborated by Microsoft FY24 Q1 earnings (October 2023).
- TikTok. (2021, September 27). *Thanks a billion!*. TikTok Newsroom. https://newsroom.tiktok.com/en-us/1-billion-people-on-tiktok [R] — primary disclosure of 1B MAU. TikTok has not issued an official MAU update since; later figures (≥1.5B) are third-party analyst estimates (e.g., Statista, 2024).
- Touvron, H., Lavril, T., Izacard, G., et al. (2023a). LLaMA: Open and efficient foundation language models. arXiv:2302.13971. [P] [OA cit: 3878] — original Llama release (cit refreshed 2026-05-12; OpenAlex W4322718191).
- Touvron, H., Martin, L., Stone, K., et al. (2023b). Llama 2: Open foundation and fine-tuned chat models. arXiv:2307.09288. [P] [OA cit: 2612] — second Llama release (OpenAlex W4384918448).
- Grattafiori, A., Dubey, A., Jauhri, A., et al. (2024). The Llama 3 herd of models. arXiv:2407.21783. [P] — third Llama release; ~500 author Meta technical report (first author alphabetical convention).
- McMahan, B., Moore, E., Ramage, D., Hampson, S., & Agüera y Arcas, B. (2017). Communication-efficient learning of deep networks from decentralized data. *AISTATS 2017* (PMLR vol. 54, pp. 1273–1282). arXiv:1602.05629. [C] [OA cit: 5604]
- Birch, K., Cochrane, D. T., & Ward, C. (2021). Data as asset? The measurement, governance, and valuation of digital personal data by Big Tech. *Big Data & Society, 8*(1). https://doi.org/10.1177/20539517211017308 [J] [OA cit: 286] [CR cit: 241] — CrossRef retraction check: clean (verified 2026-05-05 and 2026-05-12; `update-to: None`).
- Sandoval, M. (2020). Entrepreneurial activism? Platform cooperativism between subversion and co-optation. *Critical Sociology, 46*(6), 801–817. https://doi.org/10.1177/0896920519870577 [J] [OA cit: 111] — anchor for the platform-cooperativism / data-cooperatives §6 governance proposal. CrossRef retraction check: clean (verified 2026-05-12; `update-to: None`). Online-first 2019-11-13; print volume 2020.
- Schneider, N. (2018). An Internet of ownership: Democratic design for the online economy. *The Sociological Review, 66*(2), 320–340. https://doi.org/10.1177/0038026118758533 [J] [OA cit: 90] [CR cit: 66] — peer-reviewed scholarly statement of the cooperativist economic-design tradition by the co-editor (with Trebor Scholz) of the 2016 *Ours to Hack and to Own* anthology; the [J] anchor for §6's "cooperativist economic-design tradition" framing. CrossRef retraction check: clean (verified 2026-05-19; `update-to: None`).
- Bühler, M. M., Calzada, I., Cane, I., Jelinek, T., Kapoor, A., et al. (2023). Unlocking the power of digital commons: Data cooperatives as a pathway for data sovereign, innovative and equitable digital communities. *Digital, 3*(3), 146–171. https://doi.org/10.3390/digital3030011 [J] [OA cit: 88] [CR cit: 85] — direct peer-reviewed anchor for §6's claim that data cooperatives constitute a pathway to data sovereignty; specifically on *data* cooperatives rather than platform cooperatives more broadly. CrossRef retraction check: clean (verified 2026-05-19; `update-to: None`).
- Bunders, D. J., Arets, M., Frenken, K., & De Moor, T. (2022). The feasibility of platform cooperatives in the gig economy. *Journal of Co-operative Organization and Management, 10*(1), 100167. https://doi.org/10.1016/j.jcom.2022.100167 [J] [OA cit: 91] [CR cit: 69] — empirical feasibility analysis of platform cooperatives; identifies member governance and capitalisation as the binding constraints on cooperative scaling, directly applicable to any AI-training data cooperative proposal. CrossRef retraction check: clean (verified 2026-05-19; `update-to: None`).
- Longpre, S. et al. (2025). Economies of open intelligence. arXiv:2512.03073. [PDF: Kilder/Longpre2025_EconomiesOpenIntelligence.pdf] [P] [iCit: 8]
- Bommasani, R. et al. (2024). The Foundation Model Transparency Index v1.1: May 2024. arXiv:2407.12929. [PDF: Kilder/Bommasani2024_FoundationModelTransparencyIndex.pdf] [P] [OA cit: 7] — corrected (2026-05-06): downgraded from [J] to [P] (preprint, no journal venue confirmed); the prior [iCit: 174] figure is not reproducible in OpenAlex (W4406058595 = 7 cit; the 2023 v1.0 W4387839193 = 41 cit).
- Gray, M. L., & Suri, S. (2019). *Ghost work: How to stop Silicon Valley from building a new global underclass*. Houghton Mifflin Harcourt. [R] — book; ISBN 9781328566249.

---

## Changelog

See `Chapter drafts/changelogs/av-changelog.md` for full iteration history.
