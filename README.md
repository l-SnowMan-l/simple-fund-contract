# FundMe Smart Contract

A lightweight Solidity-based smart contract that allows users to send ETH donations to the contract owner. Donations must meet a minimum USD-denominated threshold, determined via Chainlink price feeds. This ensures consistent donation values regardless of ETH price fluctuations. The contract also tracks contributors for potential future incentives.

## Table of Contents

- [Overview](#overview)
- [Usage](#usage)
  - [Deploying the Contract](#deploying-the-contract)
  - [Running Tests](#running-tests)
    - [Test Coverage](#test-coverage)
- [Network Deployment](#network-deployment)
  - [Scripts](#scripts)
    - [Withdrawing Funds](#withdrawing-funds)
  - [Gas Estimation](#gas-estimation)
- [Code Formatting](#code-formatting)
- [Additional Notes](#additional-notes)

## Overview

This project demonstrates a simple funding mechanism where ETH donations are only accepted if they exceed a predefined minimum value in USD. The project uses Chainlink's decentralized oracles to fetch real-time ETH/USD prices.

## Usage

### Deploying the Contract

Use the following command to deploy the smart contract locally:

```bash
forge script script/DeployFundMe.s.sol
```

### Running Tests

The project includes various levels of testing, with a focus on unit and forked tests.

```bash
forge test
```

You can also match specific tests using:

```bash
forge test --match-test testFunctionName
```

Or run tests against a forked network:

```bash
forge test --fork-url $SEPOLIA_RPC_URL
```

#### Test Coverage

To assess how thoroughly the code is tested:

```bash
forge coverage
```

## Network Deployment

To deploy to a live testnet like Sepolia, follow these steps:

1. Set the following environment variables:
   - `SEPOLIA_RPC_URL`: Your RPC endpoint (e.g., from Alchemy or Infura).
   - `PRIVATE_KEY`: A private key for deployment. **Use a test account only.**
   - Optionally: `ETHERSCAN_API_KEY` for contract verification.

2. Acquire test ETH from [Chainlink Faucets](https://faucets.chain.link/).

3. Deploy:

```bash
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
```

### Scripts

After deployment, you can interact with the contract via scripts.

Examples:

```bash
cast send <CONTRACT_ADDRESS> "fund()" --value 0.1ether --private-key <PRIVATE_KEY>
```

```bash
forge script script/Interactions.s.sol:FundFundMe --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast
forge script script/Interactions.s.sol:WithdrawFundMe --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast
```

#### Withdrawing Funds

To withdraw all funds from the contract:

```bash
cast send <CONTRACT_ADDRESS> "withdraw()" --private-key <PRIVATE_KEY>
```

## Gas Estimation

Estimate the gas cost of contract functions with:

```bash
forge snapshot
```

A `.gas-snapshot` file will be generated with detailed gas usage.

## Code Formatting

To format your Solidity code consistently:

```bash
forge fmt
```

## Additional Notes

The Chainlink contracts used in this project follow the standard release process via the official `@chainlink/contracts` package on npm. This ensures reliable integration with Chainlink price feeds.

---

Feel free to explore, modify, or build on this project to expand your smart contract development skills.