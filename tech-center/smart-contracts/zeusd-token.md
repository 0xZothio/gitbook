# ZeUSD Token

## Overview

ZeUSD is an upgradeable ERC-20 token that serves as the core stable asset of the ZeUSD protocol. It implements advanced compliance features including blacklisting and role-based access control through OpenZeppelin's AccessManager.

## Key Features

### 1. Token Configuration

* **Name:** ZeUSD
* **Symbol**: ZeUSD
* **Decimals**: 18
* **Implementation**: ERC-20 Upgradeable with UUPS proxy pattern

### 2. Access Control System

The token uses OpenZeppelin's AccessManager for role-based permissions:

* **Registry Integration**: Core contract addresses managed through central Registry
* **Access Manager**: Handles role-based permissions
* **Router**: Exclusive minting/burning privileges

### 3. Security Features

#### Blacklist System

```solidity
function setBlacklistStatus(address account, bool status) external {
    // Only authorized roles can blacklist
    // Emits Blacklisted event
}

function isBlacklisted(address account) external view returns (bool) {
    // Returns blacklist status of account
}
```

* Prevents blacklisted addresses from using the token
* Affects all token operations (transfers, approvals)
* Managed by authorized roles
* Events emitted for all blacklist changes

#### Router Control

```solidity
function mint(address to, uint256 amount) external {
    // Only authorized router can mint
    // Validates blacklist status
    // Emits Transfer event
}
```

* Only authorized router can mint/burn tokens
* Ensures protocol security and integrity
* Validates all operations through Registry



## Core Functions

### 1. Minting

```solidity
function mint(address to, uint256 amount) external;
```

* Restricted to authorized router
* Creates new tokens based on validated deposits
* Includes blacklist validation
* Emits Transfer event

### 2. Burning

```solidity
function burn(uint256 amount) external;

function burnFrom(address account, uint256 amount) external;
```

* Destroys tokens during withdrawal process
* Requires proper authorization
* Includes blacklist checks
* Updates total supply
* Emits Transfer event

### 3. Error Handling

```solidity
error ZeUSD_Unauthorized(string _message);
error ZeUSD_InvalidRegistryAddress();
error ZeUSD_InvalidAccessManagerAddress();
```

* Custom errors for better error handling
* Specific error types for different scenarios
* Clear error messages for debugging

### 4. Events

* Standard ERC20 events (Transfer, Approval)
* Custom events for blacklist changes
* Detailed event parameters for tracking

### 5. Upgradability

* Implements UUPS upgrade pattern
* Managed through AccessManager roles
* Preserves state during upgrades
* Supports future protocol improvements

This updated documentation reflects the current implementation with 18 decimals (instead of 6), the new access control system through AccessManager, and the more comprehensive error handling system using custom errors.

\
