# Key Terms — Chapter 3 (Core Distributed Systems)

Interview-oriented definitions for the distributed-systems vocabulary in Chapter 3. Each entry pairs a crisp definition with *why it matters* in a design round. Terms already defined in Chapters 1–2 (e.g., QPS, feature store, latency) are cross-referenced rather than repeated. Feeds the cumulative book glossary.

---

### Scaling & performance
- **Vertical scaling (scale-up)** — Adding CPU/RAM/disk to one machine. *Why it matters:* simple but has a hard ceiling and a single point of failure; fine for prototypes.
- **Horizontal scaling (scale-out)** — Adding more machines to a cluster. *Why it matters:* the default answer for "how does this grow?"; requires statelessness or a sharding strategy.
- **Throughput** — Operations completed per unit time (RPS/TPS). *Why it matters:* the capacity axis, paired with latency as the two headline non-functional metrics.
- **P50 / P95 / P99 (latency percentiles)** — 50% / 95% / 99% of requests finish within this time. *Why it matters:* SLAs are written on tails (P99), not averages; one slow dependency shows up here first.
- **Tail latency** — The slow end of the distribution (P99+). *Why it matters:* fan-out amplifies it — a request hitting 100 services waits on the slowest of 100.
- **Consistent hashing** — Maps keys and nodes onto a ring so adding/removing a node reshuffles only ~1/N of keys. *Why it matters:* the standard technique for sharding caches and load balancers without mass remapping; name it whenever you shard.
- **Auto-scaling** — Adjusting instance count from live metrics (CPU, QPS, queue depth, custom ML latency). *Why it matters:* controls cost vs performance; use **cooldowns** to avoid thrashing and min/max bounds.
- **Capacity planning** — Estimating peak load and sizing for it with headroom (≈1.5×) and N+1 redundancy. *Why it matters:* connects BoE estimates to a concrete instance/shard count.

### Load balancing
- **Load balancer (L4 vs L7)** — Distributes traffic across backends; L4 routes on TCP/IP, L7 on HTTP content. *Why it matters:* L7 enables path/header routing and retries; L4 is faster/cheaper.
- **LB strategies** — Round-robin, least-connections, weighted, IP/consistent-hash. *Why it matters:* pick least-connections for uneven request costs; consistent hash for sticky/cacheable routing.

### Data storage
- **ACID** — Atomicity, Consistency, Isolation, Durability. *Why it matters:* the guarantee set relational DBs give; invoke when correctness (payments, inventory) is non-negotiable.
- **Sharding (partitioning)** — Splitting data across DBs by a partition key. *Why it matters:* scales writes/storage but makes cross-shard joins and transactions hard — choosing the key is the real design decision.
- **Replication (primary-replica)** — Keeping copies of data; one primary for writes, replicas for reads. *Why it matters:* scales reads and adds durability/HA.
- **Synchronous vs asynchronous replication** — Sync waits for replicas before ack (strong consistency, higher latency); async acks immediately (low latency, risk of loss on failover). *Why it matters:* the core consistency-vs-latency lever; ties directly to RPO.
- **NoSQL** — Non-relational stores (document, key-value, wide-column) optimized for scale/flexibility over joins. *Why it matters:* pick for high write volume, flexible schema, or huge unstructured datasets. e.g., MongoDB, Cassandra.
- **Vector database** — Stores high-dimensional embeddings for similarity/semantic search (ANN). *Why it matters:* the storage layer for RAG and semantic retrieval. e.g., Milvus, Qdrant.
- **Columnar database** — Stores columns contiguously for compression and fast aggregation. *Why it matters:* analytics/observability/feature debugging (ClickHouse, Druid, Pinot); bad for point updates.
- **Graph database** — Stores nodes/edges; efficient for many-hop relationship queries. *Why it matters:* knowledge graphs behind agentic/reasoning systems. e.g., Neo4j.
- **Object/blob storage** — Cheap, unlimited, HTTP-accessed store for unstructured data (S3, GCS, Azure Blob). *Why it matters:* the home for media, backups, and data-lake files — not a database.

### Caching
- **Cache-aside (lazy loading)** — App checks cache, on miss reads DB and populates it. *Why it matters:* most common pattern; resilient (cache down ≠ app down) but first read is a miss.
- **Read-through** — Cache itself fetches from the DB on a miss; app talks only to the cache. *Why it matters:* simpler app logic, centralizes the read path.
- **Write-through** — Writes go to cache and DB synchronously. *Why it matters:* cache always fresh; adds write latency.
- **Write-behind (write-back)** — Writes hit cache immediately, flush to DB async. *Why it matters:* high write throughput but risks data loss on crash.
- **Cache invalidation** — Keeping cached data fresh via **TTL**, **event-driven** (pub/sub on write), or **versioning**. *Why it matters:* "there are only two hard things…"; state your invalidation strategy explicitly.
- **Cache stampede (thundering herd)** — Many requests miss and hit the DB simultaneously when a hot key expires. *Why it matters:* mitigate with request coalescing, jittered TTL, or leases.
- **Distributed cache** — Sharded/replicated cache tier (Redis Cluster, Memcached). *Why it matters:* Redis for data structures/persistence/replication; Memcached for pure high-throughput KV.

