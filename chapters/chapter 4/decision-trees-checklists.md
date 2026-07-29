# Decision Trees & Checklists — Model Selection and Feature Stores

Fast, defensible decision aids for the two choices interviewers push on most: **which model/approach** and **how to handle features/serving**. Includes explicit **Generative-AI and agentic** branches, since modern rounds almost always go there.

Use these to *reason out loud* — narrate the branch you take and why, then state the trade-off.

---

## 1. "Does this need AI?" (gate before anything else)

```
Is the task a solved, deterministic computation (math, sorting, exact lookup)?
├─ YES → Use code/rules. Do NOT use ML.
└─ NO → Can a small set of stable rules/heuristics hit the target quality?
         ├─ YES → Ship rules first. Add ML only where rules plateau.
         └─ NO → Are there labeled/learnable patterns, tolerance for some error,
                 and payoff > (build + serve + maintain + nondeterminism) cost?
                 ├─ NO  → Rules / human-in-the-loop / defer.
                 └─ YES → Use ML. Proceed to model-selection tree.
```
**Say this:** "AI adds complexity and nondeterminism, so I need to justify it with a measurable gain."

---

## 2. Model-selection decision tree

```
What is the data modality / task?

STRUCTURED / TABULAR
  ├─ Need interpretability or tiny data? → Logistic/Linear, Decision Tree
  └─ Want strong accuracy on tabular? → Gradient-Boosted Trees (XGBoost/LightGBM)  ← usually the default
       └─ Ensemble (bagging/boosting/stacking) for extra robustness

UNSTRUCTURED (image / audio / text / signal)
  ├─ Images → CNN / Vision Transformer (or pretrained backbone + fine-tune)
  ├─ Sequence/time series → RNN/LSTM/Temporal, or Transformer
  └─ Text understanding (classify, NER, sentiment) → fine-tuned encoder (BERT-family)

RETRIEVAL / SEMANTIC SEARCH / RECOMMENDATION
  └─ Embedding model (bi-encoder) + ANN/vector DB  →  candidate generation
       └─ Add a cross-encoder RE-RANKER on the top-k for a quality step-change

LANGUAGE GENERATION / OPEN-ENDED / MULTIMODAL REASONING
  └─ Foundation model (LLM) → see the GenAI tree below

SCALE + PRECISION BOTH MATTER (search, ads, feed)
  └─ Multi-stage funnel: cheap retrieval → ranking → re-ranking (heavy models only on a small candidate set)
```
**Guiding trade-off:** bigger/deeper models raise accuracy but cost latency and money. In a funnel, keep candidate generation fast and spend the compute budget on the final ranking of a small set.

---

## 3. Generative-AI approach tree (prompt → RAG → fine-tune → agent)

```
Does the task need external/private/fresh knowledge the base model lacks?
├─ NO, it's general reasoning/formatting → PROMPTING (zero/few-shot) first. Cheapest, fastest to iterate.
│     └─ Still failing on format/consistency? → few-shot + structured output / constrained decoding.
└─ YES → Is the knowledge factual/lookup-style and changes often?
         ├─ YES → RAG (retrieve → (re-rank) → generate). No retraining; update the index, not the model.
         └─ Knowledge is a STYLE/SKILL/DOMAIN behavior, not lookup facts?
              ├─ YES → FINE-TUNE (LoRA/QLoRA for cheap adaptation; full FT rarely needed).
              └─ Both facts + behavior → RAG + light fine-tune.

Does the task require multi-step planning, tools/APIs, or actions in the world?
└─ YES → AGENTIC design (plan → call tools → observe → iterate). Otherwise keep it single-shot.
```

**Prompt vs RAG vs Fine-tune — quick comparison**

| | Prompting | RAG | Fine-tuning |
|---|---|---|---|
| Best for | General tasks, formatting | Fresh/private facts, citations | Domain style, tone, narrow skills |
| Updates knowledge by | Editing the prompt | Updating the index | Retraining |
| Cost / effort | Lowest | Medium (retrieval infra) | Highest (data + compute) |
| Hallucination control | Weak | Strong (grounded + citable) | Medium |
| Latency | Base | +retrieval/re-rank | Base |

