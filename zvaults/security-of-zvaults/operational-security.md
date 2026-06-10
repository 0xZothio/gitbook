# Operational Security

zVaults are operated under a layered security framework that treats key custody, internal access, platform infrastructure, and on-chain activity as separate control domains, each independently enforced so a failure in one does not cascade into the others.

### Custody and Key Management

Zoth has established partnerships with [ForDeFi](https://fordefi.com/) as the leading MPC wallet providers to ensure fund managers have access to battle-tested, enterprise-grade custody infrastructure.&#x20;

The highest-privilege layer. Control over vault funds and protocol state is held in multi-party computation (MPC) wallets, never single keys.

* **Threshold custody:** privileged wallets require a 3-of-5 signing quorum, so no individual can move funds or change protocol state alone.
* **Hardware-only signing:** the highest-authority signers are restricted to hardware wallets.
* **Role separation:** super-admin, vault-admin, screening, and NAV-update authorities are held by distinct wallets, so no single role concentrates control.
* **Out-of-band confirmation:** each privileged transaction is approved by the required quorum on a live video call before it is signed.
* **Minimal deployment footprint:** the temporary key used to deploy the contracts is decommissioned once setup completes, leaving no standing single-key authority over live vaults.

### Cross-Chain Bridge Security

For fund strategies requiring cross-chain asset movement, the protocol enforces strict security standards for bridge infrastructure. \
\
Zoth has partnered with [LiFi](https://li.finance/). In future only verified bridge partners with extensive operational history, proven security track records, and comprehensive insurance coverage are approved for protocol use. This whitelist approach prevents fund managers from using untested or high-risk bridge solutions that could expose vault assets to bridge-specific vulnerabilities.

The protocol continuously monitors cross-chain transfers, with anomaly detection systems flagging unusual bridge activity.

### Personnel Security

* **Vetting:** every team member completes a background check before joining.
* **Ongoing awareness:** the team receives continuous security advisories and periodic targeted training to stay current on emerging threats.

### Internal Access Control

* **Zero Trust:** access to internal systems is granted per request and per identity, not by network location.
* **Hardware-backed authentication:** privileged access requires a hardware security key, so a stolen password or phishing attempt alone cannot grant entry.
* **Compartmentalized access:** critical cloud and infrastructure accounts are segmented and reachable only from dedicated, hardened machines.
* **Endpoint monitoring:** corporate devices run continuous detection and response with behavioral analysis and rapid containment.

### Platform and Infrastructure

* **Environment isolation:** staging and production are fully separated, so development activity cannot reach live systems.
* **Edge protection:** the public application sits behind DDoS mitigation, a web application firewall, rate limiting, API protection, and enforced TLS.
* **Verified authorship:** Git commits require cryptographic signatures from hardware-backed keys, confirming authorship and preventing unauthorized code changes.
* **Supply-chain scanning:** the CI/CD pipeline scans third-party dependencies for known vulnerabilities before any deployment.

### On-Chain Monitoring and Audit

Independent pre-deployment audits are covered under Smart Contract Security; the controls below are the continuous, runtime layer that operates once a vault is live.

* **Continuous on-chain monitoring:** real-time surveillance of contract interactions, fund flows, and vault-share movements flags anomalous behavior as it happens.
* **Pre-execution screening:** transactions are simulated and screened before execution to block malicious smart-contract interactions.
