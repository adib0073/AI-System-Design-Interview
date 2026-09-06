# Chapter 18 — Deep Research & Planning Agent

Companion resources for Chapter 18, the capstone agentic case study (anchored on **travel planning and booking**). It's the most complex system in the book: **long-horizon, multi-agent, and transactional** — with real money on the line.

Chapter 18 covers orchestrator + sub-agent decomposition, multi-source parallel research, grounded/cited synthesis, planning/replanning/itinerary construction, tool use & transactions (booking with confirmation, idempotency, compensation), human-in-the-loop approval gates, memory & long-running traces (checkpointing/durable orchestration), cost/latency for fan-out, and evaluation (plan quality, faithfulness, cost-per-task).

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 18 glossary slice (orchestrator/sub-agent, fan-out/fan-in, grounding/citation, faithfulness, replanning, read/write tools, idempotency key, saga/compensation, approval gate, checkpointing, durable orchestration, cost-per-task, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — when to use sub-agents, grounding/citations, booking as a transaction, approval gates, durable state, and controlling fan-out cost. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Anthropic multi-agent research, OpenAI/Gemini Deep Research, saga pattern, durable workflow engines, and agent evaluation. |

> **How to use:** the graded spine is **plan → ground → tool → verify → gate, with durable state and cost control** — and the **plan-vs-execute separation** (a human gate before money moves). This is the culmination of the book's agentic arc (7 → 13 → 17 → 18).
