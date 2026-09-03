# Supported Payouts

Payouts are delivered in the beneficiary’s local currency through regulated local rails operated by a regional payout partner. Coverage is confirmed per corridor at onboarding rather than published as a list, because supported markets change.

### **Payout modes**

| **Mode**     | **Delivery**                                                                                                   | **Beneficiary details required**                                                 |
| ------------ | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| BANK         | Transfer into a bank account, cleared through the destination market’s own clearing or instant-payment network | Account number, bank and branch, beneficiary name and address, country, currency |
| MOBILEWALLET | Deposit into a regional mobile wallet                                                                          | Wallet number and provider, beneficiary name and address, country, currency      |

Banks and branches are selected from the payout partner’s own reference data rather than typed in, which removes the most common cause of a failed payout. Where the destination market supports it, the account is validated against the beneficiary name before the payout is created.

A beneficiary record is created once and reused for every later payout to that recipient. Country and currency are fixed at the point the record is created, so a beneficiary belongs to one destination market.

### **Out of scope**

* Buying digital assets with fiat. There is no on-ramp.
* Converting one digital asset into another.
* Cash pickup. Payouts go to accounts and wallets only.
* Deposit assets other than USDC.
