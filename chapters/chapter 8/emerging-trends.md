# Emerging Trends in AI Systems (Living Page)

The highest-churn material in the book — which is exactly why it lives in the repo, not in print. Extends Chapter 8's "Emerging trends" section. In interviews, **mention a trend to show awareness, then discuss its trade-offs and current maturity** (naming a buzzword without judgment is a weak signal).

> ⚠️ **Living document — verify before quoting.** Vendors, model names, and specifics change monthly. Reason about the *direction* and *trade-offs*, not the latest release. Last reviewed: 2026.

---

## 1. The new compute economy
- **NeoClouds** — pure-play GPU clouds (CoreWeave, Nebius, Lambda, Crusoe, Nscale) with faster provisioning than hyperscalers. *Trade-off:* changes build-vs-buy economics; **power & data-center capacity**, not just GPUs, are becoming the constraint.
- **AI Factories** (NVIDIA framing) — data centers that turn energy + data into intelligence; measured in **tokens/s, tokens/watt, cost/token**. *Trade-off:* capacity planning shifts from request-based to AI-throughput metrics (see infra drill D8).
- **Sovereign AI** — national infra, local foundation models, regional compute (India's Sarvam/BharatGen, Europe/Mistral). *Trade-off:* drives regional deployment, data residency, compliance, model localization.
- **Novel & edge hardware** — inference accelerators, neuromorphic chips, on-device NPUs. *Trade-off:* privacy-preserving low-latency edge inference, but immature/fragmented.

## 2. Model direction
- **Reasoning models** — models that "think" (extended internal deliberation / test-time compute) before answering; strong on math, coding, planning. *Trade-off:* higher latency and token cost; budget "thinking" tokens and route only hard queries to them.
- **Small Language Models (SLMs)** — compact models (often 1–8B, distilled/quantized) that are cheap, fast, private, edge-deployable. *Trade-off:* "smallest model that meets quality"; pair with routing/cascades — big models only when justified.
- **Compound AI systems** — solving tasks with **systems of components** (models + retrieval + tools + verifiers) rather than one monolithic model. *Trade-off:* modular and often better/cheaper than scaling a single model, but more moving parts to orchestrate/evaluate. (RAG and agents are early instances.)
- **Multimodal & long-context** — native text/image/audio/video and very long contexts. *Trade-off:* KV-cache/memory and cost grow with context; frame sampling matters for video.
- **Open-weight vs frontier gap** — capable open-weight models narrow the gap for many tasks. *Trade-off:* cost/privacy/control vs peak capability (Ch. 6 open-vs-proprietary).

## 3. The agent engineering stack
- **Context engineering** — the evolution of prompt engineering: control *everything the agent sees* (retrieval selection, memory, structured context, pruning). *Trade-off:* biggest lever for accuracy *and* cost.
- **Agentic harness** — the software wrapping a model into an agent: `Agent = Foundation Model + Harness` (system prompts + tools/MCP + memory + loop + sandbox + guardrails). *Trade-off:* production failures increasingly trace to **harness design** (tool orchestration, memory), not the model.
- **Loop engineering** — designing the execution cycle (discover → plan → act → observe → verify → update memory → decide → stop) with independent verification, durable state, explicit stop conditions. *Trade-off:* the difference between a reliable agent and a runaway one.
- **Evaluation as infrastructure** — continuous eval of prompts/tools/retrieval/behaviors (regression suites, LLM-as-a-Judge, production telemetry, business metrics). *Trade-off:* task success / cost-per-task / recovery rate now matter more than static benchmarks.

## 4. Serving & governance control planes
- **AI Gateway (LLM Gateway)** — centralized proxy across model providers: unified API, routing, failover, semantic caching, budget/cost control, auth, guardrails, PII redaction, rate limiting, observability. Examples: **LiteLLM, Portkey, Cloudflare AI Gateway, Kong AI Gateway, OpenRouter**. *Interview note:* the preferred answer for **multi-model deployments / vendor portability**.
- **Agent control plane & spend governance** — centralized identities, permissions, tool access, policies, observability, and cost across fleets of agents. *Trade-off:* complement latency SLOs with **task-oriented objectives** (task completion rate, max tool calls, cost per completed task).
- **Fine-tuning as a Service (FTaaS) & per-user adapters** — managed training/versioning/deploy of lightweight **LoRA** adapters dynamically loaded at inference to personalize a shared base model. *Trade-off:* big cost/ops savings vs dedicated training infra; adapter management complexity.

## 5. Regulation & responsible AI (moving fast)
- **EU AI Act** — risk-based obligations phasing in; high-risk systems need governance, transparency, human oversight, documentation, conformity assessment. *Design impact:* build oversight/documentation in from the start.
- **NIST AI RMF** — voluntary Govern/Map/Measure/Manage risk framework; common US reference.
- **Sector rules** — HIPAA, FCRA, FDA (medical AI), plus emerging state/national laws. *Design impact:* data residency, audit trails, model/agent cards.
- **Provenance & content authenticity** — watermarking and standards (e.g., C2PA) for AI-generated media. *Trade-off:* traceability vs robustness of watermarks.

---

### How to use this in an interview
Weave **one or two** relevant trends into a design, always with a trade-off:
- "I'd front multiple providers with an **AI gateway** for routing, caching, and budget control."
- "I'd route simple queries to an **SLM** and reserve the **reasoning model** for hard cases to control latency/cost."
- "This is a **compound AI** system — retrieval + a small ranker + an LLM + a verifier — rather than one giant model."
- "Given EU AI Act high-risk exposure, I'd bake in human oversight and documentation."

### Maintaining this page
Bump "Last reviewed", add/retire trends. Corrections via issue/PR.
