# Expanded Estimation Drill Bank

**29 back-of-the-envelope problems with worked solutions**, extending the 6 worked examples in Chapter 5. Grouped by type: traffic/QPS, storage, bandwidth, GPU memory, KV cache, embeddings/vector DB, training cost, and latency/concurrency.

Every calculation here was verified numerically. But the point is the *method*: state assumptions → apply the formula → round hard → say what the number means for the design.

> **Formulas & reference numbers used** (from Chapter 5):
> - **QPS** = `DAU × requests/user/day ÷ 86,400`, then × peak multiplier (2–3× consumer, 5–10× e-commerce spikes, 10–20× news).
> - **Storage** = `records × bytes/record × replication` (+ overhead).
> - **Bandwidth** = `QPS × payload`; ×8 for bits/s.
> - **GPU model memory (inference)** ≈ `params × bytes/param × 1.5`. Bytes/param: FP32=4, FP16/BF16=2, INT8=1, INT4=0.5.
> - **KV cache/token (fp16)** ≈ `8 × Layers × Hidden` bytes ⇒ 7B≈1 GB, 13B≈1.6 GB, 70B≈5 GB **per 1,000 tokens**.
> - **Embedding storage** = `dim × count × bytes/dim` (fp32=4, fp16=2, int8=1). HNSW index ≈ ×1.5.
> - **Training FLOPs** ≈ `6 × params × tokens × epochs`; **GPU-hours** = `FLOPs ÷ (effective TFLOPS × 1e12 × 3600)`; **cost** = GPU-hours × $/GPU-hr × #GPUs.
> - **Concurrency (Little's Law)** = `QPS × latency (s)`. GPU A100 ≈300 eff. TFLOPS, H100 ≈400 eff. TFLOPS; A100 ≈$3.50/hr, H100 ≈$2/hr (rough). Storage uses decimal (1 TB = 1e12 B).

---

## A. Traffic & QPS

**A1 — Video platform.** 800M DAU · 8 views/user/day · peak 3×.
`800M×8 = 6.4B/day; ÷86,400 ≈ 74K avg; ×3 ≈ 220K peak QPS.`
→ **~220K QPS.** Over 100K ⇒ CDN + aggressive caching + sharded metadata store.

**A2 — Messaging app (writes).** 500M DAU · 40 messages sent/user/day · peak 4×.
`500M×40 = 20B/day; ÷86,400 ≈ 231K avg; ×4 ≈ 900K write QPS.`
→ **~900K write QPS.** Partition by conversation/user; buffer with a message queue; async fan-out.

**A3 — E-commerce flash sale.** 100M DAU · 5 req/user/day baseline · 10× event spike.
`100M×5 = 500M/day; ÷86,400 ≈ 5.8K avg; ×10 ≈ 58K peak QPS.`
→ **~58K QPS.** Pre-warm capacity, autoscale early, queue checkout writes; don't size for average.

**A4 — Enterprise RAG chatbot (work-hours concentration).** 50K employees · 20 queries/day, concentrated in an 8-hour window · peak 3×.
`50K×20 = 1M/day; ÷(8×3,600) ≈ 35 avg; ×3 ≈ 104 QPS.`
→ **~100 QPS.** Sits in the 100–1K band where the **latency budget** (retrieve + rerank + LLM), not throughput, is the design driver.

**A5 — Agentic assistant fan-out.** 200K user requests/day · each fans out to 10 LLM calls · peak 3×.
`User peak ≈ 200K/86,400×3 ≈ 7 QPS. LLM calls = 2M/day; ÷86,400 ≈ 23 avg; ×3 ≈ 70 LLM QPS.`
→ **~70 LLM QPS vs ~7 user QPS.** Size capacity (and cost) on **LLM QPS**, not user QPS; add caching and step limits.

---

## B. Storage

**B1 — Tweet store, 1 year.** 500M tweets/day · ~1.3 KB each (text + metadata) · replication 3×.
`500M×1.3KB = 650 GB/day; ×365 ≈ 237 TB/yr; ×3 ≈ 712 TB ≈ 0.7 PB.`
→ **~0.7 PB/yr.** Shard by time/user; tier past the hot window.

**B2 — Feature store.** 200M users · 800 features × 8 B · replication 2× · +20% overhead.
`800×8 = 6.4 KB/user; ×200M = 1.28 TB; ×2 = 2.56 TB; ×1.2 ≈ 3 TB.`
→ **~3 TB.** Fits a modest online store; watch freshness/serving latency, not size.

**B3 — Chat-history logs.** 10M DAU · 20 conversations × 10 turns/day · ~2 KB/turn · 90-day hot retention.
`Turns/day = 10M×20×10 = 2B; ×2 KB = 4 TB/day; ×90 ≈ 360 TB.`
→ **~360 TB hot.** Retention is the driver — archive to cold storage after 90 days.

**B4 — Model-checkpoint storage.** 70B params · FP16 (2 B) · keep 10 versions (weights only).
`70B×2 = 140 GB/checkpoint; ×10 = 1.4 TB.`
→ **~1.4 TB.** Object storage; full training checkpoints (with optimizer state) are ~2–3× larger.

---

## C. Bandwidth

**C1 — Feed egress.** 200K peak QPS · 25 items × 1 KB = 25 KB/response.
`200K×25KB = 5 GB/s; ×8 = 40 Gbps.`
→ **~40 Gbps.** Offload media to CDN, compress payloads; raw origin egress is costly.

**C2 — Video streaming.** 100K concurrent streams · 5 Mbps each.
`100K×5 Mbps = 500 Gbps = 0.5 Tbps.`
→ **~0.5 Tbps.** CDN is mandatory; adaptive bitrate to control it.

**C3 — LLM text streaming egress.** 280K concurrent decode streams · 50 tok/s · ~4 B/token.
`280K×50 = 14M tok/s; ×4 B = 56 MB/s ≈ 0.45 Gbps.`
→ **~56 MB/s (negligible).** Teaching point: for text LLMs, **GPU compute is the constraint, not bandwidth**.

---

## D. GPU memory & serving

**D1 — Serve 70B in FP16.** `70B×2 = 140 GB; ×1.5 = 210 GB.`
→ **210 GB ⇒ 3× 80 GB GPUs** (before KV cache — which pushes it higher).

**D2 — Serve 13B in INT8.** `13B×1 = 13 GB; ×1.5 ≈ 20 GB.`
→ **~20 GB ⇒ fits a single 24 GB GPU.**

**D3 — Will 7B fit a 16 GB GPU?** FP16: `7B×2×1.5 = 21 GB` → **no.** INT4: `7B×0.5×1.5 ≈ 5.25 GB` → **yes**, with room for KV cache.
→ Quantization is what makes edge/consumer-GPU serving feasible.

**D4 — Serve 405B in FP16.** `405B×2 = 810 GB; ×1.5 ≈ 1,215 GB; ÷80 ≈ 15.2.`
→ **16× 80 GB GPUs (2 nodes)** with tensor/pipeline parallelism.

---

## E. KV cache

**E1 — 70B at 8K context, batch 32 (fp16).** `5 GB/1K tokens × 8 = 40 GB/request; ×32 = 1,280 GB.`
→ **1.28 TB of KV cache** — dwarfs the 140 GB of weights. KV cache, not weights, caps batch size ⇒ paged attention, KV quantization, shorter context.

**E2 — Concurrency in a 40 GB KV budget (7B, 2K context).** `1 GB/1K × 2 = 2 GB/request; 40 ÷ 2 = 20.`
→ **~20 concurrent requests** per GPU's KV budget.

**E3 — KV/token for a custom model** (48 layers, hidden 6,144, fp16). `8 × 48 × 6,144 = 2,359,296 B ≈ 2.36 MB/token.`
→ **~2.36 GB per 1,000 tokens.** Deeper/wider ⇒ linearly more KV.

---

## F. Embeddings & vector DB

**F1 — 500M docs, 1536-dim, float32.** `1536×4 = 6 KB/vec; ×500M ≈ 3.07 TB raw; ×1.5 index ≈ 4.6 TB.`
→ **~4.6 TB** ⇒ dedicated, sharded vector DB.

**F2 — Same corpus, INT8-quantized.** `1536×1 = 1.5 KB/vec; ×500M = 768 GB raw; ×1.5 ≈ 1.15 TB.`
→ **~1.15 TB** — quantization cuts vector storage 4×; validate recall impact.

**F3 — Shard 1B docs (768-dim fp32) at ≤400 GB/shard.** `768×4×1B = 3.07 TB raw; ×1.5 = 4.6 TB; ÷400 GB ≈ 11.5.`
→ **12 shards.**

---

## G. Training FLOPs, time & cost

**G1 — Pretrain compute, 7B on 1T tokens.** `6 × 7B × 1e12 = 4.2e22 FLOPs.`
→ **~4.2×10²² FLOPs.**

**G2 — GPU-hours for G1** on H100s at 400 effective TFLOPS. `4.2e22 ÷ (400e12×3600) ≈ 29,200 GPU-hours; ÷512 GPUs ≈ 57 hours (~2.4 days).`
→ **~29K GPU-hours ⇒ ~2.4 days on 512 H100s.**

**G3 — Cloud cost for G2** at ~$2/GPU-hr. `29,200 × $2 ≈ $58K.`
→ **~$58K** (spot instances 60–70% cheaper if interruption-tolerant).

**G4 — LoRA fine-tune 13B**, 5M tokens, 3 epochs, A100 @300 eff. TFLOPS, $3.50/hr. `FLOPs = 6×13B×5M×3 = 1.17e18` (the forward pass runs the **full** 13B even under LoRA); `÷ (300e12×3600) ≈ 1.08 GPU-hr; × $3.50 ≈ $4.`
→ **~1 GPU-hour, ~$4.** LoRA saves *memory*, not forward-pass FLOPs.

---

## H. Latency & concurrency

**H1 — Ranking GPUs.** 60K peak QPS · p99 40 ms · 300 QPS/GPU. `60K÷300 = 200; ×1.5 headroom ≈ 300 GPUs.` Little's Law: `60K×0.04 = 2,400 concurrent`.
→ **~300 GPUs.**

**H2 — LLM serving GPUs.** 70K turn QPS · 200 tokens @ 50 tok/s = 4 s/stream · 40 concurrent/GPU (continuous batching). `Concurrent = 70K×4 = 280K; ÷40 = 7,000 GPUs.`
→ **~7,000 GPUs** (matches the Ch. 5 chatbot example's 6K–14K range; batch efficiency dominates cost).

**H3 — Latency-budget split.** SLA 200 ms; network 20 + preprocess 10 + postprocess 10 = 40 ms overhead ⇒ **160 ms model budget**. A 3-step agent at 50 ms/call = 150 ms.
→ **Fits (150 < 160 ms)**, but with almost no margin — cut a step or speed up inference.

---

### Using this bank
- Cover the solution, solve aloud, then check.
- For every answer, end with the **design consequence** (cache, shard, quantize, add GPUs, change the approach).
- Interactive versions of the AI-specific formulas (GPU memory, KV cache, embedding storage, training cost) are in [`estimation-calculators.ipynb`](./estimation-calculators.ipynb); the one-page number card is in [`reference-card.md`](./reference-card.md).
