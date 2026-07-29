# FAQ / Practice Bank — Chapter 4 (Core AI System Concepts)

A practice set for the three questions that come up in almost every AI system design round:

- **A. "Does this actually need AI/ML?"** — problem framing
- **B. Metric selection** — offline → online → business
- **C. Drift scenarios** — diagnose the drift type and respond

Work each problem before reading the answer. The goal is a *repeatable reasoning pattern*, not memorized answers.

---

## A. Does this problem need AI/ML?

> **Framing rule (from §4.1):** always ask "*Could we solve this with simpler logic?*" AI adds complexity, maintenance, and nondeterminism — it must be justified by a measurable gain. Use ML when the rules are too many/changing, patterns are learnable from data, some error is tolerable, and the payoff beats the cost.

**A1. Detect profanity in usernames at signup.**
*Answer:* **Start with rules** (blocklist + regex + normalization for leetspeak). A fixed, well-understood vocabulary, near-zero error tolerance, and instant explainability. Add a small classifier only for adversarial evasion the list can't catch. ML is a *fallback*, not the default.

**A2. Rank a personalized home feed for 100M users.**
*Answer:* **Needs ML.** Preferences are per-user, high-dimensional, and shift over time — un-encodable as rules. Some error is tolerable (a mediocre item is cheap). Clear online payoff (engagement). Classic ranking problem; likely a multi-stage funnel.

**A3. Compute a customer's monthly invoice total.**
*Answer:* **No AI.** Deterministic arithmetic with zero error tolerance and legal/audit requirements. ML here is actively harmful (nondeterminism, no exact explainability). A hard no — say so confidently.

**A4. Route support tickets to the right team.**
*Answer:* **It depends — start with rules, graduate to ML.** If a handful of keywords/queue rules get you 90%, ship that. Move to a text classifier when categories are many, overlapping, or drifting, and volume justifies maintaining a model. Good example of *earning* the ML.

**A5. Flag likely-fraudulent transactions in real time.**
*Answer:* **Needs ML, but hybrid.** Patterns are adversarial and evolving (rules alone get gamed), so a model adds real lift. Keep deterministic rules for hard constraints (velocity limits, blocklists) as a fast, explainable first layer. Note the CP/consistency requirement (Ch. 3) and tight latency budget.

**A6. Sort a list of numbers.**
*Answer:* **No AI — trap question.** A solved algorithmic problem. If a candidate reaches for ML here, it signals poor judgment. The value is in *recognizing* it.

**A7. Summarize long support threads for agents.**
*Answer:* **Needs GenAI (LLM).** Open-ended natural-language generation with no rule-based equivalent. But scope it: is an off-the-shelf hosted LLM + prompt enough, or do cost/privacy push you to a self-hosted open-weight model? Define success (faithfulness, no hallucinated facts) before choosing.

---

## B. Metric selection

> **Framing rule (from §4.1):** never stop at the model metric. Chain **offline → online → business**. Offline metrics drive online metrics, which drive business outcomes. Match the offline metric to the *task type*.

**B1. Fraud detection (heavy class imbalance).**
- *Offline:* **Precision/Recall, PR-AUC** (not plain accuracy — 99.9% "not fraud" makes accuracy meaningless). Often optimize recall at a fixed precision.
- *Online:* fraud caught vs false-decline rate; alert-review load.
- *Business:* $ fraud loss prevented, customer friction / false-decline complaints.
- *Trap:* quoting accuracy or AUC-ROC alone on imbalanced data.

**B2. Search / RAG retrieval relevance.**
- *Offline:* **Recall@k, Precision@k, MRR, NDCG** (rank-aware). Add a cross-encoder for a reranking-quality signal.
- *Online:* CTR, click position, query reformulation rate, dwell time; answer thumbs-up for RAG.
- *Business:* task success rate, deflection (fewer support escalations), retention.

