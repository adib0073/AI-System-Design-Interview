# Self-Assessment: Map Your Role → Expected Depth

A worksheet to calibrate *how deep* you need to go in each area of an AI system design interview, based on the role and level you're targeting. Use it to find your gaps and build a focused prep plan.

> **How to use**
> 1. Pick your **target role** and **target level**.
> 2. Read the expected-depth row for that role in the matrix below.
> 3. Work through your role's checklist, ticking what you can already do *out loud, under time pressure*.
> 4. Turn unchecked items into your prep plan (Section 4).

Depth scale used throughout: **Awareness** (can define it) → **Working** (can design it and pick reasonable options) → **Deep** (can compare alternatives, quantify trade-offs, discuss failure modes) → **Strategic** (can set multi-year direction across teams).

---

## 1. Expected-depth matrix (role × dimension)

| Dimension | ML Engineer | AI/ML Architect | Eng. Manager | Staff/Principal | Applied Scientist | Data Engineer (ML) |
|-----------|-------------|-----------------|--------------|-----------------|-------------------|--------------------|
| Problem scoping & requirements | Deep | Deep | Deep | Strategic | Working | Working |
| High-level architecture | Deep | Strategic | Working | Strategic | Working | Working |
| Data pipelines & quality | Deep | Deep | Working | Deep | Working | **Strategic** |
| Feature engineering & feature store | Deep | Deep | Working | Deep | Working | Deep |
| Modeling & algorithm choice | Deep | Deep | Working | Deep | **Strategic** | Awareness |
| Evaluation (offline/online, A/B) | Deep | Deep | Working | Deep | **Strategic** | Awareness |
| Serving & inference (tiers, latency) | Deep | Deep | Working | Deep | Working | Working |
| Scalability & fault tolerance | Deep | Deep | Working | Strategic | Awareness | Deep |
| MLOps / monitoring / drift | Deep | Deep | Working | Deep | Working | Working |
| Trade-off articulation | Deep | Strategic | Deep | Strategic | Deep | Working |
| Cross-system / org impact | Working | Strategic | Deep | **Strategic** | Working | Working |
| Communication to stakeholders | Working | Deep | **Strategic** | Strategic | Working | Working |

**Bolded** cells are the *signature* areas each role is most scored on. Everything else still needs to reach at least "Working" to clear the bar.

---

## 2. Level modifier (applies on top of your role)

The rubric doesn't change with level — the **bar** does. Adjust your expectations:

- [ ] **L4 (Mid):** Design a single component or small system correctly. Structure provided by the interviewer is fine.
- [ ] **L5 (Senior):** Own an end-to-end system; go deep in 1–2 areas; name 2–3 real trade-offs; handle moderate ambiguity.
- [ ] **L6 (Staff):** Think cross-system and multi-team; discuss extensibility, adoption/migration, and multi-year evolution.
- [ ] **L7+ (Principal / technical EM):** Frame the problem as much as solve it; show vision, strategy, and stakeholder alignment; thrive in ambiguity.

> If you're targeting a level up, deliberately raise scope and ambition even when the fundamentals are the same.

---

## 3. Per-role readiness checklists

Tick only what you can do *while narrating your reasoning, in ~45 minutes*.

### ML / AI Engineer — end-to-end ownership
- [ ] Frame an ambiguous product ask as an ML problem (task type, labels, success metrics)
- [ ] Draw an end-to-end architecture: ingestion → features → training → serving → monitoring
- [ ] Design offline vs. online feature computation and explain train/serve skew
- [ ] Pick a model type with justification, not by hype
- [ ] Connect offline metrics → online metrics → business metrics
- [ ] Design an A/B test (assignment, guardrails, duration, significance)
- [ ] Explain serving tiers and hit a stated latency budget
- [ ] Describe drift detection and a retraining trigger strategy
- [ ] Discuss rollback, canary/shadow deploys, and graceful degradation

### AI / ML Architect — cross-system breadth
- [ ] Show how this system interoperates with platform/data/other ML systems
- [ ] Justify framework/infra/tooling choices against org constraints
- [ ] Design for extensibility and avoid decisions that become tech debt
- [ ] Balance competing stakeholder needs explicitly
- [ ] Sketch a multi-year evolution path for the system

### Engineering Manager — technical bar
- [ ] Explain the design clearly to a non-technical stakeholder
- [ ] Factor team size, skills, and delivery timelines into the design
- [ ] Identify the riskiest areas and where you'd invest research/staffing
- [ ] Demonstrate enough depth to pressure-test an IC's design
- [ ] Tie technical choices to business/customer outcomes

### Staff / Principal Engineer — organizational impact
- [ ] Position the system in the broader product/platform ecosystem
- [ ] Describe how you'd drive alignment across teams (influence without authority)
- [ ] Articulate a technical vision and prioritize among competing initiatives
- [ ] Handle deliberately under-specified prompts by framing the problem

### Applied Scientist — research-to-production rigor
- [ ] Justify model/algorithm choices with depth (assumptions, alternatives)
- [ ] Design rigorous offline evaluation (datasets, leakage, metrics)
- [ ] Design experiments with statistical validity (power, duration, guardrails)
- [ ] Explain how you'd bridge prototype → production
- [ ] Reach at least "Working" on serving/infra so the system is deployable

### Data Engineer (ML-adjacent) — pipelines for ML
- [ ] Design scalable ETL; choose batch vs. streaming with trade-offs
- [ ] Handle schema evolution and data quality/validation
- [ ] Design feature storage and low-latency feature serving
- [ ] Address lineage, governance, and compliance in an ML context
- [ ] Show how your pipelines support downstream training and inference

---

## 4. Build your prep plan

1. **Circle your signature (bolded) dimensions** in Section 1 — these must reach **Deep/Strategic**. If any are only "Working," they're your #1 priority.
2. **List every unchecked box** from your role's checklist in Section 3.
3. **Flag your "at least Working" gaps** — any dimension in your row rated Deep/Strategic that you can't yet design at all.
4. **Sequence it:** signature gaps → clear-the-bar gaps → level modifier (Section 2) → company specifics (see `interview-prep-resources.md`).

> Re-take this after each mock interview. Movement from "Awareness → Working → Deep" across your signature dimensions is the signal you're interview-ready.
