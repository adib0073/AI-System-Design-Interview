# Responsible-AI Checklist (Worksheet)

A design-time checklist mirroring Chapter 8's Responsible AI sections: **fairness, bias mitigation across the pipeline, explainability, privacy, and governance/regulation.** Use it when a design touches consequential decisions (hiring, credit, healthcare, education, moderation).

> **Framing (Ch. 8):** Responsible AI is a **core system design consideration, not an afterthought.** Interviewers want practical mitigation mechanisms across the lifecycle — not memorized fairness formulas. Bias is a **data and system problem**, not just a model problem.

Tick each item or write "N/A — because…".

---

## 1. Fairness (pick the definition deliberately)
- [ ] **Defined the fairness objective** for this domain and stated the trade-off:
  - **Demographic parity** — similar positive rates across groups.
  - **Equalized odds** — similar TPR *and* FPR across groups.
  - **Individual fairness** — similar individuals get similar outcomes (needs a similarity metric — itself a bias risk).
- [ ] **Acknowledged conflicts** — when base rates differ across groups, parity and equalized odds generally can't both hold. Chose based on domain, regulation, stakeholders, and relative cost of error types.
- [ ] **Identified protected attributes** and the relevant groups to measure across.

## 2. Bias detection & mitigation across the pipeline
Bias enters at *every* stage — mitigate system-wide (Ch. 8 Fig 8.2).
- [ ] **Data collection** — audit for sampling/historical bias and underrepresented groups; apply stratified/balanced sampling or synthetic augmentation.
- [ ] **Feature engineering** — find & remove **proxy variables** (e.g., ZIP code ~ race); use fairness-aware feature selection.
- [ ] **Model training** — apply fairness constraints (reweighting, adversarial debiasing, fairness-aware objectives) where warranted.
- [ ] **Serving & monitoring** — track performance/fairness metrics **per group**, run periodic fairness audits, apply post-processing (threshold adjustment) if appropriate; include fairness metrics in A/B tests.

## 3. Explainability (match the audience)
- [ ] **Global vs local** — decided whether you need to explain overall behavior, individual predictions, or both.
- [ ] **Stakeholder-appropriate explanations** — regulators (compliance reports), domain experts (evidence), end users (concise/understandable).
- [ ] **Traditional ML** — chose techniques (SHAP, LIME, feature importance, partial dependence, attention) as relevant.
- [ ] **For LLM/agent systems:**
  - [ ] **Trajectory as explanation** — record plan, reasoning steps, tool calls/outputs, observations as a human-readable audit trail (same trace used for observability + safety).
  - [ ] **Grounding & provenance** — attribute every claim to evidence (retrieved docs, records, tool outputs); citations often beat model-internal explanations.
  - [ ] **Chain-of-Thought caution** — treat CoT as a UX/debugging aid, **not** a faithful causal account; back important decisions with evidence + independent validation.
  - [ ] **Agent Cards** — document objectives, tools, permitted data sources, guardrails, escalation policies, limitations, known failure modes.
  - [ ] **Multi-agent attribution** — record which agent performed each action.
  - [ ] **Confidence & escalation** — expose confidence and explain why a task was escalated to a human.

## 4. Privacy & data protection
- [ ] **Data minimization & retention limits** — collect/keep only what's needed; enforce retention + forgetting (incl. memory in agents — Ch. 7).
- [ ] **PII handling** — detect/redact PII before training, logging, and in agent memory.
- [ ] **Privacy-preserving techniques** where warranted — differential privacy, federated learning (Ch. 4).
- [ ] **Access control & encryption** — least privilege, encryption in transit/at rest, audit logging (Ch. 3).
- [ ] **Right to erasure / data subject rights** — supported (GDPR/CCPA).

## 5. Governance & regulatory compliance
- [ ] **Mapped applicable frameworks:**
  - **EU AI Act** — risk-based; high-risk uses (hiring, credit, critical infra) need data governance, transparency, human oversight, documentation, conformity assessment.
  - **NIST AI RMF** — Govern / Map / Measure / Manage.
  - **Sector-specific** — HIPAA (health), FCRA (credit), FDA (medical devices), etc.
- [ ] **Risk classification** of the AI use case (and stricter controls as risk rises).
- [ ] **Internal governance:**
  - [ ] Responsible-AI review board for high-risk applications.
  - [ ] Pre-deployment impact & risk assessment.
  - [ ] Human oversight/approval workflow for high-stakes decisions.
  - [ ] Incident response & rollback procedures for AI failures.
  - [ ] Documentation of design decisions, trade-offs, and policies (model cards / agent cards) for audit.

## 6. Ongoing operation
- [ ] **Monitoring across three dimensions** (Ch. 8): system health (latency/errors), behavior (drift, fairness per group, task success), business impact (cost, quality, safety).
- [ ] **Drift & degradation alerts** wired to retraining/rollback runbooks.
- [ ] **Feedback & escalation loop** for harmful/unfair outcomes reported by users.

---

### Interview one-liners
- *Fairness:* "I'd pick equalized odds here because false positives and false negatives have very different costs, and I'd state that it conflicts with demographic parity given unequal base rates."
- *Bias:* "Bias isn't just a model issue — I'd mitigate at data collection, feature engineering, training, and monitoring."
- *Explainability (agents):* "The execution trajectory plus source provenance is my explanation; I'd treat chain-of-thought as a UX aid, not ground truth."
- *Governance:* "This is likely EU AI Act high-risk, so I'd add human oversight, documentation, and a pre-deployment risk assessment."
