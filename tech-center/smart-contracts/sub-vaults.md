# Sub Vaults

## Product Overview

Sub Vaults serve as specialized asset managers within the Zoth. They handle specific collateral types and their interactions with external protocols, acting as secure vaults for user deposits and managing protocol-specific integrations.

## Core Responsibilities

1. Asset Management
2. Protocol Integration
3. Price Feed Management
4. Emergency Controls

## Core Components

### 1. Asset Management System

The Asset Management System is responsible for securely tracking, storing, and managing all assets within the Sub Vault. It maintains a comprehensive registry of supported assets and their configurations, ensuring proper handling of both primary collateral and secondary assets.

#### 1.1 Asset Registry

Controls which assets can be used in the Sub Vault and maintains their configurations. It distinguishes between primary assets (like ZTLN-P) and secondary assets (like USDC), managing their specific requirements and limitations.

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (22) (1).png" alt=""><figcaption></figcaption></figure>

The registry maintains critical asset parameters through a structured configuration:

```solidity
struct AssetConfig {
   bool isSupported;        // Is asset supported
   bool isPrimary;         // Is primary asset
   address priceOracle;    // Chainlink oracle address
   uint256 minDeposit;     // Minimum deposit amount
   uint256 maxDeposit;     // Maximum deposit amount
   uint256 lastUpdate;     // Last config update
}
mapping(address => AssetConfig) public assetConfigs;
```

### 2. Protocol Integration Layer

This layer serves as the bridge between the Sub Vault and external protocols. It handles all interactions with these protocols, ensuring secure and proper asset transfers and investments.

#### 2.1 Deposit Flow

Manages the process of depositing assets into external protocols, handling price checks, validations, and protocol-specific interactions. This ensures all deposits are properly processed and tracked.

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (23).png" alt=""><figcaption></figcaption></figure>

### 3. Price Oracle Integration

The oracle integration system provides reliable price data for all supported assets, with fallback mechanisms to ensure continuous operation even when primary price feeds fail.

#### 3.1 Price Resolution Flow

Implements a robust price discovery system with multiple layers of validation and fallback options to ensure reliable price data is always available.

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (24) (1).png" alt=""><figcaption></figcaption></figure>

### 4. Emergency Control System

Provides critical safety mechanisms to protect user assets in case of system anomalies or external threats. This system includes time-delayed emergency actions and controlled asset withdrawal procedures.

#### 4.1 Emergency Mode Flow

Implements a time-delayed emergency system that allows for controlled shutdown and asset protection in crisis situations.

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (27).png" alt=""><figcaption></figcaption></figure>

### 5. Asset Support Management

Manages the lifecycle of supported assets within the Sub Vault, from addition to removal, ensuring proper configuration and validation at each step.

#### 5.1 Asset Addition Flow

Provides a secure way to add new assets to the SubVault while maintaining system integrity and proper configurations.

```solidity
function addAsset(
   address asset,address oracle,
   uint256 minDeposit,
   uint256 maxDeposit,
   string calldata reason
) external onlyRole(ADMIN_ROLE) {
   // Validate asset isn't primary
   if (asset == primaryAsset)
       revert CannotModifyPrimaryAsset();
    // Check for duplicates
   if (assetConfigs[asset].isSupported)
       revert AssetAlreadySupported(asset);
   // Set up new asset configuration
   assetConfigs[asset] = AssetConfig({
       isSupported: true,
       isPrimary: false,
       priceOracle: oracle,
       minDeposit: minDeposit,
       maxDeposit: maxDeposit,
       lastUpdate: block.timestamp
   });
   emit AssetAdded(asset, oracle, reason);
}
```

Each component works together to provide a secure, efficient, and flexible asset management system within the ZeUSD protocol.
