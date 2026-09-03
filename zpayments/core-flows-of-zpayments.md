# Core Flows of zPayments

Three flows run through the platform: money coming in, money going out, and what happens when a payout does not complete. The full sequence is shown below, with the two independent sets of states that a sender sees.

&#x20; 1\. Sender verified        Identity checked, deposit address recorded

&#x20;           |

&#x20; 2\. USDC deposited         From the recorded address    Balance: PENDING

&#x20;           |

&#x20; 3\. Held in Zoth custody   Segregated MPC wallet

&#x20;           |

&#x20; 4\. Forwarded to partner   Partner confirms receipt     Balance: AVAILABLE

&#x20;           |

&#x20; 5\. Quote requested        Rate includes the FX fee

&#x20;           |

&#x20; 6\. Payout created         Transaction: UNCONFIRMED

&#x20;           |

&#x20; 7\. Operator approves      Transaction: CONFIRMED

&#x20;           |

&#x20; 8\. Partner executes       Transaction: PROCESSING

&#x20;           |

&#x20; 9\. Beneficiary paid       Transaction: COMPLETED

<br>

Balance states and transaction states are separate. A payout can be in progress while a later deposit is still pending. The two do not affect each other.

### **Deposit Flow**

A sender funds their account by sending USDC from the wallet address recorded during verification. Deposits from any other address are not attributed automatically.

The deposit listener detects the transfer on chain and credits the sender’s account as pending. Zoth then forwards the amount to the payout partner. When the partner confirms it has received the amount, the sender’s balance becomes available.

| **Balance state** | **Meaning**                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------- |
| PENDING           | The deposit has been seen on chain and attributed to the account. Visible, but cannot yet be used |
| AVAILABLE         | The payout partner has confirmed receipt. The balance can be used for a payout                    |

### **Payout Flow**

The sender selects a saved beneficiary, enters an amount in USDC, and states the source of funds and the purpose of the payment. The available balance is checked as the amount is entered, so a quote cannot be requested against a balance that is still pending.

The platform returns a quote. The rate shown includes the Zoth FX fee. The local network commission is shown separately at the review step, together with the amount the beneficiary will receive.

When the sender confirms, the payout is created and enters the operator queue. An operator reviews the amount, the source of funds, the screening results and the beneficiary details, then approves or rejects it. Every payout goes through this review. The operator who approves a payout is never the person who created it.

Once approved, the instruction goes to the payout partner, and the partner’s status updates drive the rest of the flow.

| **Transaction state** | **Meaning**                                                                         |
| --------------------- | ----------------------------------------------------------------------------------- |
| UNCONFIRMED           | Created and waiting for operator review. The amount is reserved                     |
| CONFIRMED             | Approved by an operator and sent to the payout partner                              |
| PROCESSING            | The local banking network has accepted the instruction and the payment is in flight |
| COMPLETED             | Local fiat has reached the beneficiary                                              |
| FAILED                | The payout could not be delivered                                                   |
| REJECTED              | An operator rejected the payout. The reserved USDC returns to the available balance |

### **Failure and Refund Flow**

A payout can stop for four reasons, and each has a defined outcome.

| **What happened**                      | **Outcome**                                                                                                                                                               |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The sender’s balance is not sufficient | The quote cannot be requested. This is checked as the amount is entered, before a quote is issued                                                                         |
| An operator rejects the payout         | The transaction is voided and the reserved USDC returns to the available balance                                                                                          |
| The payout fails at the partner        | Usually incorrect beneficiary bank details or a network error at the destination. The beneficiary record has to be corrected before the payout is attempted again         |
| A status update does not arrive        | The transaction stays in its last confirmed state and is reconciled by the operations team against the partner’s records. A transaction never moves forward on assumption |

Zoth acknowledges every status update it receives from the payout partner, so the partner stops resending that event.
