# Engineering Blogs & Papers — Chapter 11 (Harmful-Content Detection / Trust & Safety)

Curated, interview-relevant reading. Focus on *policy + system* design (severity, prevalence, graded enforcement), not just model architectures. Search titles if links move.

> **Living note:** platform policies, transparency reports, and regulation (DSA, online-safety laws) evolve — treat specifics as directional.

## Start here (highest signal)
- **Meta Community Standards Enforcement Report** — the canonical source for **prevalence** as a north-star metric and proactive detection rate. Read how they define and report prevalence.
- **Microsoft PhotoDNA** overview — perceptual hashing for CSAM; why hash-first for known-bad.
- **Meta open-source PDQ & TMK+PDQF** — perceptual hashing for images and video; robustness to transformations.

## Hashing & known-bad sharing
- **GIFCT** (Global Internet Forum to Counter Terrorism) — cross-platform hash sharing for terrorist content.
- **NCMEC** reporting flow — the legal/reporting side of CSAM.
- **YouTube Content ID** — hashing/matching at scale (copyright, but same matching ideas).

## Classifiers & multimodal
- **Perspective API / Jigsaw** (Google) — toxicity classification; calibration and bias lessons.
- **XLM-R** (Conneau et al., 2019) — multilingual transformer for cross-language moderation.
- **Meta "Hateful Memes" challenge** — multimodal (image+text) understanding; why unimodal fails on memes.
- **Whisper** (OpenAI) or comparable ASR — transcribing audio/video for moderation.

## Adversarial robustness & coordination
- Research on **adversarial text/image evasion** (perturbations, homoglyphs, leetspeak).
- **Coordinated Inauthentic Behavior (CIB)** takedown write-ups (Meta) — behavioral/graph detection beyond content.
- Red-teaming and evasion case studies from platform integrity teams.

## Policy, human review & governance
- **Santa Clara Principles** — transparency and appeal in content moderation.
- **EU Digital Services Act (DSA)** overviews — legal obligations shaping design.
- Write-ups on **reviewer wellbeing** and human-review queue design.

## How to use in prep
1. Read Meta's enforcement report to internalize **prevalence** and proactive detection.
2. Be able to explain **hash-match-then-classify** and why hashing is used for CSAM.
3. Have a crisp **severity × confidence → graded action** matrix ready to draw.
4. Prepare one adversarial-evasion example (text-in-image) and how OCR + robustness handles it.
