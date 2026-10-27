# What is zMAG7

**zMAG7 Documentation**

Zoth Magnificent Seven | Built on Coinbase Tokenized Stocks | Powered by zVaults

**1. Overview**

zMAG7 (Zoth Magnificent Seven) is an equal-weighted basket vault by Zoth that provides onchain exposure to seven leading US-listed technology companies through a single position. Built on Coinbase US Tokenized Stocks on Base, it spans AI, cloud computing, semiconductors, consumer technology, digital advertising, e-commerce, and electric mobility. Eligible users can fund zMAG7 with stablecoins and hold their position in a self-custody wallet, without requiring a traditional brokerage account. zMAG7 does not represent direct ownership of the underlying shares.

Each underlying Coinbase US Tokenized Stock is issued as a B20 token on Base, an extension of the ERC-20 standard designed for real-world assets. Each token is uniquely identified onchain by its contract address rather than its ticker or symbol. At issuance, each token is backed one-to-one by the corresponding underlying share, with its token multiplier subsequently adjusted to reflect applicable corporate actions.

**2. Token Composition**

* **Basket:** 7 Coinbase Tokenized Stocks at approximately 14.3% each.
* **Holdings:** Alphabet (GOOGLc), Amazon (AMZNc), Apple (AAPLc), Meta (METAc), Microsoft (MSFTc), NVIDIA (NVDAc), Tesla (TSLAc).
* **Backing:** Each token represents a beneficial interest in a US-listed share held with a regulated custodian in a segregated, bankruptcy-remote account.

**3. Rebalancing**

* **Frequency:** The basket is rebalanced everyday back to equal weights of approximately 14.3% per holding.
* **Dividends and corporate actions:** Reflected through an onchain multiplier. Dividends are reinvested into additional underlying shares, raising the redeemable value per token without changing the token balance. Stock splits follow the same mechanism.

**4. Smart Contracts**

* **Network:** Base.
* **Token standard:** B20, an extension of ERC-20 purpose-built for real-world assets.
* **Identification:** Each token is identified onchain by its contract address, not its ticker. Always verify the address before interacting.
* **Backing at issuance:** One-for-one with the underlying share; the multiplier adjusts for corporate actions.
* **Pricing:** Chainlink total return data feeds.
* **Structure:** Issuer: Coinbase Onchain SPV Ltd (ADGM, regulated by the FSRA). Custody: Alpaca Securities LLC (SEC-registered broker-dealer, FINRA and SIPC member). Distribution: Zoth zVaults.

**5. Underlying Token Contract Addresses (Base)**

| **Token** | **Role**  | **Contract address (Base)**                |
| --------- | --------- | ------------------------------------------ |
| AAPLc     | Apple     | 0xb200000000000000000000C2e324d24d7eEcd1fb |
| AMZNc     | Amazon    | 0xb200000000000000000000d9192b6B456483C2E8 |
| GOOGLc    | Alphabet  | 0xb2000000000000000000002D0BA3164cc74f58B7 |
| METAc     | Meta      | 0xb2000000000000000000008bC8786B856E61707C |
| MSFTc     | Microsoft | 0xB200000000000000000000Ab99cFa739E253872B |
| NVDAc     | NVIDIA    | 0xb20000000000000000000078ee7ce2fE4908108C |
| TSLAc     | Tesla     | 0xb2000000000000000000001e800a7f5189430cD0 |

**6. zMAG7 Smart Contract Addresses (Base)**

| **Token** | **Role**           | **Contract address (Base)**                |
| --------- | ------------------ | ------------------------------------------ |
| zMAG7     | zMAG7 basket token | 0xCe154D6C180526905C0e26514055Afb99f833fdd |
| zMAG7     | Holdings           | 0x6E7eD82c87576Fc81a7934210D65926C3790fbE2 |
| zMAG7     | Deposit            | 0x3323c503d17aA989DeB4F999c479da0C3C116362 |
| zMAG7     | Withdrawal         | 0x32103982BeBf2DB399A3535E66e95D0C908c97b8 |

**7. Key Product Details**

* **Minting:** Instant. Minimum $1. Fee 0.25%. Funded in stablecoins (USDC).
* **Redemption:** Requested. Settles T+2 from acceptance of the request, paid in stablecoins. Fee 0.1%.
* **Ongoing fees:** Management fee 0.5% per annum. Performance fee 0%. Gas and third-party network fees are excluded.
* **Trading:** Underlying tokens are transferable and priced 24/7/365.
* **Eligibility:** Offered under Regulation S to eligible non-US persons only. Not available in the US or other restricted jurisdictions.
