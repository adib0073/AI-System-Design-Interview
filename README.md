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

Supplementary content is under [`chapters/`](./chapters/), with **one folder per book chapter** (chapters 1–18). Each folder has its own `README.md` index. There is also a bank of **[timed mock system design problems](./mock_ai_system_design_problems/)** (see below).

### Part 1 & 2 — Foundations and building blocks (chapters 1–8)

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

### Part 3 — Case-study chapters (chapters 9–18)

Each case-study folder carries a consistent set: a `README.md` index, a **`key-terms.md`** glossary slice (scanned from the chapter), a **`common-doubts.md`** FAQ, and an **`engineering-blogs.md`** curated real-world reading list.

| Folder | Book chapter | Signature focus |
|---|---|---|
| [`chapter 9`](./chapters/chapter%209/) | 9 · Recommendation & Feed Ranking | Multi-stage funnel · two-tower + ANN · multi-task ranking · cold start/diversity |
| [`chapter 10`](./chapters/chapter%2010/) | 10 · Ads Ranking & Computational Advertising | Auctions (GSP/VCG) · eCPM · pCTR/pCVR **calibration** · pacing · privacy |
| [`chapter 11`](./chapters/chapter%2011/) | 11 · Harmful-Content Detection / Trust & Safety | Asymmetric costs · hash matching · severity × confidence · **prevalence** |
| [`chapter 12`](./chapters/chapter%2012/) | 12 · Fraud & Anomaly Detection | Imbalance/PR-AUC · velocity & graph features · rules+ML · **step-up auth** · delayed labels |
| [`chapter 13`](./chapters/chapter%2013/) | 13 · Agentic Customer Support | LLM agent · RAG over policies · **read/write split** · approval gates · deflection/CSAT |
| [`chapter 14`](./chapters/chapter%2014/) | 14 · Computer Vision | **Visual search (embeddings + ANN)** · ViT/YOLO/CLIP/SAM · OCR · on-device/edge |
| [`chapter 15`](./chapters/chapter%2015/) | 15 · Forecasting & Prediction | **No leakage · rolling-origin backtesting** · global vs. local · probabilistic · WAPE/MASE |
| [`chapter 16`](./chapters/chapter%2016/) | 16 · Notifications & Delivery Optimization | **Value − annoyance** · volume optimization · long-term holdouts · GenAI/agentic |
| [`chapter 17`](./chapters/chapter%2017/) | 17 · Code Review & Code-Quality Agent | **Precision > recall / trust** · ground + verify (sandbox) + gate · untrusted code |
| [`chapter 18`](./chapters/chapter%2018/) | 18 · Deep Research & Planning Agent | **Orchestrator + sub-agents** · transactions (saga/idempotency) · approval gates · durable state |

### Mock system design problems (timed practice)

The [`mock_ai_system_design_problems/`](./mock_ai_system_design_problems/) folder holds **15 self-contained, timed (35–40 min) mock interviews** — each with the prompt, a minute-by-minute game plan, a full CHASE walkthrough, frequently asked follow-ups, tips/do's-and-don'ts, and a 60-second close. They span classic ML, LLM/RAG, multimodal, and agentic archetypes (churn, NotebookLM, Glean, Google Lens, Amazon Rufus, autonomous SWE agents, and more).

> **Note on coverage:** folders `chapter 1`–`chapter 18` map one-to-one to the book's chapters. The case-study folders (9–18) focus on glossary, common doubts, and curated reading; the timed practice lives in `mock_ai_system_design_problems/`.

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
