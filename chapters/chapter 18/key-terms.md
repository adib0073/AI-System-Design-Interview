# Key Terms — Chapter 18 (Deep Research & Planning Agent)

Interview-oriented definitions for the vocabulary in Chapter 18 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Orchestration & research
- **Orchestrator (planner)** — The top-level agent that decomposes the goal, dispatches sub-agents, integrates results, and replans. *Why it matters:* the coordination brain; drawing it is the clearest senior signal.
- **Sub-agent (worker)** — A scoped agent doing one part of the task (flights, hotels…) with its own tools/context. *Why it matters:* enables specialization and parallelism.
- **Fan-out / fan-in** — Dispatching subtasks in parallel and merging their results. *Why it matters:* makes long tasks tractable/fast — but multiplies token cost.
- **Deep research** — Multi-source, tool-grounded investigation synthesized into a cited output. *Why it matters:* the pattern (decompose → research → synthesize → cite) generalizes far beyond travel.

### Grounding & synthesis
- **Grounding / citation** — Basing claims on retrieved sources and attributing each fact to its source. *Why it matters:* trust + verifiability; bookable facts must be tool-grounded, never invented.
- **Faithfulness** — Whether generated claims are supported by sources (vs. hallucinated). *Why it matters:* a beautiful itinerary on hallucinated prices is worse than useless; a key eval metric.
- **Replanning** — Revising the plan when constraints change, options fail, or infeasibility is detected. *Why it matters:* real plans evolve (sold-out flight, over budget); a first-class loop with global re-verification.

### Transactions (the money path)
- **Read vs. write tools** — Safe/reversible tools (search, prices) vs. side-effectful/money-moving ones (book, charge). *Why it matters:* research flows freely; execution is gated — the same split as Ch. 13.
- **Idempotency key** — A token making a booking action safe to retry without duplicate charges. *Why it matters:* prevents double-booking on retries — a real money bug.
- **Saga / compensation** — Pattern for multi-step transactions: undo completed steps when a later step fails. *Why it matters:* no true atomicity across independent suppliers, so you compensate (cancel/refund) — the signature transactional answer.
- **Approval gate (HITL)** — Human consent required before an irreversible/spend action. *Why it matters:* the core safety mechanism when spending the user's money.
- **Bounded autonomy** — Pre-authorized actions within hard scope/spend caps. *Why it matters:* lets the agent act without open-ended money authority.

### Durability & cost
- **Checkpointing** — Persisting agent state so a long task can resume after interruption. *Why it matters:* minutes-long tasks *will* be interrupted; resume without redoing work or double-booking.
- **Durable orchestration** — Running the agent as a resumable workflow rather than an in-memory loop. *Why it matters:* in-memory loops lose long tasks on a restart; durability is the senior answer.
- **Cost-per-task** — Total tokens + tool + compute cost to complete one task. *Why it matters:* the key fan-out metric; multi-agent research is expensive — budget it.
- **Trace** — The full record of an agent run (subtasks, tool calls, decisions). *Why it matters:* essential for debugging multi-agent runs, audit after a booking, and process-level evaluation.

---

*Cross-refs:* agent fundamentals, ReAct, multi-agent, memory, HITL, sandboxing → Ch. 7. RAG/grounding → Ch. 6. Read/write split, approval gates, idempotency → Ch. 13. Ground-verify discipline → Ch. 17. Autonomous SWE multi-agent → mock problem 15.
