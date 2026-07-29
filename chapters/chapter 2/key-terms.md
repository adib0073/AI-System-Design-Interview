# Key Terms — Chapter 2

The glossary slice for Chapter 2, focused on terms this chapter introduces or leans on heavily. Definitions are interview-oriented. These feed the cumulative book-wide glossary (`/GLOSSARY.md`). Terms already defined in Chapter 1 (drift, feature store, A/B testing, offline evaluation, inference, training pipeline) are cross-referenced rather than repeated.

---

**CHASE framework** — A five-phase template for AI system design interviews: Clarify & Scope, High-Level Design, AI/ML Deep Dive, System & Infra Deep Dive, Extensions & Trade-offs.
*Why it matters:* Guarantees you cover every evaluation area within a 45–60 minute round; "structure beats brilliance."

**Functional requirements** — What the system must *do*: core functionality, user operations, workflows, inputs/outputs, integrations, roles, edge-case handling.
*Why it matters:* Categorizing them explicitly signals clarity of thought in Phase C.

**Non-functional requirements** — How the system must *perform*: latency, throughput, scalability, availability, reliability, consistency, durability, security/privacy, cost, maintainability.
*Why it matters:* They directly dictate architecture (e.g., a <100 ms budget rules out reasoning-heavy LLMs on the hot path).

**Latency** — Maximum acceptable response time (often expressed as a percentile budget, e.g., p99 < 100 ms).
*Why it matters:* A primary driver of serving, caching, and model-size decisions.

**Throughput** — The volume of requests the system must handle, e.g., peak QPS.
*Why it matters:* Sets scaling and capacity targets.

**Availability** — Percentage of time the system is operational (e.g., 99.9% uptime).
*Why it matters:* "Non-negotiable" for customer-facing systems; motivates horizontal scaling and redundancy.

**Consistency (requirement)** — How current/correct data must be across a distributed system (strong vs. eventual).
*Why it matters:* Payments need strong consistency; feeds can tolerate eventual — a classic trade-off to name.

**Durability** — Guarantee that committed data is never lost.
*Why it matters:* Motivates replication and reliable storage for critical records.

**ML problem type** — The underlying task: classification, regression, ranking, retrieval, generation (often multi-stage).
*Why it matters:* Naming it early shapes model, data, and evaluation choices.

**Retrieval → Ranking → Re-ranking** — The multi-stage pattern: narrow billions of candidates (retrieval), score/order them (ranking), then adjust for diversity/freshness/business goals (re-ranking).
*Why it matters:* The canonical framing for recommendation/search design.

**Cold start** — The problem of serving new users, new items, or new creators that lack historical data. *(Also, at the infra level: the time to boot a large model container.)*
*Why it matters:* A go-to edge case in Phase E; senior candidates design for both product and infra cold start.

**Online vs. offline features** — Online features are computed at inference time (low latency); offline features are computed in batch during training.
*Why it matters:* Central to feature-store design and avoiding train-serve skew. *(See feature store, Ch1.)*

**Training-serving skew** — Inconsistency between how a feature is computed for training vs. serving, degrading production performance.
*Why it matters:* Mentioning how you prevent it (shared feature logic) is a senior signal.

**Model registry** — A service that versions and tracks model artifacts plus metadata (code version, hyperparameters, data lineage, metrics).
*Why it matters:* Enables pointing inference to a new model version with no downtime, and reproducibility.

**Online vs. offline inferencing** — Online = real-time predictions (low latency, high concurrency, costly); offline = precomputed/batch predictions (high throughput, higher storage).
*Why it matters:* Choosing the cheaper acceptable mode per use case is good judgment.

**Horizontal vs. vertical scaling** — Horizontal = add more (ideally stateless) instances behind a load balancer; vertical = make one machine more powerful.
*Why it matters:* Horizontal is preferred for availability/fault tolerance; vertical hits a hard ceiling and adds a single point of failure.

**Stateless server** — An inference server that stores no session data locally; it fetches features from a remote store per request.
*Why it matters:* Prerequisite for clean horizontal scaling.

**Bottleneck** — The slowest stage limiting overall performance (e.g., feature-store throughput, GPU memory, network latency).
*Why it matters:* Naming a concrete bottleneck (and its fix) shows production experience.

**HPA (Horizontal Pod Autoscaler)** — Kubernetes autoscaler that adds/removes pods based on resource usage.
*Why it matters:* Works on CPU/RAM but often fails for GPU-bound AI workloads, so name a better signal.

**KEDA (Kubernetes Event-Driven Autoscaling)** — Scales on external events (e.g., Kafka queue depth) and can scale to zero.
*Why it matters:* A big cost-saver for expensive idle GPUs; a strong autoscaling answer.

**Node autoscaler (e.g., Karpenter, Cluster Autoscaler)** — Provisions new physical/GPU nodes when pods are pending.
*Why it matters:* GPU node provisioning takes 2–5 min — a critical latency discussion point.

**Prediction cache** — A key-value cache of final inference results (e.g., top-20 recommendations per user) with a TTL.
*Why it matters:* Reuses expensive GPU passes; a core AI cost-containment strategy.

**Feature/embedding cache** — Caching expensive intermediate features or embeddings so the extraction step can be skipped.
*Why it matters:* Skips the feature-extraction bottleneck for sub-2 ms lookups.

**Cache invalidation** — Removing/refreshing stale cache entries (mostly event-driven in AI systems).
*Why it matters:* Stale caches cause bad UX (e.g., recommending a just-purchased item).

**Cache stampede** — When a popular key expires and many concurrent requests hit the backend to recompute it at once.
*Why it matters:* Dangerous in AI because each recompute is a heavy model pass.

**TTL (time-to-live)** — How long a cache entry stays valid before expiring.
*Why it matters:* The knob in the hit-rate vs. freshness trade-off.

**Eviction policy (e.g., LRU)** — The rule for removing entries when the cache is full (Least Recently Used).
*Why it matters:* Controls the memory footprint of embedding/prediction caches.

**Guardrail metric** — A metric that must not regress during experimentation (defined in Ch1).
*Why it matters:* Emphasized in Meta-style rounds; part of a rigorous A/B design.

**Signposting** — Verbal cues that guide the interviewer through your structured thinking ("Moving to the serving layer…").
*Why it matters:* Helps the interviewer check off rubric items; a scored communication behavior.

**T-shaped answer** — Breadth across all components plus depth in one or two areas of expertise.
*Why it matters:* The recommended strategy; shallow-everywhere and deep-in-only-one both raise flags.

**Observability (p50/p95/p99)** — Post-production monitoring of model performance, data drift, latency percentiles, and business impact, with alerts.
*Why it matters:* Deep-diving monitoring signals real production experience.

**MCP (Model Context Protocol)** — A protocol modern agentic systems use to connect models to external tools/resources (detailed in Chapter 7).
*Why it matters:* Mentioned as a serving/connection option; know it exists at this stage.

---

*This slice covers terms featured in Chapter 2. The merged, deduplicated version lives in `/GLOSSARY.md`.*
