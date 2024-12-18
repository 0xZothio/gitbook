---
description: Protocol's Central Registry and Price Coordinator
---

# Collateral Vault

## Core Purpose

#### The Collateral Vault serves as the backbone of the ZeUSD protocol, performing three critical functions:

1. #### Central registry for all sub vaults and their collateral configurations
2. #### Price coordinator for ZeUSD minting calculations
3. #### Ledger for all user deposit positions

### Role as Central Registry

* #### Master Configuration: Stores and manages all supported collateral types and their corresponding sub vaults
* #### Integration Management: Tracks different integration types (ZTLN-P and more) and their specific parameters
* #### Activity Control: Manages active/inactive states of different collateral types and sub vaults

### Price Coordination Role

The Collateral Vault implements a sophisticated dual-path pricing mechanism:

1. Primary Path (Oracle Pricing)
   * Queries oracle price from sub vault
   * Validates price freshness and reasonability
   * Applies necessary scaling and conversions
   * Used when oracle is available and healthy
2. Fallback Path (Stored Pricing)
   * Uses administratively set prices
   * Activated when:
     * Oracle is unavailable
     * Oracle returns invalid price
     * Oracle price is stale
     * Price validation fails

### Position Tracking

* Maintains comprehensive records of all user positions
* Tracks active and historical deposits
* Records minted ZeUSD amounts per position
* Manages position lifecycle (creation, updates, closure)



## Key Functionalities Explained

### 1. Sub Vault Registration System

The sub Vault registration process follows a strict validation and storage pattern:

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (20).png" alt=""><figcaption></figcaption></figure>

This ensures:

* No duplicate registrations for same collateral
* Proper configuration updates
* Clear audit trail through events

### 2. Mint Amount Calculation

The mint calculation process is a critical function that determines how much ZeUSD can be minted against collateral:

* For Primary Collateral:

$$
mintAmount = \frac{{collateralAmount \times collateralPrice \times LTV}}{{10^6}}
$$

* For Stable coins:

$$
mintAmount = \frac{{stableAmount \times \left( oraclePrice \, ? \, \frac{{oraclePrice}}{{100}} \, : \, STABLE\_PRICE \times 10^6 \right) \times LTV}}{{10^6}}
$$

Key Considerations:

* Price scaling for different decimal places
* LTV (Loan-to-Value) ratio application
* Overflow protection in calculations
* Proper decimal handling for different tokens

### 3. Deposit Recording System

The deposit recording system maintains the protocol's state:

1. Deposit Creation:
   * Assigns unique deposit ID
   * Records collateral details
   * Tracks minted ZeUSD
   * Links to specific sub vault
2. State Updates:
   * Handles position modifications
   * Manages active/inactive status
   * Updates minted amounts
3. Query Capabilities:
   * User position lookup
   * Active deposits filtering
   * Collateral type aggregation
   * Historical position tracking



### 4. Price Management

Price management involves multiple layers of validation and calculation:

* Oracle Price Resolution:

```
Step 1: Check if oracle exists for asset
Step 2: If exists, query oracle price
Step 3: Validate price (freshness, bounds)
Step 4: Scale price to protocol decimals
Step 5: Apply fallback if any step fails
```

* Price Validation Rules:
  * Non-zero check
  * Staleness check (if from oracle)
  * Bounds check against min/max
  * Decimal place verification
* Price Application:
  * Properly scaled for calculations
  * Correctly applied with LTV
  * Maintains precision throughout



## Security Architecture

### 1. Access Control Layers

Three-tiered access control system:

1. Admin Layer: Configuration and emergency functions
2. Router Layer: Operational functions
3. Public Layer: View functions

### 2. Value Validation

Comprehensive validation system:

* Input parameter checks
* State validity checks
* Balance and allowance verification
* Price sanity checks

### 3. State Protection

Multiple safeguards for state integrity:

* Reentrancy protection
* Proper state updates
* Event emission for tracking
* Failure recovery mechanisms



## Integration Patterns

#### 1. Router Integration

Router interaction flow:

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio (21) (1).png" alt=""><figcaption></figcaption></figure>

### 2. Sub Vault Integration

Each sub vault integration requires:

* Registration in Collateral Vault
* Price feed configuration
* LTV ratio setting
* Activity status management

### 3. Oracle Integration

Oracle integration patterns:

* Primary price source
* Fallback mechanisms
* Price validation rules
* Update frequency check
