# Faulty ERC20 Smart Contract

This repository is built using [Hardhat](https://hardhat.org/) and contains a version of a production ERC20 smart contract with intentional faults and vulnerabilities for auditing purposes.

---

## Table of Contents

- [Overview](#overview)
- [Smart Contracts](#smart-contracts)
  - [ERC20F](#erc20f)
  - [Allowlist](#allowlist)
  - [Denylist](#denylist)
  - [VestingVault](#vestingvault)
  - [UUPS Proxy](#uups-proxy)
  - [Trusted Forwarder](#trusted-forwarder)
  - [Fungible LayerZero Adapter](#fungible-layerzero-adapter)
- [Gasless Variants](#gasless-variants)
- [Gasless Upgrades](#gasless-upgrades)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
  - [Compile](#compile)
  - [Verify](#verify)

---

## Overview

The repository includes upgradeable templates for issuing and managing fungible, non-fungible, and semi-fungible tokens. These contracts are designed for:

- Tokenizing assets
- Managing access controls
- Reducing gas costs

Each contract uses the [UUPS proxy pattern](https://eips.ethereum.org/EIPS/eip-1822) for upgrades, maintaining state and functionality while enabling improvements over time.

---

## Smart Contracts

### [ERC20F](./contracts/ERC20F.sol)

An upgradeable ERC-20 token template for:

- Serving as a unit of account
- Issuing stablecoins or CBDCs
- Supporting tokenized fundraising
- Recovering funds from blacklisted accounts

### [AllowList](./contracts/library/AccessRegistry/AllowList.sol)

A utility contract for managing access control via an allowlist of approved addresses. Supports:

- Integration with ERC-20F contract
- Shared usage across multiple token contracts
- Upgradeability via the UUPS proxy pattern

### [DenyList](./contracts/library/AccessRegistry/DenyList.sol)

A utility contract for managing access control via a denylist of restricted addresses. Supports:

- Integration with ERC-20F
- Shared usage across multiple token contracts
- Upgradeability via the UUPS proxy pattern

### [VestingVault](./contracts/vaults/VestingVault.sol)

A non-upgradeable contract for managing token vesting schedules with:

- Multi-period vesting schedules with linear vesting and cliff options
- Global vesting mode for synchronized schedule starts across all beneficiaries
- Granular claim/release operations at beneficiary, schedule, or period level
- Schedule cancellation with pro-rated vesting up to cancellation time
- Role-based access control with VESTING_ADMIN and FORFEITURE_ADMIN roles

### [UUPS Proxy](./contracts/library/Proxy/Proxy.sol)

Provides upgradeable functionality for all smart contracts using the UUPS proxy pattern, ensuring flexibility and forward compatibility.

### [Trusted Forwarder](./contracts/gasless-contracts/TrustedForwarder.sol)

Enables seamless meta-transactions, supporting off-chain signing and gasless interactions with token contracts.

### [Fungible LayerZero Adapter](./contracts/bridge-adapter/FungibleLayerZeroAdapter.sol)

An adapter for integrating ERC20 tokens with LayerZero, enabling cross-chain fungible token transfers.

---

## Getting Started

### Prerequisites

1. Install [Node.js](https://nodejs.org/).

### Setup

Clone the repository and install dependencies:

```bash
git clone https://github.com/phelipebf/ERC20Faulty.git
cd ERC20Faulty
npm install --force
```

### Compile

```bash
npx hardhat compile
```

### Verify

Verify, dont trust. Always make sure your deployed bytecode matches the bytecode in the [artifacts](./artifacts/) directory