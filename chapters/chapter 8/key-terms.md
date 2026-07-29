# Key Terms — Chapter 8 (AI at Scale: Infrastructure, MLOps, Responsible AI)

Interview-oriented definitions for the scale/infra/governance vocabulary in Chapter 8. Each pairs a crisp definition with *why it matters* in a design round. Terms defined earlier (KV cache, feature store, drift basics, canary/shadow, observability basics) are cross-referenced. Feeds the cumulative book glossary.

---

### GPU & compute infrastructure
- **Accelerator (GPU/TPU/NPU)** — Specialized hardware for dense matrix math. *Why it matters:* AI scale/cost is set as much by hardware as by the model; right-size it.
- **NVLink** — High-bandwidth intra-node GPU-to-GPU interconnect. *Why it matters:* why **tensor parallelism stays within a node** — it needs the fastest link.
- **InfiniBand / RDMA** — High-speed low-latency inter-node network. *Why it matters:* the fabric for cross-node all-reduce and pipeline parallelism at cluster scale.
- **All-reduce** — Collective that sums/averages gradients across GPUs. *Why it matters:* the main communication cost of data parallelism.
- **HBM (High-Bandwidth Memory)** — On-package GPU VRAM (e.g., 80 GB). *Why it matters:* the hard cap weights + KV cache + activations must fit in.

### Distributed training
- **Data parallelism (DP)** — Replicate the model, split the batch; sync via all-reduce. *Why it matters:* simplest; works only when the model fits one GPU.
- **Model (tensor) parallelism (TP)** — Split individual layers across GPUs. *Why it matters:* for layers too big for one GPU; keep intra-node (NVLink).
- **Pipeline parallelism (PP)** — Split consecutive layers into stages; overlap micro-batches. *Why it matters:* fits very deep models across nodes; micro-batches reduce idle "bubbles."
- **3D parallelism** — Combine DP × TP × PP. *Why it matters:* how the largest models train; `total GPUs = DP × TP × PP`.
- **FSDP / ZeRO** — Shard parameters/gradients/optimizer states across GPUs. *Why it matters:* the fix when a full model+optimizer (~16 B/param) won't fit a DP replica.
- **Checkpointing** — Periodically saving training state to durable storage. *Why it matters:* enables resume after preemption/failure — and unlocks cheap **spot** GPUs.
- **Megatron-LM / DeepSpeed** — Frameworks implementing these strategies. *Why it matters:* you use these, not hand-rolled parallelism.

### Scheduling & cost
- **Scheduler (Kubernetes / Slurm / Ray)** — Allocates jobs to GPUs, manages priority/placement. *Why it matters:* utilization of expensive GPUs hinges on it.
- **Spot / preemptible instances** — Discounted interruptible VMs (~60–70% off). *Why it matters:* great for checkpointed training; unsafe for latency-critical serving.
- **Reserved / committed capacity** — Long-term commitments for predictable workloads. *Why it matters:* big discount vs on-demand.
- **Right-sizing** — Matching accelerator to workload (e.g., L4/A10G for small models). *Why it matters:* better cost-performance than defaulting to the biggest GPU.
- **Utilization / idle GPUs** — Keeping GPUs busy (batching, multi-tenancy). *Why it matters:* idle GPUs are the top source of wasted spend.

### AI platforms & serving
- **AI Gateway / model router** — Unified proxy across LLM providers (routing, failover, caching, budget, guardrails, observability). *Why it matters:* the go-to answer for multi-model deployments / vendor portability.
- **Orchestration layer** — Coordinates planning, tool calls, multi-agent, task sequencing. *Why it matters:* turns isolated model calls into multi-step workflows.
- **Evaluation harness** — Continuous offline/online + LLM-as-a-Judge evaluation gating deployments. *Why it matters:* agent promotion relies on **evaluation, not labels**.
- **Model mesh** — Sharing GPU pools across many models / LoRA adapters. *Why it matters:* raises utilization when serving many models.
- **KV-cache-aware routing** — Route a session to the replica already holding its KV cache. *Why it matters:* avoids recompute; big win for multi-turn/agent serving.
- **Disaggregated prefill/decode** — Separate the compute-heavy prefill from memory-heavy decode. *Why it matters:* independent scaling of the two very different stages.
- **Durable execution / session affinity** — Persisting long-running agent state so a failure doesn't restart it. *Why it matters:* agent serving resembles workflow orchestration (Temporal), not stateless prediction.
- **Deployable unit = agent configuration** — Version prompt + model + tools + memory + retrieval as one artifact. *Why it matters:* changing any part changes behavior; version them together.

