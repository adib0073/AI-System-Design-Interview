# Infrastructure Estimation Drills

Eight drills that **bridge Chapter 5 (estimation) and Chapter 8 (infrastructure at scale)**: cluster sizing for training, GPU-hours & cost, the 3D-parallelism split, training memory (why data-parallel alone fails), and inference-fleet sizing for models and agents. All arithmetic verified.

> **Formulas & reference numbers** (from Ch. 5 + Ch. 8):
> - **Training FLOPs** ≈ `6 × params × tokens × epochs`.
> - **GPU-hours** = `FLOPs ÷ (effective TFLOPS × 1e12 × 3600)`; **GPUs for a deadline** = `GPU-hours ÷ wall-clock hours`.
> - **Training memory rule of thumb** ≈ **~16 bytes/param** (fp16 weights + fp16 grads + fp32 Adam m/v ≈ 2+2+4+4+…). Inference ≈ `params × bytes × 1.5` (Ch. 5).
> - **3D parallelism:** `total GPUs = DP × TP × PP`. Keep **TP within a node** (NVLink), **PP across nodes**, **DP** for the rest.
> - **Concurrency** = `QPS × latency (s)`; **replicas** = `concurrent ÷ concurrent-per-replica`; a large model's *replica* may span several GPUs.
> - Effective throughput: A100 ≈300 TFLOPS, H100 ≈400 TFLOPS (30–50% of peak). Cost: H100 ≈ $2/GPU-hr; spot ≈ 60–70% cheaper. Decimal units (1 TB = 1e12).

---

## D1 — Cluster size to train within a deadline
**Problem:** Train a 70B model on 2T tokens in **30 days**. GPUs?
**Assumptions:** H100 @ ~400 effective TFLOPS.
`FLOPs = 6 × 70B × 2e12 = 8.4e23.`
`GPU-hours = 8.4e23 ÷ (400e12 × 3600) ≈ 583,000.`
`30 days = 720 h ⇒ 583,000 ÷ 720 ≈ 810 GPUs.`
→ **~800–1,000 GPUs** (add MFU margin). ⇒ multi-node 3D parallelism + checkpointing to object storage for preemption recovery.

## D2 — The 3D-parallelism split
**Problem:** You're given **512 GPUs** (8 per node, NVLink within node). Split into DP × TP × PP.
**Assumptions:** the model layer needs **TP=8** (fits within one node over NVLink); pipeline **PP=4** across nodes.
`DP = 512 ÷ (TP × PP) = 512 ÷ (8 × 4) = 16.`
→ **DP=16, TP=8, PP=4.** TP stays intra-node (high bandwidth), PP spans nodes, DP replicates the rest. Global batch = micro-batch × DP × grad-accumulation.

## D3 — Training memory: why data-parallel alone fails
**Problem:** Can a 70B model train with plain data parallelism on 80 GB GPUs?
`Training state ≈ 70B × 16 B/param = 1,120 GB.`
`÷ 80 GB ≈ 14 GPUs just to *hold* one replica.`
→ A DP replica must fit the **whole** model+optimizer — it doesn't (needs ~14 GPUs). So you **shard** state (FSDP / DeepSpeed ZeRO) or use **model/pipeline parallelism**. This is the classic "why not just data-parallel?" answer.

## D4 — Training cost (and spot savings)
**Problem:** Cloud cost for D1.
`583,000 GPU-hours × $2/GPU-hr ≈ $1.17M on-demand.`
`Spot/preemptible (~70% off) ≈ $350K` (viable because we checkpoint).
→ **~$1.2M on-demand, ~$350K on spot.** Checkpointing is what unlocks the spot discount.

## D5 — LLM inference fleet
**Problem:** Serve the 70B model at **20K peak QPS** of chat turns, 200 output tokens @ 40 tok/s.
`Time per stream = 200 ÷ 40 = 5 s. Concurrency = 20K × 5 = 100K streams.`
`At 30 concurrent/replica ⇒ 100K ÷ 30 ≈ 3,333 replicas.`
`Each 70B replica ≈ 3× 80 GB GPUs (FP16, Ch. 5) ⇒ 3,333 × 3 ≈ 10,000 GPUs.`
→ **~10,000 GPUs.** Enormous ⇒ push back with quantization, a smaller model, model routing/cascades, KV-cache-aware routing, disaggregated prefill/decode.

## D6 — Classic-model fleet (an ML tool for the agent)
**Problem:** A fraud model (agent tool) at **50K peak QPS**, p99 15 ms, one CPU server handles 200 QPS.
`Servers = 50K ÷ 200 = 250; × 1.5 headroom ≈ 375.`
`Concurrency check = 50K × 0.015 = 750 in-flight.`
→ **~375 CPU servers** (no GPU justified at 15 ms CPU inference — see Ch. 5 fraud example).

## D7 — Agent fan-out capacity (bridges Ch. 7)
**Problem:** 1M user tasks/day; each agent run makes ~**12 LLM calls**; peak 3×; avg LLM call 3 s.
`LLM calls/day = 12M ⇒ avg 12M ÷ 86,400 ≈ 139 LLM QPS; peak ×3 ≈ 417 LLM QPS.`
`Concurrency = 417 × 3 s = 1,251; ÷ 30 per replica ≈ 42 replicas.`
→ **~420 peak LLM QPS, ~42 replicas.** Size on **LLM QPS, not user QPS**; enforce step/token budgets and caching (a runaway loop multiplies this).

## D8 — AI-factory metrics: cost & tokens-per-watt
**Problem:** A serving node of **8× H100** (~700 W each) produces ~**4,000 tokens/s** aggregate. Cost per 1M tokens? Tokens/watt?
`Tokens/hour = 4,000 × 3600 = 14.4M.`
`Node cost = 8 × $2/hr = $16/hr ⇒ $16 ÷ 14.4 ≈ $1.11 per 1M tokens.`
`Tokens/watt = 4,000 ÷ (8 × 700) ≈ 0.71 tokens/s per watt.`
→ **~$1.1 per 1M tokens, ~0.71 tokens/s/W.** These "AI factory" metrics (tokens/s, tokens/watt, cost/token) increasingly replace request-based capacity planning; power, not just GPUs, is becoming the constraint.

---

### Using these in an interview
1. State assumptions (model size, tokens, effective TFLOPS, $/GPU-hr).
2. Separate **training** sizing (FLOPs → GPU-hours → GPUs/deadline → cost) from **serving** sizing (QPS → concurrency → replicas → GPUs).
3. Remember a big model's *replica* spans multiple GPUs — don't confuse "concurrent slots" with "GPUs."
4. End with the lever: shard/parallelize (training), or quantize/route/batch (serving), and use spot + checkpointing to cut cost.

*See also:* Chapter 5 [`estimation-problems.md`](../chapter%205/estimation-problems.md) and [`estimation-calculators.ipynb`](../chapter%205/estimation-calculators.ipynb) for the underlying GPU-memory/KV-cache/training-cost math.
