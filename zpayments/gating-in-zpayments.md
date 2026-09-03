# Gating in zPayments

Three gates control whether a payout can happen. They are enforced continuously, not only at sign-up.

### **Verification gate**

An account cannot pay out until identity verification is approved. A rejected verification cannot proceed. If an approved verification is later downgraded, or a screening match appears, payout functionality is switched off for that account until the matter is resolved.

### **Wallet whitelisting**

A sender can only deposit from a wallet address recorded and verified during onboarding. Ownership of the address is declared by the customer and verified through the identity provider. A declaration on its own is not enough, and an address that has not been verified cannot fund a payout. Deposits arriving from an unrecorded address are not attributed automatically and have to be resolved manually.

### **Pre-execution checks**

Seven conditions are confirmed before a payout is approved. If any one of them fails, the transaction is suspended, escalated to compliance, and does not resume until the failure is cleared and the resolution recorded.

| **#** | **Condition**                         |
| ----- | ------------------------------------- |
| 1     | Customer approved                     |
| 2     | Wallet approved                       |
| 3     | Sanctions checks complete             |
| 4     | Blockchain screening complete         |
| 5     | Beneficiary validated                 |
| 6     | Purpose of the transaction understood |
| 7     | Liquidity confirmed                   |
