<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/10xGraph/.github/main/profile/assets/10xgraph-logo-3d.png">
  <img alt="10xGraph Logo" src="https://raw.githubusercontent.com/10xGraph/.github/main/profile/assets/10xgraph-logo-3d.png" width="460">
</picture>

<h3>State-Graph Engine for Autonomous AI Agents</h3>

<p align="center">
  Compile typed Python state graphs into self-hosted, replay-safe production servers.<br />
  Durable Redis checkpoints, zero double tool executions, per-tool RBAC, and real-time SSE streaming.
</p>

<p align="center">
  <a href="https://pypi.org/project/10xgraph"><img src="https://img.shields.io/pypi/v/10xgraph.svg?color=005BE6&labelColor=0f172a&logo=pypi&logoColor=white" alt="PyPI Version"></a>
  <a href="https://pypi.org/project/10xgraph"><img src="https://img.shields.io/pypi/pyversions/10xgraph.svg?color=005BE6&labelColor=0f172a&logo=python&logoColor=white" alt="Python Versions"></a>
  <a href="https://github.com/10xGraph/.github/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?color=005BE6&labelColor=0f172a" alt="MIT License"></a>
  <a href="https://docs.10xgraph.com"><img src="https://img.shields.io/badge/Docs-docs.10xgraph.com-005BE6?labelColor=0f172a&logo=googledocs&logoColor=white" alt="Documentation"></a>
  <a href="https://10xgraph.com"><img src="https://img.shields.io/badge/Website-10xgraph.com-005BE6?labelColor=0f172a" alt="Website"></a>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-why-10xgraph">Why 10xGraph</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-benchmarks">Benchmarks</a> •
  <a href="#-organization-repositories">Repositories</a> •
  <a href="#-contributing">Contributing</a>
</p>

---

</div>

## ⚡ Highlights & Superpowers

- **🛡️ Replay-Safe Tool Ledger**: When an agent worker process crashes or times out, 10xGraph resumes from the exact state snapshot. Committed tool calls (e.g. `execute_payment()`) are intercepted and **skipped** instead of double-executed.
- **⚡ Two-Tier State Storage**: Sub-millisecond prompt context from **Redis hot memory cache** (`<0.8ms`) paired with **PostgreSQL cold storage** for auditable telemetry and compliance.
- **🔐 Per-Tool RBAC & Guardrails**: Annotate tools with granular permission scopes (`@tool(permissions=["billing:write"])`). Unprivileged invocations are blocked before the model ever runs them.
- **🚀 Production Server Included**: A single call to `.to_production_server()` compiles your Python graph into an OpenAPI-documented **FastAPI** microservice with JWT auth, owner-only threads, and Docker/k8s specs.
- **🌊 Native SSE & WebSocket Streaming**: Zero-lag event streams for token chunks, tool inputs, and node state transitions.
- **🤝 Multi-Agent Swarms**: Compose autonomous agent clusters with typed Pydantic state contracts and deterministic router $\rightarrow$ specialist handoffs.

---

## 🚀 Quick Start

### 1. Installation

```bash
pip install 10xgraph 10xgraph-api
```

### 2. Define a State Graph Agent (8 Lines)

```python
from 10xgraph import ReactAgent, tool

@tool(permissions=["billing:write"])
async def dispatch_refund(order_id: str, amount: float) -> str:
    """Executes refund through gateway with ledger replay-safety."""
    return f"Approved refund of ${amount} for order {order_id}"

# Compile graph with durable Redis checkpointing
agent = ReactAgent(
    model="gemini-2.5-pro",
    tools=[dispatch_refund],
    checkpointer="redis://localhost:6379",
    max_steps=10
)

# Generates self-hosted FastAPI server with JWT & SSE streaming
app = agent.to_production_server()
```

### 3. Run Production Server

```bash
uvicorn agent_service:app --host 0.0.0.0 --port 8000
```

---

## 🏛️ Architecture

