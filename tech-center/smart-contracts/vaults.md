# Vaults

## Product Overview

Vaults are specialized asset managers in the ZeUSD protocol, implementing the BaseVault interface to handle specific asset types and their interactions. The current implementation focuses on USYC vault management with support for secondary assets.

<figure><img src="../../.gitbook/assets/Product Overview (1).png" alt=""><figcaption></figcaption></figure>

## Core Components

### 1. Asset Management System

The Asset Management System handles both primary (USYC) and secondary assets through a structured approach:

<figure><img src="../../.gitbook/assets/Asset Management System.png" alt=""><figcaption></figcaption></figure>

#### 1.1 Asset Registry

```solidity
// Supported assets tracking
mapping(address => bool) private _supportedAssets;
address private immutable _primaryAsset;
```

Key Features:

* Primary asset immutability
* Dynamic secondary asset support
* Asset validation checks
* Event emission for tracking

### 2. Deposit Flow

<figure><img src="../../.gitbook/assets/Deposit Flow (1).png" alt=""><figcaption></figcaption></figure>

Key Components:

* Asset type detection
* Amount validation
* Slippage protection
* Transfer security

### 3. Emergency Control System

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Features:

* Emergency mode activation
* Time-delayed withdrawals
* Admin-only controls
* Event logging

### 4. Asset Support Management

<figure><img src="../../.gitbook/assets/Asset Support Management.png" alt=""><figcaption></figcaption></figure>

Implementation:

```solidity
function addAsset(
    address asset,
    string calldata reason
) external override {
    // Validation and addition logic
    emit Vault_AssetAdded(asset, reason);
}
```

### 5. Error Handling

Comprehensive error system:

```solidity
error Vault_Unauthorized(address caller);
error Vault_AssetNotSupported(address asset);
error Vault_InvalidAmount();
error Vault_EmergencyModeActive(uint256 timestamp);
error Vault_SlippageExceeded(uint256 expected, uint256 actual, uint256 maxSlippage);
```

### 6. Events

```solidity
event VaultPrimaryAssetOperation(
    address indexed user,
    uint256 amount,
    bool isDeposit
);

event VaultSecondaryAssetOperation(
    address indexed asset,
    address indexed user,
    uint256 amount,
    bool isDeposit
);
```

### 7. Security Features

<figure><img src="../../.gitbook/assets/Security Features (1).png" alt=""><figcaption></figcaption></figure>

Key Security Features:

* Role-based access control
* Pausable operations
* Emergency mode
* Slippage protection
* Amount validation
* Asset verification

### 8. Integration Flow

<figure><img src="../../.gitbook/assets/Integration Flow.png" alt=""><figcaption></figcaption></figure>

Integration Points:

* Router interface
* Registry validation
* Asset transfers
* Event emission



This documentation reflects the current implementation focusing on:

* USYC vault specifics
* Secondary asset support
* Emergency controls
* Security features
* Integration patterns



The system provides a secure and flexible framework for managing USYC and secondary assets while maintaining protocol security and efficiency.
