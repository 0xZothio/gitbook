# Fees in zPayments

There is no platform access fee and no subscription fee. Two costs apply to a payout: the Zoth FX fee and the local network commission charged by the payout partner.

| **Cost**                 | **Where it appears**                                                                                            |
| ------------------------ | --------------------------------------------------------------------------------------------------------------- |
| Zoth FX fee              | Built into the exchange rate shown in the app. The rate displayed is the rate the sender receives after the fee |
| Local network commission | Shown as a separate line at the review step, before the sender confirms                                         |

Total pay-in is the amount being sent, plus the Zoth FX fee, plus the local network commission.

### **How the fee is set**

When a payout is priced, three lookups run in order and the first match applies: a rate agreed for that specific account, then a rate set for that destination market, then the default rate.

### **Worked example**

The figures below are an example of how the total is calculated. They are not zPayments pricing. Fees are confirmed per account and per destination market.

On a reference rate of 1 USDC to 100 INR, with an FX fee of 1 per cent and a network commission of 7:

| **Line**                  | **Amount** |
| ------------------------- | ---------- |
| Amount being sent         | 100 USDC   |
| Zoth FX fee at 1 per cent | 1 USDC     |
| Local network commission  | 7 USDC     |
| Total pay-in              | 108 USDC   |
