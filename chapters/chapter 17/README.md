# Chapter 17 — Code Review & Code-Quality Agent

Companion resources for Chapter 17, the second agentic case study. Its governing constraint is unusual: **developer trust is fragile, so precision matters far more than recall.** A noisy reviewer gets muted within a week.

Chapter 17 covers traditional static analysis/linters/defect prediction, the agentic approach (reasoning over diffs), repository context/code grounding, sandboxed test execution & tool use, high-precision comment generation, false-positive/trust management, CI/CD & VCS integration, safety/security (untrusted code, prompt injection, secrets/IP), evaluation (acceptance rate, injected-bug catch), and infra/serving.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 17 glossary slice (static analysis/SAST, code grounding, symbol/dependency graph, sandbox, verify-before-comment, precision gating, acceptance/dismissal rate, injected-bug testing, incremental review, model routing, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — precision vs. recall, hybrid vs. LLM-only, grounding, verify-by-execution, security of untrusted code, CI/CD, and evaluation without labels. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Google Tricorder, CodeGuru, CodeRabbit/Qodo, SWE-bench, and prompt-injection/sandboxing for code agents. |

> **How to use:** the graded spine is **ground + verify + gate** (retrieve repo context, run tests in a sandbox to confirm, gate hard on confidence) and the **trust economy** (advisory-first, learn from dismissals). Pair with Chapter 7.
