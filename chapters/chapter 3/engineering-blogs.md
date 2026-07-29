# Engineering-Blog Index — Distributed Systems at Scale

Curated reading on the Chapter 3 building blocks: **sharding, replication & consistency, load balancing, caching, consensus/CAP, streaming, reliability, and observability**. These are the systems whose real-world write-ups interviewers love to hear referenced.

> **Link maintenance:** company blogs restructure URLs often. If a deep link 404s, search the post title on the linked blog root or your search engine. Papers are cited by title (durably findable). Last reviewed: 2026.

---

## Sharding & partitioning
- **Instagram — Sharding IDs at Instagram** — how they generate sortable, shard-aware 64-bit IDs. → https://instagram-engineering.com/
- **Notion — Sharding Postgres** — the "why and how" of moving a monolithic Postgres to shards. → https://www.notion.so/blog/sharding-postgres-at-notion
- **Discord — How Discord stores trillions of messages** — Cassandra → ScyllaDB partitioning story. → https://discord.com/blog/how-discord-stores-trillions-of-messages
- **Vitess** — horizontal sharding layer for MySQL (born at YouTube). → https://vitess.io/docs/
- **Figma — How Figma's databases team lived to tell the scale** — sharding Postgres in production. → https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/

## Replication, consistency & consensus
- **Amazon — Dynamo: Amazon's Highly Available Key-value Store** (2007) — the AP/eventual-consistency classic. → search "Dynamo paper Amazon"
- **Google — Spanner: Google's Globally-Distributed Database** — externally consistent global transactions (TrueTime). → search "Spanner paper Google"
- **Raft — In Search of an Understandable Consensus Algorithm** (Ongaro & Ousterhout) + interactive viz. → https://raft.github.io/
- **Leslie Lamport — Paxos Made Simple** — the foundational consensus paper. → search "Paxos Made Simple"
- **Jepsen (Kyle Kingsbury)** — adversarial consistency testing of real databases; superb for understanding failure modes. → https://jepsen.io/analyses
- **Kleppmann — *Designing Data-Intensive Applications*** — the single best reference for this entire chapter. → https://dataintensive.net/

## Load balancing at scale
- **Google — Maglev: A Fast and Reliable Software Network Load Balancer** — L4 LB with consistent hashing. → search "Maglev paper Google"
- **Envoy Proxy** — modern L7 proxy/service-mesh data plane; docs explain retries, circuit breaking, outlier detection. → https://www.envoyproxy.io/docs
- **Cloudflare blog** — global load balancing, anycast, and traffic steering write-ups. → https://blog.cloudflare.com/tag/load-balancing/

## Caching
- **Facebook — Scaling Memcache at Facebook** (NSDI) — the definitive large-scale caching paper (lease-based stampede control, regional pools). → search "Scaling Memcache at Facebook"
- **Netflix — EVCache** — distributed caching tier for the streaming stack. → https://netflixtechblog.com/
- **Redis — docs on clustering, eviction & persistence** — hash slots, replication, TTL. → https://redis.io/docs/

## CAP / trade-off framing
- **Eric Brewer — CAP Twelve Years Later: How the "Rules" Have Changed** (IEEE). → search "CAP twelve years later Brewer"
- **Daniel Abadi — Consistency Tradeoffs in Modern Distributed Database System Design (PACELC)**. → search "PACELC Abadi paper"

## Message queues & event streaming
- **Apache Kafka documentation** — partitions, replication, delivery semantics, retention. → https://kafka.apache.org/documentation/
- **LinkedIn — The Log: What every software engineer should know about real-time data's unifying abstraction** (Jay Kreps). → search "The Log Jay Kreps LinkedIn"
- **Uber — enabling seamless Kafka async queuing / trillions of messages** — streaming at scale. → https://www.uber.com/en-US/blog/engineering/

## Reliability, DR & chaos engineering
- **Netflix — Principles of Chaos Engineering** + Chaos Monkey. → https://principlesofchaos.org/
- **AWS — Fault Injection Service docs** — controlled failure experiments. → https://docs.aws.amazon.com/fis/
- **Google — Site Reliability Engineering (free book)** — SLIs/SLOs/SLAs, error budgets, DR patterns. → https://sre.google/books/

## Observability
- **Google SRE Workbook — Monitoring & Alerting chapters** — the four golden signals. → https://sre.google/workbook/
- **OpenTelemetry docs** — traces/metrics/logs standard used across microservices. → https://opentelemetry.io/docs/

---

### Role-specific starting picks
| If you're interviewing as… | Read first |
|---|---|
| **Backend / platform SWE** | DDIA (Kleppmann), Scaling Memcache, Kafka docs |
| **ML / MLOps engineer** | DDIA (Ch. on replication & stream processing), Redis clustering, SRE book |
| **Infra / SRE** | Google SRE book, Maglev, Principles of Chaos, Jepsen |
| **Senior / staff (breadth)** | Dynamo + Spanner (the AP vs CP contrast), PACELC, CAP-twelve-years-later |
