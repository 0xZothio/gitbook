# What are zVaults?

zVaults are the foundational infrastructure layer of the Zoth protocol: specialized, yield-generating investment vehicles that bring institutional fund management on-chain. Each zTOKEN is an ERC-20 compliant, interest-bearing token whose price appreciates over time to reflect yield accrued from the vault's underlying strategies.

zTOKENs are not stablecoins. Where a stablecoin holds fixed value parity, a zTOKEN behaves as a tokenized fund share: each token is a proportional claim on the vault's net asset value (NAV), and its value moves with the NAV as the strategies perform. This share-based model mirrors conventional mutual fund and hedge fund structures, with blockchain settlement adding transparency, composability, and efficient settlement.

A zVault can run a single strategy or combine several. zOPAL, the first live vault, allocates across two: BlackOpal's LiquidStone II credit strategy and Superstate's market-neutral basis trading. Each vault carries a defined mandate and risk profile, so investors and auditors can assess exposure against clear parameters rather than an open-ended basket.

zVaults draw exposure from across these strategy categories:

| Strategy category          | Exposure                                                                                         |
| -------------------------- | ------------------------------------------------------------------------------------------------ |
| Real-World Asset (RWA)     | Tokenized traditional assets like ETFs, gold etc: commodities, secured lending, equity positions |
| DeFi Strategy              | On-chain yield via liquidity provision, lending, derivatives, and trading                        |
| Private Credit and Lending | Direct credit facilities and structured lending arrangements                                     |
| Geographic-Specific        | Strategies focused on a particular jurisdiction or region                                        |

Fund managers retain full operational control over strategy execution and may deploy capital across any DeFi protocol, network, or asset within their vault's mandate.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
