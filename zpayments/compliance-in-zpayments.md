# Compliance in zPayments

Screening, Travel Rule handling, beneficiary validation and transaction monitoring run inside every transaction. They do not replace a customer’s own regulatory obligations, which remain with the customer.

### **Onboarding**

Verification is carried out through Sumsub, embedded in the product.

| **Individual senders**                                                        | **Business senders**                                                                                                                       |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Government identity document                                                  | Legal entity name, registration number and country of incorporation                                                                        |
| Address verification where the risk profile or destination market requires it | Registered address and nature of business                                                                                                  |
| Politically exposed person, sanctions and adverse media screening             | Ultimate beneficial owners, directors and authorised signatories identified                                                                |
| Risk assessment producing a low, medium or high classification                | Every beneficial owner, director and authorised representative screened for sanctions, politically exposed person status and adverse media |

Approval authority rises with the risk classification. Low risk is approved by a compliance analyst, medium risk by a compliance manager, and high risk by the head of compliance with enhanced due diligence required.

### **Screening**

Screening runs at three points rather than only at onboarding: when the account is opened, again before each transaction is executed, and continuously thereafter through daily automated rescreening and rescreening triggered by a change to a sanctions list or a customer record.

If a screening match is found, the transaction is suspended immediately, a compliance review is opened, the matter is escalated to the head of compliance, and the resolution is recorded. No transaction proceeds until the match is cleared.

### **Blockchain analytics**

Every wallet is screened for exposure to sanctioned entities, darknet markets, mixers, fraud, ransomware and illicit financing. Screening runs on Chainalysis at the Zoth group level.

| **Risk score** | **Result**                                     |
| -------------- | ---------------------------------------------- |
| Low            | Approved automatically                         |
| Medium         | Manual review before the transaction proceeds  |
| High           | Rejected, or escalated for a recorded decision |

### **Travel Rule**

The Travel Rule requires information about the sender and the beneficiary to travel with a transfer between institutions. zPayments collects sender details during verification and beneficiary details when the beneficiary record is created, and transmits them to the receiving institution where the destination jurisdiction requires it.

This is why the beneficiary form changes depending on the destination market, the payout mode and whether the beneficiary is a person or a business. The record is built to meet the destination market’s requirement when it is created, rather than being corrected at the point of payment.

### **Transaction monitoring**

Transactions are monitored for payments split into amounts that sit below a reporting threshold, activity that does not match the profile given at onboarding, funds deposited and paid out in quick succession, destination markets carrying higher risk, and deposit addresses whose on-chain exposure changes after they were approved.
