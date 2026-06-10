# zTOKEN

ERC-20 token representing a proportional share of the vault's NAV. The token price starts at parity and moves with the NAV as the strategies perform. Holders never claim; value is reflected automatically in the token's redemption value.

| Function                    | Access           | Description                                                                                       |
| --------------------------- | ---------------- | ------------------------------------------------------------------------------------------------- |
| `initialize(ac, sanctions)` | Once (deploy)    | Links the token to `ZothAccessControl` and the sanctions oracle.                                  |
| `mint(to, amount)`          | `MINT_OPERATOR`  | Create new tokens. Called exclusively by `DepositVault` after a valid deposit.                    |
| `burn(from, amount)`        | `BURN_OPERATOR`  | Destroy tokens. Called exclusively by `RedemptionVault` after a valid redemption.                 |
| `pause()`                   | `PAUSE_OPERATOR` | Halt all transfers globally. Emergency use only.                                                  |
| `unpause()`                 | `PAUSE_OPERATOR` | Resume transfers after a pause.                                                                   |
| `transfer(to, amount)`      | Token holder     | Standard ERC-20 transfer. Checks sender and `recipient` against the blacklist and sanctions list. |
| `setMetadata(key, data)`    | `DEFAULT_ADMIN`  | Store arbitrary bytes32 key to bytes metadata on-chain.                                           |

#### Transfer Restrictions

Every transfer, including mint and burn, must pass all five conditions at once:

* Sender is not blacklisted.
* Sender is not sanctioned.
* Recipient is not blacklisted.
* Recipient is not sanctioned.
* The contract is not paused.
