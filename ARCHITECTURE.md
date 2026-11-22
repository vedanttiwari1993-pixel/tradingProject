# Architecture

## Approach

Use a modular monolith with clear domain boundaries. Deploy frontend and backend as separate processes/containers, but keep backend domains in one codebase until scale or team boundaries justify extraction.

## High-level shape

```text
Next.js UI
   |
   | HTTPS / WebSocket
   v
FastAPI application
   |-- Identity and configuration
   |-- Instruments and market data
   |-- Analytics and scanners
   |-- Options analytics and strategies
   |-- Backtesting and paper trading
   |-- Portfolio and risk
   |-- Execution orchestration
   |-- Broker adapters (Upstox Sandbox only)
   |-- AI analyst (advisory only)
   |-- Audit
   |
   +-- PostgreSQL
   +-- Redis (only if justified)
   +-- External market/broker APIs
```

## Module boundaries

- **Market data:** Provider ingestion, normalization, freshness and instrument mapping. Consumers must not each create their own upstream feed.
- **Analytics:** Indicators and scanners, deterministic and independent of UI.
- **Options:** Chain normalization, Greeks/IV and payoff calculations with explicit assumptions.
- **Research:** Strategy definitions, historical data access and backtest engine.
- **Paper trading:** Local simulation; never submits broker orders.
- **Risk:** Deterministic validation, exposure limits and kill switch.
- **Execution:** Order intent/state orchestration. Initially restricted to Upstox Sandbox and must call the risk layer first.
- **Broker adapter:** Provider-specific API and authentication details behind interfaces.
- **AI analyst:** Read-only curated context and structured advisory output; no execution permissions.
- **Audit:** Append-only records for security-sensitive and trading lifecycle events.

## Environment isolation

Use a closed enum/configuration for `BACKTEST`, `PAPER` and `UPSTOX_SANDBOX`. Reject any unknown or unsupported value at startup. Production/live mode is not an available runtime mode in this phase.

Do not share credentials, clients or base URLs between Sandbox and production. Sandbox configuration must use explicit Sandbox hosts and tokens. A missing Sandbox setting must fail startup, not select a production default.

## Data conventions

- Canonical timestamps stored in UTC; market-session logic uses Asia/Kolkata.
- Explicit exchange, segment, instrument identifier, currency and interval.
- Persist source and received-at timestamps where useful for freshness analysis.
- Distinguish null/missing data from numeric zero.

## Resilience

Bound upstream timeouts, concurrency, retries, queues and caches. Apply backpressure to streams. Handle reconnects and duplicate events. Make order submission retries idempotent where the API supports it; reconcile uncertain order outcomes rather than blindly resubmitting.

## Security

Secrets remain server-side. Validate every external input. Apply centralized authorization and risk checks. Avoid sensitive logs. AI-generated content is untrusted and cannot call execution actions.
