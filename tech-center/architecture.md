---
description: >-
  Explore the detailed architecture of our Solidity contracts, designed for
  scalability, transparency, and seamless integration.
cover: ../.gitbook/assets/Banner 14.png
coverY: 0
---

# Architecture

<figure><img src="../.gitbook/assets/Practice - Architecture 3 (2).jpg" alt=""><figcaption></figcaption></figure>

The Zoth protocol contracts are meticulously designed to handle intricate operations, including asset swaps between Real World Assets (RWAs) and stable token, lifecycle management of the ZeUSD stable token, issuance of structured financial products, efficient asset exchange without relying on traditional liquidity pools, and precise asset pricing for dependable transaction execution.

## **ZeUSD Token**

Represents the stable token that can be minted or burned through the **Router** contract.

## **Router**&#x20;

Serves as the central contract coordinating operations such as:

* Minting and burning ZeUSD tokens.
* Facilitating collateral deposits (e.g., stablecoins or RWAs) into the **Sub Vault**.
* Fetching information from the **Collateral Vault** for minting purposes.

## **Collateral Vault**

Provides collateral-related data and interacts with the Router for minting ZeUSD tokens.



## **Sub Vault**

Acts as a repository for deposited collateral (e.g., stablecoins like USDC) and provides data to the Router and other contracts.



## **Oracle Contracts (Oracle RWA & Oracle USDC)**

These provide price data for Real World Assets (RWA) and stablecoins (e.g., USDC) to ensure accurate valuations during transactions and collateral operations.



## **RWA Issuance Contract**

Handles the deposit of USDC to issue RWAs, interacting with the **Sub Vault**.





