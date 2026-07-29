# Chapter 3 — Core Distributed Systems Concepts

Companion resources for Chapter 3. Maintained here (not in the printed book) so they can be kept current.

Chapter 3 is the distributed-systems foundation every AI system design round assumes: scaling & capacity, storage selection, caching, networking, messaging, reliability (CAP/PACELC, replication, DR), observability, and security.

| File | What it is |
|------|------------|
| [`estimation-drills.md`](./estimation-drills.md) | 10 back-of-the-envelope drills (QPS, storage, bandwidth, cache sizing, capacity, sharding, streaming) with stated assumptions, verified arithmetic, and the design decision each number drives. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated blog/paper index on sharding, replication & consistency, load balancing at scale, caching, consensus/CAP, streaming, reliability, and observability — with role-specific starting picks. |
| [`key-terms.md`](./key-terms.md) | Chapter 3 glossary slice (P50/P95/P99, quorum, RPO/RTO, consistent hashing, CAP/PACELC, sharding, cache patterns, …). Feeds the cumulative book glossary. |
| [`common-doubts.md`](./common-doubts.md) | Answers to the questions candidates most often have — SQL vs NoSQL, when to shard, CAP in practice, monolith vs microservices, how much security to mention. |

> **Note on links:** external company blogs move their URLs often. If a deep link is dead, search the post title on the linked blog root, or open an issue/PR.
