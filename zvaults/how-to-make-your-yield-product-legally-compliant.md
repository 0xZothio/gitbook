# How to Make Your Yield Product Legally Compliant

A zVault can be plugged into a compliant stack with FAAST whenever its creator wants a regulated legal substrate behind the token. The vault is the technical layer: an ERC-20 interest-bearing token, deposit and redemption contracts, NAV-based pricing, and MPC custody. It works on its own. FAAST is a separate legal layer a vault creator opts into on top of those rails.

FAAST is a regulated fund structure operated as a Segregated Portfolio Company (SPC) under the Cayman Islands Monetary Authority (CIMA) and the BVI Financial Commission. It runs as a fully managed legal framework: independent directors hold governance, a licensed fund administrator processes subscriptions and redemptions and calculates NAV, an appointed custodian holds the assets, and an external auditor verifies them. The SPC form lets the fund hold assets and liabilities in separate, walled-off portfolios, which is what delivers ring-fenced, bankruptcy-remote protection. A vault plugged into FAAST therefore sits inside a structure that meets the governance, NAV reporting, and asset-segregation standards professional allocators expect.

This is the distinction from most yield infrastructure. Other providers ship the technical rails and stop there: smart contracts, a token, a yield source, with the legal wrapper left to the creator. Zoth provides both. A team can launch a zVault on technical rails alone, or plug it into FAAST and get a regulated fund structure underneath the same token.

What each layer provides:

| Layer                           | What it provides                                                                                                                                                                      |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| zVault (technical architecture) | ERC-20 interest-bearing token, deposit and redemption contracts, NAV-based pricing, MPC custody, on-chain transparency                                                                |
| FAAST (legal architecture)      | Regulated fund structure under CIMA and BVI, Segregated Portfolio Company isolation, independent fund administrator, custodian, auditor, ring-fenced and bankruptcy-remote protection |

When a vault creator plugs into FAAST, the vault gets its own segregated portfolio inside the SPC. Capital flowing through the on-chain contracts maps to a regulated fund position: assets are custodied and administered under the fund's mandate, NAV is attested by an independent administrator, and token holder claims are isolated from protocol insolvency and from other vaults' performance. The same on-chain token now carries a legal claim on regulated, audited assets.

This combination is the differentiator. Institutional allocators need a regulated structure, independent NAV attestation, segregation, and bankruptcy remoteness before they can deploy, and smart contracts alone do not deliver any of it. Technical-only infrastructure leaves that allocator to either stay off-chain or accept unsecured protocol risk.
