# Contracts Security

Beyond the access-control and compliance design described earlier, a zVault carries an explicit set of defensive controls: a graduated emergency-response system that can halt activity at the precise scope a situation requires, and a controlled upgrade path that lets the protocol fix issues without disrupting live vaults. Both are governed by the same separated-key model, so no defensive action depends on a single party.

### Emergency Controls

Emergency authority is graduated rather than all-or-nothing. The protocol can intervene at the narrowest scope that addresses a threat, from disabling a single function up to freezing all token movement, which contains incidents without halting more of the system than necessary.

| Control                       | Function                               | Access                   | Effect                                                                                           |
| ----------------------------- | -------------------------------------- | ------------------------ | ------------------------------------------------------------------------------------------------ |
| Pause a single vault function | `vault.pauseFn(selector)`              | Vault admin              | Targeted: disables one operation, for example instant deposits, while the rest of the vault runs |
| Pause an entire vault         | `vault.pause()`                        | Vault admin              | Halts all operations on that vault                                                               |
| Pause token transfers         | `zTOKEN.pause()`                       | Pause operator           | Stops all transfers, mints, and burns of the token globally                                      |
| Blacklist an address          | `grantRole(BLACKLISTED_ROLE, address)` | Blacklist operator       | Blocks a specific address from every operation                                                   |
| Replace the sanctions oracle  | `setSanctionsList(newOracle)`          | Default admin (multisig) | Points the protocol at an updated sanctions screening source                                     |

Each control is gated to a distinct role held in a separate wallet, so triggering an emergency action requires the corresponding authority and no single key can exercise all of them.

### Upgradeability and the Proxy Pattern

Four contracts (`ZothAccessControl`, the `zTOKEN`, `DepositVault`, and `RedemptionVault`) use OpenZeppelin's transparent proxy pattern. `ProxyAdmin`, owned by the multisig, is the sole account that can trigger an upgrade, and it lets the protocol ship security fixes and improvements without migrating user balances or redeploying live vaults. The `PriceOracle` and `FunctionsAccessControl` are deliberately non-upgradeable, fixing the price path in place to maximize trust in the NAV feed.

Upgrades intentionally carry no on-chain time-lock, so the protocol can respond immediately to a critical vulnerability rather than waiting out a delay window while funds are at risk. To keep that capability from becoming an unchecked authority, all non-emergency upgrades follow an internal governance process with team review before execution, and the upgrade key itself is the multisig rather than any single signer.

### Daily On-Chain Configuration Checks

The protocol does not assume its deployed contracts stay configured as intended; it checks. An automated routine reads the on-chain state of every vault contract on a fixed daily schedule (the vaults, the price oracle, the access-control store, and the proxy admin) and compares each critical parameter against its expected, governance-approved value. The parameters under watch include deposit and withdrawal limits, fee settings, the supply cap, pause status across the token and vaults, the oracle's tolerance and staleness bounds, and the configured oracle and sanctions addresses. Any drift between the on-chain configuration and the approved baseline raises an alert for the operations team to investigate, so an unauthorized or accidental parameter change is caught within a day rather than discovered after it has been exploited.

Critical role assignments are part of the watched configuration. Each pass verifies that:

* `DEFAULT_ADMIN_ROLE` is held only by the multisig, never the deployer key.
* `ProxyAdmin` ownership resolves to the multisig address.
* The mint-operator role is held only by the `DepositVault` proxy address.
* The burn-operator role is held only by the `RedemptionVault` proxy address.
* `PRICE_ADMIN` is held only by the dedicated NAV-update MPC wallet.
* `GREENLIST_OPERATOR` is held only by the compliance MPC wallet.
* `CONFIG_ROLE` is held only by the approved ops wallet, since it can change the oracle's tolerance, staleness, and decimals.

### Price Manipulation Protection

The protocol guards the NAV price and execution with on-chain bounds, each set per vault. The tolerance and staleness checks both treat a value of zero as disabled, so the daily configuration check verifies that neither has drifted to zero or away from its approved value.

| Protection          | Mechanism                                                                                                                      | Configuration                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| Tolerance check     | A newly submitted price must fall within the tolerance bound of the current price, or the submission reverts                   | Configurable by the fund manager |
| Staleness check     | Price reads revert if the last update is older than the staleness window, halting vault activity until a fresh price is posted | Configurable by the fund manager |
| Variation tolerance | When an admin approves a redemption request, the supplied rate must fall within the variation tolerance of the oracle price    | Configurable by the fund manager |
| Min receive         | The user sets the minimum acceptable output on a deposit or redemption; the transaction reverts if the result falls below it   | Set by the user per transaction  |

Alongside the bounds themselves, the daily check confirms the supporting oracle state has not drifted:

| Check                  | Verify                                                     | Risk if it drifts                                                                                                    |
| ---------------------- | ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `priceDecimals`        | Matches the decimals the fund administrator reports NAV in | A mismatch silently mis-scales every price, producing a NAV wrong by orders of magnitude with no revert              |
| Price freshness        | Current price age sits well below the staleness window     | Near the window the next read reverts and halts all vault activity; catching it early avoids an outage               |
| Current price          | Price is set and sits within an expected band              | An unset price reverts all reads; a price far outside band signals a bad feed even when each update passed tolerance |
| Access-control pointer | Resolves to the expected access-control contract           | A wrong pointer changes who can post prices and change the bounds above                                              |
