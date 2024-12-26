---
cover: ../../.gitbook/assets/Banner 10.png
coverY: 0
---

# Minting Reward and Withdrawal Fees

When minting rewards and withdrawal fees are high:

* Issuers are incentivized to mint ZeUSD
* Issuers are disincentivized to redeem ZeUSD
* This increases the ZeUSD supply
* The increased supply tends to put downward pressure on the ZeUSD price

When withdrawal fees, minting rewards are low:

* Users are incentivized to redeem/withdraw
* Users are disincentivized to mint ZeUSD
* This decreases the ZeUSD supply
* The decreased supply tends to put upward pressure on the ZeUSD price

At the current stage, protocol implements a simplified state machine for both minting rewards and redemption fees, characterized by the following parameters:

**Minting Rewards States:**

1. **Fixed Stability Rate:** A predetermined positive rate offered to incentivize minting
2. **Zero Rate:** No minting incentives provided

**Redemption Fee States:**

1. **Positive Fee:** A non-zero fee applied to redemptions
2. **Zero Fee:** No cost barrier for redemptions