**B3. Product recommendations.**
- *Offline:* NDCG / MAP / Recall@k on held-out interactions.
- *Online:* CTR, conversion rate, add-to-cart, diversity/coverage.
- *Business:* revenue per session, GMV, long-term retention (watch for filter bubbles).
- *Note:* offline gains don't always translate — that's *why* you A/B test online.

**B4. LLM assistant (open-ended generation).**
- *Offline:* golden-set + **human evaluation** (faithfulness, helpfulness, safety); task-specific automatic metrics where they exist. Accuracy is rarely enough.
- *Online:* thumbs up/down, regeneration rate, task completion, escalation-to-human.
- *Business:* CSAT/NPS, containment/deflection, cost per resolved query.

**B5. "The model improved offline AUC by 1% — do we ship it?"**
*Answer:* **Not yet.** Offline lift is necessary, not sufficient. Validate with an **online A/B test** (or shadow/interleaving) for statistically significant movement on the online metric, confirm no regression on guardrail metrics (latency, fairness, complaints), *then* tie it to the business metric. Shipping on offline metrics alone is the classic red flag called out in §4.1.

---

## C. Drift scenarios — diagnose and respond

> **The three drifts (from §4.4 monitoring):**
> - **Data (covariate) drift** — input distribution `P(X)` shifts; the feature-target relationship may be unchanged.
> - **Concept drift** — the relationship `P(Y|X)` itself changes; the world's rules moved.
> - **Prediction drift** — the output distribution shifts; an *early warning* before ground-truth labels arrive.

**C1. A new app version adds a feature that's `null` in 40% of requests, and precision drops the next day.**
*Diagnosis:* **Data drift + a pipeline bug** (training-serving skew). The input distribution changed because a feature broke, not because user behavior changed.
*Response:* alert on feature null-rate/schema; fix the pipeline; enforce train-serve consistency via the feature store; add data-quality gates.

**C2. A spam classifier's accuracy slowly decays over 3 months even though inputs look statistically similar.**
*Diagnosis:* **Concept drift** — spammers changed tactics, so `P(spam|features)` moved while `P(features)` looks stable.
*Response:* scheduled/triggered **retraining** on fresh labels; monitor performance against a rolling labeled sample; consider online/continuous learning.

**C3. Predicted "fraud" rate jumps from 2% to 9% overnight, but labels won't confirm for weeks.**
*Diagnosis:* **Prediction drift** — output distribution shifted; use it as an early warning before ground truth lands.
*Response:* investigate upstream inputs (new merchant, new geo, ingestion bug); shadow/canary the change; hold or roll back if a feature source broke; don't wait for labels.

**C4. A demand-forecasting model that was accurate for two years suddenly fails after a market shock.**
*Diagnosis:* **Concept drift** (abrupt) — the underlying relationship changed. Historical patterns no longer hold.
*Response:* trigger emergency retrain on recent data; temporarily widen prediction intervals / add human-in-the-loop; add a drift-threshold retraining trigger going forward.

**C5. Offline metrics are great, but online metrics disappoint after launch.**
*Diagnosis:* likely **training-serving skew** (feature computed differently in serving) and/or **selection bias** in the training data (trained on logged data from the *old* policy).
*Response:* audit feature parity offline vs online (feature store as single source of truth); check point-in-time correctness to rule out label leakage; use online experiments and logging/replay to close the loop.

**C6. How would you *monitor* for all of the above proactively?**
*Answer:* track input feature distributions (PSI/KL divergence, null rates), prediction distributions, and — where labels arrive — live performance vs a baseline; set thresholds that trigger alerts and automated **retraining pipelines** (with rollback). Tools: Evidently AI, plus cloud monitoring. This is the difference between an "up" service and a *correct* one (§3 observability).

---

### How to use this bank
1. Cover the answer, reason aloud, then compare.
2. For every problem, force yourself to (a) name the framing/metric/drift *type* and (b) state the *response or design consequence*.
3. Pair with the [decision trees & checklists](./decision-trees-checklists.md) for the "how would you build it" follow-up.
