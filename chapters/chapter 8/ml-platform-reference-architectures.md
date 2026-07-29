# ML-Platform Reference Architectures (Annotated)

Annotated tours of the ML platforms interviewers expect you to recognize. Each has the same skeleton Chapter 4 introduced — **data → features → training → registry → deployment → monitoring** — plus the extras Chapter 8 adds for LLM/agentic systems. Use these as vocabulary and as templates for "design an ML platform" questions.

> **Why study these:** naming a real platform and *what problem each layer solves* signals production experience. Don't memorize internals — learn the recurring components and trade-offs.

---

## The canonical ML-platform skeleton (baseline)
```
Data ingestion → Feature engineering (feature store) → Training pipeline
→ Model registry (versioning/lineage) → Deployment (serving) → Monitoring (drift/quality) → back to Data
```
Every platform below is a variation on this loop. Judge each by how it handles: **feature consistency (train/serve skew), reproducibility/lineage, safe rollout, and monitoring.**

---

## 1. Uber — Michelangelo
**One line:** the platform that popularized the **feature store** and end-to-end ML productization.
**Annotated layers:**
- **Palette feature store** — shared offline (training) + online (serving) features → prevents **training-serving skew** (Ch. 4's core feature-store lesson).
- **Managed training** — scalable distributed training + hyperparameter search.
- **Model registry & management** — versioned artifacts, metadata, lineage.
- **Serving** — online (low-latency) + offline (batch) prediction; monitoring for quality/drift.
**What to take to an interview:** the offline/online feature split and why a single source of truth matters; Michelangelo is the archetypal answer to "design an ML platform."
→ https://www.uber.com/blog/michelangelo-machine-learning-platform/

## 2. Meta — FBLearner Flow
**One line:** reusable ML **workflows** at massive internal scale.
**Annotated layers:**
- **Workflow authoring** — pipelines as reusable, shareable operators (write once, reuse across teams).
- **Experiment management** — launch/track many experiments; central catalog of models/features.
- **Automated training + deployment** — the pipeline handles retraining and pushing to serving.
**What to take:** the value of **reusable pipeline components** and a shared experiment/model catalog for org-wide velocity.
→ search "FBLearner Flow engineering Facebook"

## 3. Google — TFX (TensorFlow Extended)
**One line:** the open, **component-based** production ML pipeline with strong data validation.
**Annotated components:**
- **ExampleGen → StatisticsGen → SchemaGen → ExampleValidator** — ingest + **data validation** (catches schema/skew/anomalies early — maps to Ch. 4 data-quality dimensions).
- **Transform** — feature engineering applied *identically* in training and serving (skew prevention).
- **Trainer → Evaluator (TFMA) → Pusher** — train, gate on metrics (incl. sliced/fairness metrics), push only if better.
- **ML Metadata (MLMD)** — lineage/provenance across runs.
- Orchestrated by Airflow / Kubeflow / Beam.
**What to take:** **data validation as a first-class pipeline stage** and metric-gated promotion; great template for a rigorous pipeline answer.
→ https://www.tensorflow.org/tfx

## 4. Netflix — Metaflow
**One line:** **human-friendly** ML infrastructure that scales from laptop to cloud.
**Annotated ideas:**
- **Python-first DAGs** — data scientists write flows; infra (compute, data, scheduling) is abstracted.
- **Built-in versioning & artifact tracking** — every run/step is snapshotted for reproducibility.
- **Seamless scale-out** — same code runs locally or on cloud compute.
**What to take:** developer experience *is* a platform feature; reproducibility by default.
→ https://metaflow.org/

---

## What LLM / agentic platforms add (Ch. 8 §8.2)
The classic skeleton stays, but foundation-model/agent platforms **wrap it with seven layers** (since orgs *consume* pretrained models rather than train them):

| Added layer | Solves |
|---|---|
| **AI Gateway / model router** | Unified entry to many LLM providers; routing, failover, caching, budget enforcement |
| **Orchestration layer** | Planning, tool invocation, multi-agent, task sequencing |
| **Context & memory stores** | Vector DBs, knowledge graphs, session memory, retrieval (RAG + agent memory) |
| **MCP registry** | Standardized, governed discovery/invocation of external tools |
| **Guardrails** | Prompt filtering, PII detection, jailbreak prevention, output validation |
| **Evaluation harness** | Offline benchmarks, LLM-as-a-Judge, regression tests, online experiments |
| **Observability & tracing** | End-to-end traces, tool calls, latency, token/cost tracking |

**Deployment shift:** the deployable unit is the **complete agent configuration** (prompt + model + tools + memory + retrieval), promotion relies on **evaluation not labels**, long-running sessions need **version consistency**, and metrics extend beyond latency to **task success, cost/execution, tool-failure, loop/timeout, escalation rate**.

---

### How to use this in an interview
- Asked to "design an ML platform"? Draw the **canonical skeleton**, then name a reference (Michelangelo/TFX) for credibility.
- Asked about **LLM/agent** platforms? Start from the skeleton and add the **seven wrapper layers**; stress feature stores now serve *ML-model tools*, while retrieval/memory/context serve the agent itself.
- Always tie a layer to the **problem it solves** (skew, reproducibility, safe rollout, cost, governance).

*See also:* Chapter 4 [`engineering-blogs.md`](../chapter%204/engineering-blogs.md) (feature stores, MLOps) and [`decision-trees-checklists.md`](../chapter%204/decision-trees-checklists.md); Chapter 8 [`emerging-trends.md`](./emerging-trends.md) (AI gateways, control planes).
