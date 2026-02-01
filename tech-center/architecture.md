---
description: >-
  Explore the detailed architecture of our Solidity contracts, designed for
  scalability, transparency, and seamless integration.
hidden: true
cover: ../.gitbook/assets/Banner 14.png
coverY: 0
---

# Architecture

The Zoth protocol contracts are meticulously designed to handle intricate operations, including asset swaps between Real World Assets (RWAs) and stable token, lifecycle management of the ZeUSD stable token, issuance of structured financial products, efficient asset exchange without relying on traditional liquidity pools, and precise asset pricing for dependable transaction execution.

## Core Components

### **1. ZeUSD Token**

* ERC20 stablecoin implementation with compliance features
* Maintains 18 decimal places (standard ERC20 decimal format)
* Implements UUPS upgradeable pattern
* Supports minting/burning through authorized Router
* Includes blacklisting functionality for regulatory compliance
* Enforces role-based access control for critical operations

### 2. ZeUSD Router V2

Central coordinator for protocol operations including:

* &#x20; Deposit handling and ZeUSD minting
* Withdrawal initiation and processing
* Asset validation and conversion coordination
* Whitelist management with merkle proof verification
* NFT (CDP) minting to represent deposits
* Integration with VaultRegistry for deposit parameters

### 3. Withdrawal System

* Manages the complete withdrawal lifecycle
* Handles batch processing of withdrawal requests
* Maintains withdrawal request queue and status tracking
* Coordinates with vaults for asset withdrawals
* Implements cooldown periods and request validation
* Supports emergency withdrawal procedures

### 4. VaultRegistry

* Manages vault configurations and validations
* Handles Loan-to-Value (LTV) ratios per vault (1-1000000, 6 decimals precision)
* Coordinates with price oracle for asset valuations
* Maintains vault status (active/inactive)
* Supports stable and non-stable asset configurations
* Manages slippage parameters for asset conversions

### 5. Vault System

**BaseVault**: Abstract base implementation with:

* Asset support management
* Emergency mode controls
* Pause/unpause functionality
* Multi-asset support

### 6. USYCVault

Specialized implementation for USYC handling:

* Primary asset operations
* Secondary asset support
* Slippage protection
* Emergency withdrawal procedures

### 7. ZeDP (CDP NFT)

* ERC721 implementation representing deposits
* Stores deposit metadata and ownership
* Supports enumeration for user position tracking
* Integrates with withdrawal system for position management
* Maintains deposit history and metadata

## Price System

### Price Oracle

* Manages price feeds for supported assets
* Implements staleness checks for price validity
* Supports custom oracle integration per asset
* Provides standardized price data interface
* Configurable staleness thresholds per asset

## Access Control

### 1. Registry

* Central contract address registry
* Manages contract versions and updates
* Provides single source of truth for contract addresses
* Essential for protocol upgrades and maintenance

### 2. Access Manager

* Implements role-based access control
* Manages protocol permissions including:
  1. ROUTER\_ROLE: For deposit/withdrawal operations
  2. GUARDIAN\_ROLE: For emergency controls and upgrades
  3. GATEKEEPER\_ROLE: For compliance operations
  4. ORCHESTRATOR\_ROLE: For vault management
  5. WHITELISTER\_ROLE: For managing whitelisted addresses and merkle roots
  6. TREASURY\_ROLE: For managing withdrawal processing and batch operations

## Error Handling

* Comprehensive error system with specific error types per contract
* Standardized error interfaces for consistent error handling
* Detailed error messages for debugging and monitoring
* Custom errors for specific operational scenarios

## Event System

* Rich event emission for all critical operations
* Standardized event interfaces per contract
* Detailed event parameters for transaction tracking
* Support for off-chain monitoring and indexing

## Security Features

* Emergency mode for critical situations
* Slippage protection for asset conversions
* Cooldown periods for sensitive operations
* Role-based access control throughout
* Blacklisting capability for compliance
* Whitelist verification with merkle proofs
* Comprehensive input validation
* Pause mechanisms for risk mitigation







