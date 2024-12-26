---
cover: ../../.gitbook/assets/Banner 10.png
coverY: 0
---

# Mechanics of ZeUSD

**RWA Collateralization and ZeUSD Minting Process**

ZeUSD is created when users deposit eligible RWA as collateral to open a collateralized debt position. Currently accepted collateral includes both on-chain and off-chain assets—specifically, Treasuries, ETFs, Money Markets Funds, etc. These assets are secured either through:

* Isolated access-controlled escrow smart contract vaults for on-chain assets
* A traditional escrow account or an omnibus account for off-chain assets

To maintain stability, ZeUSD implements Safe Loan-to-Value (LTV) ratios that create a protective buffer against potential collateral price fluctuations. This system helps preserve ZeUSD's stability even if the underlying collateral value decreases.

The Safe LTV is determined here:

{% content-ref url="../../tech-center/ltv-mechanism.md" %}
[ltv-mechanism.md](../../tech-center/ltv-mechanism.md)
{% endcontent-ref %}

ZeUSD issuers receive minting rewards when contributing either on-chain or off-chain Real World Assets (RWAs) to the issuance engine. Currently, ZeUSD issuance is available exclusively on the Ethereum network, with planned expansion to additional blockchain networks. As an omnichain token, ZeUSD can be bridged to any supported network after issuance, providing users with enhanced flexibility.

**Redemption Mechanism**

To retrieve collateral, users must repay their ZeUSD position and incur a nominal withdrawal fee. These fees contribute to protocol revenue, which is subsequently distributed among $ZOTH token stakers.

**Liquidation Mechanism**

**I**n the event that users do not redeem their ZeUSD positions against the underlying RWAs, Zoth initiates a liquidation process. This involves either liquidating the underlying assets or reinvesting them in the same RWA product. The Loan-to-Value (LTV) ratio of the underlying collateral determines the specific liquidation parameters.
