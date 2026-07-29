---
name: Read a wallet's Kamino portfolio
description: Fetch a Solana wallet's Kamino positions, loans, vault positions and
  rewards from the read-only Public API.
api: openapi/kamino-public-openapi-original.json
operations:
- GET /portfolio/{pubkey}
- GET /portfolio/{pubkey}/rewards
- GET /klend/loans/{pubkey}
- GET /kvaults/users/{pubkey}/positions
---

# Read a wallet's Kamino portfolio

All endpoints are on `https://api.kamino.finance` and are **read-only and unauthenticated** (rate-limited; request an API key for higher limits). Addresses are Solana base58 pubkeys. Select the cluster with `?env=mainnet-beta|devnet|localnet` (default `mainnet-beta`).

## Steps
1. `GET /portfolio/{pubkey}` — full cross-product portfolio for the wallet.
2. `GET /portfolio/{pubkey}/rewards` — claimable/earned rewards.
3. `GET /klend/loans/{pubkey}` — the wallet's Kamino Lend loans (obligations).
4. `GET /kvaults/users/{pubkey}/positions` — Kamino Earn (kvault) positions.

## Rules
- Errors return a flat `{ "error": "<message>" }` envelope (not RFC 9457) — see `errors/kamino-problem-types.yml`. On `500`, retry with backoff; a `404` means the wallet/market was not found on the selected `env`.
- These are pure reads: safe to call repeatedly (naturally idempotent). See `conventions/kamino-conventions.yml`.

