# How USDZe Generates Yield

USDZe generates sustainable yield through a diversified allocation strategy spanning both real-world assets (RWA) and decentralized finance protocols. This dual-approach architecture maximizes risk-adjusted returns while maintaining appropriate diversification across asset classes and yield generation mechanisms.

### Real-World Asset (RWA) Strategy

The RWA component of USDZe's backing encompasses tokenized exposure to traditional financial instruments and commodities. This includes allocations to physical gold, secured credit lines, equity positions, and other institutional-grade assets. These RWA integrations provide stable, predictable yield streams that are uncorrelated with crypto-native volatility, serving as a stabilizing foundation for the protocol's overall yield profile.

### DeFi Allocation Strategy

The DeFi component leverages on-chain protocols to generate additional yield through multiple mechanisms. Strategies include providing liquidity to decentralized exchanges, writing covered options, lending assets through money markets, and capturing funding rates in perpetual futures markets. This DeFi allocation captures opportunities unique to blockchain-based finance while maintaining risk management protocols appropriate to each strategy type.

### Risk-Weighted Optimization via Allocator

Capital deposited into USDZe is managed through a risk-weighted allocator contract that determines the distribution of funds across individual yield-generating vaults. The aggregate net asset value (NAV) of these constituent vaults determines the current value of USDZe. This modular architecture allows the protocol to optimize yield generation while maintaining granular risk management at the vault level.

The risk-weighted allocation parameters are not algorithmically determined but rather established through ZOTH token holder governance. ZOTH holders can propose and vote on allocation changes every two weeks, with proposals requiring approval from at least 10% of the circulating ZOTH supply to take effect. This governance-driven approach ensures that allocation decisions reflect the collective judgment of protocol stakeholders while maintaining sufficient flexibility to adapt to changing market conditions. Notably, the protocol does not impose maximum allocation caps per vault, allowing governance to optimize allocations based on opportunity set and risk assessment.

While the allocator automates fund distribution according to approved parameters, reallocation events require manual intervention to execute governance-approved weight changes, ensuring that significant capital movements are subject to appropriate oversight and review.
