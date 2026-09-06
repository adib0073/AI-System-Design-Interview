# Key Terms — Chapter 9 (Recommendation & Feed Ranking)

Interview-oriented definitions for the vocabulary in Chapter 9 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters* in a design round. Feeds the cumulative book glossary.

---

### The funnel & retrieval
- **Multi-stage funnel** — Retrieval → filtering → ranking → re-ranking, narrowing millions of items to a handful. *Why it matters:* the backbone of the answer; derive it from the latency × catalog-size constraint rather than reciting it.
- **Candidate generation / retrieval** — First stage; recall-oriented narrowing from millions to thousands. *Why it matters:* optimize recall and speed here, precision later.
- **Two-tower model** — Separate user and item encoders producing embeddings compared by dot product. *Why it matters:* lets you precompute item embeddings and serve via ANN — the scalable retrieval workhorse.
- **ANN (Approximate Nearest Neighbor)** — Index (ScaNN, FAISS/IVF-PQ, HNSW) for fast top-K similarity retrieval over item embeddings. *Why it matters:* trades exact recall for speed/memory; what makes million-item retrieval real-time.
- **In-batch / sampled-softmax negatives** — Efficient negative sampling for two-tower training. *Why it matters:* needs popularity (log-Q) correction or the model over-favors popular items.
- **Cross features** — User×item interaction features (e.g., past affinity to this creator). *Why it matters:* powerful in ranking but **not usable** in separable two-tower retrieval — a classic "why can't the retrieval tower use them?" probe.

### Ranking
- **DLRM (Deep Learning Recommendation Model)** — Large embedding tables + MLPs for large-scale ranking/CTR. *Why it matters:* the standard heavy-ranking architecture; embedding tables dominate memory.
- **Learning-to-rank (LTR)** — Directly optimizing ranking quality (e.g., LambdaMART for NDCG). *Why it matters:* ranking is about order, not pointwise scores.
- **Multi-objective ranking** — Predicting several engagement signals and combining them into one value score. *Why it matters:* real feeds optimize watch time + likes + shares + long-term value, not one metric.
- **MMoE / PLE** — Multi-task architectures (multi-gate mixture of experts / progressive layered extraction) sharing representation while limiting negative transfer. *Why it matters:* the go-to when predicting many correlated objectives at once.
- **Value model** — The function/weights combining multi-task predictions into the final score. *Why it matters:* encodes product priorities; **objective design beats architecture.**
- **Wide & Deep** — Linear (memorization) + deep (generalization) components. *Why it matters:* influential CTR baseline; good to cite for lineage.

### Re-ranking & challenges
- **Re-ranking** — List-aware final stage applying diversity, freshness, policy, and blending. *Why it matters:* the funnel's last stage; where business rules and diversity live.
- **MMR (Maximal Marginal Relevance)** — Balances relevance with diversity relative to already-selected items. *Why it matters:* the standard answer to "how do you avoid 20 near-identical items?"
- **Cold start** — Recommending with little/no data for a new user or item. *Why it matters:* mandatory topic; frame it as an exploration problem + content/embedding features.
- **Feedback loop** — Recommendations shape the data that trains the next model. *Why it matters:* causes popularity concentration and filter bubbles; needs exploration + logging of what was shown.
- **Position bias** — Higher-ranked items get more engagement regardless of relevance. *Why it matters:* must be debiased (e.g., position as a feature, IPS) or the model learns "top = good."
- **Diversity & exploration** — Deliberately varying and probing uncertain items. *Why it matters:* counters feedback loops and staleness; ties cold start and diversity together.

### Modern & frontier
- **Sequential recommender** — Treats user history as an ordered sequence (GRU4Rec, SASRec, BERT4Rec, transformers). *Why it matters:* captures short- and long-term intent; the "modern route" upgrade to ranking.
- **Generative retrieval** — Modeling the next item as generated tokens rather than embedding matching (e.g., TIGER). *Why it matters:* frontier shift from "retrieve-then-rank" to "generate the next item."
- **Semantic ID** — A short sequence of discrete, content-derived codes (e.g., via RQ-VAE) identifying an item. *Why it matters:* enables generalization and cold start in generative recommenders.
- **LLM / agentic recommender** — Using LLMs for steerable, conversational, or multi-step recommendation. *Why it matters:* mention with honest cost/latency trade-offs; not a default replacement for the funnel.

### Serving & evaluation
- **Train/serve skew** — Discrepancy between features/logic in training vs. serving. *Why it matters:* a leading cause of "great offline, bad online"; feature store parity fixes it.
- **Latency budget** — Allocating the SLA across retrieval, ranking, and re-ranking stages. *Why it matters:* make the numbers add up; interviewers probe whether your design fits the budget.
- **Offline → online → business evaluation** — Offline metrics (NDCG/recall) → online A/B (engagement) → business (retention), with guardrails. *Why it matters:* the metric ladder; offline wins must be validated online.

---

*Cross-refs:* embeddings, ANN, RAG → Ch. 4/6. Latency/QPS/caching → Ch. 3/5. Feature stores, drift, A/B → Ch. 4/8. Ads ranking reuses this funnel → Ch. 10.
