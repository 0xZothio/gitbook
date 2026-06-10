# DepositVault

Accepts USDC/USDT deposits and mints `zTOKEN`. Supports two deposit paths: instant (atomic, single transaction) and request-based (admin-approved, for large deposits).

| Function                                              | Access                | Description                                                                                                    |
| ----------------------------------------------------- | --------------------- | -------------------------------------------------------------------------------------------------------------- |
| `depositInstant(token, amount, minReceive, referrer)` | Greenlisted           | Atomic deposit. Stablecoins transferred and `zTOKEN` minted in the same transaction.                           |
| `depositInstant(..., recipient)`                      | Greenlisted           | Mint `zTOKEN` to a different address. Both depositor and `recipient` must be greenlisted.                      |
| `depositRequest(token, amount, referrer)`             | Greenlisted           | Create a pending deposit request. Returns a `requestId`. No tokens minted until an admin approves.             |
| `approveRequest(id, rate)`                            | `DEPOSIT_VAULT_ADMIN` | Approve a pending request at the specified exchange rate. Mints `zTOKEN`.                                      |
| `safeApproveRequest(id, rate)`                        | `DEPOSIT_VAULT_ADMIN` | Same as `approveRequest` but validates the rate is within `variationTolerance` of the oracle price. Preferred. |
| `rejectRequest(id)`                                   | `DEPOSIT_VAULT_ADMIN` | Cancel a pending request. Returns stablecoins to the user. No `zTOKEN` minted.                                 |
| `addPaymentToken(...)`                                | `DEPOSIT_VAULT_ADMIN` | Register a new accepted stablecoin with its `TokenConfig`.                                                     |
| `removePaymentToken(token)`                           | `DEPOSIT_VAULT_ADMIN` | Deregister a payment token.                                                                                    |
| `setMaxSupplyCap(cap)`                                | `DEPOSIT_VAULT_ADMIN` | Update the maximum total `zTOKEN` supply allowed.                                                              |
| `pause()` / `unpause()`                               | `DEPOSIT_VAULT_ADMIN` | Emergency halt and resume of all vault operations.                                                             |
