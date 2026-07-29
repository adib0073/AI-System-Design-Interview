# Agent-Pattern Selection Guide (Cheat Sheet)

Two decisions interviewers push on: **(1) which single-agent reasoning pattern**, and **(2) single agent vs. multi-agent — and if multi-agent, orchestrator vs. supervisor vs. swarm.** Lead with the cheapest thing that meets the requirement, then justify added complexity.

---

## Step 0 — Do you even need an agent?
```
Task well-defined, fixed steps, no exploration/tools needed?
└─ YES → a PIPELINE/WORKFLOW is simpler, cheaper, deterministic. Use that.
Task needs exploration, tool use, or multi-step reasoning that adapts to results?
└─ YES → an AGENT is justified.
```
> "A pipeline is deterministic and stateless; an agent decides, uses tools, and adapts. The differentiators are **autonomy** and **tool use**." Don't reach for an agent to look sophisticated.

## Choose the level of autonomy first
| Level | Human role | Use when |
|---|---|---|
| **Copilot** | Human decides & acts | Suggestions only (code completion, writing) |
| **Assistant** | Human approves significant actions | Enterprise workflows needing compliance/accuracy |
| **Agent** | Human sets the goal; agent runs, escalates when needed | Multi-step tasks with acceptable risk |
| **Autonomous** | Minimal/no supervision | High-scale ops with strong guardrails + fallback |
Pick based on **task complexity, business risk, regulatory requirements, and need for oversight.**

---

## Step 1 — Single-agent reasoning pattern
| Pattern | Best for | Strengths | Watch-outs |
|---|---|---|---|
| **ReAct** (reason + act) | Exploratory, tool-driven tasks | Transparent, easy to debug, natural loop | Verbose; reasoning tokens cost; needs iteration caps |
| **Plan-and-Execute** | Well-structured, multi-step tasks | Clear plan, validatable, supports human approval | Rigid; poor with surprises; can over-plan |
| **Reflexion** (self-critique + retry) | Complex reasoning, code gen | Improves over iterations | Higher latency/cost; loops if reflection is weak |
| **Tree/Graph of Thought** | Search, planning, optimization, math | Explores alternatives, backtracks | Expensive; needs good pruning to stay tractable |

**Quick routing:**
```
Need transparency + tools, tasks vary?          → ReAct
Need up-front, approvable plan (compliance)?     → Plan-and-Execute
Output quality improves with self-critique?      → Reflexion
Many candidate solutions to search/evaluate?     → ToT / GoT
```
Also decide: **stateful?** (needs memory across turns/sessions → add long-term memory, Ch. 7 §memory) and **tool-augmented?** (needs external data/actions → function calling / MCP + sandboxing).

---

## Step 2 — Single agent vs. multi-agent
```
Can one agent (with the right tools) do it within context + latency budgets?
├─ YES → SINGLE AGENT. Cheaper, simpler, easier to debug. Default here.
└─ NO → distinct specialized roles (research/code/retrieve/validate),
        parallelism, or independent scaling needed? → MULTI-AGENT.
```
Multi-agent buys modularity, specialization, and parallelism — at the cost of coordination, communication, latency, and harder failure handling. Justify it.

## Step 3 — Multi-agent coordination pattern
| Pattern | Structure | Best when | Cost |
|---|---|---|---|
| **Orchestrator** (central coordinator) | One coordinator decomposes, delegates to specialists, aggregates | Most cases; clear task decomposition, easy to monitor | Central point of coordination (and failure) |
| **Supervisor** | Coordinator also monitors quality, retries/reassigns, escalates | Correctness/QA/reliability > latency | Extra oversight overhead/latency |
| **Swarm** | Decentralized peers, no central coordinator | Highly distributed problems, no single agent has full knowledge; scale via parallelism | Hard to coordinate/debug; emergent behavior |

**Quick routing:**
```
Need a single, monitorable point of control?          → Orchestrator
Need quality control, retries, human escalation?      → Supervisor
Problem is inherently distributed / peer-collaborative? → Swarm
```
Pair with **A2A** (agent-to-agent) for inter-agent communication and **conflict resolution** (voting / mediator / rule-based). Use **parallel execution** for independent sub-tasks; manage dependencies + synchronization.

---

## The one-paragraph interview answer
> "First, is an agent even warranted, or would a pipeline do? Given [exploration/tool use], I'll use an agent at the **[assistant]** autonomy level so high-risk actions need approval. For reasoning I'd start with **ReAct** (transparent, tool-friendly) and add **Reflexion** only if quality needs iterative self-correction. It's a single agent unless we have distinct specialist roles — then I'd use an **orchestrator** (or **supervisor** if QA/reliability dominates), reserving **swarm** for genuinely distributed problems. Throughout, I'd cap iterations, sandbox tools, and gate destructive actions." → then see [`safety-governance-checklist.md`](./safety-governance-checklist.md).

*Also see* [`key-terms.md`](./key-terms.md) for pattern definitions and [`../chapter 4/decision-trees-checklists.md`](../chapter%204/decision-trees-checklists.md) for the broader GenAI/agentic build checklist.
