# Mock AI System Design Problems

> Practice bank for **timed (35–40 minute) AI system design rounds**, companion to *Cracking the AI System Design Interview*.

Each file below is a **self-contained mock interview**: the prompt as an interviewer would give it, a **40-minute game plan**, a full walkthrough using the **CHASE** framework, a **Mermaid** high-level diagram and a comprehensive **final architecture** diagram, plus — inside *every* CHASE phase — **Tips & suggestions** and **Expected interviewer follow-ups** (with answers). Read a file end-to-end and you should be able to reproduce a strong answer out loud.

> **Diagrams:** high-level and final-architecture diagrams are written in [Mermaid](https://mermaid.js.org/), which renders automatically on GitHub. In an editor without Mermaid support you'll see the diagram source in a code block.

## How to use this bank

1. **Simulate the clock.** Set a 40-minute timer, read only the *Prompt* section, and design out loud before reading the solution.
2. **Practice the framework, not memorization.** Every problem uses the same spine — internalize CHASE so any unseen prompt is tractable.
3. **Calibrate to your role.** Each file flags where depth shifts for junior / senior / staff / EM / architect.
4. **Rehearse the follow-ups.** The *Expected interviewer follow-ups* under each phase are the questions interviewers actually ask when they probe — practice answering them out loud before reading the model answer.

## The CHASE framework (used throughout)

| Phase | Name | Typical time (of 40 min) |
|---|---|---|
| **C** | Clarify & Scope | 6–8 min |
| **H** | High-Level Design | 8–10 min |
| **A** | AI/ML Deep Dive | 10–12 min |
| **S** | System & Infra Deep Dive | 6–8 min |
| **E** | Extensions & Trade-offs | 4–5 min |
| — | Recap & close | 1–2 min |

> **Golden rule for a 40-minute round:** you cannot cover everything. **Signpost, prioritize, and drive.** State the plan, get buy-in on scope, go deep where the *AI* is, and name trade-offs instead of exhausting them.

## Problem index

| # | Problem | Primary archetype |
|---|---|---|
| [01](./01-customer-churn-prediction.md) | Predict customer churn for a subscription service | Classic ML / tabular prediction |
| [02](./02-google-notebooklm.md) | Design Google NotebookLM | RAG over user corpus + multimodal generation |
| [03](./03-google-antigravity.md) | Design Google Antigravity (agentic IDE) | Agentic coding platform |
| [04](./04-creative-writing-assistant.md) | Generative creative-writing assistant | LLM generation + feedback loops |
| [05](./05-google-maps-storefront-detection.md) | Storefront image detection in Google Maps | Computer vision at scale |
| [06](./06-glean-enterprise-search.md) | Design Glean (enterprise knowledge search) | Enterprise RAG + permissions |
| [07](./07-ai-monitoring-auto-remediation.md) | AI-assisted monitoring & auto-remediation | AIOps / agentic ops |
| [08](./08-google-lens.md) | Design Google Lens | Visual search & recognition |
| [09](./09-workspace-fraud-bot-defense.md) | Real-time fraud & coordinated-bot defense (Workspace) | Adversarial abuse detection |
| [10](./10-amazon-rufus.md) | Design Amazon Rufus (shopping assistant) | Conversational commerce RAG agent |
| [11](./11-mock-interview-agent.md) | Virtual mock-interview agent | Conversational eval agent |
| [12](./12-interior-designer-agent.md) | Interior-designer agentic system | Multimodal generative agent |
| [13](./13-amazon-fashion.md) | Design Amazon Fashion | Recommendations + visual + GenAI |
| [14](./14-amazon-ring-authentication.md) | User identification & authentication in Amazon Ring | Biometric / face recognition + security |
| [15](./15-autonomous-swe-agent-platform.md) | Autonomous software-engineering agent platform | Multi-agent coding at repo scale |

---

*These problems intentionally mix classic ML, LLM/RAG, multimodal, and agentic archetypes so you practice choosing the right tool, not forcing one pattern onto every prompt.*
