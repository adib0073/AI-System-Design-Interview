# Chapter 5 — References & External Links

Consolidated home for the URLs referenced in Chapter 5. Keeping them here (rather than as bare links printed in the chapter) keeps the page clean and lets us fix dead links without a reprint.

> **In the book:** replace inline URLs with a pointer such as *"See `chapter 5/references.md` in the companion repository (github.com/adib0073/AI-System-Design-Interview)."*

---

## Latency numbers ("Numbers Everyone Should Know")
The latency ladder in §5.2 is adapted from Jeff Dean's widely cited talk and the Google SRE rule-of-thumb sheet.

- **Jeff Dean — "Numbers Everyone Should Know" (talk):** https://www.youtube.com/watch?v=l2mSDst_E0o
- **Google SRE — Rule-of-thumb latency numbers (PDF):** https://static.googleusercontent.com/media/sre.google/en//static/pdf/rule-of-thumb-latency-numbers-letter.pdf
- Interactive version (community): "Latency Numbers Every Programmer Should Know" — search for Colin Scott's interactive chart, which shows how these numbers evolve by year.

## Companion code & worked examples
- **This repository:** https://github.com/adib0073/AI-System-Design-Interview
- Additional worked estimation examples referenced in §5.7 live in this repo (see the `chapter 5/` folder).

## Hardware / cost references (for sizing)
These back the GPU-compute and cost figures in §5.5. They are **volatile** — verify current specs and prices before quoting.
- **NVIDIA A100 datasheet** (≈312 FP16 TFLOPS, 80 GB): https://www.nvidia.com/en-us/data-center/a100/
- **NVIDIA H100 datasheet** (≈989 FP16 / ≈1,979 FP8 TFLOPS, 80 GB): https://www.nvidia.com/en-us/data-center/h100/
- Cloud GPU pricing varies by provider/region and changes often — check AWS/GCP/Azure/Lambda/CoreWeave directly. Spot/preemptible instances are typically 60–70% cheaper.

---

### Link-maintenance note
If any link here is dead, please open an issue or PR. External datasheets and pricing pages move frequently; the formulas in [`reference-card.md`](./reference-card.md) do not.
