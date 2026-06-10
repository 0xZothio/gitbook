# Architecture of zVaults

A zVault is a layered smart-contract system, not a single contract. Responsibilities are split across distinct contracts so that each does one job and the boundaries between them are auditable. The architecture is deployment-agnostic: every vault launched on the protocol reuses the same contract set, regardless of its underlying strategy. The design separates what must stay open and transparent (the token, the price feed) from what must stay tightly controlled (role administration, upgrades, custody authority).

### The Five Layers

The protocol stacks into five horizontal layers, from upgrade control at the top to external integrations at the bottom.

| Layer            | Contracts                                 | Responsibility                                                                                                                 |
| ---------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Proxy            | ProxyAdmin                                | Owns all upgradeable proxies. Multisig-controlled. Enables upgrades without state migration                                    |
| Access control   | ZothAccessControl, FunctionsAccessControl | Single source of truth for roles. ZothAccessControl governs vault and token roles; FunctionsAccessControl governs oracle roles |
| Token and oracle | zTOKEN, PriceOracle                       | The ERC-20 NAV-share token (upgradeable) and the non-upgradeable NAV price feed                                                |
| Vault layer      | DepositVault, RedemptionVault             | DepositVault mints the zTOKEN against deposits; RedemptionVault burns it and returns deposit asset                             |
| External         | Screener                                  | Screens addresses and correctly identifies risks before authorizing transactions                                               |

### The Seven Contracts

| Contract               | Type   | Upgradeable | Purpose                                                |
| ---------------------- | ------ | ----------- | ------------------------------------------------------ |
| ZothAccessControl      | Access | Yes (proxy) | Central role management for all contracts              |
| zTOKEN                 | Token  | Yes (proxy) | ERC-20 interest-bearing token with compliance controls |
| DepositVault           | Vault  | Yes (proxy) | Accepts deposits, mints the zTOKEN                     |
| RedemptionVault        | Vault  | Yes (proxy) | Burns the zTOKEN, returns deposit assets               |
| PriceOracle            | Oracle | No          | NAV price feed with tolerance and staleness checks     |
| FunctionsAccessControl | Access | No          | Role management scoped to the oracle                   |
| ProxyAdmin             | Admin  | No          | Controls all proxy upgrades                            |

### Centralized Access Control

Every guarded action in the protocol checks a role against a single contract, ZothAccessControl. This concentrates risk by design: compromise of ZothAccessControl is compromise of the entire protocol, which is why the roles it administers are held by separate keys rather than any single one. The custody and signing model that enforces that separation is set out under Operational Security. Additionally oracle roles live in a separate access-control contract, FunctionsAccessControl, so the price feed's authority does not share a control surface with the vaults.

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

### Token, Mint, and Burn

The zTOKEN is an ERC-20 representing a proportional share of the vault's NAV, the interest-bearing claim described earlier. New tokens can be created only by the DepositVault and destroyed only by the RedemptionVault, each through a dedicated minter / burner role assigned to that contract alone. No other address can mint or burn. Compliance is enforced on the token itself: every transfer, including mint and burn, is screened against the greenlist, blacklist and sanctions list before it executes.

### Price Oracle and Safety Bounds

NAV is published to the non-upgradeable PriceOracle by a dedicated multisig in a 3-of-5 MPC configuration. The oracle is deliberately immutable to maximize trust in the price feed. It enforces two guards; a tolerance check rejects any submitted price that deviates from the current price by more than a configured bound, blocking sudden manipulation. On read, a staleness check reverts if the price has not been refreshed within a configured window, halting all vault activity rather than letting deposits and redemptions execute against an outdated NAV.

### Compliance Built Into the Contracts

Compliance is not a separate service bolted on; it is inherited into the vault and token contracts, so the compliance sequence runs inside the same transaction as the operation it guards and a failure reverts the whole transaction. This places the compliance perimeter at the contract level, where it cannot be bypassed by interacting with the contracts directly. The gates themselves (greenlist, blacklist, and sanctions) are detailed under Access Control.

### Upgradeability

Four of the seven contracts are upgradeable behind proxies; the price path (PriceOracle and FunctionsAccessControl) is deliberately fixed. Upgrade authority rests solely with ProxyAdmin, which is owned by the multisig. The upgrade mechanism and its governance are detailed under Smart Contract Security.

### Key Separation and Deployment Handover

Authority over a live vault is distributed across separate keys by design, never merged, so no single role concentrates control and no single compromise is protocol-wide. The contracts are deployed by a temporary key that is decommissioned at handover, after which no standing single-key authority over a live vault exists. The custody and signing mechanics that enforce this are detailed under Operational Security.
