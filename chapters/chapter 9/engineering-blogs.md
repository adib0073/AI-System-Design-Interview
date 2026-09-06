# Engineering Blogs & Papers — Chapter 9 (Recommendation & Feed Ranking)

Curated, interview-relevant reading. Prefer understanding the *design decisions and trade-offs* over memorizing architectures. Links may move — search the title if one is dead.

> **Living note:** recsys tooling and frontier methods (generative recommendation, LLM recommenders) move fast — treat frontier entries as directional.

## Start here (highest signal)
- **"Deep Neural Networks for YouTube Recommendations"** (Covington et al., 2016) — the canonical **candidate-generation + ranking two-stage** paper. Read this first.
- **Sampling-Bias-Corrected Two-Tower** (Yi et al., Google, 2019) — why two-tower retrieval needs **log-Q / popularity correction**.
- **Wide & Deep Learning** (Cheng et al., Google, 2016) — memorization + generalization; foundational CTR design.

## Retrieval & embeddings
- **ScaNN** (Google) and **FAISS** (Meta) — the ANN libraries to name; understand IVF-PQ vs. HNSW trade-offs.
- Pinterest **"PinSage"** — GraphSAGE at web scale for related-pins retrieval.
- Google **"Mixed Negative Sampling"** / two-tower retrieval follow-ups — practical negative-sampling lessons.

## Ranking & multi-task
- **MMoE** (Ma et al., Google KDD 2018) and **PLE** (Tang et al., Tencent RecSys 2020, best-paper) — multi-task ranking; PLE addresses negative transfer/seesaw.
- **DLRM** (Naumov et al., Meta, 2019) — open-source large-scale ranking model; embedding-table scale.
- **DCN / DCN-v2** (Google) — explicit feature-cross networks for ranking.

## Real-world systems (design blogs)
- **Instagram / Meta feed & Reels ranking** engineering posts — multi-stage, multi-objective value models at scale.
- **TikTok / ByteDance Monolith** — real-time recommendation with collisionless embedding tables.
- **Netflix Tech Blog** — recommendations, page/row optimization, and A/B culture.
- **Pinterest & Twitter (the open-sourced "the-algorithm")** — end-to-end home-feed pipelines.
- **Spotify** — sequential/session-based and audio-embedding recommendations.

## Diversity, bias & evaluation
- **Maximal Marginal Relevance (MMR)** (Carbonell & Goldstein, 1998) — the diversity re-ranking classic.
- **Position-bias / IPS for LTR** — unbiased learning-to-rank literature (Joachims et al.).
- Off-policy evaluation / counterfactual estimation overviews — for reasoning about feedback loops.

## Frontier (directional)
- **TIGER: "Recommender Systems with Generative Retrieval"** (Rajput et al., Google, 2023) — **semantic IDs** + generative retrieval.
- **RQ-VAE** — residual-quantized codes underpinning semantic IDs.
- Recent **LLM-for-recommendation / conversational recommender** surveys — steerability with cost/latency caveats.

## How to use in prep
1. Read the YouTube two-stage paper and one modern feed blog (Instagram/TikTok) — that covers 80% of what you'll be asked.
2. Be able to explain **two-tower + ANN** and **MMoE/PLE + value model** from memory.
3. Skim TIGER so you can credibly mention generative recommendation in Extensions.
