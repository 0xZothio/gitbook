# Security of zPayments

### **Custody security**

USDC is held in a segregated wallet on ForDefi, secured by multi-party computation with three of five signatures required to move funds. No single person holds a complete signing key.

| **Control**       | **Detail**                                                                       |
| ----------------- | -------------------------------------------------------------------------------- |
| Custody           | Segregated MPC wallet on ForDefi, three-of-five signing                          |
| Deposit sources   | Only wallet addresses recorded and verified at onboarding                        |
| Deposit detection | On-chain listener, monitored continuously                                        |
| Wallet screening  | Blockchain analytics on every wallet, run on Chainalysis at the Zoth group level |
| Threat monitoring | Real-time monitoring by Cyvers                                                   |
| Audits            | Contracts audited by Entersoft                                                   |

### **Operational security**

Six control pairs run across the platform on a maker and checker basis. In each pair the person who performs an action and the person who approves it must be different people. Applied to a payout, the person who creates a transaction is never the person who approves it, and neither is the person who reconciles it.

Six functions are held by different teams: customer onboarding, transaction execution, settlement, monitoring, systems administration and audit. No employee controls onboarding, approval, execution and settlement at the same time.

Activity is written to an immutable, tamper-evident log. Each entry records the user, the time, the source IP address, the action taken, the previous value, the new value and any approval given.