**Hosted vs open-weight LLM**

```
Hard privacy/residency, heavy volume, or need to fine-tune freely / run on-prem/edge?
├─ YES → Open-weight, self-hosted (Llama/Qwen/Gemma/Mistral). You own cost, latency, GPUs, ops.
└─ NO, want best quality fast with least ops → Hosted API (GPT / Claude / Gemini). Pay per token; data leaves your VPC.
```

---

## 4. Agentic-system checklist (when the design is an "agent")

- [ ] **Justify the agent** — is multi-step planning/tool use actually required, or would a single RAG call do? (Agents add latency, cost, and failure surface.)
- [ ] **Tool/function registry** — well-typed tools, input validation, timeouts, and least-privilege scopes per tool.
- [ ] **Planning/orchestration** — single-agent loop vs multi-agent; bounded max steps to prevent runaway loops.
- [ ] **Memory** — short-term (context window) vs long-term (vector store / summary); what to persist and for how long.
- [ ] **Grounding** — RAG for facts; cite sources; avoid letting the model invent tool outputs.
- [ ] **Guardrails** — prompt-injection defenses, output sanitization before any code/DB execution, human-in-the-loop for high-stakes actions.
- [ ] **Capacity note** — agents fan out to **5–20× more LLM calls** than user requests; size on LLM QPS, not user QPS (see Ch. 5).
- [ ] **Observability** — step-by-step tracing (which tool/step caused latency or a wrong answer); a **prompt registry** alongside the model registry.
- [ ] **Cost controls** — caching, cheaper models for sub-tasks, early stopping.

---

## 5. Feature-store / feature-engineering checklist

**When do I even need a feature store?**
```
Do the same features feed both training AND low-latency online serving,
and/or are features reused across teams/models?
├─ NO (single offline batch model) → a feature table / pipeline is enough; skip the store.
└─ YES → Use a feature store (Feast/Tecton/Chronon/Feathr). It's the single source of truth.
```

**Design checklist**
- [ ] **Offline store** (training, batch) + **online store** (low-latency serving) — both fed from consistent transformation logic.
- [ ] **Training-serving skew prevention** — same code/definition computes a feature in both paths (the store's core job).
- [ ] **Point-in-time correctness** — join features as-of the label timestamp to prevent **data leakage** from the future.
- [ ] **Freshness / staleness SLAs** — how current must each feature be? Track ingestion lag.
- [ ] **Online vs offline features** — precompute stable/expensive features offline; compute volatile ones (recency, session) online at inference and merge.
- [ ] **Reuse & discovery** — versioned, documented feature definitions shared across teams.
- [ ] **Materialization & backfill** — batch vs streaming ingestion; ability to backfill history for new features.
- [ ] **Monitoring** — feature null-rates, distribution drift, and freshness alerts (ties into the drift monitoring in the practice bank).

**GenAI / retrieval-specific "feature" additions**
- [ ] **Embedding pipeline** — which encoder, dimension, precision (float32/16); store in a **vector DB** with the right ANN index.
- [ ] **Embedding freshness & re-embedding** — re-embed when the encoder or documents change; version the embedding model.
- [ ] **Prompt registry** — version prompts/templates like model artifacts (rollback + lineage).
- [ ] **Retrieval caching** — cache hot query→results / embeddings to cut cost and latency.

---

## 6. Deployment & rollout checklist (safe model changes)

- [ ] **Shadow** the new model (log predictions, no user impact) to check parity.
- [ ] **Backtest** against historical logs vs the current baseline.
- [ ] **Canary / A-B** a small traffic slice; watch online + guardrail metrics for significance.
- [ ] **Rollback plan** for models *and prompts* (registry-backed) to avoid downtime.
- [ ] **Monitoring + retraining triggers** live before full ramp (scheduled, drift-threshold, perf-drop, or enough new labels).

---

*Pair with:* [`practice-bank.md`](./practice-bank.md) for the "does this need ML / which metric / which drift" drills, and Chapter 5 for GPU/KV-cache/cost sizing once the approach is chosen.
