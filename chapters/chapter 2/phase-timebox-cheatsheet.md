# CHASE Time-Box Cheat Sheet (Printable One-Pager)

Print this and keep it beside you during mock interviews. Times assume a 45–60 minute round; the **first 5–10 minutes** go to introductions and reading the problem, leaving ~35–40 min (45-min round) or ~50 min (60-min round) for design.

---

## The clock at a glance

```
| C: Clarify & Scope   | 5–7 min   | ████                       |
| H: High-Level Design | 8–10 min  |     ██████                 |
| A: AI/ML Deep Dive   | 12–15 min |           █████████         |
| S: System & Infra    | 10–15 min |                   ███████   |
| E: Extensions/Trade  | 5–8 min   |                          ███|
```
*Rule of thumb: if you're past a phase's upper bound and the interviewer hasn't steered you there, move on and say so.*

---

## C — Clarify & Scope · 5–7 min
**Goal:** Understand the real problem before designing. Most candidates who fail do so in the first 10–15 minutes.
**Do:**
- Probe four dimensions: **product context · scale · constraints · success metrics**.
- Write a short **requirements doc** on the board.
- Separate **functional** (what) vs. **non-functional** (latency, throughput, scale, availability, consistency, cost) requirements.
- Name the **ML problem type** (classification / ranking / retrieval / generation — often multi-stage).
- State assumptions explicitly ("Assume 100M DAU, p99 < 100 ms").
**Output:** A scoped problem + written assumptions everyone agrees on.
**Watch out:** Don't rush this, and don't interrogate for 15 min — cap it and commit.

## H — High-Level Design · 8–10 min
**Goal:** An end-to-end architecture a colleague could grasp in 30 seconds.
**Do:**
- Draw the flow: data sources → ingestion/storage → training → registry → serving → client.
- Separate **offline** from **online** paths (color/line style).
- **Label every arrow** ("User request", "Features", "Predictions", "Events").
- Narrate while drawing; say the first draft isn't final.
**Output:** A clean, labeled block diagram of major components + data flow.
**Watch out:** Spending >10 min perfecting the diagram is a trap — it starves Phases A and S.

## A — AI/ML Deep Dive · 12–15 min
**Goal:** Show fluency where AI design diverges from software design.
**Do:**
- **Data:** sources, collection (stream vs. batch), labeling / implicit-label generation.
- **Features:** types (user/item/context/cross), offline vs. online, feature store & train-serve skew.
- **Model:** justify the choice by trade-offs (simplicity vs. accuracy, latency vs. cost, size, explainability).
- **Pipeline:** triggers, data pipeline, experiment tracking, versioning.
- **Evaluation:** offline (precision/recall/AUC, recall@k/MRR/NDCG) → online (A/B) → business metrics.
**Output:** A defensible data→model→evaluation story.
**Watch out:** Superficial model treatment is a red flag (especially at Meta). Always connect offline → online → business metrics.

## S — System & Infra Deep Dive · 10–15 min
**Goal:** Tie the model to production infrastructure.
**Do:**
- **Serving:** API vs. edge vs. MCP; online vs. offline (batch) inference.
- **Scaling:** horizontal (stateless servers + LB) vs. vertical; name **bottlenecks** (feature-store throughput, GPU memory, network).
- **Autoscaling:** justify the signal — QPS, queue depth, GPU utilization, p99 latency; HPA vs. **KEDA** (scale-to-zero); node autoscalers (Karpenter); container **cold start**.
- **Storage:** feature store (online Redis/DynamoDB + offline S3/Snowflake), model registry, event data + feedback loop, retention policies.
- **Caching:** prediction cache & feature/embedding cache; TTL; pitfalls (invalidation, stampede); eviction (LRU); global vs. local.
- **Observability:** model performance, data drift, p50/p95/p99, business impact + alerts.
**Output:** Production-ready system meeting the non-functional requirements.
**Watch out:** "Just use autoscaling" without a scaling signal is weak. Every infra choice ties back to an ML/product requirement.

## E — Extensions & Trade-offs · 5–8 min
**Goal:** Demonstrate maturity and senior-level thinking.
**Do:**
- **Edge cases / failure modes:** cold start (new users/items), stale features, model failure, drift.
- **Cost optimization:** training/inference, caching, storage, model selection.
- **Future improvements:** better models/architectures, richer features, multi-task learning, explainability, responsible-AI guardrails.
**Output:** A short list of what you'd improve next and the trade-offs involved.
**Watch out:** Running out of time before you reach trade-offs is itself a red flag — protect this phase.

---

## Company adaptation (quick reference)
- **Google** — ask about scale early; lead with trade-offs; expect 10× stress tests; be comfortable with ambiguity.
- **Meta** — march the rubric: Data → Features → Model → Training → Serving → Eval → Experimentation; A/B testing is not optional.
- **Amazon** — tie decisions to customer impact; show end-to-end ownership; weave in Leadership Principles; be pragmatic.

> **Golden rule:** *Structure beats brilliance.* A time-boxed answer covering all five phases outperforms a brilliant but chaotic one.
