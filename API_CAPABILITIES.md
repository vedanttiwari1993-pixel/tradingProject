# Broker/API Capability Register

**Policy:** Upstox Sandbox only. This document is a verification checklist, not proof that an endpoint is currently available. Confirm the official documentation and actual Sandbox behavior before implementation.

Official references:
- https://upstox.com/developer/api-documentation/
- https://upstox.com/developer/api-documentation/sandbox/
- https://upstox.com/developer/api-documentation/build-using-sandbox/
- https://upstox.com/developer/api-documentation/authentication/

## Capability status definitions

- **Sandbox supported:** Verified in current official documentation and/or a controlled Sandbox test.
- **Locally simulated:** Implemented locally without broker execution.
- **Not implemented:** Planned but no implementation exists.
- **Not verified:** Must be checked before use.
- **Live only — prohibited:** Production-only capability; do not call in this project phase.

## Initial register

| Capability | Environment | Status | Notes |
|---|---|---|---|
| Sandbox authentication/token | Upstox Sandbox | Not verified | Re-check token generation, expiry and scopes |
| Instrument master | Market data | Not verified | Confirm supported instrument source and identifiers |
| Historical candles | Market data | Not verified | Confirm history coverage and rate limits |
| Quotes / market feed | Market data | Not verified | Confirm Sandbox vs market-data host behavior |
| Place order | Upstox Sandbox | Not verified | Verify supported order API version and required fields |
| Modify order | Upstox Sandbox | Not verified | Verify Sandbox support |
| Cancel order | Upstox Sandbox | Not verified | Verify Sandbox support |
| Order status / trades | Upstox Sandbox | Not verified | Verify response and lifecycle semantics |
| Paper order placement | Local | Locally simulated | Must never call broker |
| Historical backtest | Local | Locally simulated | State fees, slippage and fill assumptions |

## Verification record

No API capability is considered verified solely because it appears in an older note or a sample. Record the date, documentation URL, endpoint, environment, auth scopes, request/response observations and limitations when verifying.
