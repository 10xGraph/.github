# Contributing to 10xGraph

Thank you for your interest in contributing to **10xGraph**! 🚀

10xGraph is an open-source, high-performance state-graph engine designed to run production-grade autonomous AI agents without cloud lock-in or runtime bloat. We welcome contributions from developers, researchers, technical writers, and users of all experience levels.

---

## Code of Conduct

All contributors and participants are expected to adhere to our [Code of Conduct](CODE_OF_CONDUCT.md). Please read it to ensure a respectful and inclusive community.

---

## How You Can Contribute

- 🐛 **Report Bugs**: Submit detailed issues with minimal reproducible state graphs.
- 💡 **Suggest Features**: Propose new graph primitives, checkpointer backends, or provider integrations.
- 📖 **Improve Documentation**: Enhance guides, tutorials, API docs, and architectural diagrams at [docs.10xgraph.com](https://docs.10xgraph.com).
- ⚡ **Submit Code**: Add new capabilities, optimize Redis/Postgres state serialization, or expand test suites.
- 🧪 **Write Tests**: Increase test coverage for edge failure modes, tool replay loops, and SSE streaming.

---

## Repositories Overview

The 10xGraph ecosystem is organized across several key repositories:

| Repository | Focus | Tech Stack |
|---|---|---|
| [**10xGraph/10xgraph**](https://github.com/10xGraph/10xgraph) | Core Python state-graph engine, checkpointers, and production server compiler | Python 3.10+, FastAPI, Pydantic, Redis |
| [**10xGraph/10xgraph-docs**](https://github.com/10xGraph/10xgraph-docs) | Official documentation and marketing landing page | Astro 7, Starlight, Tailwind CSS, Lucide |
| [**10xGraph/10xgraph-cli**](https://github.com/10xGraph/10xgraph-cli) | Developer CLI for scaffolding graphs and testing replay checkpoints | Python / Click |
| [**10xGraph/10xgraph-client**](https://github.com/10xGraph/10xgraph-client) | Web and Node client SDK with SSE streaming hooks | TypeScript, React |
| [**10xGraph/.github**](https://github.com/10xGraph/.github) | Organization profile, community health files, issue & PR templates | Markdown, GitHub Actions |

---

## Local Development Workflow (Python Core)

### 1. Prerequisites

- Python 3.10, 3.11, or 3.12
- [uv](https://docs.astral.sh/uv/) (recommended) or standard `pip` + `venv`
- Docker (optional, for running Redis and Postgres locally during integration tests)

### 2. Fork and Clone

```bash
git clone https://github.com/<your-username>/10xgraph.git
cd 10xgraph
git remote add upstream https://github.com/10xGraph/10xgraph.git
```

### 3. Create a Virtual Environment

```bash
uv venv .venv
# On macOS / Linux:
source .venv/bin/activate
# On Windows (PowerShell):
.venv\Scripts\Activate.ps1
```

### 4. Install Dependencies

```bash
uv pip install -e ".[dev,test]"
```

### 5. Running Tests

```bash
# Run unit tests
pytest tests/unit

# Run full test suite with coverage
pytest --cov=tenxgraph --cov-report=term-missing

# Run Redis checkpoint integration tests (requires Redis on :6379)
pytest tests/integration/test_redis_checkpointer.py
```

### 6. Linting and Formatting

We use [Ruff](https://astral.sh/ruff) for fast linting and formatting, and [MyPy](https://mypy-lang.org/) for static type checking:

```bash
# Format code
ruff format .

# Check lint rules
ruff check .

# Fix auto-fixable lint issues
ruff check --fix .

# Static type check
mypy src/10xgraph
```

---

## Local Development Workflow (Documentation)

To contribute to [docs.10xgraph.com](https://docs.10xgraph.com):

```bash
git clone https://github.com/10xGraph/10xgraph-docs.git
cd 10xgraph-docs
npm install
npm run dev
```

Visit `http://localhost:4321` in your browser. Documentation content is located under `src/content/docs/`.

---

## Pull Request Guidelines

1. **Branch Naming**:
   - `feat/feature-name` (e.g. `feat/postgres-checkpointer`)
   - `fix/bug-description` (e.g. `fix/sse-disconnection-cleanup`)
   - `docs/topic-name` (e.g. `docs/replay-ledger-guide`)
   - `refactor/area-name` (e.g. `refactor/serialization-buffer`)

2. **Commits**:
   - Write clear, concise commit messages using [Conventional Commits](https://www.conventionalcommits.org/):
     - `feat: add support for DynamoDB checkpointer`
     - `fix(ledger): prevent double execution during socket timeout`
     - `docs: update quickstart guide with SSE streaming example`

3. **Checklist Before Submitting**:
   - [ ] All new code includes unit or integration tests.
   - [ ] `pytest` passes with 100% success.
   - [ ] `ruff check .` and `ruff format --check .` report no errors.
   - [ ] Public API functions and classes include clear docstrings and type annotations.
   - [ ] Documentation has been updated if user-facing behavior changed.

4. **Review Process**:
   - Maintainers will review your PR and provide feedback.
   - Once all automated checks pass and an approval is granted, a maintainer will squash and merge your PR.

---

## Reporting Issues

- **Security Concerns**: Please do **not** open public GitHub issues for security vulnerabilities. Instead, refer to our [Security Policy](SECURITY.md).
- **Bug Reports**: Use our [Bug Report Template](https://github.com/10xGraph/.github/issues/new?template=bug_report.yml) and include:
  - Exact Python and OS version
  - Minimal code reproducing the issue
  - Expected vs. actual behavior
  - Full stack trace / logs
- **Feature Requests**: Use our [Feature Request Template](https://github.com/10xGraph/.github/issues/new?template=feature_request.yml) describing the motivation, API design, and trade-offs.

---

## Questions?

- Join our [GitHub Discussions](https://github.com/orgs/10xGraph/discussions).
- Check our documentation at [docs.10xgraph.com](https://docs.10xgraph.com).
- Reach out to maintainers via [hello@10xgraph.com](mailto:hello@10xgraph.com).
