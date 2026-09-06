# Common Interviewee Doubts — Chapter 11 (Harmful-Content Detection / Trust & Safety)

The questions candidates most often have about trust-and-safety rounds. Grouped by theme.

---

## Framing & metrics

**1. What's the single most important framing for this problem?**
**Asymmetric error costs by severity.** Missing CSAM or terror content is catastrophic; over-removing a benign joke erodes trust and free expression. There is no single threshold — you set operating points **per severity tier** and choose the feared error accordingly. Say this first.

**2. Why not optimize accuracy or even F1?**
Because violating content is rare and harm is **reach-weighted**. Accuracy is dominated by the benign majority. The north-star is **prevalence** — the share of *views* that are violating — because it measures the harm users actually experience. Also track proactive detection rate and appeal/overturn rate.

**3. What does "graded enforcement" buy me?**
It lets you act **under uncertainty** without a binary remove/allow. Options: remove, reduce reach, label/inform, age-gate, restrict features, require review. Low confidence + medium severity → reduce reach rather than delete. This is a senior-level move.

## Techniques

**4. Hashing or a classifier — which?**
Both, layered. **Perceptual hash matching** (PhotoDNA, PDQ, Content ID) handles *known* bad content — cheap, precise, and legally required for CSAM; robust to crops/re-encodes. **ML classifiers** handle *novel* content the hashes miss. Lead with "hash the known, classify the unknown."

**5. How do I handle images, audio, and video, not just text?**
Multi-modal understanding: image/video classifiers, **OCR** for text-in-images (a huge evasion vector), **ASR** to transcribe audio/video into text for text models, and multimodal encoders. Mention that a lot of abuse hides text inside images specifically to dodge text filters.

**6. Content is in 100+ languages — what do I do?**
Use a **multilingual model** (e.g., XLM-R) rather than per-language models, augment low-resource languages, and route uncertain cases to human reviewers with the right language skills. Don't assume English-only.

## Humans & labels

**7. Where do humans fit?**
Human-in-the-loop for **uncertain and high-impact** cases; their decisions become training labels (**active learning** targets the uncertain ones). Design the review queue by severity × confidence, protect reviewer wellbeing (especially for graphic content), and measure reviewer agreement.

**8. Where do labels come from and why are they tricky?**
User reports (noisy, biased), human review (accurate but slow/expensive), and hash databases (precise, known-only). Reports are biased toward what users notice; active learning and audits reduce that bias.

## Adversaries

**9. How do I handle evasion?**
Assume it's **adversarial**: leetspeak, homoglyphs, image perturbations, code-switching, splitting content across posts. Favor robust/multimodal signals, retrain fast, **red team** your own system, and use coordinated-behavior/graph signals (CIB) that are harder to fake than content text.

**10. How do I decide the action from a model score?**
A **severity × confidence policy matrix**: high severity + high confidence → auto-remove (and report, for CSAM); medium → reduce reach or route to human; low → label or allow. The action is a policy decision, not just "score > threshold."

## Delivery

**11. How do I structure the answer under time pressure?**
Clarify (which harms, which surfaces, severity tiers) → architecture (hash match → multimodal classifiers → severity × confidence policy → enforcement) → OCR/ASR/multilingual coverage → human-in-the-loop + active learning → adversarial robustness → metrics (**prevalence**, proactive rate, appeal/overturn). Keep asymmetric costs and prevalence front and center.

**12. What's the most common mistake?**
Treating it as a single binary classifier optimized for accuracy. That ignores severity, reach-weighting, graded actions, adversaries, and human review — i.e., everything that makes trust-and-safety hard.