### Networking & communication
- **REST vs gRPC vs GraphQL** — JSON/HTTP simplicity vs binary/HTTP-2 performance vs flexible client-driven queries. *Why it matters:* gRPC for low-latency internal/ML serving; REST for public/broad compatibility; GraphQL to avoid over/under-fetching.
- **Synchronous vs asynchronous calls** — Caller blocks for a response vs fires-and-continues (callback/poll). *Why it matters:* async decouples long operations and absorbs spikes.
- **WebSockets vs SSE** — Full-duplex persistent connection vs one-way server push. *Why it matters:* WebSockets for chat/interactive; SSE (simpler) for token streaming/notifications.
- **API gateway** — Single entry point for external traffic: auth, rate limiting, routing, aggregation. *Why it matters:* offloads cross-cutting concerns from services.
- **Service mesh** — Manages internal service-to-service traffic: mTLS, retries, circuit breaking, observability (e.g., Envoy/Istio). *Why it matters:* the "internal" counterpart to the gateway.
- **CDN / edge computing** — Caching/compute at PoPs near users. *Why it matters:* cuts latency and origin load for media and static/edge inference.
- **Rate limiting / throttling** — Capping request (or token) rate per client. *Why it matters:* protects the serving tier from abuse and spikes; often per-API-key or per-IP.

### Messaging
- **Message queue vs event stream** — Queues deliver a task to one consumer then delete it; streams are a persistent, replayable log many consumers read. *Why it matters:* queues for task decoupling (SQS/RabbitMQ); streams for replay/analytics/multiple consumers (Kafka).
- **Delivery semantics** — At-most-once, at-least-once, exactly-once. *Why it matters:* "exactly-once" is expensive/limited; most systems do at-least-once + idempotent consumers.
- **Stream vs batch processing** — Continuous low-latency vs scheduled high-throughput. *Why it matters:* streaming for real-time features/dashboards; batch for large historical scans/training data.

### Architecture
- **Monolith / microservices / modular monolith** — One deployable / many independent services / one deployable with strict internal module boundaries. *Why it matters:* start modular-monolith and split later; don't reach for microservices "because they're cool."
- **Circuit breaker** — Stops calling a failing dependency to let it recover. *Why it matters:* prevents cascading failures; pair with retries + timeouts + bulkheads.

### Reliability & disaster recovery
- **CAP theorem** — Under a partition you must choose Consistency or Availability (partition tolerance is mandatory). *Why it matters:* frame data-store trade-offs — CP for fraud/balances, AP for feeds/recommendations.
- **PACELC** — Extends CAP: if Partition → A vs C; Else → Latency vs C. *Why it matters:* captures the everyday latency-vs-consistency trade-off even without a partition.
- **Quorum** — Requiring responses from a majority (e.g., R + W > N) before a read/write is accepted. *Why it matters:* the tunable knob (Dynamo/Cassandra) for balancing consistency, availability, and latency.
- **Consensus (Raft / Paxos)** — Protocols for nodes to agree on a value/log despite failures. *Why it matters:* underpins leader election and replicated state (etcd, ZooKeeper, Spanner); know that it exists and needs a majority.
- **Failover: active-passive vs active-active** — Standby takes over on failure vs all nodes serve simultaneously. *Why it matters:* active-active is the norm for stateless inference (lose a node, lose only capacity); active-active on shared writable data needs conflict resolution.
- **RPO (Recovery Point Objective)** — Max acceptable data loss, in time. *Why it matters:* tighter RPO → more frequent/synchronous replication.
- **RTO (Recovery Time Objective)** — Max acceptable downtime. *Why it matters:* tighter RTO → active-passive/active-active, runbooks, automation.
- **Chaos engineering** — Deliberately injecting failures to validate resilience (Chaos Monkey, Gremlin, AWS FIS). *Why it matters:* signals you design for the non-happy path; start small with clear abort criteria.

### Observability & security
- **Metrics / logs / traces** — Aggregated numbers / event records / per-request path across services. *Why it matters:* traces localize the slow hop in a multi-service (or agentic) chain.
- **SLI / SLO / SLA** — Indicator (measured) / objective (internal target) / agreement (external, with penalties). *Why it matters:* frame reliability quantitatively; P99 latency is a classic SLI.
- **Deployment strategies** — Canary, blue-green, rolling. *Why it matters:* safe rollout/rollback; canary limits blast radius (also used for model rollouts — see Ch. 4).
- **AuthN vs AuthZ** — Who you are (OAuth 2.0, OIDC, JWT, mTLS) vs what you can do (RBAC, least privilege, scoped access). *Why it matters:* protects data/model pipelines from poisoning and theft.
- **mTLS** — Mutual TLS; both client and service prove identity. *Why it matters:* standard for service-to-service auth inside a mesh.
- **GDPR / CCPA** — EU/California privacy laws (right to erasure, opt-out, privacy-by-design). *Why it matters:* AI systems process personal data — mention data minimization, retention limits, anonymization.
- **Prompt injection** — Malicious input that overrides an LLM's instructions. *Why it matters:* an AI-native threat; pair with output sanitization and least privilege on tools.

---

*Cross-refs:* QPS, latency, throughput basics → Chapter 1/2 key-terms. Feature store, drift, canary/shadow (ML-specific) → Chapter 4 key-terms.
