# Self-Scoring Scorecard (Mock Interview Worksheet)

Grade your own recorded mock interviews with the same rubric structure interviewers use (from Chapter 1), mapped onto the CHASE phases. Score each dimension 1–4, multiply by its weight, and track your weighted total over time.

> **How to use**
> 1. Record a timed mock (45 or 60 min). 2. Score each dimension below using the descriptors. 3. Compute the weighted total. 4. Re-take after practice and watch the trend.

---

## Core rubric (weighted — sums to 100%)

| Dimension | CHASE phase | Weight | 1 · Poor | 2 · Below bar | 3 · Meets bar | 4 · Strong | Your score (1–4) | Weighted (score × weight) |
|-----------|-------------|--------|----------|---------------|---------------|------------|------------------|----------------------------|
| Requirement gathering | C | 15% | Jumped straight to design | Asked a few questions | Covered scale, latency, constraints | Proactively surfaced edge cases & assumptions | ☐ | |
| High-level design | H | 25% | Incoherent / incomplete | Major components missing | Reasonable, labeled structure | Clean, well-justified, offline/online separated | ☐ | |
| Component depth | A + S | 25% | Superficial everywhere | Surface-level only | Solid depth in 1–2 areas | Deep in multiple areas, real trade-offs | ☐ | |
| Trade-off articulation | E + throughout | 15% | None | Mentioned, not analyzed | Articulated key trade-offs | Quantified / compared alternatives | ☐ | |
| ML-specific reasoning | A | 20% | Model as black box | Minimal ML reasoning | Covered data, model, eval | Comprehensive; offline→online→business metrics | ☐ | |
| **Weighted total** | | **100%** | | | | | | **____ / 4.0** |

**Weighted total = Σ (score × weight).** Interpretation:
- **< 2.0** — Below bar. Focus on the lowest-scoring dimension first.
- **2.0–2.7** — Approaching bar. Usually a depth or trade-off gap.
- **2.8–3.4** — Meets bar (hireable at senior).
- **3.5+** — Strong (staff-level signal).

---

## Communication & collaboration (scored separately, but can sink a strong design)

Rate each 1–4; average them. Chapter 2 stresses these heavily.

| Behavior | 1–4 |
|----------|-----|
| Thought out loud / narrated while drawing | ☐ |
| Used signposting to guide the interviewer | ☐ |
| Drove the conversation (proposed next steps) without ignoring cues | ☐ |
| Paused for feedback & invited participation | ☐ |
| Stated assumptions explicitly | ☐ |
| Read and responded to interviewer cues | ☐ |
| **Communication average** | **____ / 4.0** |

---

## Per-phase execution checklist (did you actually do it?)

**C — Clarify & Scope**
- [ ] Probed product context, scale, constraints, success metrics
- [ ] Wrote a requirements doc
- [ ] Split functional vs. non-functional requirements
- [ ] Named the ML problem type
- [ ] Finished within ~7 minutes

**H — High-Level Design**
- [ ] Drew end-to-end flow with labeled arrows
- [ ] Separated offline vs. online
- [ ] Kept it under ~10 minutes
- [ ] Flagged it as a first draft to refine later

**A — AI/ML Deep Dive**
- [ ] Data sources + collection + labeling strategy
- [ ] Feature types + offline/online + feature store / skew
- [ ] Model choice justified by trade-offs
- [ ] Pipeline: triggers, tracking, versioning
- [ ] Evaluation offline → online → business

**S — System & Infra Deep Dive**
- [ ] Serving method + online/offline inference
- [ ] Scaling + named a concrete bottleneck
- [ ] Justified an autoscaling signal (not just "use autoscaling")
- [ ] Storage: feature store, registry, event/feedback data
- [ ] Caching with a pitfall (invalidation/stampede)
- [ ] Observability + alerts

**E — Extensions & Trade-offs**
- [ ] Edge cases / failure modes (cold start, drift, stale features)
- [ ] Cost optimization
- [ ] Future improvements + responsible-AI note
- [ ] Reached this phase before time ran out

---

## Progress log

| Date | Problem | Company style | Weighted total | Comm. avg | Biggest gap to fix |
|------|---------|---------------|----------------|-----------|--------------------|
|      |         |               |                |           |                    |
|      |         |               |                |           |                    |
|      |         |               |                |           |                    |

> Aim to move each dimension from 2 → 3 → 4 across sessions. A rising **Component depth** and **Trade-off** score is usually what separates a "meets bar" from a "strong" result.
