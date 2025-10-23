---
hidden: true
---

# ZeUSD Debt Position (ZeDP)

The ZeUSD Debt Position (ZeDP) is an ERC 721 token implementation that represents Collateralized Debt Positions (CDPs) as transferable NFTs. It adds transferability and composability for on-chain CDPs issued on Zoth.

**Minting ZeDP**

Minting ZeDP when a CDP is created to issue ZeUSD, a ZeDP token is minted and transferred to the issuer's wallet.

**Redeeming ZeDP**

The ZeDP token grants its holder the right to claim the underlying collateral. During redemption, the associated ZeUSD is burned, and the collateral is released to the token holder.

Each ZeDP token maintains a link to the original asset used to create its CDP, ensuring redemption returns the same type of asset initially deposited. For example:

* Users who deposited USDC can redeem their ZeDP for USDC
* Users who deposited RWA collateral can redeem their ZeDP for the underlying RWA

**Yield Distribution**

ZeDP holders can claim both RWA asset yield and $ZOTH rewards, subject to the following condition:

`The total ZeUSD value across the issuer's wallet and ZeUSD positions on various platforms must equal: Collateral Value × LTV`

When this condition is met, ZeDP holders can claim their yield and rewards on a daily basis.
