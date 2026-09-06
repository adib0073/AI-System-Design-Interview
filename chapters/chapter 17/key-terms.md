# Key Terms — Chapter 17 (Code Review & Code-Quality Agent)

Interview-oriented definitions for the vocabulary in Chapter 17 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Traditional layer
- **Static analysis (SAST)** — Analyzing code without running it to find bugs/vulns (Semgrep, CodeQL, SonarQube). *Why it matters:* fast, precise on known patterns, hallucination-free — the foundation layer you keep.
- **Linter** — Tool flagging style/simple-bug patterns (ESLint, Ruff). *Why it matters:* cheap deterministic checks; let it handle nitpicks so the agent doesn't.
- **Defect prediction** — ML predicting bug-prone files/changes from metrics (churn, complexity). *Why it matters:* prioritizes review effort; classic ML baseline.

### Agentic reasoning & grounding
- **Diff** — The set of changes in a PR (added/removed lines). *Why it matters:* the unit the agent reasons over — but the diff alone is rarely enough.
- **Code grounding** — Retrieving relevant repo context (defs, call sites, conventions) so the agent reasons in situ. *Why it matters:* most real bugs are about interaction with *other* code; grounding prevents hallucinated claims.
- **Symbol / dependency graph** — Structured map of definitions/references/calls used for precise code retrieval. *Why it matters:* more precise than embedding search for "who calls this?" — the crux of cross-file review.
- **Model routing** — Sending easy cases to small/cheap models and hard cases to large reasoning models. *Why it matters:* controls cost per PR at org scale.

### Verification (the precision engine)
- **Sandbox** — Isolated, ephemeral, egress-free environment for safely executing untrusted code. *Why it matters:* mandatory because PR code is untrusted; enables verification without security risk.
- **Verify-before-comment** — Running tests/code to confirm a hypothesized issue before posting it. *Why it matters:* the single biggest lever against hallucinated findings — a bug backed by a failing test is trustworthy.
- **Precision gating** — Only surfacing findings above a high confidence bar; dropping the rest. *Why it matters:* converts many candidate findings into a *few* trustworthy comments — the product's core discipline.

### Trust & measurement
- **Acceptance / dismissal rate** — Share of comments resolved/acted-on vs. dismissed. *Why it matters:* the proxy for precision and the **trust health metric**; rising dismissals mean you're losing the team.
- **Injected-bug / mutation testing** — Introducing known bugs to measure catch rate (recall) with controlled ground truth. *Why it matters:* how you measure recall when you can't label every PR.
- **Incremental review** — Reviewing only new commits on PR update, not the whole PR again. *Why it matters:* cheaper, faster, and avoids re-posting resolved comments (idempotency).

### Integration & safety
- **Advisory vs. blocking check** — Informational status vs. a required check that can block merges. *Why it matters:* start advisory to build trust; block only for proven high-precision categories.
- **Prompt injection** — Malicious text in code/comments attempting to manipulate the agent. *Why it matters:* treat code as untrusted data; injected instructions must not trigger privileged actions.
- **SWE-bench / SWE-agent** — Benchmark/agent for autonomous software issue-fixing. *Why it matters:* the cousin/extension (auto-fix) and a reference for verifiable evaluation.

---

*Cross-refs:* agent fundamentals, tools, sandboxing, guardrails → Ch. 7. RAG (here over code) → Ch. 6. Read/write split, approval gates, prompt injection → Ch. 13. Autonomous SWE agents → Ch. 18 & mock problems 03/15.
