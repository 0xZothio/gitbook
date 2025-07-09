---
description: Protocol's Central Registry and Price Coordinator
---

# Vault System Architecture

## Overview

The Vault system forms the backbone of the ZeUSD protocol, managing asset deposits, configurations, and price coordination. It consists of two primary components that work together to ensure secure and efficient asset management:

1. **VaultRegistry**: Acts as the central coordinator for vault configurations, price validation, and deposit parameters
2. **Vault Implementation (BaseVault/USYCVault)**: Handles the actual asset operations and storage

<figure><img src="../../.gitbook/assets/VaultImplementation (6).png" alt=""><figcaption></figcaption></figure>

## VaultRegistry: Configuration and Price Coordination

The VaultRegistry serves three critical functions:

* Central registry for all vault configurations
* Price coordinator for ZeUSD minting calculations
* Validator for deposit parameters and constraints

### 1. Vault Registration System

The registration system ensures proper configuration and tracking of all vaults in the protocol:

<figure><img src="../../.gitbook/assets/Vault registration system.png" alt=""><figcaption></figcaption></figure>

```solidity
function registerVault(
    string calldata vaultName,
    address rwaAddress,
    address vaultAddress,
    uint256 ltv,
    bool isActive,
    bool isStable,
    uint256 slippage
) external;
```

Key Features:

* **Comprehensive Configuration**: Stores and manages all supported vault types
* **Parameter Validation**: Ensures valid LTV ratios (1-1000000) and slippage settings
* **Activity Management**: Controls active/inactive states of vaults
* **Event Tracking**: Emits detailed events for all configuration changes

### 2. Price Management

The price management system implements a robust validation and scaling mechanism:

<figure><img src="../../.gitbook/assets/Price Management (1).png" alt=""><figcaption></figcaption></figure>

Key Components:

* **Oracle Integration**: Direct connection to price feeds
* **Validation Rules**:
  * Non-zero price verification
  * Staleness checks
  * Bounds validation
  * Decimal normalization
* **Scaling Logic**: Handles different token decimal places

### 3. Deposit Validation System

Ensures secure and valid deposits through multi-layer validation:

<figure><img src="../../.gitbook/assets/Deposit Validation System.png" alt=""><figcaption></figcaption></figure>

Validation Steps:

1. Asset Support Verification
2. Vault Status Check
3. Price Validation
4. LTV Compliance
5. Amount Validation

## Vault Implementation

### 1. Base Vault Architecture

The vault system uses a hierarchical implementation for flexibility and security:

<figure><img src="../../.gitbook/assets/Base Vault Architecture.png" alt=""><figcaption></figcaption></figure>

Features:

* **Modular Design**: Separates core functionality from specific implementations
* **Extensibility**: Easy to add new vault types
* **Security**: Common security features in base implementation
* **Asset Management**: Flexible primary and secondary asset handling

### 2. Asset Management

Comprehensive asset handling system:

<figure><img src="../../.gitbook/assets/Asset Management.png" alt=""><figcaption></figcaption></figure>

Capabilities:

* **Primary Asset Operations**: Core asset handling with strict controls
* **Secondary Asset Support**: Flexible additional asset management
* **Emergency Controls**: Quick response mechanisms for security
* **Slippage Protection**: Prevents unfavorable transactions

## Error Handling

Comprehensive error system for precise problem identification:

```solidity
// VaultRegistry Errors
error VaultRegistryUnauthorizedRouter(address caller);
error VaultRegistryInvalidAddress(address addr);
error VaultRegistryInvalidParameters(string message);
error VaultRegistryInvalidLTV();
error VaultRegistryVaultNotRegistered(address rwaAddress);

// Vault Errors
error Vault_Unauthorized(address caller);
error Vault_AssetNotSupported(address asset);
error Vault_InvalidAmount();
error Vault_EmergencyModeActive(uint256 timestamp);

```

Benefits:

* Clear error identification
* Gas-efficient error handling
* Detailed error information
* Consistent error patterns

## Events System

Comprehensive event emission for tracking and monitoring:

```solidity
// VaultRegistry Events
event VaultRegistryVaultRegistered(
    address indexed rwaAddress,
    address indexed vaultAddress,
    string vaultName,
    uint256 ltv,
    bool isActive,
    bool isStable,
    uint256 slippage
);

// Vault Events
event VaultPrimaryAssetOperation(
    address indexed user,
    uint256 amount,
    bool isDeposit
);
```

Purpose:

* Transaction tracking
* State change monitoring
* Audit trail maintenance
* Integration support

## Security Architecture

### 1. Access Control System

Features:

* Role-based access control
* Granular permission management
* Clear responsibility separation
* Audit-friendly structure

### 2. State Management

<figure><img src="../../.gitbook/assets/State Management.png" alt=""><figcaption></figcaption></figure>

States:

* **Normal**: Full functionality
* **Paused**: Temporary halt
* **Emergency**: Critical operations only

## Integration Patterns

### 1. Router Integration Flow

<figure><img src="../../.gitbook/assets/Router Integeration Flow.png" alt=""><figcaption></figcaption></figure>

Key Aspects:

* Seamless operation flow
* Clear responsibility chain
* Error handling at each step
* Event emission for tracking

### 2. Price Oracle Integration

<figure><img src="../../.gitbook/assets/Price Oracle Integeration.png" alt=""><figcaption></figcaption></figure>

Features:

* Real-time price updates
* Validation checks
* Fallback mechanisms
* Decimal handling



This comprehensive documentation provides both technical details and explanatory text, making it suitable for the documentation page while maintaining technical accuracy.



\