```
                    ┌─────────────────────────────────────┐
                    │      Client Application (Web/CLI)    │
                    └──────────────────┬──────────────────┘
                                       │ HTTP / SSE / WebSockets
                                       ▼
                    ┌─────────────────────────────────────┐
                    │      FastAPI Production Server      │
                    │   • JWT Auth  • Per-Tool RBAC       │
                    └──────────────────┬──────────────────┘
                                       ▼
┌────────────────────────────────────────────────────────────────────────┐
│                        10xGraph Runtime Engine                         │
│                                                                        │
│   ┌──────────────┐       ┌────────────────┐       ┌────────────────┐   │
│   │ Router Agent │ ───►  │ Specialist LLM │ ───►  │ Tool Execution │   │
│   └──────────────┘       └────────────────┘       └────────┬───────┘   │
│                                                            │           │
│                                                            ▼           │
│                                                   ┌────────────────┐   │
│                                                   │ Replay Ledger  │   │
│                                                   └────────────────┘   │
└──────────────────────────────────────┬─────────────────────────────────┘
                                       │
                    ┌──────────────────┴──────────────────┐
                    ▼                                     ▼
        ┌───────────────────────┐             ┌───────────────────────┐
        │    Redis Hot Cache    │             │   PostgreSQL Archive  │
        │ < 0.8ms Thread State  │             │   Auditable Telemetry │
        └───────────────────────┘             └───────────────────────┘
```

---

## 📊 Architectural Benchmarks

| Feature | 10xGraph | LangGraph | CrewAI |
|---|---|---|---|
| **License** | **MIT (100% Free & Open Source)** | MIT (Server is Closed Cloud) | MIT (Enterprise Cloud) |
| **Production Server** | **Built-in (FastAPI + JWT + RBAC)** | Requires LangSmith Managed Cloud | Separate Enterprise Server |
| **Tool Crash Protection** | **Native Replay-Safe Ledger** | Manual custom implementation | Basic session replay |
| **External Dependencies** | **Zero (No LangChain required)** | Requires `langchain-core` | Heavy ecosystem dependencies |
| **Memory Architecture** | **Redis Hot (<0.8ms) + Postgres** | Manual store wiring | Custom Chroma / Vector store |
| **Deployment Specs** | **Auto Docker & Kubernetes specs** | Cloud Deployment only | Manual containerization |

---

## 📦 Organization Repositories

| Repository | Description | Status |
|---|---|---|
| **[10xGraph/10xgraph-docs](https://github.com/10xGraph/10xgraph-docs)** | Monorepo containing the landing page (`10xgraph.com`) and complete documentation (`docs.10xgraph.com`). | ![Build](https://img.shields.io/badge/Astro%207-Passing-005BE6) |
| **[10xGraph/10xgraph](https://github.com/10xGraph/10xgraph)** | Core Python state-graph engine, checkpointer, and server compiler. | ![Python](https://img.shields.io/badge/Python-3.10%2B-005BE6) |
| **[10xGraph/10xgraph-cli](https://github.com/10xGraph/10xgraph-cli)** | CLI for scaffolding agent graphs, testing checkpoints, and managing deployments. | ![CLI](https://img.shields.io/badge/CLI-v0.9.2-005BE6) |
| **[10xGraph/10xgraph-client](https://github.com/10xGraph/10xgraph-client)** | TypeScript/JavaScript SDK with SSE streaming hooks for Next.js and React. | ![TypeScript](https://img.shields.io/badge/TypeScript-SDK-005BE6) |
| **[10xGraph/.github](https://github.com/10xGraph/.github)** | Organization profile, community health files, issue templates, and governance. | ![Profile](https://img.shields.io/badge/Org-Profile-005BE6) |

---

## 🤝 Contributing

We welcome contributions of all kinds! Please review our guidelines before submitting a pull request:

- [Contributing Guide](https://github.com/10xGraph/.github/blob/main/CONTRIBUTING.md)
- [Code of Conduct](https://github.com/10xGraph/.github/blob/main/CODE_OF_CONDUCT.md)
- [Security Policy](https://github.com/10xGraph/.github/blob/main/SECURITY.md)
- [Support Guidelines](https://github.com/10xGraph/.github/blob/main/SUPPORT.md)

---

## 📄 License

10xGraph is free and open-source software licensed under the [MIT License](https://github.com/10xGraph/.github/blob/main/LICENSE).  
*Formerly published as Agentflow.*
