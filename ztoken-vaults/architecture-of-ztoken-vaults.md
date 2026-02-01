# Architecture of zTOKEN Vaults

The zTOKEN vault architecture implements a permissioned, institutionally-oriented design that balances fund manager autonomy with protocol-level security and compliance requirements.

#### <mark style="color:$info;">Smart Contract Infrastructure</mark>

All zTOKEN vaults are deployed as ERC-20 compliant smart contracts adhering to a standardized interface template. This standardization ensures interoperability across the Zoth ecosystem while allowing customization of strategy-specific parameters and logic.

Vault contracts implement upgradeable proxy patterns, enabling protocol improvements and bug fixes without requiring migration of user funds or disruption of vault operations. However, upgrade authority is restricted exclusively to the Zoth Foundation, preventing fund managers from unilaterally modifying core contract logic. This governance structure protects investors from potential malfeasance while allowing the protocol to adapt to evolving security best practices and technological improvements.

### <mark style="color:$info;">Vault Creation and Onboarding</mark>

<figure><img src="../.gitbook/assets/unknown (4).png" alt=""><figcaption></figcaption></figure>

zTOKEN vault creation follows a permissioned process requiring comprehensive Know Your Business (KYB) verification and compliance screening. The onboarding pathway accommodates fund managers across the operational maturity spectrum:

For established fund managers with existing legal entities and operational infrastructure, Zoth conducts KYB due diligence and, upon approval, deploys a customized vault contract tailored to the fund's specific strategy and requirements.

For emerging fund managers without existing infrastructure, Zoth provides comprehensive turnkey services spanning the entire fund establishment lifecycle. This includes corporate incorporation, legal documentation, regulatory compliance frameworks, and data analytics infrastructure. This white-glove onboarding model reduces barriers to entry for qualified managers while maintaining institutional-grade operational standards.

### <mark style="color:$info;">Custody and Key Management</mark>

Fund managers are required to utilize multi-party computation (MPC) wallets for all vault asset custody and transaction execution. MPC technology distributes private key material across multiple parties, eliminating single points of failure and substantially reducing risks of private key compromise, theft, or unauthorized access. This institutional-grade custody requirement aligns zTOKEN vaults with best practices in traditional asset management while leveraging cryptographic innovations unique to blockchain infrastructure.

#### <mark style="color:$info;">Fund Administration and Attestation</mark>

Each zTOKEN vault is subject to ongoing oversight by independent fund administrators who audit portfolio positions, verify NAV calculations, and attest to reported performance metrics. These administrators serve as the primary attestors in the oracle network, providing biweekly price updates that flow through to on-chain oracle contracts. The administrator attestation model imports traditional fund industry checks and balances into the blockchain environment, creating accountability and verification layers familiar to institutional investors.

### <mark style="color:$info;">Operational Autonomy</mark>

Within the framework of protocol-level security and compliance requirements, fund managers retain comprehensive operational control over investment execution. Managers can deploy capital to any DeFi protocol, operate across any blockchain network (subject to protocol-supported integrations), and trade any digital or tokenized asset consistent with their vault's stated strategy. This operational flexibility enables managers to pursue alpha-generating opportunities without artificial constraints while maintaining appropriate risk management and compliance boundaries.

### <mark style="color:$info;">Integration with ZEUSD</mark>

The zTOKEN vault architecture serves as the foundational layer for ZEUSD, which functions as a vault-of-vaults allocating capital across multiple constituent zTOKEN vaults. When users deposit into ZEUSD, the protocol actually acquires and holds the underlying zTOKENs representing shares in each allocated vault. This direct ownership model ensures that ZEUSD's value transparently reflects the aggregate performance of its constituent positions.

Allocation decisions—determining what percentage of ZEUSD assets are deployed to each underlying zTOKEN vault—are implemented through a combination of smart contract enforcement and operational execution. The allocation framework operates at both layers: smart contract logic enforces deposit and withdrawal limits and routing rules, while operational processes managed by the Zoth team execute rebalancing transactions according to governance-approved allocation weights.

\
\
<br>
