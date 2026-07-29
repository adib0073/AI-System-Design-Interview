# Key Terms — Chapter 1

The glossary slice for Chapter 1. Definitions are interview-oriented: each includes a short *why it matters* note. These entries feed the cumulative book-wide glossary (`/GLOSSARY.md`).

---

**A/B testing** — A controlled experiment in which users are randomly assigned to a treatment (new model/feature) or control (baseline) to measure causal impact.
*Why it matters:* Designing an ML system without mentioning experimentation is a common red flag; teams ship many model experiments per week.

**Ambiguity handling** — The ability to make progress when a problem is under-specified: asking sharp clarifying questions, stating assumptions, and framing the problem.
*Why it matters:* Weighted more heavily at higher levels (L6/L7+), where "framing the problem" is as important as solving it.

**Applied Scientist** — A role with a stronger research background, evaluated more on modeling, evaluation, and experimental rigor than on infrastructure depth.
*Why it matters:* Know which areas your role is scored on most; ASes get latitude on infra but must be rigorous on ML methodology.

**Architectural thinking** — Decomposing a problem into coherent components with clear interfaces, data flow, and failure modes — and justifying those choices.
*Why it matters:* One of the three high-level signals interviewers scan for.

**Back-of-the-envelope estimation** — Quick, order-of-magnitude calculations (QPS, storage, bandwidth, GPU memory) used to justify design decisions.
*Why it matters:* You're not expected to have operated at scale, but you are expected to reason about it. (Full treatment in Chapter 5.)

**Canary deployment** — Releasing a change to a small fraction of traffic first to validate it before a full rollout.
*Why it matters:* Signals production maturity; pairs with shadow deployment for de-risking model changes.

**Data-centric design** — An approach where the primary lever for improving a system is the data (collection, labeling, quality, features), not the code.
*Why it matters:* A core differentiator of AI system design from traditional software design.

**Deterministic logic** — Behavior that returns the same output for the same input every time; characteristic of traditional software.
*Why it matters:* Contrast with non-determinism forces design decisions around fallbacks, reproducibility, and evaluation.

**Drift (model / data / concept drift)** — Degradation of model performance over time as input distributions or the target relationship change.
*Why it matters:* Treating a model as "deploy once and forget" signals inexperience; interviewers expect explicit drift monitoring and retraining plans.

**Explicit feedback** — Direct user signals such as ratings, thumbs up/down, or reports. Clear but sparse.
*Why it matters:* Part of designing the feedback loop that lets a system self-improve.

**Feature store** — A centralized repository for storing, versioning, and serving features for both training and inference, keeping offline and online use consistent.
*Why it matters:* A recurring deep-dive component; central to avoiding train/serve skew.

**Feedback loop** — The mechanism by which user behavior is collected, stored, and fed back into retraining so the system improves.
*Why it matters:* A system that can't close the loop stagnates; interviewers look for how you capture and reuse signals.

**Graceful degradation** — Serving stale, cached, or simplified results when part of the system fails, instead of failing entirely.
*Why it matters:* Key to fault-tolerance reasoning, especially for online serving tiers.

**Guardrail metric** — A metric that must not regress during an experiment (e.g., latency, revenue, user complaints), used to prevent harmful launches.
*Why it matters:* Shows statistical and operational rigor in experimentation design.

**High-level architecture** — The end-to-end diagram of major components and data flow, expected within the first ~10–15 minutes.
*Why it matters:* A large rubric weight; a clean, justified architecture anchors the rest of the interview.

**Implicit feedback** — Indirect behavioral signals such as clicks, dwell time, or purchases (no direct labeling).
*Why it matters:* Often the primary training signal; contrast with sparse explicit feedback and delayed feedback.

**Inference** — Applying a trained model to new inputs to produce predictions at serving time.
*Why it matters:* Its latency tier (offline/nearline/online) drives much of the serving architecture.

**Levels (L4 / L5 / L6 / L7+)** — Seniority bands: L4 mid, L5 senior, L6 staff, L7+ principal/technical EM.
*Why it matters:* The rubric is constant but the *bar* rises with level; the same answer can pass at L5 and fail at L6.

**ML/AI system design round** — A dedicated design loop focused on ML-specific concerns (data, features, training, inference, evaluation, drift), distinct from the general system design round.
*Why it matters:* Confusing it with the general round is a top preparation mistake; they use different rubrics.

**Nearline** — A processing tier with seconds-to-minutes latency, typically event-triggered.
*Why it matters:* Choosing the right tier per use case simplifies infrastructure and cuts cost; not everything needs real-time inference.

**Non-deterministic output** — Output that can vary across invocations for the same input; characteristic of probabilistic ML models.
*Why it matters:* Forces explicit handling of fallbacks, reproducibility/audit, and metric-based evaluation.

**Offline evaluation** — Assessing model quality on historical data before deployment (e.g., AUC, NDCG), as opposed to live A/B testing.
*Why it matters:* Strong answers connect offline metrics to online metrics to business metrics.

**Offline / online serving tiers** — Offline = batch (hours–days); online = real-time (milliseconds). With nearline in between.
*Why it matters:* Matching each use case to the cheapest acceptable tier is a mark of good judgment.

**Problem scoping (requirement gathering)** — Clarifying scale, constraints, and must-haves vs. nice-to-haves before designing.
*Why it matters:* Diving into design without scoping is a classic failure; cap it at ~5–7 minutes, then commit.

**QPS (queries per second)** — A measure of request throughput; peak QPS is typically estimated as a multiple of average.
*Why it matters:* A staple of back-of-the-envelope sizing for serving and storage.

**RAG (Retrieval-Augmented Generation)** — An architecture that retrieves relevant documents and feeds them to a generative model (e.g., an LLM) to produce grounded, factual responses.
*Why it matters:* Increasingly common in 2024–2026 AI design rounds; introduce it only when the problem justifies it. (Chapter 6.)

**Retraining trigger** — The policy that decides when to retrain: event-based (e.g., weekly), metric-based (accuracy drop), or hybrid.
*Why it matters:* Demonstrates you plan for drift rather than reacting to it.

**Scoring rubric** — The structured set of weighted dimensions (scoping, architecture, depth, trade-offs, ML-specific, etc.) interviewers grade against.
*Why it matters:* Covering every rubric dimension deliberately beats a brilliant but lopsided answer.

**Shadow deployment** — Running a new model on live traffic without serving its output to users, to validate it against production before rollout.
*Why it matters:* A low-risk validation technique interviewers like to hear for model rollouts.

**Trade-off articulation** — Explicitly naming what a decision sacrifices to gain something else (e.g., accuracy for latency), ideally quantified.
*Why it matters:* One of the three core signals; "we use Redis for speed" is weak, "Redis because our p99 budget is 20 ms" is strong.

**Training pipeline** — The end-to-end workflow: ingest data → compute features → train → evaluate → register artifacts for deployment.
*Why it matters:* A common component deep-dive; interviewers probe how training is triggered and how experiments are managed.

---

*This slice covers terms introduced in Chapter 1. Later chapters extend the glossary; the merged version lives in `/GLOSSARY.md`.*
