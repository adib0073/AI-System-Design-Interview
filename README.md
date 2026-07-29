# Cracking the AI System Design Interview

### A Comprehensive Guide for Engineering Managers, AI Engineers & AI Architects

Companion repository for the book **_Cracking the AI System Design Interview_** (in development with Manning). This repo holds the **living supplementary material** — practice banks, estimation drills, cheat sheets, decision guides, glossaries, and curated blog/paper indexes — that accompany the chapters.

> **Why a companion repo?** AI system design moves fast. Model families, serving frameworks, prices, and even regulations change month to month. Keeping the fast-moving material here (instead of only in print) lets it stay current, correct, and improvable via issues and pull requests. The book teaches the durable concepts; this repo keeps the specifics fresh.

---

## Who this is for

- **AI / ML engineers** preparing for AI system design rounds
- **Engineering managers & tech leads** who need breadth across the AI stack
- **AI architects & senior/staff engineers** who must reason about trade-offs, scale, cost, and governance
- Anyone moving from traditional software system design into **AI/ML, LLM, RAG, and agentic** system design

The material is **role- and level-aware**: most chapters flag what depth is expected for different roles and seniority levels.

---

## How the book is organized

The book is structured in three parts, plus appendices.

### Part 1 — Foundations & Interview Framework
1. The AI System Design Interview Landscape
2. A Framework for Acing the Interview (the phase-by-phase interview template)
3. Core Distributed Systems Concepts
4. Core AI/ML System Design Concepts
5. Back-of-the-Envelope Estimation for AI Systems

### Part 2 — Modern AI System Building Blocks
6. Foundation Model Systems: LLMs, RAG, and Multimodal AI
7. Agentic AI Systems
8. AI at Scale: Infrastructure, MLOps, and Responsible AI

### Part 3 — Practical AI System Design Case Studies
9. Recommendation & Feed Ranking · 
10. Ads Ranking & Computational Advertising · 
11. Harmful-Content Detection / Trust & Safety · 
12. Fraud & Anomaly Detection · 
13. Agentic Customer Support · 
14. Computer Vision · 
15. Forecasting & Prediction · 
16. Notifications & Delivery Optimization · 
17. Code Review & Code-Quality Agent · 
18. Deep Research & Planning Agent

### Appendices
- Diagram templates
- quick-reference cards
- role-based interview checklists
- estimation reference tables
- prep cheatsheet template
- 30-day study plan.

---

## What's in this repository

Supplementary content is under [`chapters/`](./chapters/), with **one folder per book chapter** for Parts 1 and 2 (chapters 1–8). Each folder has its own `README.md` index.

| Folder | Book chapter | Highlights |
|---|---|---|
| [`chapter 1`](./chapters/chapter%201/) | 1 · The AI System Design Interview Landscape | Common interviewee doubts · interview-prep resource list · role→depth self-assessment · key-terms glossary |
| [`chapter 2`](./chapters/chapter%202/) | 2 · A Framework for Acing the Interview | Phase-by-phase time-box cheat sheet · self-scoring scorecard · signposting & recovery scripts · common-pitfalls checklist · doubts · glossary |
| [`chapter 3`](./chapters/chapter%203/) | 3 · Core Distributed Systems Concepts | 10 verified estimation drills (QPS/storage/bandwidth/cache) · engineering-blog index · key-terms · common doubts |
| [`chapter 4`](./chapters/chapter%204/) | 4 · Core AI/ML System Design Concepts | "Does this need ML?" practice bank · model-selection & feature-store decision trees (incl. GenAI/agentic) · blog index · key-terms |
| [`chapter 5`](./chapters/chapter%205/) | 5 · Back-of-the-Envelope Estimation | **29-problem drill bank** · **interactive calculators notebook** · reference-numbers quick card · consolidated references · key-terms |
| [`chapter 6`](./chapters/chapter%206/) | 6 · Foundation Model Systems: LLMs, RAG & Multimodal | Prompt vs. fine-tune vs. RAG matrix · model/serving landscape (living) · blog/paper index · key-terms |
| [`chapter 7`](./chapters/chapter%207/) | 7 · Agentic AI Systems | Agent-pattern selection guide · safety/governance checklist · MCP & A2A references (living) · key-terms · common doubts |
| [`chapter 8`](./chapters/chapter%208/) | 8 · AI at Scale: Infrastructure, MLOps & Responsible AI | Infra estimation drills (bridges Ch. 5) · ML-platform reference architectures · responsible-AI checklist · emerging-trends (living) · blog/paper index · key-terms |

