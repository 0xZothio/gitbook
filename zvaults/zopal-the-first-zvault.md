# zOPAL - The first zVault

### Factsheet

&#x20;[https://docsend.com/view/a6vjaruvisqzmxqx](https://docsend.com/view/a6vjaruvisqzmxqx)

### How it works

[https://docsend.com/view/78iy599ksa2twhsm](https://docsend.com/view/78iy599ksa2twhsm)

### zOPAL Contracts

| Contract                 | Address                                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| `ProxyAdmin`             | [0x5A9916C8B89F4Cc97B782d5138Ea54A17EB79b84](https://basescan.org/address/0x5A9916C8B89F4Cc97B782d5138Ea54A17EB79b84) |
| `ZothAccessControl`      | [0x11E5c20a11e8b75BB2Ae6F136DaB1cBB1DA9CBb1](https://basescan.org/address/0x11E5c20a11e8b75BB2Ae6F136DaB1cBB1DA9CBb1) |
| `zOPAL`                  | [0x2E9705d95f1624faB9CAAba775234571BD557f24](https://basescan.org/address/0x2E9705d95f1624faB9CAAba775234571BD557f24) |
| `FunctionsAccessControl` | [0x58722C4F1a8BCa491dCF074AE3C6B519cC859cB7](https://basescan.org/address/0x58722C4F1a8BCa491dCF074AE3C6B519cC859cB7) |
| `PriceOracle`            | [0x2756bF902563B6e767A6E9EC20abFaB3706715Eb](https://basescan.org/address/0x2756bF902563B6e767A6E9EC20abFaB3706715Eb) |
| `zOPALDepositVault`      | [0x6578Fe7a4A8c0B8C34FC8c85A8f99cc16affe850](https://basescan.org/address/0x6578Fe7a4A8c0B8C34FC8c85A8f99cc16affe850) |
| `RedemptionVault`        | [0x87e86d6930f7e922E02cD92821fBaaF9D5e9B403](https://basescan.org/address/0x87e86d6930f7e922E02cD92821fBaaF9D5e9B403) |

### ForDefi MPC

<table><thead><tr><th>Role</th><th width="256.3228759765625">Address</th></tr></thead><tbody><tr><td><code>depositVaultAdmin</code></td><td><a href="https://basescan.org/address/0x57a134a61915163F4b3F69fED708c7a8836AE277">0x57a134a61915163F4b3F69fED708c7a8836AE277</a></td></tr><tr><td><code>redemptionVaultAdmin</code></td><td><a href="https://basescan.org/address/0x17Fb5D88Ec259466b31760d9E2599891ffFD5441">0x17Fb5D88Ec259466b31760d9E2599891ffFD5441</a></td></tr><tr><td><code>zOPALHolding</code></td><td><a href="https://basescan.org/address/0x01481AECcFff338Fcbb16Cb6aB6b9e4BfCa5E5Eb">0x01481AECcFff338Fcbb16Cb6aB6b9e4BfCa5E5Eb</a></td></tr><tr><td><code>pauseOperator</code></td><td><a href="https://basescan.org/address/0xf7dec551FAaA4EC4d7b31087BB58102bBbD379a1">0xf7dec551FAaA4EC4d7b31087BB58102bBbD379a1</a></td></tr><tr><td><code>greenlistOperator</code></td><td><a href="https://basescan.org/address/0xb9dD4396f0f849508E96e656af1a10f83ea314C6">0xb9dD4396f0f849508E96e656af1a10f83ea314C6</a></td></tr><tr><td><code>blacklistOperator</code></td><td><a href="https://basescan.org/address/0xb9dD4396f0f849508E96e656af1a10f83ea314C6">0xb9dD4396f0f849508E96e656af1a10f83ea314C6</a></td></tr><tr><td><code>priceAdmin</code></td><td><a href="https://basescan.org/address/0x15925A7571f5bD7CE67EeeddFAA31136E565683e">0x15925A7571f5bD7CE67EeeddFAA31136E565683e</a></td></tr><tr><td><code>configRole</code></td><td><a href="https://basescan.org/address/0x973Bd2510d866b1F2494c97ca9fd9595037B2F04">0x973Bd2510d866b1F2494c97ca9fd9595037B2F04</a></td></tr></tbody></table>

### Payment Token Configuration

| Token   | Address                                                                                                               | Stable? | Fee   |
| ------- | --------------------------------------------------------------------------------------------------------------------- | ------- | ----- |
| `USDC`  | [0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913](https://basescan.org/address/0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913) | Yes     | 0 bps |
| `USDbC` | [0xd9aAEc86B65D86f6A7B5B1b0c42FFA531710b6CA](https://basescan.org/address/0xd9aAEc86B65D86f6A7B5B1b0c42FFA531710b6CA) | Yes     | 0 bps |

### Chainalysis Sanctions Oracle

| Field                             | Value                                                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Address (Base, Ethereum, Polygon) | [0x40C57923924B5c5c5455c48D93317139ADDaC8fb](https://basescan.org/address/0x40C57923924B5c5c5455c48D93317139ADDaC8fb) |
| Called on                         | Every deposit, redemption, and zOPAL transfer                                                                         |
| Checks                            | Both sender and recipient                                                                                             |
| On sanctioned party               | Transaction reverts immediately                                                                                       |

