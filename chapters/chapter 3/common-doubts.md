# Common Interviewee Doubts — Chapter 3 (Core Distributed Systems)

Real questions candidates ask about the distributed-systems fundamentals behind AI system design rounds. Grouped by theme.

---

## Scope & expectations

**1. This is an AI book — why so much "traditional" distributed systems?**
Because every AI system *is* a distributed system. The model is one box in a diagram full of load balancers, databases, caches, queues, and replicas. Interviewers assume fluency here even in AI-focused rounds; weak fundamentals sink an otherwise good ML answer. Treat Chapter 3 as the non-negotiable baseline.

**2. How deep do I need to go on each topic?**
Breadth over depth for most of it — you should be able to *name and justify* a choice (SQL vs NoSQL, cache pattern, LB strategy) in one or two sentences, then go deep only where the interviewer pulls you. Depth expectations scale with level and role (see the Chapter 1 role-depth self-assessment). Staff/infra candidates get grilled on consensus, quorums, and failure modes; ML-leaning candidates need enough to not get stuck.

**3. Do I really need to memorize latency and power-of-2 numbers?**
Yes, a handful. "L1 ~1 ns, memory ~100 ns, SSD ~100 µs, cross-datacenter round trip ~500 µs–150 ms," and 2^10≈1K / 2^20≈1M / 2^30≈1B. You won't be quizzed on them directly, but using them fluently during estimation signals seniority. See the estimation drills and Chapter 5.

## Data storage

**4. SQL vs NoSQL — how do I decide fast without overthinking?**
Ask two questions: *Do I need multi-row ACID transactions/joins?* → SQL. *Do I need massive write throughput, flexible schema, or horizontal scale over strict consistency?* → NoSQL. Then match the access pattern (key-value, document, wide-column, columnar for analytics, vector for embeddings, graph for relationships). Say the access pattern out loud — that's what interviewers grade.

**5. When do I actually need a vector database vs just adding a column?**
Only when you're doing similarity/semantic search over embeddings at scale (RAG, semantic dedup, recommendations). For a few thousand vectors, a library index or `pgvector` is plenty. Reach for a dedicated vector DB (Milvus/Qdrant/Pinecone) when you're at millions+ vectors and need ANN performance and sharding.

**6. When should I bring up sharding, and by what key?**
Bring it up when writes or storage exceed a single node (your estimate shows it). Pick a key with high cardinality and even distribution that matches your dominant query (e.g., `user_id`). Then immediately acknowledge the cost: cross-shard queries and transactions get hard. Naming that trade-off is the point.

## Caching

**7. Which caching pattern is the "right" one?**
There's no universal winner; state the trade-off. **Cache-aside** is the safe default (resilient, but first-read misses). **Write-through** keeps the cache fresh at the cost of write latency. **Write-behind** maximizes write throughput but risks loss on crash. Then always mention an **invalidation** strategy (TTL / event-driven / versioning) — forgetting invalidation is the classic miss.

**8. What's a cache stampede and do I need to mention it?**
It's when a hot key expires and thousands of requests miss simultaneously, hammering the DB. Worth a sentence in any read-heavy design: mitigate with jittered TTLs, request coalescing, or leases. It's an easy way to show production maturity.

## Reliability & trade-offs

**9. Do interviewers actually expect the CAP theorem?**
Yes — but use it as a *decision tool*, not a definition to recite. Say: "During a partition this is CP because stale balances are unacceptable (fraud), so we sacrifice availability," or "AP here because a slightly stale feed is fine." Mentioning PACELC (latency vs consistency even without a partition) is a nice level-up.

**10. How much consensus (Raft/Paxos) do I need to know?**
Know *what* it does (nodes agree on a replicated log despite failures, needs a majority/quorum) and *where* it lives (etcd, ZooKeeper, Spanner, leader election). You rarely need to derive the protocol unless you're interviewing for an infra/database role. Don't volunteer to implement Paxos on a whiteboard.

**11. When do RPO/RTO come up, and what do I say?**
Whenever reliability/DR is in scope (payments, healthcare, anything "mission-critical"). Connect them to concrete mechanisms: tighter **RPO** → more frequent or synchronous replication; tighter **RTO** → active-passive/active-active + automated failover + runbooks. Giving a number ("RPO 5 min, RTO 15 min") shows you understand the cost dial.

## Architecture & communication

**12. Monolith or microservices — what's the expected answer?**
"It depends, and I'd start simpler." A modular monolith is often the mature choice; split into microservices once you've found the real bottlenecks and the org needs independent deploys. Jumping straight to microservices without justifying the operational tax is a red flag.

**13. REST or gRPC for model serving?**
gRPC for internal, low-latency, high-throughput service-to-service calls (binary, HTTP/2, streaming) — great for inference microservices. REST/JSON for public APIs and broad compatibility. GraphQL when clients need flexible, aggregated queries. Say why, don't just name one.

**14. Message queue or event stream — which do I reach for?**
Queue when you're handing off discrete tasks to workers and can delete after processing (SQS, RabbitMQ). Stream when you need a replayable log, multiple independent consumers, or analytics/feature pipelines (Kafka). For ML feature ingestion and feedback loops, it's almost always a stream.

## Method & delivery

**15. Should I compute exact numbers or estimate?**
Estimate, out loud, with stated assumptions, and round hard ("~100K QPS", "~4 TB"). The method and the *design consequence* of the number matter far more than precision. Then connect it: "100K read QPS → I'll add read replicas and a cache."

**16. How much security and compliance should I mention unprompted?**
A quick pass shows maturity: authN/authZ (OAuth/JWT/mTLS, RBAC, least privilege), encryption in transit, rate limiting, and a nod to GDPR/CCPA when personal data is involved. Go deep only if asked or if it's a security-sensitive domain. For LLM systems, mention prompt injection and output handling.
