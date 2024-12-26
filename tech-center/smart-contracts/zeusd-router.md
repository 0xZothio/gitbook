# ZeUSD Router

## Product Overview

The **ZeUSD Router** is the primary gateway for users to interact with the ZeUSD protocol. It acts as a central hub that enables users to:

* Create ZeUSD by depositing collateral or stable coins
* Bridge ZeUSD across different blockchain networks
* Burn ZeUSD to retrieve their collateral
* Manage their positions and interactions with the protocol

## Core Components

### 1. Access Control System

The access control system ensures secure and compliant protocol usage through multiple layers:

#### 1.1 Administrative Control

* DEFAULT\_ADMIN\_ROLE (Owner)
  * Highest level of access in the protocol
  * Can grant/revoke other roles
  * Controls critical protocol parameters
  * Manages emergency operations
* ADMIN\_ROLE (Admin)
  * Manages day-to-day operations
  * Controls whitelist
  * Updates protocol configurations
  * Monitor system health

#### 1.2 User Access Management

* Whitelist System
  * Ensures KYC/KYB compliance
  * Controls who can mint ZeUSD
  * Maintains regulatory standards
  * Tracks user permissions
* Blacklist Integration
  * Blocks malicious actors
  * Enforces compliance requirements
  * Protects protocol security
  * Maintains system integrity

### 2. Protocol Integration Components

#### 2.1 [Collateral Vault](collateral-vault.md) Integration

The Collateral Vault manages all collateral positions in the protocol:

* Tracks user deposits and positions
* Calculates collateral ratios
* Manages liquidation thresholds
* Provides price feed integration

#### 2.2 [ZeUSD Token](zeusd-token.md) Management

Direct interface with the ZeUSD token contract for:

* Minting new tokens based on collateral
* Burning tokens during redemption
* Managing token supply
* Tracking user balances

#### 2.3 LayerZero Cross-Chain Operations

Enables seamless cross-chain functionality through:

* Secure message passing between chains
* Token bridging capabilities
* Cross-chain position management
* Unified liquidity across networks

#### 2.4 Sub Vault Interactions

Manages specialized vaults for different asset types:

* RWA (Real World Asset) vaults
* Stable coin vaults
* Protocol-specific integrations
* Custom asset handlers



## Key Features

### 1. CDP Minting Engine

Users can create ZeUSD through two primary methods:

#### 1.1 Direct Collateral Deposits

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (12) (1).png" alt=""><figcaption></figcaption></figure>

In this process:

1. Users deposit supported collateral (e.g., ZTLN)
2. System validates collateral and user eligibility
3. Calculates appropriate ZeUSD amount based on:
   * Collateral value
   * Current oracle prices
   * LTV ratios
4. Mints ZeUSD to user's wallet
5. Records position in Collateral Vault

#### 1.2 Stablecoin Deposits

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (13).png" alt=""><figcaption></figcaption></figure>

In this process:

1. Deposit supported stablecoins (e.g., USDC)
2. System routes to appropriate SubVault
3. SubVault invests in underlying protocol
4. Mints equivalent ZeUSD based on deposit

#### 1.3 Cross-Chain Bridging

When users want to move ZeUSD across chains:

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (14) (1).png" alt=""><figcaption></figcaption></figure>

This enables:

* Seamless cross-chain movement
* Unified liquidity across networks
* Chain-agnostic usage
* Optimized gas efficiency

### 2. Burning Mechanism

Users can redeem their ZeUSD for underlying collateral through a secure process:

#### 2.1 Collateral Redemption

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (16).png" alt=""><figcaption></figcaption></figure>

The system:

1. Verifies user's ZeUSD balance
2. Checks position exists and is active
3. Burns specified ZeUSD amount
4. Returns equivalent collateral
5. Updates position records

#### 2.2 Position Management

* Tracks all user positions
* Manages partial redemptions
* Updates collateral ratios
* Maintains position history

