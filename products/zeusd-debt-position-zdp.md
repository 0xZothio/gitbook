# ZeUSD Debt Position (ZDP)

The ZeUSD Debt Position (ZDP) is an ERC 721 token implementation that represents Collateralized Debt Positions (CDPs) as transferable NFTs. It adds transferability and composability for on-chain CDPs issued on Zoth.

**Minting ZDP**

Minting ZDP when a CDP is created to issue ZeUSD, a ZDP token is minted and transferred to the issuer's wallet.

**Redeeming ZDP**

Redeeming ZDP The ZDP token grants its holder the right to claim the underlying collateral. During redemption, the associated ZeUSD is burned, and the collateral is released to the token holder.

Each ZDP token maintains a link to the original asset used to create its CDP, ensuring redemption returns the same type of asset initially deposited. For example:

* Users who deposited USDC can redeem their ZDP for USDC
* Users who deposited RWA collateral can redeem their ZDP for the underlying RWA

**Yield Distribution**

ZDP holders can claim both RWA asset yield and $ZOTH rewards, subject to the following condition:

`The total ZeUSD value across the issuer's wallet and ZeUSD positions on various platforms must equal: Collateral Value × LTV`

When this condition is met, ZDP holders can claim their yield and rewards on a daily basis.
