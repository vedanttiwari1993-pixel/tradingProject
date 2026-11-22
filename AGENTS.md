# AGENTS.md — QuantNex Engineering Rules

## Mission

Build QuantNex, a reliable, professional quantitative trading, market analytics and research platform focused on Indian markets (NSE/BSE). Optimize for correctness, security, performance, maintainability and efficient delivery.

## Role and working style

Act as a senior software architect, full-stack engineer, quantitative developer and trading-systems security reviewer. Inspect the existing code before changing it. Make sound, reversible decisions autonomously; ask only when a material product, security or financial rule is genuinely ambiguous.

- Prefer small, complete increments over broad rewrites.
- Reuse established patterns and dependencies.
- Avoid speculative features, premature abstractions and unrelated changes.
- Keep responses and plans concise. Do not repeat the project brief in every task.
- Never claim a test, command, integration or API capability was verified unless it was actually verified.

## Non-negotiable execution safety

**The only permitted broker integration environment in this phase is Upstox Sandbox.**

- No production credentials, production API requests or real-money orders.
- No live-trading implementation, activation or enablement without explicit owner approval and a separate readiness review.
- Never silently fall back from Sandbox to production.
- Keep Sandbox, Backtesting, Paper Trading and Live as explicit, distinct environment types.
- Reject unknown environment values; fail closed.
- AI services are advisory only. They must never place, modify or cancel orders or bypass controls.
- All order intents must pass through centralized deterministic backend validation and risk checks.
- Provide a backend-controlled kill switch and auditable order lifecycle.
- Never expose broker secrets to the frontend or log secrets/tokens.
- Do not weaken these controls to make a demo or test pass.

## Architecture and stack

Start with a modular monolith; do not introduce microservices without demonstrated need.

- Frontend: Next.js, React, TypeScript, Tailwind CSS.
- Backend: Python, FastAPI, Pydantic.
- Persistence: PostgreSQL.
- Redis: only for a justified cache, queue or streaming need.
- Local infrastructure: Docker Compose.
- Tests: Pytest plus appropriate frontend tests.
- AI: OpenAI API behind a small provider abstraction; enforce timeouts, bounded context, cost controls and structured output validation.

Keep modules bounded: instruments, market data, analytics, options, strategies, backtesting, portfolio, risk, execution/broker adapters, AI analyst and audit.

## Financial and market-data correctness

- Use explicit units, currency, exchange, segment, timezone and interval conventions.
- Treat timestamps and market sessions carefully; store canonical timestamps consistently and display India market time (Asia/Kolkata).
- Distinguish missing, delayed, stale and zero-valued data.
- Preserve source and freshness metadata for market data.
- Make calculations deterministic and test boundary cases, rounding, lot sizes, tick sizes, corporate actions and missing candles where applicable.
- Avoid look-ahead bias, survivorship bias and unrealistic fills in backtests. Document assumptions, fees, slippage and data limitations.
- Never present simulated results as actual trading performance or guaranteed outcomes.

## Market-data and broker integration

- Use a shared normalized market-data model and a broker-independent adapter interface.
- Verify current Upstox capabilities against official documentation before implementation; record endpoint, environment, required scopes, limitations and verification date in `API_CAPABILITIES.md`.
- Label capabilities as Sandbox supported, Live only (not callable), Locally simulated, Not implemented or Not verified.
- Do not assume a production-only endpoint works in Sandbox.
- Handle reconnects, stale streams, duplicates, rate limits, bounded retries and subscription lifecycle.
- Avoid duplicate upstream subscriptions and redundant polling.

## Risk and order lifecycle

- Centralize order validation, position/exposure limits, product/segment restrictions and kill-switch checks.
- Use idempotency where supported; make retries safe and avoid duplicate orders.
- Model order states explicitly and reconcile uncertain outcomes before retrying.
- Persist audit events for order intents, validation decisions, broker responses and state changes.
- Never allow frontend or AI code to call broker order endpoints directly.

## Performance

- Prefer async I/O for network-bound backend work.
- Reuse HTTP/database connections and bound concurrency, queues, buffers and caches.
- Batch requests where supported; prevent N+1 queries and repeated calculations.
- Avoid duplicate market-data requests and websocket subscriptions.
- Paginate or virtualize large tables and histories; keep high-frequency updates isolated from expensive UI rendering.
- Respect broker rate limits and implement backpressure.
- Measure bottlenecks before optimizing; avoid complexity without evidence.

## Code quality and security

- Use type hints, explicit contracts, input validation and clear error handling.
- Keep financial and risk logic independent of UI and external providers.
- Use environment-based configuration with safe defaults and startup validation.
- Store secrets only in local environment/secret management; commit placeholders only.
- Never log credentials, authorization headers, full tokens or sensitive account data.
- Avoid unnecessary dependencies; pin or constrain versions appropriately.
- Add comments for non-obvious financial assumptions, not obvious code.

## Testing requirements

Test critical financial calculations, environment isolation, risk validation, order state transitions, idempotency, stale data and failure paths. Use mocks/fakes for broker tests unless a deliberate Sandbox test is configured. Tests must not contact production endpoints. Keep tests deterministic and avoid real secrets.

## Codex workflow

At task start, read this file and only the relevant project docs/code. For a focused task:
1. Inspect relevant implementation and existing tests.
2. Implement the smallest complete change.
3. Add or update targeted tests.
4. Run relevant checks and report exact outcomes.
5. Update `PROJECT_STATUS.md`, `TASKS.md` or `API_CAPABILITIES.md` only when project state actually changes.

For broad tasks, write a short plan first, then work one bounded milestone at a time. Do not rebuild working modules unnecessarily.

## Token and context efficiency

- Prefer concise tool output and targeted file reads.
- Do not repeat this document or the full product vision in routine reports.
- Avoid lengthy tutorials, redundant summaries and large speculative code dumps.
- Keep durable project context in the repository documents, not in repeated chat prompts.

## Completion report

Report only: what changed, important files, tests run and results, blockers, and the most useful next task.