### 3. Security Framework

#### 3.1 Access Protection

Multiple layers of security ensure safe operations:

```solidity
   modifier whitelistedOnly() {
       if (!_whitelisted[msg.sender]) revert NotWhitelisted(msg.sender);
       _;
   }
   modifier notBlacklisted() {
       if (zeusdToken.isBlacklisted(msg.sender)) revert Blacklisted(msg.sender);
       _;
   }
   modifier whenNotPaused() {
       if (depositsPaused) revert DepositsArePaused();
       _;
   }
```

#### 3.2 Operation Safeguards

* Reentrancy Guards: Prevent multiple calls
* Pause Mechanism: Emergency stops
* Role Validation: Access control
* Amount Validation: Input checking



## Implementation Details

### 1. Mint With Collateral Flow

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (17).png" alt=""><figcaption></figcaption></figure>

In this flow:

1. User Initiation: User calls mintWithCollateral with their chosen collateral asset (e.g., ZTLN) and amount
2. Access Verification: Router checks if user is whitelisted and not blacklisted
3. SubVault Location: Gets the appropriate SubVault address for the collateral type
4. Asset Validation: Verifies the collateral is supported by the SubVault
5. Collateral Transfer: Transfers user's collateral to the designated SubVault
6. Position Recording: Records the deposit details in CollateralVault for tracking
7. Amount Calculation: Calculates how much ZeUSD to mint based on collateral value and LTV
8. Token Minting: Mints the calculated amount of ZeUSD to user's wallet

### 2. Mint With Stable Flow

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (18).png" alt=""><figcaption></figcaption></figure>

This process involves:

1. User Request: User initiates stable token deposit (e.g., USDC)
2. Access Checks: Verifies user's permission to use the protocol
3. Vault Verification: Locates correct Sub Vault for the stable token
4. Asset Validation: Confirms stable token is supported
5. Token Transfer: Moves stable tokens to Sub Vault
6. Protocol Integration: Sub Vault deposits stables into underlying protocol
7. Record Keeping: Records the stable deposit in Collateral Vault
8. ZeUSD Issuance: Mints equivalent ZeUSD based on stable deposit

### 3. Burn Flow

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (19).png" alt=""><figcaption></figcaption></figure>

The burn process includes:

1. Burn Request: User initiates burn of ZeUSD to reclaim their collateral
2. Permission Check: Verifies user's authorization
3. Vault Location: Identifies correct Sub Vault storing user's collateral
4. Asset Verification: Confirms asset type matches original deposit
5. Position Update: Marks the deposit as inactive in Collateral Vault
6. Token Burning: Burns the specified amount of ZeUSD
7. Collateral Release: Withdraws collateral from Sub Vault
8. Return Assets: Transfers collateral back to user's wallet

## Oracle Integration

The Router relies on price oracles through the Collateral Vault for calculating mint amounts:

1. Price Discovery
   * Collateral prices from Chainlink oracles
   * Price validation and fallback mechanisms
   * Staleness checks and safety bounds
2. Mint Amount Calculation

$$
mintAmount = \frac{{collateralAmount \times price \times LTV}}{{SCALE \times PRICE\_DECIMALS}}
$$

3. Oracle Safety Measures
   * Price deviation checks
   * Minimum/maximum bounds
   * Heartbeat verification
   * Multiple oracle support for critical assets



## Error Handling

1. Custom Errors

```solidity
error NotWhitelisted(address account);
error Blacklisted(address account);
error InvalidAddress(address address);
error ZeroAmount();
error DepositsArePaused();
error InsufficientBalance(string token);
```

2. State Validation

* Pre-condition checks
* Balance verification
* Allowance validation
* Asset support verification

## Upgradeability

The Router implements UUPS upgradeability pattern:

* State variable organization
* Implementation slot management
* Proper initialization sequence
* Storage gap for future upgrades
