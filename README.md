# QuantNex

AI-powered quantitative trading, research and analytics platform for Indian markets.

> **Safety status:** Initial development is restricted to Upstox Sandbox, local paper trading and historical backtesting. Live trading is disabled and must not be enabled by configuration fallback or AI output.

## Product scope

- Indian market overview, instruments, indices, watchlists and charts
- Normalized market-data ingestion and technical indicators
- Equity scanners and options-chain analytics (OI, IV, Greeks, PCR)
- Multi-leg options strategy builder and payoff analysis
- Historical backtesting, paper trading, portfolio, risk and trade journal
- Upstox Sandbox integration
- AI market analyst (advisory only)

## Architecture

Start as a modular monolith:

- **Frontend:** Next.js, React, TypeScript, Tailwind CSS
- **Backend:** Python, FastAPI, Pydantic
- **Database:** PostgreSQL
- **Cache/streaming support:** Redis only where justified
- **Infrastructure:** Docker Compose
- **Testing:** Pytest and frontend tests

## Repository layout

```text
frontend/          Web terminal (initial scaffold)
backend/           FastAPI application (initial scaffold)
tests/             Cross-module and integration tests
docs/              Product and engineering documentation
infrastructure/    Local development infrastructure
scripts/           Developer utilities
AGENTS.md          Persistent instructions for Codex
PROJECT_STATUS.md  Current delivery status
TASKS.md           Ordered engineering backlog
ARCHITECTURE.md    Architecture decisions and boundaries
API_CAPABILITIES.md Broker/API capability verification
CHANGELOG.md       Project changes
```

## Getting started

The initial commit establishes project rules and structure. Runtime setup commands will be added with the foundation milestone.

1. Read [AGENTS.md](AGENTS.md) before making changes.
2. Review [PROJECT_STATUS.md](PROJECT_STATUS.md) and [TASKS.md](TASKS.md).
3. Copy `.env.example` to `.env` when the application configuration is implemented. Never commit secrets.

## Development environments

| Environment | Purpose | Execution |
|---|---|---|
| Backtesting | Historical strategy research | Local simulation |
| Paper Trading | Simulated orders using market data | Local simulation |
| Upstox Sandbox | Broker API integration testing | Sandbox endpoints/tokens only |
| Live | Real-money execution | **Disabled; not implemented or authorized** |

## Security

- Never commit API keys, access tokens, passwords, certificates or account data.
- Use Upstox Sandbox credentials only for broker integration in this phase.
- Never call production trading endpoints or silently fall back to production.
- AI outputs are untrusted advisory content and cannot place, modify or cancel orders.
- All order flows must pass deterministic backend validation and risk controls.
