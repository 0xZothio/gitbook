# Custody and Operational Security

#### <mark style="color:$info;">Multi-Party Computation (MPC) Wallets</mark>

All vault assets are held in multi-party computation (MPC) wallets operated by fund managers, eliminating single points of failure inherent in traditional private key custody. MPC technology cryptographically distributes key material across multiple parties such that no individual party ever possesses a complete private key. Transactions require collaborative computation among multiple key share holders, preventing unauthorized asset movement even if one party is compromised.

This institutional-grade custody model substantially reduces risks of private key theft, insider fraud, and operational key management errors that have plagued both traditional and crypto-native financial institutions. The MPC requirement applies uniformly across all fund managers, ensuring consistent security standards regardless of individual vault strategy or risk profile.

Zoth has established partnerships with leading MPC wallet providers to ensure fund managers have access to battle-tested, enterprise-grade custody infrastructure. While specific provider details remain confidential for operational security reasons, all approved MPC solutions undergo rigorous security review and meet institutional custody standards.

#### <mark style="color:$info;">Cross-Chain Bridge Security</mark>

For fund strategies requiring cross-chain asset movement, the protocol enforces strict security standards for bridge infrastructure. Only verified bridge partners with extensive operational history, proven security track records, and comprehensive insurance coverage are approved for protocol use. This whitelist approach prevents fund managers from using untested or high-risk bridge solutions that could expose vault assets to bridge-specific vulnerabilities.

When assets move cross-chain, both the sending and receiving transactions occur through MPC wallets under fund manager control, maintaining custody security standards across the entire transfer lifecycle. The protocol continuously monitors cross-chain transfers, with anomaly detection systems flagging unusual bridge activity for manual review.

#### <mark style="color:$info;">Insurance Coverage</mark>

Recognizing that no security framework eliminates all risks, Zoth provides insurance coverage to users, protecting against losses resulting from smart contract exploits, custody failures, and certain operational risks. This insurance layer adds a financial backstop beyond technical security controls, ensuring that users can be made whole even in catastrophic failure scenarios.

Insurance arrangements are structured to align incentives appropriately, with coverage terms designed to encourage prudent risk management by fund managers while protecting users from low-probability, high-impact events. Specific coverage details, policy limits, and exclusions are disclosed in user-facing documentation and updated as the protocol scales and insurance markets evolve.
