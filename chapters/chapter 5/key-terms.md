# Key Terms — Chapter 5 (Back-of-the-Envelope Estimation)

Interview-oriented definitions for the estimation vocabulary in Chapter 5. Each pairs a crisp definition with *why it matters* in a design round. Terms defined earlier (QPS, latency percentiles, sharding) are cross-referenced. Feeds the cumulative book glossary.

---

### Traffic & capacity
- **DAU (Daily Active Users)** — Unique users active in a day. *Why it matters:* the starting point of nearly every traffic estimate.
- **Peak multiplier (peak-to-average ratio)** — Factor from average to peak load (2–3× consumer, 5–10× e-commerce events, 10–20× breaking news). *Why it matters:* systems must be sized for peak, not average; state which multiplier and why.
- **Requests per user per day** — Actions a user triggers daily. *Why it matters:* the assumption that turns DAU into daily request volume; justify it out loud.
- **Little's Law** — `concurrency = arrival rate × latency`. *Why it matters:* converts QPS + latency into in-flight requests, which sizes threads/GPUs.
- **Headroom / N+1 redundancy** — Extra capacity (≈1.5×) plus a spare node. *Why it matters:* absorbs spikes and survives a single failure.

### Storage
- **Replication factor** — Number of data copies (typically 2–3×). *Why it matters:* multiplies raw storage; ties to durability and RPO.
- **Retention** — How long data is kept (hot 30–90 days, warm 1–3 yr, cold 7+ yr). *Why it matters:* often the true storage driver; shortening it is a lever.
- **Growth projection** — 1-yr (+20–50%), 3-yr (2–3×), 5-yr (5–10×). *Why it matters:* capacity plans should survive expected growth without redesign.

### Compute & FLOPs
- **FLOPs (floating-point operations)** — Total arithmetic work; training ≈ `6 × params × tokens`. *Why it matters:* the basis for training time and cost estimates. (Not to be confused with FLOP/s, a *rate*.)
- **TFLOPS (tera-FLOP/s)** — Trillions of FLOP per second a GPU can do. *Why it matters:* the denominator in GPU-hour math; use *effective* (~30–50% of peak), not peak.
- **MFU (Model FLOPs Utilization)** — Fraction of peak FLOP/s actually achieved. *Why it matters:* explains why "effective TFLOPS" is far below the datasheet number.
- **Arithmetic intensity** — FLOPs performed per byte moved from memory. *Why it matters:* decides whether a workload is **compute-bound** or **memory-bound**; LLM decoding is memory-bound (KV cache traffic), which is why batching and paged attention help.
- **Spot / preemptible instance** — Discounted (60–70%) interruptible cloud VM. *Why it matters:* great for fault-tolerant batch training/inference; unsafe for latency-critical online serving.

### GPU memory & LLM serving
- **Bytes per parameter** — FP32=4, FP16/BF16=2, FP8/INT8=1, INT4=0.5. *Why it matters:* precision choice directly scales model memory and how many GPUs you need.
- **Overhead multiplier** — ×1.2–1.5 (inference) or +20–30% (training optimizer states) on raw weight memory. *Why it matters:* raw `params × bytes` under-counts real VRAM.
- **KV cache** — Cached key/value tensors for prior tokens; ≈`8 × layers × hidden` bytes/token (fp16). *Why it matters:* grows with batch × context and often exceeds weight memory — the real cap on serving throughput.
- **Prefill vs decode** — Processing the prompt (parallel, compute-heavy) vs generating tokens one at a time (sequential, memory-bound). *Why it matters:* prefill drives TTFT; decode drives TPS.
- **TTFT (Time-to-First-Token)** — Delay before the first output token. *Why it matters:* dominates *perceived* responsiveness in chat; set by prefill + queueing.
- **TPS (Tokens-per-Second)** — Post-first-token generation rate. *Why it matters:* determines streaming smoothness and how many concurrent streams a GPU sustains.
- **Continuous batching** — Admitting new requests as others finish, instead of fixed batches. *Why it matters:* raises GPU utilization and concurrent streams/GPU (20–50), slashing GPU count.
- **HBM (High-Bandwidth Memory)** — On-package GPU VRAM (e.g., 80 GB on A100/H100). *Why it matters:* the hard limit weights + KV cache must fit within.

### Embeddings & vector storage
- **Embedding storage** — `dim × count × bytes/dim`. *Why it matters:* at 1 TB+ you need a dedicated, sharded vector DB.
- **HNSW index overhead** — ANN index adds ≈1.5× over raw vectors. *Why it matters:* don't forget it when sizing RAM/disk.
- **Vector quantization** — Storing vectors at lower precision (fp32→int8). *Why it matters:* cuts storage ~4×; validate recall impact.

### Latency
- **Inference latency components** — network + preprocessing + model inference + postprocessing. *Why it matters:* break the SLA into a budget to show where time goes.
- **Latency budget** — Allocating the total SLA across stages (e.g., 20 ms net + 10 ms pre + 160 ms model). *Why it matters:* a concrete budget signals production awareness and bounds model/agent complexity.

---

*Cross-refs:* QPS, latency percentiles (P50/P95/P99), sharding, caching, CDN → Chapter 3. Feature store, embeddings, quantization/distillation, drift → Chapter 4. LLM serving optimizations (paged attention, speculative decoding) → Chapter 6.
