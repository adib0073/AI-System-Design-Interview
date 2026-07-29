# Interview Prep Resources — Chapter 1

A curated, role-aware reading/watching list for AI system design interviews: official company engineering & AI blogs, official YouTube channels, and company careers/interview-prep pages.

> **How to use this list**
> - Start with the **official company resources** for your target employer — especially Meta, which shares real prep materials with candidates.
> - Follow 3–5 **engineering blogs** relevant to your target domain (recsys, search, ads, infra) rather than trying to read them all.
> - Use the **role-specific picks** at the bottom to focus.
>
> **Link maintenance:** URLs drift over time. These are checked periodically; if one is dead, please open an issue/PR. Prefer searching the site name if a deep link 404s.

---

## 1. Official company careers & interview-prep pages

| Company | Resource | URL |
|---------|----------|-----|
| Meta | Candidate prep hub (interview overview; ML/system design prep, mock recordings shared via the candidate portal after scheduling) | https://www.metacareers.com/jobs & https://www.metacareers.com/life/preparing-for-your-software-engineering-interview-at-meta |
| Google | Google Careers "How we hire" + interview prep | https://careers.google.com/how-we-hire/ |
| Google | Tech Dev Guide (study resources) | https://techdevguide.withgoogle.com/ |
| Amazon | Amazon Jobs interview prep | https://www.amazon.jobs/content/en/how-we-hire/interviewing-at-amazon |
| Amazon | Leadership Principles (woven into design + behavioral) | https://www.amazon.jobs/content/en/our-workplace/leadership-principles |
| Microsoft | Microsoft Careers interview tips | https://careers.microsoft.com/ |
| Apple | Apple Jobs | https://www.apple.com/careers/ |
| Netflix | Netflix Jobs | https://jobs.netflix.com/ |

> **Tip:** Ask your recruiter explicitly which loop you're in (general vs. ML/AI system design) and whether official prep material exists — several companies provide it but don't advertise it.

---

## 2. Official engineering blogs (systems + ML in production)

| Company | Blog | URL |
|---------|------|-----|
| Meta | Engineering at Meta | https://engineering.fb.com/ |
| Google | Google Research Blog | https://research.google/blog/ |
| Netflix | Netflix TechBlog | https://netflixtechblog.com/ |
| Uber | Uber Engineering | https://www.uber.com/blog/engineering/ |
| Airbnb | Airbnb Tech Blog | https://medium.com/airbnb-engineering |
| LinkedIn | LinkedIn Engineering | https://engineering.linkedin.com/blog |
| Pinterest | Pinterest Engineering | https://medium.com/pinterest-engineering |
| Spotify | Spotify Engineering | https://engineering.atspotify.com/ |
| Instagram | Instagram Engineering | https://instagram-engineering.com/ |
| Stripe | Stripe Blog (payments/fraud/scale) | https://stripe.com/blog/engineering |
| DoorDash | DoorDash Engineering | https://careersatdoordash.com/engineering-blog/ |
| Amazon | AWS Machine Learning Blog | https://aws.amazon.com/blogs/machine-learning/ |
| Microsoft | Microsoft Developer Blogs | https://devblogs.microsoft.com/ |

---

## 3. Official AI / research blogs (models, LLMs, applied research)

| Org | Blog | URL |
|-----|------|-----|
| Meta | AI at Meta | https://ai.meta.com/blog/ |
| Google DeepMind | DeepMind Blog | https://deepmind.google/discover/blog/ |
| Amazon | Amazon Science | https://www.amazon.science/ |
| Apple | Apple Machine Learning Research | https://machinelearning.apple.com/ |
| Microsoft | Microsoft Research Blog | https://www.microsoft.com/en-us/research/blog/ |
| OpenAI | OpenAI Research/News | https://openai.com/news/ |
| Anthropic | Anthropic Research/News | https://www.anthropic.com/research |
| NVIDIA | NVIDIA Technical Blog | https://developer.nvidia.com/blog/ |

---

## 4. Official YouTube channels

| Channel | Focus | URL |
|---------|-------|-----|
| Google for Developers | Talks, ML, infra | https://www.youtube.com/@GoogleDevelopers |
| Google Cloud Tech | Cloud + ML architecture | https://www.youtube.com/@googlecloudtech |
| Google DeepMind | Research talks | https://www.youtube.com/@Google_DeepMind |
| AI at Meta | Meta AI research/eng | https://www.youtube.com/@AIatMeta |
| Amazon Web Services | Architecture, ML, re:Invent | https://www.youtube.com/@amazonwebservices |
| Microsoft Developer | Azure AI, dev talks | https://www.youtube.com/@MicrosoftDeveloper |
| Microsoft Research | Research talks | https://www.youtube.com/@MicrosoftResearch |
| NVIDIA Developer | GPU/inference/training | https://www.youtube.com/@NVIDIADeveloper |
| OpenAI | Product/research updates | https://www.youtube.com/@OpenAI |

---

## 5. High-quality third-party prep (clearly not official)

Useful for structure and mock practice, but treat as supplements — verify claims against primary sources.

| Resource | What it's good for | URL |
|----------|--------------------|-----|
| ByteByteGo (Alex Xu) — blog & YouTube | System design fundamentals, diagrams | https://bytebytego.com/ · https://www.youtube.com/@ByteByteGo |
| Evidently AI blog | ML monitoring, drift, evaluation | https://www.evidentlyai.com/blog |
| MLOps Community | Production ML practices, talks | https://mlops.community/ |
| Chip Huyen — writing / "Designing ML Systems" | End-to-end ML system design | https://huyenchip.com/blog/ |
| Eugene Yan | Applied ML system design essays | https://eugeneyan.com/writing/ |
| Exponent | Company-specific interview guides | https://www.tryexponent.com/ |

---

## 6. Foundational papers worth skimming (evergreen)

These recur in recsys/search/ads design discussions and are safe to cite by name in an interview.

- **Deep Neural Networks for YouTube Recommendations** (Covington et al., Google, 2016)
- **Wide & Deep Learning for Recommender Systems** (Cheng et al., Google, 2016)
- **Deep Learning Recommendation Model (DLRM)** (Naumov et al., Meta, 2019)
- **The Dynamo paper** (Amazon, 2007) — availability & eventual consistency
- **In Search of an Understandable Consensus Algorithm (Raft)** (Ongaro & Ousterhout, 2014)
- **Hidden Technical Debt in Machine Learning Systems** (Sculley et al., Google, 2015)

---

## 7. Role-specific starting picks

**ML / AI Engineer**
- Engineering at Meta + AI at Meta (recsys/ranking in production)
- Chip Huyen "Designing ML Systems"; Evidently AI (monitoring/drift)
- Uber / DoorDash / Airbnb engineering (feature stores, real-time ML)

**AI / ML Architect**
- Google Research + Google Cloud Tech (reference architectures)
- Netflix TechBlog, LinkedIn Engineering (multi-system ML platforms)
- Amazon Science (breadth across ML domains)

**Applied Scientist**
- DeepMind, Microsoft Research, Amazon Science, Apple ML Research (methodology, evaluation)
- Foundational papers in §6

**Engineering Manager (technical bar)**
- Amazon Leadership Principles page + Amazon Jobs prep
- Meta candidate prep hub; ByteByteGo for shared vocabulary with your team

**Data Engineer (ML-adjacent)**
- Uber, Airbnb, LinkedIn engineering (pipelines, feature/data platforms)
- AWS ML blog (data + feature infrastructure)

---

*Suggest an addition by opening a PR against this file.*
