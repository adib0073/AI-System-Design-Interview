# Engineering Blogs & Papers — Chapter 17 (Code Review & Code-Quality Agent)

Curated, interview-relevant reading. Focus on *precision/trust and verification*, not model size. Search titles if links move.

> **Living note:** AI code-review products evolve fast — treat vendor entries as directional and read claims critically.

## Start here (highest signal)
- **Google "Tricorder: Building a Program Analysis Ecosystem"** (Sadowski et al., ICSE 2015) — the thesis of the whole chapter: **low false positives + per-check opt-in** drive adoption. Read first.
- **"Lessons from building static analysis tools at Google"** (CACM) — why developer trust and false-positive rate matter more than coverage.
- **Anthropic "Building effective agents"** — grounding, tool use, and keeping agents simple (shared with Ch. 7/13).

## Static analysis foundations
- **Semgrep** and **CodeQL (GitHub)** docs — pattern/data-flow static analysis; what rules catch and their false-positive behavior.
- **SonarQube / Coverity** overviews — enterprise SAST context.
- **Meta Infer** — static analysis for null-deref/leaks at scale.

## AI code review (products & write-ups)
- **GitHub Copilot code review** — LLM PR review with inline comments + suggestions; incremental review.
- **Amazon CodeGuru Reviewer** — early ML-based reviewer at scale.
- **CodeRabbit / Qodo (Codium) PR-Agent / Graphite Diamond / Cursor Bugbot** — modern LLM reviewers; read on the precision-vs-noise battle.

## Grounding & code retrieval
- **Sourcegraph** code-graph/search write-ups — symbol/dependency navigation for grounding.
- LSP / code-embedding retrieval discussions — structured vs. semantic code search.

## Autonomous fixing & evaluation
- **SWE-bench** (Jimenez et al., 2023) and **SWE-agent** — verifiable evaluation via hidden tests; the auto-fix extension.
- **Mutation testing** references — measuring recall with injected bugs.

## Safety
- **OWASP Top 10 for LLM Applications** — prompt injection, excessive agency; maps to untrusted-code and action-gating.
- Sandboxing/isolation guides (gVisor, Firecracker, ephemeral containers) — safely executing untrusted PR code.

## How to use in prep
1. Read the Tricorder paper — it justifies **precision-over-recall / trust** better than anything.
2. Memorize the **ground → verify (sandbox) → gate** spine.
3. Have the **injected-bug + acceptance/dismissal** evaluation answer ready.
4. Prepare crisp answers on **untrusted-code sandboxing**, **prompt injection**, and **self-hosted models for IP**.
