# What is zPayments?

zPayments is the payout layer of the Zoth ecosystem. It converts USDC into local fiat currency and delivers it to a beneficiary’s bank account or mobile wallet in the destination market.

A sender deposits USDC into a Zoth custody wallet. Zoth forwards that balance to a regulated regional payout partner, and the partner pays the beneficiary in local currency against a credit facility Zoth holds with them. The sender never funds the payout partner directly. This arrangement is called postfunding, and it means a business does not have to hold a pre-funded balance in every market it pays into.

zPayments is custodial. Between deposit and payout the USDC is held by Zoth in a segregated MPC wallet, not in a wallet the sender controls. The custody model is described in Security of zPayments.

The service runs in one direction only. zPayments converts USDC to fiat. It does not buy digital assets with fiat, does not convert between digital assets, and does not support cash pickup.

### **Who uses zPayments**

| **User**                                | **What they use it for**                                                                                        |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Money transfer operators                | Paying out in new corridors without opening a banking relationship and holding a pre-funded balance in each one |
| Payment service providers               | Adding a fiat off-ramp without building their own screening and approval workflow                               |
| Importers and exporters                 | Paying overseas suppliers in local currency at a rate quoted before the payment is sent                         |
| Marketplaces, gig and payroll platforms | Many small payouts across several countries, each with its own beneficiary format                               |
| Treasury teams                          | Larger-value conversion with a named contact at Zoth and a full audit record                                    |

Both individuals and businesses can send, and both can receive. The combination determines the service type recorded against the transaction: individual to individual is C2C, individual to business is C2B, business to individual is B2C, and business to business is B2B. The service type is derived from the verified account records,

**Relationship management**

Accounts running high-value volume are assigned a named relationship manager at Zoth, who handles onboarding, confirms coverage for a destination market before volume is committed to it, helps structure beneficiary records for a new market, and agrees fee terms at the account level. The controls are the same for every account. A relationship manager does not approve transactions and cannot pass a payout that has failed a check.
