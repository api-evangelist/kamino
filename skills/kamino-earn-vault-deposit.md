---
name: Deposit into a Kamino Earn vault
description: Discover Kamino Earn (kvault) vaults and build UNSIGNED deposit/withdraw
  transactions.
api: openapi/kamino-transactions-openapi-original.json
operations:
- GET /kvaults/vaults
- POST /ktx/kvault/deposit
- POST /ktx/kvault/withdraw
- GET /kvaults/users/{pubkey}/positions
---

# Deposit into a Kamino Earn vault

## Steps
1. `GET /kvaults/vaults` (Public API) — list available Kamino Earn vaults and pick a `vaultPubkey`.
2. `POST /ktx/kvault/deposit` (Transactions API) — build an unsigned deposit tx for that vault.
3. Sign and submit with the user's wallet.
4. Track the resulting position with `GET /kvaults/users/{pubkey}/positions`; withdraw with `POST /ktx/kvault/withdraw`.

## Rules
- Deposit/withdraw return unsigned transactions — sign client-side.
- Select `env` to target devnet for testing (see `sandbox/kamino-sandbox.yml`).
- Handle the `{ "error": ... }` envelope and retry `500`s with backoff.

