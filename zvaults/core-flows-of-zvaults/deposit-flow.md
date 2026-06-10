# Deposit Flow

The request path is used for large deposits above the daily instant limit, or when admin review is required. The user's stablecoins are held by the vault until the request is resolved. Compliance is checked at request creation; on approval the vault mints at the admin-set rate, validated against the oracle within variation tolerance. The flow has two outcomes, approve and reject.

| Step         | Actor          | Action                                                                                                                                                                      |
| ------------ | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1            | User           | Call `depositRequest(token, amount, referrerId)`. Stablecoins transferred to the vault. `requestId` returned.                                                               |
| 2            | `DepositVault` | Create a pending request object. No tokens minted yet. Emit `DepositRequest` event.                                                                                         |
| 3            | Admin          | Review the request off-chain. Validate source of funds and current NAV.                                                                                                     |
| 4a (approve) | Vault Admin    | Call `safeApproveRequest(requestId, newRate)`. Rate must be within `variationTolerance` of the oracle price. If valid, mint `zTOKEN` to the user and emit `ApproveRequest`. |
| 4b (reject)  | Vault Admin    | Call `rejectRequest(requestId)`. Stablecoins returned to the user. No `zTOKEN` minted. Emit `RejectRequest`.                                                                |
