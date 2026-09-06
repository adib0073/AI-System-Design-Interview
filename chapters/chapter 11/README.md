# Chapter 11 — Harmful-Content Detection / Trust & Safety

Companion resources for Chapter 11. The defining feature of this domain is **asymmetric error costs** (missing CSAM ≠ over-removing a joke) and **multi-modal, adversarial, multilingual** content at massive scale.

Chapter 11 covers asymmetric costs and severity, multi-modal understanding (text/image/audio/video, OCR, ASR), perceptual **hash matching** (CSAM/PhotoDNA/PDQ), severity × confidence **action policies**, graded enforcement, human-in-the-loop, adversarial robustness, and **prevalence** metrics.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 11 glossary slice (prevalence, hash matching, severity, graded enforcement, CSAM/GIFCT, OCR/ASR, active learning, red teaming, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — asymmetric costs, why prevalence (not accuracy), hashing vs. classifiers, action policies, human review, and adversarial evasion. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Meta community-standards enforcement reports, PhotoDNA/PDQ, Content ID, Perspective API, and adversarial robustness. |

> **How to use:** internalize the **severity × confidence → graded action** framing and **prevalence** as the north-star. Those two ideas separate a real trust-and-safety answer from a generic classifier.
