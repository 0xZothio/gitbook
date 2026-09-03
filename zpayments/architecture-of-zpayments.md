# Architecture of zPayments

zPayments separates the digital asset side of a payment from the fiat side. USDC is received and held by Zoth; fiat is delivered by a payout partner. Each handoff between the two has a recorded state, and no state advances until the system receives confirmation for it.

### **Components**

| **Component**         | **Function**                                                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Web application       | Where a sender verifies their identity, deposits USDC, saves beneficiaries, requests quotes, and views transaction history |
| Operations console    | Where a Zoth operator reviews and approves or rejects each payout, and monitors deposits and balances                      |
| Custody wallet        | A segregated MPC wallet, operated on ForDefi, holding USDC between deposit and payout                                      |
| Deposit listener      | Detects incoming USDC on chain and attributes it to the sender’s account                                                   |
| Identity verification | Sumsub, embedded in the product, for individual and business verification and for capturing the sender’s deposit address   |
| Authentication        | Privy, for sign-in by email or Google account                                                                              |
| Payout partner        | A regulated regional partner that quotes the rate and delivers local fiat to the beneficiary                               |
| Screening             | Sanctions, politically exposed person and adverse media screening, and blockchain analytics on every wallet                |

### **Roles**

| **Role**   | **Can do**                                                                             | **Cannot do**                                                                |
| ---------- | -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Sender     | Verify, deposit, add beneficiaries, request quotes, create payouts, view history       | Approve their own payout, or send from an address that has not been verified |
| Operator   | Review and approve or reject payouts, monitor deposits and balances                    | Create the payout they approve, or approve a payout that has failed a check  |
| Compliance | Set risk classification, review screening matches, suspend an account or a transaction | Execute a payout                                                             |
