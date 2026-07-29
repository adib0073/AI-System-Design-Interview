# MCP & A2A — Specs, Frameworks & Links (Living Reference)

Pointers to the protocols and frameworks behind agentic systems: **MCP** (agent ↔ tools/data), **A2A** (agent ↔ agent), and the major agent frameworks. This space moves fast.

> ⚠️ **Living document — verify before relying on specifics.** Protocol versions, framework APIs, and vendor support change frequently. In interviews, focus on *why these protocols exist and their architectural trade-offs* (permissions, latency, reliability, governance), not spec details. Last reviewed: 2026.

---

## The one-line distinction
- **MCP** connects an **agent → external tools & data** (resources, tools, prompts).
- **A2A** connects an **agent → another agent** (discover, message, delegate).
- They're **complementary** and often used together in production.

---

## Model Context Protocol (MCP)
Open standard for connecting AI models to tools, data sources, and services through one common interface — build an MCP server once, reuse across models/IDEs/frameworks.

- **Spec & docs:** https://modelcontextprotocol.io/ · spec: https://spec.modelcontextprotocol.io/
- **GitHub org (SDKs: Python, TypeScript, etc.):** https://github.com/modelcontextprotocol
- **Reference servers / examples:** https://github.com/modelcontextprotocol/servers

**What MCP defines:** Resources (read-only data), Tools (executable functions), Prompts (reusable templates). Client–server model over JSON-RPC.

**Architectural talking points (what interviews actually probe):**
- Permissions & least privilege on tools/data; explicit approval for dynamically discovered servers.
- Added latency of remote servers vs. local tools.
- Reliability: handle unavailable servers, failed invocations, timeouts.
- Tool discovery quality: too many tools → wrong-tool selection; invest in schemas/descriptions.

## Agent-to-Agent (A2A) Protocol
Open standard for autonomous agents to discover, communicate with, and delegate tasks to one another across frameworks/vendors.

- **Docs & spec:** https://a2a-protocol.org/ (project now under the Linux Foundation)
- **GitHub:** https://github.com/a2aproject/A2A
- **Concepts:** Agent Cards (capability advertisement/discovery), task delegation, structured messages, streaming updates.

**Architectural talking points:** interoperability across heterogeneous agents; conflict resolution (voting / mediator / rule-based); coordination overhead; security of inter-agent messages.

---

## Agent frameworks (build layer)
| Framework | Maintainer | Niche |
|---|---|---|
| **LangGraph** | LangChain | Graph-based stateful agent/workflow orchestration | 
| **LlamaIndex (Workflows/Agents)** | LlamaIndex | RAG-centric agents, data connectors |
| **CrewAI** | CrewAI | Role-based multi-agent "crews" |
| **AutoGen / AG2** | Microsoft / community | Conversational multi-agent orchestration |
| **OpenAI Agents SDK** | OpenAI | Lightweight tool-using agents + handoffs |
| **Google ADK (Agent Development Kit)** | Google | Agent building with A2A support |
| **Semantic Kernel** | Microsoft | Enterprise orchestration, .NET/Python |
| **Strands Agents** | AWS | Model-driven agents, MCP/A2A friendly |
| **Pydantic AI** | Pydantic | Type-safe, structured agent outputs |

**Agent "harness" tools (production agents):** Claude Code, Codex CLI, OpenHands — implement the *Agent = Foundation Model + harness* pattern (system prompts + tools/MCP + memory + loop + sandbox + guardrails).

## Sandboxing / execution runtimes
- **E2B** (https://e2b.dev/) · **Modal** (https://modal.com/) · **Daytona** · **Docker** containers · cloud **serverless** (AWS Lambda, GCP Cloud Functions) — isolated code execution for agents.

## Observability / eval for agents
- **LangSmith**, **Langfuse** (https://langfuse.com/), **Arize Phoenix**, **Braintrust**, **OpenLLMetry** — trajectory tracing, evals, cost/latency/token tracking. (See also Ch. 8 observability.)

---

### Maintaining this page
Update framework rows and protocol versions as the ecosystem shifts, and bump "Last reviewed." Keep this out of the printed book — link here instead. Corrections via issue/PR. If a link 404s, search the project name.