### Data & observability
- **Agentic data plane** — Context/memory/retrieval the agent consumes at runtime (vs feature pipelines). *Why it matters:* lead with retrieval/memory/context; feature stores serve ML-model *tools*.
- **End-to-end lineage** — Tracing a response from source doc → chunk → retrieval → tools → reasoning → output. *Why it matters:* debugging, auditing, compliance.
- **Trajectory tracing** — Full execution path (reasoning, tool calls/outputs, retries, decisions, output). *Why it matters:* the primary way to debug and *explain* non-deterministic agents.
- **Drift types** — **Data (covariate)** `P(X)`, **concept** `P(Y|X)`, **prediction** (output) drift. *Why it matters:* different causes, different responses; prediction drift is an early warning (Ch. 4).
- **Three observability dimensions** — System health (latency/errors) · agent behavior (trajectory, tool use, task success) · business impact (cost, quality, safety). *Why it matters:* infra metrics alone miss "up but wrong."
- **SLO / SLI (+ task-oriented objectives)** — Reliability targets; for agents also task-completion rate, cost/task, max tool calls. *Why it matters:* latency SLOs don't capture agent correctness/cost.

### Responsible AI
- **Fairness definitions** — Demographic parity, equalized odds, individual fairness. *Why it matters:* they conflict under unequal base rates; choose deliberately per domain.
- **Bias (pipeline-wide)** — Systematic disadvantage entering at data/feature/training/serving stages. *Why it matters:* mitigate system-wide, not just in training.
- **Proxy variable** — A feature that indirectly encodes a protected attribute (e.g., ZIP ~ race). *Why it matters:* remove/handle it during feature engineering.
- **Global vs local explainability** — Explaining overall behavior vs a single prediction. *Why it matters:* match the explanation to the stakeholder (regulator/expert/user).
- **SHAP / LIME** — Feature-attribution explainability methods. *Why it matters:* standard tools for traditional ML explanations.
- **Grounding & provenance** — Attributing each claim to supporting evidence (citations). *Why it matters:* for LLMs/RAG, often more trustworthy than model-internal explanations.
- **Model card / Agent card** — Documentation of purpose, data, tools, guardrails, limitations, failure modes. *Why it matters:* transparency for operators, auditors, regulators.
- **Differential privacy / federated learning** — Noise-based privacy / on-device training. *Why it matters:* privacy-by-design under GDPR/HIPAA (Ch. 4).
- **EU AI Act** — Risk-based regulation; high-risk uses need governance, oversight, documentation, conformity assessment. *Why it matters:* shapes design for hiring/credit/health/critical-infra systems.
- **NIST AI RMF** — Voluntary Govern/Map/Measure/Manage risk framework. *Why it matters:* common structure for AI risk management.

### Emerging trends
- **NeoCloud** — Pure-play GPU cloud provider. *Why it matters:* shifts build-vs-buy; power/capacity now constrain, not just GPUs.
- **AI Factory metrics** — tokens/s, tokens/watt, cost/token. *Why it matters:* AI-throughput capacity planning replaces request-based metrics.
- **Reasoning model** — Extended test-time deliberation before answering. *Why it matters:* better hard-task quality at higher latency/cost — route selectively.
- **SLM (Small Language Model)** — Compact, cheap, edge/private model. *Why it matters:* "smallest model that meets quality"; pair with routing/cascades.
- **Compound AI system** — Task solved by a system of models/tools/verifiers, not one model. *Why it matters:* modular, often better/cheaper than scaling one model.
- **Agent engineering (context/harness/loop engineering, eval-as-infra)** — The discipline of the infrastructure around the model. *Why it matters:* production failures increasingly come from the **harness**, not the model.
- **Fine-tuning as a Service / per-user LoRA adapters** — Managed adapters loaded at inference on a shared base. *Why it matters:* cheap personalization at scale.

---

*Cross-refs:* GPU memory, KV cache, FLOPs, training cost → Chapter 5. Agents/MCP/memory/guardrails → Chapter 7. Feature store, drift, canary/shadow, RAG → Chapter 4/6. Security, observability basics, CAP → Chapter 3.