> **Note on coverage:** folders `chapter 1`–`chapter 8` map one-to-one to the book's Part 1 (Foundations) and Part 2 (Modern AI System Building Blocks) chapters. Supplements for the Part 3 case-study chapters (9–18) will be added over time.

### Content types you'll find
- **Estimation drills** — worked, numerically-verified back-of-the-envelope problems (traffic, storage, GPU memory, KV cache, training cost, cluster sizing).
- **Interactive calculators** — a pure-Python [notebook](./chapters/chapter%205/estimation-calculators.ipynb) for GPU memory, KV cache, embedding storage, and training cost.
- **Cheat sheets & decision guides** — printable one-pagers and decision trees for fast, defensible interview answers.
- **Checklists & worksheets** — self-scoring rubrics, safety/governance and responsible-AI checklists.
- **Glossaries (key-terms slices)** — per-chapter, feeding a cumulative book glossary.
- **Blog & paper indexes** — curated, role-specific reading, with links marked *living* where they churn fast.

---

## How to use this repo

1. **Preparing for a round?** Start with your target chapter's `README.md`, then work the estimation drills and practice banks out loud.
2. **Short on time?** Print the cheat sheets and quick-reference cards (Ch. 2 time-box, Ch. 5 reference card, Ch. 6 prompt/fine-tune/RAG matrix, Ch. 7 pattern-selection).
3. **Building intuition?** Use the interactive calculators and the decision trees while reading the corresponding chapter.
4. **Going deep?** Follow the blog/paper indexes for each chapter, guided by the role-specific starting picks.

**Living documents** (model/serving landscape, MCP/A2A references, emerging trends) are intentionally kept current and flagged as such — verify specifics before quoting them in an interview.

---

## About the book & editorial process

The manuscript is being developed with **Manning Publications** and follows Manning's standard editorial workflow, including the **Manuscript Quality Review (MQR)** — a structured review of scope, pedagogy, and technical accuracy that shapes the book's content and organization. The supplementary material in this repo is designed to complement the reviewed manuscript, not replace it.

The full detailed table of contents lives in the manuscript file `TOC_bhattacharya.docx`.

---

## Author

**Aditya Bhattacharya** — AI researcher, engineer, and author.

- LinkedIn: **[linkedin.com/in/adi-phd](https://www.linkedin.com/in/adi-phd/)** — the best place for **references, questions, feedback, or citation requests** related to this book and repository.

If this material helps your preparation, connecting and sharing feedback on LinkedIn is very welcome.

---

## Contributing

Corrections and improvements are welcome — especially **dead links** and **out-of-date "living" pages**.

- Open an **issue** for errors, broken links, or suggestions.
- Open a **pull request** with fixes or additional worked examples (please keep estimation math verified and cite sources).

---

## Citation

If you reference this material, please cite:

```
Aditya Bhattacharya, "Cracking the AI System Design Interview:
A Comprehensive Guide for Engineering Managers, AI Engineers & AI Architects,"
Manning Publications (in development).
Companion repository: https://github.com/adib0073/AI-System-Design-Interview
```

For citation or reference questions, reach out via [LinkedIn](https://www.linkedin.com/in/adi-phd/).

---

## License

See [`LICENSE`](./LICENSE). Book text and figures remain © the author and Manning Publications; the supplementary code and materials in this repository are provided for learning and interview preparation.
