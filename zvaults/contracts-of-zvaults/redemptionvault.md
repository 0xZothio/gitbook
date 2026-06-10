# RedemptionVault

Burns `zTOKEN` and returns stablecoins. Supports instant redemption (from the liquidity buffer), request-based (admin-approved), and fiat off-ramp paths.

| Function                                   | Access                   | Description                                                                                               |
| ------------------------------------------ | ------------------------ | --------------------------------------------------------------------------------------------------------- |
| `redeemInstant(token, amount, minReceive)` | Greenlisted              | Atomic redemption from the vault's liquidity buffer. Burns `zTOKEN` and returns stablecoins immediately.  |
| `redeemRequest(token, amount)`             | Greenlisted              | Create a pending redemption request. `zTOKEN` locked. Returns a `requestId`.                              |
| `redeemFiatRequest(amount)`                | Always greenlisted       | Create a fiat redemption request. Off-chain settlement. Subject to `fiatAdditionalFee` and `fiatFlatFee`. |
| `approveRequest(id, rate)`                 | `REDEMPTION_VAULT_ADMIN` | Approve a pending request. Burns `zTOKEN` and transfers stablecoins from `requestRedeemer` to the user.   |
| `safeApproveRequest(id, rate)`             | `REDEMPTION_VAULT_ADMIN` | Same, with a tolerance check on the rate. Preferred.                                                      |
| `rejectRequest(id)`                        | `REDEMPTION_VAULT_ADMIN` | Cancel the request. Returns the locked `zTOKEN` to the user.                                              |
| `setRequestRedeemer(addr)`                 | `REDEMPTION_VAULT_ADMIN` | Set the source address for stablecoins used in request approvals.                                         |
| `setFiatAdditionalFee(fee)`                | `REDEMPTION_VAULT_ADMIN` | Update the percentage fee applied to fiat redemptions.                                                    |

