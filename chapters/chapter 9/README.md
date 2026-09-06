# Chapter 9 — Recommendation & Feed Ranking

Companion resources for Chapter 9, the first Part 3 case study. Recommendation/feed ranking is the **most common** AI system design prompt and a **reusable template** for search, ads, PYMK, and notifications.

Chapter 9 covers the multi-stage funnel (retrieval → filtering → ranking → re-ranking), two-tower + ANN retrieval, multi-task deep ranking (MMoE/PLE, DLRM), cold start, feedback loops, diversity, sequential/transformer rankers, generative recommendation (semantic IDs), LLM/agentic recommenders, serving/latency budgets, and evaluation.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 9 glossary slice (two-tower, ANN, DLRM, MMoE/PLE, MMR, semantic ID, position bias, train/serve skew, …). Scanned from the chapter. Feeds the cumulative book glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — deriving the funnel, retrieval vs. ranking, objective design, cold start, when to bring up generative/LLM recommenders, and how to structure the answer under time pressure. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated real-world reading: YouTube/Instagram/TikTok/Pinterest/Netflix recsys, two-tower, MMoE, semantic IDs/TIGER, and ANN libraries. |

> **How to use:** read the chapter, then rehearse `common-doubts.md` out loud and drill the terms in `key-terms.md`. The funnel is the backbone of half the case studies in this book — internalize it.
