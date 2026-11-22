# Project Status

**Overall status:** Repository initialized; application foundation not yet implemented.  
**Current phase:** Milestone 0 — project setup and architecture baseline.  
**Broker environment:** Upstox Sandbox only.  
**Live execution:** Disabled / out of scope.

## Completed

- [x] GitHub repository created and connected for Codex workflow.
- [x] Initial project scope and safety boundaries documented.
- [x] Modular-monolith architecture and build sequence recorded.
- [x] Initial directory structure established.

## In progress

- [ ] Foundation: backend/frontend skeleton, configuration, health checks, database and local Docker setup.

## Decisions

- Build a modular monolith first.
- Keep Backtesting, Paper Trading and Upstox Sandbox explicitly isolated.
- Do not implement or enable live trading.
- AI analyst is advisory only and cannot execute trades.

## Next action

Implement the foundation milestone described in `TASKS.md`. Before writing application code, inspect the repository and keep dependencies and scaffolding minimal.
