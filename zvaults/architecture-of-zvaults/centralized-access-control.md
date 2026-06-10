# Centralized Access Control

Every guarded action in the protocol checks a role against a single contract, `ZothAccessControl`. This concentrates risk by design: compromise of `ZothAccessControl` is compromise of the entire protocol, which is why the roles it administers are held by separate keys rather than any single one. The custody and signing model that enforces that separation is set out under Operational Security. Additionally oracle roles live in a separate access-control contract, FunctionsAccessControl, so the price feed's authority does not share a control surface with the vaults.

#### ZothAccessControl Roles

| Role                            | Assigned to              | Capabilities                                                                                                                |
| ------------------------------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| DEFAULT\_ADMIN\_ROLE (0x00...0) | Protocol multisig        | Grant and revoke all roles. Update sanctions oracle. Emergency override. Transfer ProxyAdmin.                               |
| DEPOSIT\_VAULT\_ADMIN\_ROLE     | Ops wallet (MPC)         | Approve and reject deposit requests. Configure fees, limits, supply cap. Add and remove payment tokens. Pause DepositVault. |
| REDEMPTION\_VAULT\_ADMIN\_ROLE  | Ops wallet (MPC)         | Approve and reject redemption requests. Configure redemption fees. Set requestRedeemer address. Pause RedemptionVault.      |
| GREENLIST\_OPERATOR\_ROLE       | Compliance wallet (MPC)  | Grant or revoke GREENLISTED\_ROLE for individual addresses.                                                                 |
| BLACKLIST\_OPERATOR\_ROLE       | Compliance wallet (MPC)  | Grant or revoke BLACKLISTED\_ROLE for individual addresses.                                                                 |
| GREENLISTED\_ROLE               | Greenlisted user wallet  | Required to call depositInstant, depositRequest, redeemInstant, redeemRequest. Fiat redemptions always require this role.   |
| BLACKLISTED\_ROLE               | Blocked wallet           | Prevents deposits, redemptions, and zTOKEN transfers, both send and receive.                                                |
| MINT\_OPERATOR\_ROLE            | DepositVault contract    | Can call [zTOKEN.mint](http://ztoken.mint)(). Assigned automatically to DepositVault at deployment.                         |
| BURN\_OPERATOR\_ROLE            | RedemptionVault contract | Can call zTOKEN.burn(). Assigned automatically to RedemptionVault at deployment.                                            |
| PAUSE\_OPERATOR\_ROLE           | Ops wallet (MPC)         | Can call zTOKEN.pause() and unpause() to halt all token transfers.                                                          |

#### FunctionsAccessControl Roles (Oracle)

| Role                 | Assigned to             | Capabilities                                                                               |
| -------------------- | ----------------------- | ------------------------------------------------------------------------------------------ |
| DEFAULT\_ADMIN\_ROLE | Protocol multisig       | Manage PRICE\_ADMIN and CONFIG roles within FunctionsAccessControl.                        |
| PRICE\_ADMIN\_ROLE   | NAV update wallet (MPC) | Call setPrice() on PriceOracle. Must be a dedicated MPC wallet separate from vault admins. |
| CONFIG\_ROLE         | Ops wallet (MPC)        | Modify oracle parameters: tolerancePercent, priceDecimals, maxStaleness.                   |
