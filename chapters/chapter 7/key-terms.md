# Key Terms — Chapter 7 (Agentic AI Systems)

Interview-oriented definitions for the agentic-AI vocabulary in Chapter 7. Each pairs a crisp definition with *why it matters* in a design round. Terms defined earlier (RAG, embedding, guardrails basics, vector DB) are cross-referenced. Feeds the cumulative book glossary.

---

### Foundations
- **Agentic AI system** — An AI system that autonomously plans, reasons, uses tools, and adapts to reach a high-level goal. *Why it matters:* the paradigm shift from "question→answer" to "goal→plan→execute→observe→iterate."
- **Agent vs. pipeline** — A pipeline is deterministic/stateless; an agent decides, uses tools, and adapts. *Why it matters:* the first thing to establish — don't use an agent when a pipeline suffices.
- **Four agentic capabilities** — Autonomy, planning, tool use, adaptation. *Why it matters:* the checklist for "is this actually agentic?"
- **Agent loop** — Perceive → Reason → Plan → Act → Observe → (Learn). *Why it matters:* the canonical execution cycle; many production agents omit "Learn."
- **Levels of autonomy** — Copilot → Assistant → Agent → Autonomous. *Why it matters:* choose based on task complexity, risk, regulation, and oversight needs.

### Reasoning / architecture patterns
- **ReAct** — Interleaves reasoning traces with tool calls (Thought → Action → Observation → … → Answer). *Why it matters:* transparent and debuggable; the common default; cap iterations to avoid runaway loops.
- **Plan-and-Execute** — Produce a full plan first, then execute step by step, replanning on failure. *Why it matters:* validatable and supports human approval; rigid for unexpected outcomes.
- **Reflexion** — After an attempt, the model critiques its output and retries with a refined strategy. *Why it matters:* improves complex reasoning/code gen at higher latency/cost.
- **Tree of Thought (ToT)** — Explores multiple reasoning branches as a tree, pruning weak paths. *Why it matters:* search/planning/optimization tasks; expensive without good pruning.
- **Graph of Thought (GoT)** — ToT generalized to a graph so paths can branch, merge, and reuse results. *Why it matters:* flexible exploration for interconnected reasoning.
- **Tool-augmented agent** — An LLM extended with external tools (APIs, DBs, code, browser, files). *Why it matters:* real-time data + actions beyond parametric knowledge; expands the attack surface (sandbox!).
- **Stateful agent** — Maintains context/state across interactions. *Why it matters:* enables long-running workflows and personalization; needs memory management + privacy care.

### Tools, skills & protocols
- **Function calling / tool schema** — Structured description (name, params, returns) telling the model when/how to use a tool. *Why it matters:* good schemas reduce wrong-tool and bad-parameter errors.
- **MCP (Model Context Protocol)** — Open standard connecting an agent to external tools/data (resources, tools, prompts) via a client–server model. *Why it matters:* build once, reuse across models/frameworks; discuss permissions, latency, reliability, discovery.
- **A2A (Agent-to-Agent) protocol** — Open standard for agents to discover, message, and delegate to one another. *Why it matters:* the interoperability layer for multi-agent systems; complementary to MCP.
- **Skills / Rules / Hooks** — Reusable capabilities / behavioral constraints / event-driven extension points. *Why it matters:* make agents modular (skills), governable (rules), and observable (hooks).
- **Execution environment (sandbox/container/serverless)** — Isolated runtime for code/tool execution. *Why it matters:* the primary safety boundary; least privilege + allowlists + resource limits.

### Multi-agent
- **Orchestrator (central coordinator)** — One coordinator decomposes, delegates to specialists, aggregates. *Why it matters:* most common multi-agent pattern; single point of control (and failure).
- **Supervisor** — Orchestrator that also monitors quality, retries/reassigns, and escalates. *Why it matters:* for correctness/QA/reliability over latency.
- **Swarm** — Decentralized peer agents, no central coordinator. *Why it matters:* for inherently distributed problems; scales via parallelism but harder to control/debug.
- **Conflict resolution** — Voting / mediator / rule-based. *Why it matters:* how disagreeing agents converge on a decision.

### Memory
- **Short-term memory** — Current-task context, usually the LLM context window (sliding window/summarization to fit limits). *Why it matters:* enables multi-step reasoning within a session.
- **Long-term memory** — Persistent info across sessions (structured DB, vector DB, or knowledge graph). *Why it matters:* personalization and knowledge retention; needs update/retention policies.
- **Episodic memory** — Records of specific past events/interactions, timestamped. *Why it matters:* recall "what happened when" across sessions.
- **Semantic memory** — Persistent facts/knowledge independent of any single event (preferences, org knowledge). *Why it matters:* foundation of personalization.
- **Procedural memory** — Reusable procedures/workflows/successful strategies ("how to do X"). *Why it matters:* cuts redundant reasoning for recurring tasks.
- **Memory management** — Summarization, compression, forgetting/retention. *Why it matters:* prevents unbounded growth, retrieval decay, cost blowup, and privacy risk.

### Planning & control
- **Task decomposition** — Hierarchical / sequential / parallel / conditional breakdown of a goal. *Why it matters:* improves parallelism and failure isolation.
- **Replanning** — Locally revising the affected part of a plan when things change. *Why it matters:* production plans evolve; don't restart from scratch.
- **Human-in-the-loop (HITL)** — Human approval before sensitive/irreversible actions. *Why it matters:* reduces risk; record approvals for audit.
- **Execution limits** — Iteration caps, per-step timeouts, overall run cap. *Why it matters:* prevents infinite loops and unpredictable cost.
- **Budget management** — Token/tool-call limits + model routing. *Why it matters:* controls the real cost of autonomous execution.

### Safety & governance
- **Guardrails** — Input filters (harmful content, prompt injection, jailbreaks) + output filters (PII, policy, unsafe content). *Why it matters:* defense-in-depth; don't rely on the LLM alone.
- **Sandboxing / least privilege / allowlist** — Isolate execution; grant minimum access; deny by default. *Why it matters:* the core "assume the agent misbehaves" controls.
- **Confirmation gate** — Mandatory human approval for high-impact actions. *Why it matters:* stops destructive/irreversible mistakes.
- **Action validation** — Pre-action parameter checks + output validation. *Why it matters:* catches injection/path-traversal/invalid inputs before they hit downstream systems.
- **Trajectory tracing** — Capturing the full reasoning/tool/observation path of a run. *Why it matters:* the primary way to debug and audit non-deterministic agents (also serves as explanation — Ch. 8).
- **Risk tiering** — Classifying actions by impact and scaling governance accordingly. *Why it matters:* balance safety, UX, and cost instead of gating everything equally.

---

*Cross-refs:* RAG, reranking, embeddings, vector DB → Chapter 6/4. KV cache, TTFT/cost → Chapter 5. Serving agents at scale, agent platforms, observability signals, agent cards → Chapter 8.
