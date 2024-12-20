# ZeUSD Token

## Overview

ZeUSD is an upgradeable ERC-20 token that serves as the core stable asset of the ZeUSD protocol. It incorporates advanced features like blacklisting, role-based access control, and cross-chain compatibility through Layer Zero.

## Key Features

### 1. Token Configuration

* Name: ZeUSD
* Symbol: ZeUSD
* Decimals: 6
* Implementation: ERC-20 Upgradeable

### 2. Access Control System

* DEFAULT\_ADMIN\_ROLE (Owner): Controls administrative functions
* ADMIN\_ROLE (Admin): Manages operational features.&#x20;
* [Router](zeusd-router.md): Exclusive minting privileges

### 3. Security Features

#### Blacklist System

* Prevents malicious actors from using the token
* Administrators can add/remove addresses
* Affects transfers and approvals

```solidity
mapping(address => bool) private _blacklist;

function setBlacklistStatus(address account, bool status) external onlyRole(ADMIN_ROLE) {
    _blacklist[account] = status;
    emit Blacklisted(account, status);
}
```

#### Router Control

* Only authorized router can mint/burn tokens
* Prevents unauthorized token creation
* Ensures protocol integrity

```solidity
modifier onlyRouter() {
    require(msg.sender == router, "Only router can call");
    _;
}
```

## Core Functions

### Minting

```solidity
function mint(address to, uint256 amount) external onlyRouter {
    _mint(to, amount);
}
```

* Called exclusively by router
* Creates new tokens based on collateral
* Emits Transfer event

### Burning

```solidity
function burn(uint256 amount) external onlyRouter {
    _burn(msg.sender, amount);
}

function burnFrom(address account, uint256 amount) external onlyRouter {
    _spendAllowance(account, msg.sender, amount);
    _burn(account, amount);
}
```

* Destroys tokens when collateral is redeemed
* Requires approval for burnFrom
* Updates total supply
