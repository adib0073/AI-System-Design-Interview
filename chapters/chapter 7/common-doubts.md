# Common Interviewee Doubts — Chapter 7 (Agentic AI Systems)

Questions candidates most often have about designing agentic systems in interviews. Grouped by theme.

---

## When (not) to use agents

**1. Everything is "agentic" now — when do I actually propose an agent?**
Only when the task needs **exploration, tool use, or adaptive multi-step reasoning**. If the steps are fixed and known, a plain pipeline/workflow is simpler, cheaper, deterministic, and easier to debug — and saying so is a *plus*. Interviewers reward candidates who *don't* over-engineer. Lead with: "Could a pipeline do this? If not, here's why an agent earns its complexity."

**2. Single agent or multi-agent — what's the safe default?**
Default to a **single agent with good tools**. Go multi-agent only when you have genuinely distinct specialist roles, need parallelism, or need to scale/deploy parts independently. Multi-agent adds coordination, latency, and failure-handling cost. Naming that trade-off matters more than picking "more agents."

**3. How do I choose orchestrator vs. supervisor vs. swarm?**
Orchestrator for most cases (one coordinator, easy to monitor). Supervisor when correctness/QA/retries/escalation matter more than latency. Swarm only for inherently distributed, peer-collaborative problems. See the [pattern-selection guide](./agent-pattern-selection.md).

## Reasoning patterns

**4. ReAct vs. Plan-and-Execute vs. Reflexion — how do I pick live?**
ReAct for transparent, tool-driven, varied tasks (the common default). Plan-and-Execute when you need an approvable up-front plan (compliance). Reflexion when quality improves via self-critique (complex reasoning, code). You can combine them. Always mention **iteration caps** so it can't loop forever.

**5. Do I need to know Tree/Graph of Thought?**
Know what they are (explore multiple reasoning paths, backtrack) and that they're expensive and need pruning. Propose them only for search/planning/optimization problems — not for a simple tool-using agent.

## Tools, MCP & A2A

**6. Will I be quizzed on the MCP spec?**
Unlikely. Know *why* MCP exists (standardize tool/data integration — build once, reuse across models) and the architectural concerns: **permissions, latency, reliability, tool discovery**. Same for A2A: MCP is agent→tools, A2A is agent→agent, and they're complementary.

**7. How many tools should an agent have?**
Fewer, well-described tools beat many. Too many tools → the model picks the wrong one. Each tool = single responsibility, descriptive name, precise parameters, graceful error handling. If you have dozens, add a router or namespacing.

## Memory

**8. Which memory types do I actually mention?**
Short-term (context window) always. Add long-term (vector DB / structured DB / knowledge graph) when the agent must persist across sessions. Distinguish episodic (events, timestamped), semantic (facts/preferences), procedural (how-to). Then — critically — say how you **manage** it (summarize, retention, forgetting). "Store everything forever" is a red flag.

**9. Vector DB, knowledge graph, or structured DB for memory?**
Vector DB for semantic/episodic (similarity retrieval), knowledge graph for highly connected/multi-hop, structured DB for exact lookups (profiles, session state). Production agents often combine them.

## Safety, cost & reliability

**10. What separates a "production-ready" agent answer from a demo?**
Operational rigor: how it **replans**, **handles failures** (retries/fallbacks/partial results/escalation), stays within **constraints** (budgets, limits), and **knows when to stop** (iteration caps, cycle detection, progress checks). Interviewers specifically look for this.

**11. How do I keep an autonomous agent from doing something catastrophic?**
Defense-in-depth: sandboxing + least-privilege + allowlists, pre-action validation, confirmation gates for high-risk actions, and human escalation. Assume the model *will* try something unsafe and design so it *can't* execute it. Use the [safety & governance checklist](./safety-governance-checklist.md).

**12. Agents are expensive — how do I control cost?**
Token budgets, tool-call limits, model routing (small models for simple steps), caching, and hard iteration caps. Remember agents fan out to many LLM calls per user request, so size and budget on **LLM calls**, not user requests (see Ch. 5 / Ch. 8).

**13. How do I evaluate an agent when there's no single "right" answer?**
Beyond accuracy: task success/completion rate, efficiency (steps, tokens, cost), safety, tool-usage correctness, and human evaluation of trajectories. Use golden trajectories + LLM-as-a-Judge, and version the **whole agent config** (prompt + tools + memory + retrieval), not just the model.

## Delivery

**14. How do I structure a whole agentic design answer under time pressure?**
(1) Is an agent warranted? (2) Autonomy level. (3) Reasoning pattern. (4) Single vs multi-agent (+ coordination pattern). (5) Tools + MCP/sandboxing. (6) Memory + management. (7) Safety/guardrails/limits + HITL. (8) Observability + eval. Narrate trade-offs at each step — that's what's being graded.
