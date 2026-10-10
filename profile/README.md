<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/10xGraph/.github/main/profile/assets/10xgraph-logo-dark.svg">
  <img alt="10xGraph" src="https://raw.githubusercontent.com/10xGraph/.github/main/profile/assets/10xgraph-logo.svg" width="360">
</picture>

### Write the Python agent. 10xGraph builds the production server around it.

10xGraph by 10xScale: graph engineering for production AI agents.

[Website](https://10xgraph.com) · [Docs](https://10xgraph.com/docs) · [Quickstart](https://10xgraph.com/docs/get-started/first-agent) · [Changelog](https://10xgraph.com/changelog)

[![PyPI 10xgraph](https://img.shields.io/pypi/v/10xgraph?label=10xgraph)](https://pypi.org/project/10xgraph/)
[![PyPI 10xgraph-api](https://img.shields.io/pypi/v/10xgraph-api?label=10xgraph-api)](https://pypi.org/project/10xgraph-api/)
[![npm 10xgraph-client](https://img.shields.io/npm/v/10xgraph-client?label=10xgraph-client)](https://www.npmjs.com/package/10xgraph-client)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](https://github.com/10xGraph/10xGraph/blob/main/LICENSE)

</div>

10xGraph is an open-source Python framework for multi-agent AI systems. Other frameworks give you the graph. 10xGraph gives you the graph and the production server around it, under the MIT license. Formerly Agentflow.

### What you get

- **The production server, in the box.** `10xgraph-api` serves your compiled graph over REST, SSE, WebSocket and realtime audio, with JWT or custom auth, scoped authorization on every endpoint, owner-only threads and rate limiting, and writes your Docker Compose and Kubernetes files. No paid tier.
- **Correct under failure.** A tool that already ran is not run again after a crash or retry: no double charge, no duplicate email. State writes are versioned, and node and tool timeouts stop a hung tool from holding a worker.
- **Built to scale.** Active threads are cached in Redis, durable history lives in PostgreSQL, and events stream to Kafka, Redis, RabbitMQ or OpenTelemetry.
- **One stack, backend to frontend.** A typed TypeScript client, and remote tools that run in the user's browser.
- **You own it.** Self-hosted, any model (OpenAI, Google Gemini, Anthropic), no LangChain dependency.

10xGraph is pre-1.0: pin your versions and read the changelog when you upgrade.

### Packages

| Package | Install | Repository |
|---|---|---|
| Core engine | `pip install 10xgraph` | [10xGraph/10xGraph](https://github.com/10xGraph/10xGraph) |
| Production server and CLI | `pip install 10xgraph-api` | [10xGraph/10xgraph-api](https://github.com/10xGraph/10xgraph-api) |
| TypeScript client | `npm install 10xgraph-client` | [10xGraph/10xgraph-client](https://github.com/10xGraph/10xgraph-client) |
| Website and docs | [10xgraph.com](https://10xgraph.com) | [10xGraph/10xgraph-docs](https://github.com/10xGraph/10xgraph-docs) |

### Get involved

Your first pull request can be small: a typed module, an example, a fixed doc. Start with the [contributing guide](https://github.com/10xGraph/10xGraph#contributing), meet the people who build 10xGraph at [10xgraph.com/maintainers](https://10xgraph.com/maintainers), and ask questions in [Discussions](https://github.com/10xGraph/10xGraph/discussions). Report security issues privately through the Security tab of the affected repository.

<sub>MIT licensed. Built and run in production by [10xScale](https://10xscale.ai).</sub>
