# ZeUSD Risks and Mitigation Strategies

### Risks Involved

1.  **RWA Interest Rate Risk**

    Fluctuations in the price and interest rates of RWA (Real World Asset) collaterals used to issue ZeUSD CDPs can impact the value and stability of the system.
2.  **RWA Counterparty Risk**

    Challenges related to RWA issuers, including issues of incumbency, regulatory uncertainties, or operational inefficiencies, could arise. This risk extends to counterparties such as banks, custodians, and fund managers.
3.  **RWA Asset Quality Risk**

    The risk of collateralizing poor-quality RWAs, leading to unstable or devalued collateral backing ZeUSD CDPs.
4.  **Smart Contract Risk**

    The potential for vulnerabilities in smart contracts to be exploited, such as hacks targeting collateral vaults or other critical components.
5.  **Liquidation Risk**

    Inability to fully or partially liquidate underlying collateral during a liquidation event, or failure to achieve the target liquidation price.

### Mitigation Strategies

1.  **RWA Interest Rate Risk Mitigation**

    Zoth mitigates interest rate risk by exclusively selecting high-quality RWA assets, primarily backed by US Treasuries and Money Market Funds. These assets are sourced from prominent and reputable issuers following thorough due diligence of the underlying assets. Additionally, a strict Loan-to-Value (LTV) ratio is applied to each issuer, determined by rigorous criteria, to ensure minimal risk and price fluctuations in the underlying collateral.
2.  **RWA Counterparty Risk Mitigation**

    Eligible RWA collateral issuers are onboarded after a rigorous due diligence on counterparties, including banks, custodians, and fund managers. Zoth also diversifies exposure across multiple, reliable issuers to minimize risk concentration.
3.  **RWA Asset Quality Risk Mitigation**

    Zoth ensures the onboarding of only high-quality assets, such as US Treasuries and Money Market Funds, which are characterized by their low default risk and minimal susceptibility to unexpected interest rate reductions.
4.  **Smart Contract Risk Mitigation**

    Zoth has engaged reputable security firms to conduct multiple periodic audits and adopt robust security practices to safeguard smart contracts and vaults.
5.  **Liquidation Risk Mitigation**

    Zoth manages liquidation risk by maintaining a diversified portfolio of RWAs, ensuring adequate liquidity to support smooth liquidation processes. The protocol employs robust contingency mechanisms to minimize price slippage during liquidation events. Additionally, Zoth enforces strict LTV ratios to buffer against potential value fluctuations during liquidations.
