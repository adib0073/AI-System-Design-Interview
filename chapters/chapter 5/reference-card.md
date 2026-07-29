# Reference-Numbers Quick Card

A one-page card to memorize before an AI system design interview. Print it. The numbers are round on purpose — interviews reward the *right order of magnitude* and a clear method, not precision.

---

## Powers of 2 (memorize)
| 2^n | ≈ | Name |
|---|---|---|
| 2^10 | 1,000 | 1 K (KB) |
| 2^20 | 1,000,000 | 1 M (MB) |
| 2^30 | 1,000,000,000 | 1 B (GB) |
| 2^32 | 4.3 B | max unsigned 32-bit |
| 2^40 | 1 trillion | 1 T (TB) |

## Latency ladder (Jeff Dean "numbers")
| Operation | ≈ Time |
|---|---|
| L1 cache reference | ~1 ns |
| Branch mispredict | ~5 ns |
| L2 cache reference | ~7 ns |
| Mutex lock/unlock | ~25 ns |
| Main memory reference | ~100 ns |
| Compress 1 KB (Zippy) | ~1 µs (1,000 ns) |
| Send 1 KB over 1 Gbps | ~10 µs |
| SSD random read | ~100 µs |
| Read 1 MB sequential from memory | ~250 µs |
| Round trip within a datacenter | ~500 µs |
| Read 1 MB sequential from SSD | ~1 ms |
| Disk seek | ~10 ms |
| Read 1 MB from disk | ~20–30 ms |
| Round trip CA ↔ Netherlands | ~150 ms |

Rule of thumb: **memory ~100 ns · SSD ~100 µs · network RTT (same DC) ~0.5 ms · cross-continent ~150 ms.**

## Storage sizes
| Item | ≈ Size |
|---|---|
| ASCII char | 1 B |
| UTF-8 char | 1–4 B |
| Tweet (text) | ~280 B |
| Basic user profile | 1–2 KB |
| Rich user profile | 10–50 KB |
| Thumbnail image | 10–50 KB |
| Full-res image | 100 KB – 5 MB |
| 1 min video @720p / @1080p | 5–10 MB / 15–25 MB |
| 1 min MP3 @128 kbps | ~1 MB |
| 768-dim embedding (fp32 / fp16) | ~3 KB / 1.5 KB |
| 1536-dim embedding (fp32) | ~6 KB |

## Peak QPS benchmarks (public services)
| Service | ≈ Peak QPS |
|---|---|
| Twitter/X tweet creation | 10K–50K |
| Uber ride requests | 10K–50K |
| AI coding assistant (Copilot) | 20K–50K |
| LLM chat (ChatGPT/Claude/Gemini) | 50K–100K+ |
| Netflix session starts | 50K–100K |
| YouTube views | 100K+ |
| Instagram feed | 500K+ |
| Facebook news feed | 1M+ |
| Google Search | 10M+ |
| Enterprise RAG chatbot | 100–1K (latency-bound) |
| Agentic systems | 5–20× the user QPS |

## Peak multipliers
Social 2–3× · Enterprise (work hours) 2–4× · Video (prime time) 2–4× · E-commerce events 5–10× · Breaking news 10–20×.

---

## Core formulas
```
QPS            = DAU × requests/user/day ÷ 86,400   (then × peak multiplier)
Storage        = records × bytes/record × replication (+ overhead)
Bandwidth      = QPS × payload size                 (×8 for bits/s)
Instances      = peak QPS ÷ per-instance QPS         (× ~1.5 headroom, + N+1)
Concurrency    = QPS × latency (seconds)             (Little's Law)
```

## AI-specific formulas
```
Model memory (inference) ≈ params × bytes/param × 1.5
KV cache/token (fp16)    ≈ 8 × layers × hidden  bytes
Embedding storage        = dim × count × bytes/dim   (HNSW index ≈ ×1.5)
Training FLOPs           ≈ 6 × params × tokens × epochs
GPU-hours                = FLOPs ÷ (effective TFLOPS × 1e12 × 3600)
Cloud cost               = GPU-hours × $/GPU-hr × #GPUs
```

**Bytes per parameter:** FP32=4 · FP16/BF16=2 · FP8=1 · INT8=1 · INT4=0.5.

**KV cache shortcuts:** 7B ≈ 1 GB · 13B ≈ 1.6 GB · 70B ≈ 5 GB **per 1,000 tokens**.

**GPU compute (approx. peak FP16 TFLOPS):** A100 80GB ≈ 312 · H100 80GB ≈ 989 (FP8 ≈ 1,979). Realistic *effective* training throughput is ~30–50% of peak.

**Overhead multipliers:** inference 1.2–1.5× · training +20–30% for optimizer states. Spot GPUs ≈ 60–70% cheaper (interruptible).

---

### Interview reminders
1. Round to one significant figure ("~50K QPS", "~4 TB").
2. State every assumption out loud.
3. Always translate the number into a **design decision** (shard / cache / quantize / add GPUs / pick a DB).
