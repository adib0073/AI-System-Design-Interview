# Key Terms — Chapter 11 (Harmful-Content Detection / Trust & Safety)

Interview-oriented definitions for the vocabulary in Chapter 11 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Costs, severity & policy
- **Severity** — Policy-defined harm level (e.g., CSAM > graphic violence > mild spam) that determines the feared error and the action. *Why it matters:* the whole system is organized around severity, not a single threshold.
- **Asymmetric error costs** — Missing a high-severity item is far worse than over-removing a benign one (and vice versa for low-severity). *Why it matters:* the defining property; you tune per-severity operating points, not one global threshold.
- **Graded enforcement** — Actions beyond remove/allow — reduce reach, label, age-gate, restrict. *Why it matters:* lets you act **under uncertainty** proportionally instead of a binary keep/delete.
- **Prevalence** — The share of content *views* that are violating. *Why it matters:* the **reach-weighted north-star** quality metric — measures harm experienced, not raw counts.
- **Proactive detection rate** — Share of violating content caught before users report it. *Why it matters:* measures how much the system catches on its own vs. relying on reports.
- **Appeal / overturn rate** — Share of decisions users appeal / share of appeals reversed. *Why it matters:* the key **over-enforcement** signal; a rising overturn rate means you're removing too aggressively.

### Detection techniques
- **Hash matching (perceptual hashing)** — Matching content against known-bad databases via robust fingerprints (PhotoDNA, PDQ, Content ID) that survive crops/re-encodes. *Why it matters:* the exact-match backbone for known CSAM/terror/copyright — cheap, precise, and legally required.
- **OCR (Optical Character Recognition)** — Extracts text embedded in images. *Why it matters:* catches text-in-image evasions (hate speech baked into a meme).
- **ASR (Automatic Speech Recognition)** — Transcribes audio to text. *Why it matters:* lets text models moderate audio/video.
- **XLM-R** — A multilingual transformer for cross-language classification. *Why it matters:* content is global; one multilingual model beats per-language models for coverage.
- **Active learning** — Selectively sampling uncertain/disagreement cases for human labeling. *Why it matters:* labels are scarce and expensive; spend them where the model is unsure.

### Specific harms & sharing
- **CSAM** — Child sexual abuse material; zero-tolerance, hash-matched, auto-removed, legally reportable (e.g., to NCMEC). *Why it matters:* the canonical zero-tolerance, hash-first, human-minimized flow.
- **GIFCT** — Global Internet Forum to Counter Terrorism; shares hashes of terrorist content across platforms. *Why it matters:* cross-platform hash sharing multiplies coverage for known-bad.
- **Coordinated inauthentic behavior (CIB)** — Networks of fake/coordinated accounts. *Why it matters:* detected via behavioral/graph signals, not content alone — links to fraud (Ch. 12).

### Humans & adversaries
- **Human-in-the-loop** — Routing uncertain/high-impact cases to human reviewers whose decisions become training labels. *Why it matters:* the accuracy backstop and label source; design the queue by severity × confidence.
- **Red teaming** — Internal adversarial testing to discover evasions before adversaries do. *Why it matters:* moderation is adversarial; you must probe your own blind spots.
- **Adversarial robustness** — Resisting deliberate evasion (leetspeak, image perturbation, code-switching). *Why it matters:* attackers adapt continuously; static models decay — favor robust signals and fast retraining.

---

*Cross-refs:* multimodal encoders, OCR/ASR, embeddings → Ch. 6/14. Graph/coordination & imbalance → Ch. 12. Human-review queues & HITL → Ch. 7/13. Drift, fairness, governance → Ch. 8.
