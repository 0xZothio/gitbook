# Tokenomics

For information purposes only. Not an offer to sell or a solicitation to buy any token or security. See Risk Factors and Legal Disclaimer.

**Executive Summary**

Zoth token is the value-capture instrument of the Zoth stack. Protocol revenue across zPayments, zVaults, Zocta Card, and zAI funds a quarterly open-market buyback of Zoth token. The full amount repurchased is distributed to staked holders. Token demand tracks that revenue: as protocol volume grows, the buyback grows with it.

Supply is capped at the 1,000,000,000 Zoth token minted at genesis. The protocol issues no tokens beyond that mint and burns none.

Holders stake Zoth token to mint sZOTH, a transferable token that represents a share of the Zoth token held in the staking contract. sZOTH carries every hold-to-access benefit, appreciates as buyback Zoth token enters the contract, and measures voting power in governance.

**Token Overview**

Zoth token is an ERC-20 token on Ethereum. Total supply is fixed at 1,000,000,000 tokens, minted once at genesis. Staking Zoth token mints sZOTH, a transferable token that represents a share of the Zoth token held in the staking contract. The amount minted depends on the contract's current Zoth token balance, so each sZOTH tracks a share of a growing pool. Buyback Zoth token flows into the contract, raising the Zoth token that backs each sZOTH over time. sZOTH balance sets the Zoth Club membership tier and measures voting power. The fixed-supply policy is stated in full under Supply Policy.

**Distribution and Vesting**

From supply and allocation to vesting and unlocks, get a clear view of how Zoth token is distributed and released over time.&#x20;

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

**Token Utility Across the Stack**

Staked Zoth token sets the economics at every layer of the Zoth stack. Benefits accrue to sZOTH, the staked receipt token.

| **Layer**      | **What sZOTH unlocks**                                                                                                                                                                                                                         |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **zVaults**    | <p>•  Priority allocation when new vault strategies open.</p><p>•  Asset managers stake 250,000 to 1,000,000 Zoth token to list a tokenized fund.</p><p>•  Listing is backed by a slashable sZOTH bond, routed to stakers on a breach.</p>     |
| **zTokens**    | <p>•  Base yield, with an added boost reserved for sZOTH holders.</p><p>•  Mint fees discounted 25% to 100% by tier.</p><p>•  Redemption fees discounted for stakers.</p><p>•  25% to 100% discount on the zVaults platform fee by tier.</p>   |
| **zPayments**  | <p>•  FX and settlement fees rebated 10% to 100% by tier.</p><p>•  Priority routing and service for sZOTH holder transactions.</p><p>•  Payment providers post a slashable sZOTH bond to integrate.</p>                                        |
| **Zocta Card** | <p>•  Tiered cashback 3% to 7%, set by sZOTH balance.</p><p>•  Metal card unlocked at Platinum.</p><p>•  Concierge, Priority Pass, and FX-free spend at upper tiers.</p><p>•  Zocta Points convert to Zoth token on redemption.</p>            |
| **zAI**        | <p>•  Agent access from the Silver tier upward.</p><p>•  Zoth token consumed as usage credits, discounted for stakers.</p><p>•  Executes zVaults and zPayments actions for the user.</p><p>•  CFO agent to manage, pay, and send invoices.</p> |

**Protocol layer utilities.** Utilities that lock supply and scale with platform usage.

| **Mechanism**             | **How it works**                                                                                                           | **Effect on Zoth token**                                      |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Staked safety module      | An opt-in sZOTH pool backstops a vault shortfall or a zToken de-peg, for an added share of protocol fees.                  | Converts staking into risk capital and deepens locked supply. |
| sZOTH as collateral       | sZOTH is accepted as collateral inside zVaults and can be borrowed against.                                                | Removes the opportunity cost of locking Zoth token.           |
| Fee payment in Zoth token | Settlement, mint, and redemption fees are payable in Zoth token at a discount, and route into the sZOTH distribution pool. | Per-transaction demand that scales with volume.               |
| Agentic spend metering    | zAI transaction and API limits scale with sZOTH held. Zoth token is consumed as credits.                                   | Usage-linked demand from the agent layer.                     |

**Zoth Club membership tiers**. Tier is set by sZOTH balance and unlocks better economics on every product.

| **Tier** | **sZOTH Stake** | **Card Cashback** | **FX Rebate** | **Key Perks**                                        |
| -------- | --------------- | ----------------- | ------------- | ---------------------------------------------------- |
| Bronze   | 5,000           | 3%                | 10%           | Beta access, community channels                      |
| Silver   | 50,000          | 4%                | 25%           | Priority vault queue, reduced fees, zAI agent access |
| Gold     | 100,000         | 5%                | 50%           | Priority Pass, premium virtual card                  |
| Platinum | 500,000         | 6%                | 75%           | Metal card, concierge, vault co-design               |
| Pinnacle | 2,000,000       | 7%                | 100%          | Founder access, bespoke vault, family office         |

_sZOTH is transferable and represents a share of the Zoth token in the staking contract. Buyback Zoth token is added to the contract each quarter, raising the Zoth token that each sZOTH redeems for. Unstaking carries a 2% withdrawal fee, retained in the contract for remaining holders, with no cooldown._

**Risk Factors and Legal Disclaimer**

This document is for information purposes only. It is not an offer to sell, or a solicitation of an offer to buy, any token or security, and it is not investment, legal, tax, or financial advice.

* **Forward-looking statements.** Projections, targets, and illustrative figures in this document, including revenue, buyback size, launch price, and valuations, are estimates. They are not guarantees of future performance and may change.
* **Regulatory risk.** Token treatment varies by jurisdiction and may change. Regulatory action could affect the token, its utility, or its availability.
* **Market risk.** Token price is volatile and liquidity is not assured.
* **Technical risk.** Smart-contract, custody, and integration failures could result in loss.
* **Execution risk.** Products, revenue, and the buyback may not materialize as modeled.
* **Governance risk.** The decentralization schedule is indicative and Foundation-controlled. Voting parameters are not final.
