# Architecture of zVaults

A zVault is a layered smart-contract system, not a single contract. Responsibilities are split across distinct contracts so that each does one job and the boundaries between them are auditable. The architecture is deployment-agnostic: every vault launched on the protocol reuses the same contract set, regardless of its underlying strategy. The design separates what must stay open and transparent (the token, the price feed) from what must stay tightly controlled (role administration, upgrades, custody authority).

{% content-ref url="contracts.md" %}
[contracts.md](contracts.md)
{% endcontent-ref %}

{% content-ref url="access-control.md" %}
[access-control.md](access-control.md)
{% endcontent-ref %}

### Token, Mint, and Burn

The `zTOKEN` is an ERC-20 representing a proportional share of the vault's NAV, the interest-bearing claim described earlier. New tokens can be created only by the `DepositVault` and destroyed only by the `RedemptionVault`, each through a dedicated minter / burner role assigned to that contract alone. No other address can mint or burn. Compliance is enforced on the token itself: every transfer, including mint and burn, is screened against the greenlist, blacklist and sanctions list before it executes.

### Price Oracle and Safety Bounds

NAV is published to the non-upgradeable `PriceOracle` by a dedicated multisig in a 3-of-5 MPC configuration. The oracle is deliberately immutable to maximize trust in the price feed. It enforces two guards; a tolerance check rejects any submitted price that deviates from the current price by more than a configured bound, blocking sudden manipulation. On read, a staleness check reverts if the price has not been refreshed within a configured window, halting all vault activity rather than letting deposits and redemptions execute against an outdated NAV.

### Compliance Built Into the Contracts

Compliance is not a separate service bolted on; it is inherited into the vault and token contracts, so the compliance sequence runs inside the same transaction as the operation it guards and a failure reverts the whole transaction. This places the compliance perimeter at the contract level, where it cannot be bypassed by interacting with the contracts directly. The gates themselves (greenlist, blacklist, and sanctions) are detailed under Access Control.

### Upgradeability

Four of the seven contracts are upgradeable behind proxies; the price path (`PriceOracle` and `FunctionsAccessControl`) is deliberately fixed. Upgrade authority rests solely with `ProxyAdmin`, which is owned by the multisig. The upgrade mechanism and its governance are detailed under Smart Contract Security.

### Key Separation and Deployment Handover

Authority over a live vault is distributed across separate keys by design, never merged, so no single role concentrates control and no single compromise is protocol-wide. The contracts are deployed by a temporary key that is decommissioned at handover, after which no standing single-key authority over a live vault exists. The custody and signing mechanics that enforce this are detailed under Operational Security.
