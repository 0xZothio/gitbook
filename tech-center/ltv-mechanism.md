---
hidden: true
cover: ../.gitbook/assets/Banner 14.png
coverY: 0
---

# LTV Mechanism

## Issuance Mechanics of ZeUSD

ZeUSD is created when users deposit eligible RWA as collateral to open a collateralized debt position. Currently accepted collateral includes both on-chain and off-chain assets—specifically, Treasuries and Money Market Funds. These assets are secured either through:

* A multi-signature escrow smart contract for on-chain assets
* A traditional escrow account for off-chain assets

To maintain stability, ZeUSD implements Safe Loan-to-Value (LTV) ratios that create a protective buffer against potential collateral price fluctuations. This system helps preserve ZeUSD's stability even if the underlying collateral value decreases.

**The Safe LTV is determined by this formula:**

```mathml
Safe LTV = 1 - Risk Buffer - (0.3 × MDD + 0.3 × (Daily Volatility × √Liquidation Time) 
+ 0.4 × (Expected Slippage + (1 - Ease of Liquidation)))
```

**Safe LTV -** This is the maximum safe loan-to-value ratio that can be offered for an asset.

**The formula then subtracts a weighted sum of three main risk factors:**&#x20;

a. **Maximum Drawdown (MDD) - weighted at 30%**

* **MDD (Max Drawdown):** Represents the historical risk of asset depreciation.
* Represents the largest peak-to-trough decline in the asset's value
* Helps protect against historical worst-case scenarios

b. **Volatility Impact - weighted at 30%**

* **VA (Volatility Adjustment):** Reflects the current volatility of the asset which is used for collateral.
* Daily Volatility × √Liquidation Time
* Accounts for price fluctuations during the liquidation period
* Square root of time is used because volatility typically scales with the square root of time

c. **Liquidation Risk - weighted at 40%**

* Expected Slippage: Price impact when selling the asset
* (1 - Ease of Liquidation): Difficulty in selling the asset
* Combined to represent total execution risk during liquidation
* **Risk Buffer:** This is a fixed percentage deducted to provide a margin of safety and cushion against unexpected market volatility.
* **LA (Liquidation Adjustment):** This encompasses factors that could impact the process of selling collateral in case of default. Liquidation Adjustment considers the following
  * **Expected Slippage:** The potential price loss when selling the collateral.
  * **Ease of Liquidation:** This is a subjective metric measured depending on the type of collateral.
  * Another factor that also might affect ease of liquidation indirectly is
    * **Liquidation Time:** How quickly the collateral can be sold.

Issuers of ZeUSD earn a **minting reward** along with the incentivizing inflow of on-chain or off-chain RWAs into the issuance engine. As the time of creation of this paper, issuers can issue ZeUSD only on Ethereum. However, Zoth protocol has plans to expand the issuance mechanism to other networks as well. Once issuance is completed, users have a choice of bridging ZeUSD to any preferred chain of choice, as ZeUSD is an omni-chain token.
