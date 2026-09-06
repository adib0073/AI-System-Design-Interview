# Common Interviewee Doubts — Chapter 9 (Recommendation & Feed Ranking)

The questions candidates most often have about recsys/feed-ranking rounds. Grouped by theme.

---

## Framing & the funnel

**1. Why do we need a multi-stage funnel at all — why not one big model?**
Latency × catalog size forces it. You can't run a heavy ranking model over millions of items in ~100 ms. Retrieval cheaply narrows millions → thousands (recall-oriented), then ranking spends compute on a precise ordering of those thousands. Derive this out loud; don't just assert "we use a funnel."

**2. Retrieval vs. ranking — what's the actual difference?**
Retrieval optimizes **recall** at massive scale with cheap models (two-tower + ANN, precomputed item embeddings). Ranking optimizes **precision/ordering** on a small candidate set with a heavy model that can use expensive cross features. Different objectives, different architectures.

**3. Why can't the two-tower retrieval model use user×item cross features?**
Because retrieval precomputes item embeddings independent of the user (so ANN can search them). Cross features couple user and item, which breaks separability. Cross features live in **ranking**, where you score one (user, item) pair at a time. This is a very common probe.

## Objective design

**4. What should the model actually optimize?**
Not raw CTR — that breeds clickbait. Optimize a **multi-objective value** blending several engagement signals (dwell/watch time, likes, shares, follows, and long-term retention proxies) with guardrails against harmful/low-quality content. Say explicitly: **objective design beats architecture.**

**5. How do I combine multiple predicted objectives?**
Predict each with a multi-task model (MMoE/PLE), then combine via a **value model** (weighted sum or learned) that encodes product priorities. Tuning those weights (and validating via A/B) is often more impactful than a fancier architecture.

## Mandatory challenges

**6. How do I handle cold start?**
New items: content/embedding features that work with zero interactions. New users: onboarding signals, context, popularity priors. Frame both as **exploration** — you must show uncertain items to learn about them. Interviewers expect this topic unprompted.

**7. What's the feedback-loop / bias problem and how do I mitigate it?**
The model's own recommendations generate its next training data → popularity concentration and filter bubbles, plus **position bias** (top items get clicks regardless of relevance). Mitigate with exploration, position debiasing (position feature / inverse-propensity weighting), and logging exactly what was shown.

**8. How do I inject diversity without tanking relevance?**
Re-rank with MMR or a diversity-aware objective at the final stage — relevance first, then de-duplicate/spread across topics/creators. It's a trade-off you tune, not a binary.

## Modern & frontier

**9. Should I bring up transformers / sequential models?**
Yes, as the "modern route": sequential rankers (SASRec/BERT4Rec/transformers) capture ordered intent better than pointwise features. Position it as a ranking upgrade with a latency/cost trade-off, gated by A/B.

**10. When do I mention generative recommendation or LLM/agentic recommenders?**
In Extensions. Generative retrieval (semantic IDs, TIGER) reframes "retrieve-then-rank" as "generate the next item" and helps cold start/generalization. LLM/agentic recommenders enable steerable, conversational recs. Mention both with **honest cost/latency caveats** — don't propose replacing the whole funnel with an LLM.

## Serving & evaluation

**11. How do I make the latency budget add up?**
Assign a slice of the SLA to each stage (retrieval, ranking, re-ranking), precompute item embeddings, cache, use real-time features with freshness limits, and add graceful fallbacks. Show the numbers summing under the SLA — a strong signal.

**12. How do I evaluate?**
The ladder: **offline** (NDCG, recall@k, calibration) → **online A/B** (engagement, with guardrails) → **business** (retention, revenue). Offline wins must survive online tests; watch for train/serve skew when offline looks great but online doesn't.

## Delivery

**13. How do I structure the whole answer in ~40 minutes?**
Clarify scope + objective → derive the funnel → retrieval (two-tower + ANN) → ranking (multi-task + value model) → challenges (cold start, bias, diversity) → serving/latency → evaluation → extensions (sequential/generative/LLM). Narrate trade-offs at each step; that's what's graded.
