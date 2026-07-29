# Chapter 8 — AI at Scale: Infrastructure, MLOps, and Responsible AI

Companion resources for Chapter 8. Maintained here (not in the printed book) so they can be kept current — especially the highest-churn "emerging trends."

Chapter 8 covers operating AI at production scale: GPU/compute infrastructure & distributed training, AI platforms & serving agents at scale, data infrastructure & observability, Responsible AI (fairness/bias/explainability/governance), and emerging trends.

| File | What it is |
|------|------------|
| [`infra-estimation-drills.md`](./infra-estimation-drills.md) | 8 verified drills bridging Ch. 5 → Ch. 8: cluster sizing for training, GPU-hours & cost, the 3D-parallelism split, training-memory (why data-parallel alone fails), and inference-fleet sizing for models and agents. |
| [`ml-platform-reference-architectures.md`](./ml-platform-reference-architectures.md) | Annotated tours of Michelangelo, FBLearner Flow, TFX, and Metaflow — the canonical ML-platform skeleton plus the seven layers LLM/agent platforms add. |
| [`responsible-ai-checklist.md`](./responsible-ai-checklist.md) | Worksheet mirroring the chapter: fairness definitions, pipeline-wide bias mitigation, explainability (incl. agents), privacy, and governance/regulation — with interview one-liners. |
| [`emerging-trends.md`](./emerging-trends.md) | **Living reference** (highest churn): the new compute economy, reasoning models & SLMs, compound AI, the agent engineering stack, control planes, and regulation — each with trade-offs. |
| [`blog-paper-index.md`](./blog-paper-index.md) | Papers & write-ups: distributed training (Megatron/ZeRO/FSDP), scheduling, ML platforms, LLM/agent observability, and governance (EU AI Act, NIST AI RMF). |
| [`key-terms.md`](./key-terms.md) | Chapter 8 glossary slice (NVLink/InfiniBand, 3D parallelism, drift types, model/agent card, AI gateway, fairness definitions, …). Feeds the cumulative book glossary. |

> **Note on links:** `emerging-trends.md` and parts of the blog index move fast — treat them as living documents and verify before quoting. If a link is dead, search the title or open an issue/PR.
