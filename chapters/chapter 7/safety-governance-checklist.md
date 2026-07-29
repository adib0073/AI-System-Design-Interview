# Agent Safety & Governance Checklist (Worksheet)

A pre-design checklist for making an agent safe to run in production. Work top to bottom when you design or review an agentic system. The guiding principle from Chapter 7:

> **Assume the agent can generate incorrect or unsafe actions.** Don't trust the model — design the system so it *cannot* perform unauthorized operations even if it tries. Safety is defense-in-depth: model-level + application-level.

Tick each item or write "N/A — because…".

---

## 1. Sandboxing & permissions (what the agent *can* touch)
- [ ] **Tool sandboxing** — code runs in isolated containers/sandboxed runtimes; no ambient network/filesystem access.
- [ ] **Filesystem allowlist** — file ops restricted to approved directories (no path traversal).
- [ ] **Network egress control** — only approved hosts/APIs reachable from the sandbox.
- [ ] **Least-privilege permissions** — read-only by default; write/admin granted per-tool, per-agent, explicitly.
- [ ] **Tool allowlist (deny by default)** — only approved tools/APIs/operations are callable.
- [ ] **Dynamic tool review** — newly discovered tools (e.g., MCP servers) are reviewed/approved before use, not auto-trusted.
- [ ] **Resource limits** — CPU/memory/disk caps per execution.

## 2. Action validation & confirmation gates (what the agent *does*)
- [ ] **Pre-action validation** — verify tool parameters before execution (types, ranges, injection, path traversal).
- [ ] **Risk classification** — actions tagged low/medium/high; governance scales with risk (don't gate everything the same).
- [ ] **Confirmation gates** — explicit human approval required before destructive/irreversible/high-value actions (delete data, refunds, payments, sending external comms).
- [ ] **Output validation** — tool outputs checked against expected format/constraints before the agent uses or displays them.
- [ ] **Idempotency** — retried actions can't double-charge/double-send.

## 3. Loop & cost limits (how long / how much)
- [ ] **Iteration caps** — max reasoning steps / retries / tool calls per task.
- [ ] **Per-step timeouts** — terminate slow/unresponsive tool calls.
- [ ] **Overall execution limit** — cap total wall-clock duration of a run.
- [ ] **Cycle detection** — detect repeated reasoning/tool patterns and halt.
- [ ] **Progress checks** — require meaningful progress each iteration; halt/recover if none over N steps.
- [ ] **Token budget** — cap input+output tokens per task.
- [ ] **Tool-call budget** — cap expensive/rate-limited external calls.
- [ ] **Model routing budget** — cheap models for simple sub-tasks; reserve large models for hard reasoning.

## 4. Rate limiting (shared-resource protection)
- [ ] **Per-user limits** — requests/tokens/tool calls per user.
- [ ] **Per-tool limits** — protect expensive/rate-limited services.
- [ ] **Global quotas** — system-wide caps to protect shared infra (often enforced at an AI Gateway / reverse proxy).

## 5. Safety guardrails (content & scope)
- [ ] **Input guardrails** — block harmful content, prompt injection, jailbreak attempts.
- [ ] **Output guardrails** — filter unsafe/policy-violating outputs.
- [ ] **PII protection** — detect/redact PII in inputs, outputs, and memory.
- [ ] **Domain restrictions** — keep the agent in scope (no unapproved medical/legal/financial advice; only approved knowledge bases).
- [ ] **Rules enforced structurally** — behavioral rules ("always cite", "never expose PII", "approve before emails") enforced via policy engine/validation/guardrails, not just the system prompt.

## 6. Human-in-the-loop
- [ ] **Plan preview** — present the proposed plan before executing high-risk work.
- [ ] **Explicit approval** for high-risk actions.
- [ ] **Escalation path** — transfer to a human when confidence is low or automated recovery fails.
- [ ] **Approvals recorded** for audit/compliance.

## 7. Failure handling & recovery
- [ ] **Retries with backoff** for transient failures.
- [ ] **Fallbacks** — alternative tools/models/agents on failure or low confidence.
- [ ] **Partial results** — return completed portions rather than failing the whole task.
- [ ] **Graceful degradation** on unavailable tools/servers/timeouts.

## 8. Observability & audit (prove what happened)
- [ ] **Logging** — model inputs/outputs, tool calls, parameters, results, errors.
- [ ] **Trajectory tracing** — full end-to-end execution path across agents/tools/services.
- [ ] **Metrics** — task success rate, latency, token usage, cost, tool utilization, failure rate, loop/timeout rate, human-escalation rate.
- [ ] **Audit trail** — durable record for compliance and incident investigation.
- [ ] **Memory hygiene** — summarization, retention policies, and forgetting (e.g., GDPR); no unbounded memory growth.

---

### Risk-tiering quick reference
| Risk tier | Examples | Minimum controls |
|---|---|---|
| **Low** | Read a doc, summarize, search | Sandbox + logging |
| **Medium** | Write to a scratch store, call an internal API | Pre-validation + rate limits + output validation |
| **High** | Delete data, payments, external comms, prod changes | Confirmation gate + human approval + audit + idempotency |

> **Interview line:** "Not every action carries the same risk — I'd classify actions and apply increasingly strict validation/approval as impact rises, balancing safety, UX, and cost." Pair with the [pattern-selection guide](./agent-pattern-selection.md).
