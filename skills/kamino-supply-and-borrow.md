---
name: Supply collateral and borrow on Kamino Lend
description: Build UNSIGNED Solana transactions to deposit collateral, borrow, repay
  and withdraw on Kamino Lend; sign client-side.
api: openapi/kamino-transactions-openapi-original.json
operations:
- POST /ktx/klend/deposit
- POST /ktx/klend/borrow
- POST /ktx/klend/repay
- POST /ktx/klend/withdraw
---

# Supply collateral and borrow on Kamino Lend

The Transactions API (`/ktx/...` on `https://api.kamino.finance`) returns **unsigned** Solana transactions. Kamino never holds keys — you sign and submit with the user's wallet.

## Steps
1. `POST /ktx/klend/deposit` — build a tx to supply collateral to a klend reserve.
2. Sign and submit the returned transaction with the user's wallet.
3. `POST /ktx/klend/borrow` — build a tx to borrow liquidity against that collateral.
4. Repay with `POST /ktx/klend/repay`; withdraw collateral with `POST /ktx/klend/withdraw`.

If you need raw instructions to compose into a larger tx, use the `*-instructions` variants (`/ktx/klend/deposit-instructions`, `-borrow-instructions`, etc.).

## Rules
- Verify the built transaction before signing; the API only constructs it.
- Health/obligation state should be read first via `GET /klend/loans/{pubkey}` (see the portfolio skill) to avoid over-borrowing.
- Idempotency is enforced on-chain at signing/submission, not by the API — see `conventions/kamino-conventions.yml`.

