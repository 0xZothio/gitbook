# Redemption Flow

`zTOKEN` redemption is built around the security considerations that arise across the technical and operational flows of a real-world-backed vault. Because capital is deployed off-chain into managed strategies, the current model handles redemption as a request rather than an unconditional on-chain swap, which keeps it aligned with how the underlying assets actually settle and removes the attack surface of assuming instant liquidity against off-chain positions. The contracts also support instant and fiat variants, available per vault.

| Path               | Status             | How it settles                                                                                                                                                                                       |
| ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Request redemption | Current model      | The `zTOKEN` is locked and a request is created; the fund manager settles from the strategy and returns stablecoins once positions clear, processed FIFO with no per-user limit                      |
| Instant redemption | Currently disabled | Where the vault's buffer allows, the user redeems directly from the stablecoin buffer in one transaction; carries a higher fee than a request, reflecting the liquidity cost of immediate settlement |
| Fiat redemption    | Currently disabled | A request variant that settles off-chain to fiat rather than returning stablecoins on-chain, subject to its own fee                                                                                  |

Whether a vault offers request redemption, instant redemption, fiat redemption, or any combination is entirely the fund manager's choice, set against the liquidity profile of the strategy: a vault holding a deep buffer can offer instant redemption, while a vault in less liquid positions operates on requests with a defined settlement window. The same contracts accommodate either, so redemption behavior tracks the strategy rather than being fixed by the protocol.

The redemption value of a `zTOKEN` is set by the oracle-reported vault NAV, so users receive fair value reflecting the vault's current positions. Yield is already compounded into that value through NAV appreciation, as described under What are zVaults.

#### Instant Redemption

On the instant path a user redeems directly from the vault's liquidity buffer in a single transaction: the user approves the vault to spend the `zTOKEN`, calls `redeemInstant`, and receives stablecoins net of fee once the compliance and limit checks pass. The full sequence is shown below.

| Step | Actor             | Action                                                                                                                    |
| ---- | ----------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 1    | User              | Call `approve(redemptionVault, zTOKENAmount)` on the `zTOKEN` contract.                                                   |
| 2    | User              | Call `redeemInstant(USDC, zTOKENAmount, minReceiveAmount)` on `RedemptionVault`.                                          |
| 3    | `RedemptionVault` | Validation: greenlist, blacklist, and sanctions checks. Amount is at least `minAmount`. Daily instant limit not exceeded. |
| 4    | `zTOKEN`          | `burn(user, zTOKENAmount - fee)`. Tokens destroyed.                                                                       |
| 5    | `zTOKEN`          | `transferFrom(user, feeReceiver, fee)`. Redemption fee deducted.                                                          |
| 6    | USDC              | `transfer(user, usdcAmount)`. Stablecoins sent from the vault buffer to the user.                                         |
| 7    | `RedemptionVault` | Emit `RedeemInstant` event. Transaction complete.                                                                         |

The redemption fee is deducted from the `zTOKEN` input before burning. USDC output equals the net `zTOKEN` (after fee) multiplied by the current oracle NAV. The instant redemption fee can be greater than or equal to the standard request redemption fee.

#### Request Redemption

The request path handles redemptions that settle from the vault's strategy rather than the instant buffer. The user approves the vault on the `zTOKEN` and calls `redeemRequest`; the vault escrows the net `zTOKEN` and takes the fee at request creation, then an admin approves or rejects. The flow has two outcomes.

| Step         | Actor             | Action                                                                                                                                                                                                                                                 |
| ------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1            | User              | Call `approve(redemptionVault, amountZTokenIn)` on the `zTOKEN` contract.                                                                                                                                                                              |
| 2            | User              | Call `redeemRequest(tokenOut, amountZTokenIn)` on `RedemptionVault`. Passes greenlist, blacklist, sanctions, and pause checks.                                                                                                                         |
| 3            | `RedemptionVault` | Validate amount is at least the minimum and compute fee. Pull the net `zTOKEN` into escrow and send the fee in `zTOKEN` to `feeReceiver`. Snapshot the NAV rate, store a pending request, emit `RedeemRequest`, and return a `requestId`. No burn yet. |
| 4a (approve) | Vault Admin       | Call `safeApproveRequest(requestId, newZTokenRate)`. Rate must be within `variationTolerance` of the request-time snapshot. Burn the escrowed `zTOKEN`, pay stablecoins from `requestRedeemer` at the approved rate, and emit `ApproveRequest`.        |
| 4b (reject)  | Vault Admin       | Call `rejectRequest(requestId)`. Set status to Canceled and emit `RejectRequest`. The `zTOKEN` refund is handled off-chain; there is no automatic on-chain return.                                                                                     |
