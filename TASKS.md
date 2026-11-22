# Engineering Backlog

Work top-to-bottom unless a dependency or verified blocker requires reprioritization. Keep each implementation task small enough to review and test.

## M0 — Repository and engineering baseline

- [x] Create repository documentation and persistent Codex instructions.
- [x] Define trading-environment isolation and safety constraints.
- [ ] Add backend FastAPI skeleton with typed settings and health endpoint.
- [ ] Add frontend Next.js/TypeScript skeleton.
- [ ] Add Docker Compose for local frontend, backend and PostgreSQL.
- [ ] Add safe `.env.example`, ignore rules and startup validation.
- [ ] Add linting, formatting and initial test setup.
- [ ] Document local setup and verify a clean startup.

## M1 — Instrument and market-data foundation

- [ ] Define instrument identity and normalized quote/candle schemas.
- [ ] Implement instrument master import and validation.
- [ ] Add provider abstraction and historical candle retrieval.
- [ ] Add market-data freshness, source and timestamp metadata.
- [ ] Add bounded caching and request de-duplication.
- [ ] Add websocket lifecycle/reconnect handling where supported.
- [ ] Test duplicates, stale data, missing candles and rate-limit behavior.

## M2 — Trading terminal

- [ ] Market overview and market-session status.
- [ ] Watchlists and instrument search.
- [ ] Candlestick chart and selectable intervals.
- [ ] Technical indicator library and chart overlays.
- [ ] Scanner UI and filter API.

## M3 — Upstox Sandbox adapter

- [ ] Verify Sandbox OAuth/token flow and current supported endpoints from official docs.
- [ ] Record verified capabilities and date in `API_CAPABILITIES.md`.
- [ ] Implement server-side Sandbox client and explicit Sandbox base URL.
- [ ] Implement supported Sandbox order lifecycle operations behind the adapter.
- [ ] Add environment isolation and tests proving no production host can be selected.
- [ ] Add order audit trail and uncertain-outcome reconciliation.

## M4 — Risk and simulated trading

- [ ] Central deterministic risk engine and configurable limits.
- [ ] Backend kill switch and fail-closed behavior.
- [ ] Local paper-trading ledger and simulated fills.
- [ ] Portfolio, positions, P&L and trade journal.
- [ ] Risk and order-state edge-case tests.

## M5 — Quant research and options

- [ ] Strategy interface and parameter model.
- [ ] Historical backtesting with fees, slippage and fill assumptions.
- [ ] Avoid look-ahead and survivorship bias; document data limitations.
- [ ] Options chain model, Greeks, IV, OI and PCR.
- [ ] Multi-leg strategy builder and payoff/risk visualizations.

## M6 — AI Market Analyst

- [ ] OpenAI provider abstraction with bounded context, timeout and cost controls.
- [ ] Read-only market context retrieval.
- [ ] Validated structured analysis output with source timestamps.
- [ ] Explicit disclaimers and no execution tool access.

## M7 — Hardening

- [ ] Security, dependency and configuration review.
- [ ] Performance profiling and load tests.
- [ ] Backup, observability and operational runbooks.
- [ ] Readiness review. Live trading remains disabled unless separately authorized.
