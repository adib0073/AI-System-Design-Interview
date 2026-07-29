# Chapter 5 — Back-of-the-Envelope Estimation for AI Systems

Companion resources for Chapter 5. Maintained here (not in the printed book) so they can be kept current.

Chapter 5 is the estimation toolkit: traffic (DAU→QPS), storage, bandwidth, and the AI-specific dimensions — GPU memory, KV cache, embedding storage, training FLOPs/time/cost — used to justify architectural decisions.

| File | What it is |
|------|------------|
| [`estimation-problems.md`](./estimation-problems.md) | Expanded drill bank: **29 problems with worked, numerically verified solutions** across traffic/QPS, storage, bandwidth, GPU memory, KV cache, embeddings, training cost, and latency — beyond the 6 worked examples in the chapter. |
| [`estimation-calculators.ipynb`](./estimation-calculators.ipynb) | Interactive (Colab/Jupyter) calculators for DAU→QPS, GPU memory, KV cache, embedding storage, and training cost. Pure Python, no dependencies — edit the inputs and re-run. |
| [`reference-card.md`](./reference-card.md) | One-page quick card: powers of 2, latency ladder, storage sizes, QPS benchmarks, peak multipliers, and all core + AI-specific formulas. Printable. |
| [`references.md`](./references.md) | Consolidated external links (Jeff Dean latency talk, Google SRE PDF, GPU datasheets, companion repo) so the chapter page carries no bare URLs. |
| [`key-terms.md`](./key-terms.md) | Chapter 5 glossary slice (FLOPs, TFLOPS, TTFT, TPS, arithmetic intensity, KV cache, prefill/decode, spot instances, …). Feeds the cumulative book glossary. |

> **Note on links:** hardware specs and cloud prices are volatile — verify before quoting. The formulas don't change. If a link is dead, open an issue/PR.
