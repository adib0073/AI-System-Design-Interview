# Distributed-Systems Estimation Drills

Ten back-of-the-envelope drills covering **QPS, storage, bandwidth, cache sizing, capacity, sharding, and streaming** — the estimates that anchor a distributed-systems design. Each drill has stated assumptions, worked arithmetic, a rounded answer, and the design decision the number drives.

> **Conventions used** (consistent with Chapters 3 and 5):
> - **DAU → QPS:** `QPS = (DAU × requests per user per day) / 86,400`, then apply a **peak multiplier** (2–5×; 3× for typical consumer apps).
> - **Storage:** `records × bytes per record × replication factor` (+ overhead for indexes/metadata).
> - **Bandwidth:** `QPS × payload size`; multiply bytes/s by 8 for bits/s.
> - **Concurrency (Little's Law):** `in-flight requests = QPS × latency (s)`.
> - **Servers/instances:** `peak QPS / per-instance QPS`, then add headroom (≈1.5×) and N+1 redundancy.
> - Powers used: 2^10 ≈ 1K, 2^20 ≈ 1M, 2^30 ≈ 1B. Storage uses decimal (1 TB = 1,000 GB) to match the book's rounding.
> - Reference sizes: tweet ≈ 280 B · user profile 1–2 KB · thumbnail 10–50 KB · full image 0.1–5 MB · 768-dim float32 embedding ≈ 3 KB.
>
> Round aggressively — the method matters more than the exact digits.

---

## Drill 1 — Peak QPS for a read-heavy social app
**Problem:** Estimate peak read and write QPS.
**Assumptions:** 200M DAU · 15 requests/user/day · read:write = 95:5 · peak = 3× average.
**Work:**
- Daily requests = 200M × 15 = **3B/day**
- Average QPS = 3B / 86,400 ≈ **34,700**
- Peak QPS = 34,700 × 3 ≈ **104,000 ≈ 100K**
- Reads = 95% × 105K ≈ **100K read QPS**; writes = 5% × 105K ≈ **5K write QPS**
**Answer:** ~100K peak read QPS, ~5K peak write QPS.
**Design implication:** 100K reads → aggressive caching + read replicas + horizontal scaling; 5K writes may still fit a single primary, but plan a sharding key early.

## Drill 2 — App-server count (capacity planning)
**Problem:** How many stateless app servers for the 100K peak QPS above?
**Assumptions:** one instance sustains ~500 QPS at the target p99.
**Work:**
- Base instances = 100,000 / 500 = **200**
- Add 1.5× spike headroom → 300; add N+1 redundancy → **~300 instances**
- Sanity check via Little's Law at 40 ms latency: in-flight = 100,000 × 0.04 = 4,000 concurrent requests spread across the fleet (~13/instance) — comfortable.
**Answer:** ~300 stateless instances behind a load balancer.
**Design implication:** stateless servers + LB enable horizontal scaling and fault tolerance; autoscale on QPS/latency, not just CPU.

## Drill 3 — Storage for text posts (with replication)
**Problem:** One year of posts.
**Assumptions:** 1B posts/year · 1 KB each (text + metadata) · replication 3× · +25% for indexes/overhead.
**Work:**
- Raw = 1B × 1 KB = **1 TB**
- × replication 3 = **3 TB**
- × 1.25 overhead = **3.75 TB ≈ 4 TB/year**
**Answer:** ~4 TB per year.
**Design implication:** shard by `user_id` or time bucket; move data past its hot-retention window (30–90 days) to warm/cold tiers.

## Drill 4 — Media storage for a photo app (object storage + growth)
**Problem:** Annual storage for uploaded photos.
**Assumptions:** 10M photos/day · 2 MB full-res + 50 KB thumbnail ≈ 2.05 MB/photo · 2 copies · object storage.
**Work:**
- Daily = 10M × 2.05 MB ≈ **20.5 TB/day**
- Yearly (×365) ≈ **7.5 PB/year** (single copy)
- × 2 copies ≈ **~15 PB/year**
**Answer:** ~7.5 PB/year raw, ~15 PB with replication.
**Design implication:** this belongs in blob storage (S3/GCS), not a database; front it with a CDN and apply lifecycle policies (infrequent-access → archive).

## Drill 5 — Egress bandwidth for a feed service
**Problem:** Peak network egress from the serving tier.
**Assumptions:** 100K peak QPS · each response returns 20 items × 1 KB = 20 KB.
**Work:**
- Egress = 100,000 × 20 KB = **2,000,000 KB/s = 2 GB/s**
- In bits: 2 GB/s × 8 = **16 Gbps**
**Answer:** ~2 GB/s (~16 Gbps) at peak.
**Design implication:** offload media to a CDN, compress payloads (gzip/Protobuf), and consider regional PoPs; raw origin egress at 16 Gbps is expensive.

## Drill 6 — Prediction-cache sizing (hot users)
**Problem:** Size a Redis cache holding precomputed top-N recommendations.
**Assumptions:** 30M users active within a 10-min window · entry = 20 item IDs × 8 B = 160 B → ~250 B with keys/overhead.
**Work:**
- Memory = 30M × 250 B = **7.5 GB**
- × ~1.5 Redis overhead ≈ **~11 GB**
**Answer:** ~11 GB — fits on one large Redis node (with a replica) or a small cluster.
**Design implication:** TTL 5–10 min, LRU eviction; guard against **cache stampede** on popular-key expiry (request coalescing / jittered TTL).

## Drill 7 — Feature/embedding cache + hit-rate effect
**Problem:** Size an embedding cache and quantify backend relief.
**Assumptions:** 5M hot items · 768-dim float32 embedding = 768 × 4 B ≈ 3 KB each · target hit rate 90% · 100K feature-lookup QPS.
**Work:**
- Memory = 5M × 3 KB = **15 GB** (× ~1.3 overhead ≈ 20 GB)
- Backend miss traffic = 100K × (1 − 0.90) = **10K QPS** hits the feature store
**Answer:** ~20 GB cache cuts feature-store load 10× (100K → 10K QPS).
**Design implication:** a hit-rate assumption is load-bearing — a 90% vs 99% hit rate changes downstream sizing by 10×; monitor it explicitly.

## Drill 8 — Read replicas & write sharding from QPS
**Problem:** How many DB replicas/shards for Drill 1's traffic?
**Assumptions:** one node serves 5K read QPS or 2K write QPS at target latency.
**Work:**
- Read replicas = 100K / 5K = **20** (+ primary) → ~30 with headroom
- Write shards = 5K / 2K = 2.5 → **3 shards**
**Answer:** ~20–30 read replicas; 3 write shards.
**Design implication:** replicas scale reads but add replication lag (eventual consistency on reads); sharding scales writes but complicates cross-shard queries/transactions.

## Drill 9 — Event-stream throughput & retention storage
**Problem:** Size a Kafka clickstream topic.
**Assumptions:** 100K events/s peak · 500 B/event · retain 7 days · replication 3×.
**Work:**
- Ingest = 100K × 500 B = **50 MB/s** (× 8 = 400 Mbps)
- 7-day storage = 50 MB/s × 86,400 × 7 ≈ **30 TB** (single copy)
- × 3 replication ≈ **~90 TB**
**Answer:** ~50 MB/s ingest, ~90 TB retained.
**Design implication:** partition count ≈ throughput ÷ per-partition throughput (and consumer parallelism); retention is the storage driver — shorten it or tier to a data lake.

## Drill 10 — Real-time inference serving tier
**Problem:** How many GPU servers for a real-time model?
**Assumptions:** 20K peak QPS · p99 model latency 40 ms · one GPU server sustains 200 QPS at p99.
**Work:**
- Base servers = 20,000 / 200 = **100**
- Little's Law check: in-flight = 20,000 × 0.04 = **800 concurrent** (~8/server) — fine
- Add 1.5× headroom + N+1 → **~150 GPU servers**
**Answer:** ~150 GPU servers.
**Design implication:** GPUs are the cost driver — autoscale on GPU utilization/queue depth (HPA on CPU misses this); consider batching and a fallback to a lighter model under load.

---

### How to use these in an interview
1. **State assumptions first** ("I'll assume 200M DAU, 15 req/user/day").
2. **Show the formula**, then plug in — narrate the arithmetic.
3. **Round hard** ("~100K QPS", "~4 TB").
4. **End with the design consequence** — the number is only useful if it changes a decision (cache, shard, replicate, add GPUs).

*More AI-specific drills (GPU memory, KV cache, training cost, embedding storage) live in the Chapter 5 companion.*
