# AssetFract Protocol

**Fractional Asset Tokenization on Stacks Layer 2**  
_Enabling secure, compliant, and decentralized ownership of real-world assets._

## Overview

**AssetFract** is a smart contract protocol for **fractionalizing high-value real-world assets** (RWAs) into **semi-fungible tokens (SFTs)** on the **Stacks Layer 2** blockchain. It introduces a robust and fully compliant framework for asset registration, ownership transfer, governance, and revenue distribution — all while integrating identity verification and oracle-based valuation.

Whether you're a fund manager, real estate owner, or digital platform, AssetFract allows you to tokenize and manage assets in a trust-minimized, Bitcoin-secured environment.

## Key Features

- **Asset Tokenization**: Register real-world assets and mint SFTs representing fractional ownership.
- **On-Chain Governance**: Token holders can initiate and vote on proposals specific to each asset.
- **Automated Dividends**: Distribute asset-generated revenue proportionally to holders.
- **KYC/AML Compliance**: Integrates KYC levels, approval checks, and expiry for regulated onboarding.
- **Oracle Integration**: Asset price feeds provided by authorized oracles with expiry validation.
- **Bitcoin Compatibility**: Built for Stacks L2 with Bitcoin finality.

## Contract Summary

| Feature | Description |
|--------|-------------|
| Asset Registry | Register new assets with metadata and appraised value |
| Fractional Tokens | SFTs per asset (default: 100,000 units) |
| Dividend Claims | Holders can claim dividends based on revenue and holding proportion |
| Proposals & Voting | Governance per asset, with threshold and expiration logic |
| KYC Compliance | Address-level verification, level, and expiry enforcement |
| Oracle Feeds | Track real-world value via off-chain price feeds signed by trusted oracles |

## Core Data Structures

### `assets`
Tracks metadata and valuation of each registered asset.

```clojure
{ asset-id: uint } => {
  owner: principal,
  metadata-uri: string,
  asset-value: uint,
  is-locked: bool,
  ...
}
```

### `token-balances`
Tracks fractional ownership of each asset by principal.

```clojure
{ owner: principal, asset-id: uint } => { balance: uint }
```

### `kyc-status`
Stores KYC level and expiry per user.

```clojure
{ address: principal } => { is-approved: bool, level: uint, expiry: uint }
```

### `proposals`, `votes`
Manages governance per asset via token-weighted voting.

## Public Functions

| Function | Description |
|---------|-------------|
| `register-asset(uri, value)` | Registers a new tokenized asset |
| `claim-dividends(asset-id)` | Claims proportional dividends |
| `create-proposal(asset-id, title, duration, min-votes)` | Propose an action on an asset |
| `vote(proposal-id, vote-for, amount)` | Vote on a proposal |

## Compliance & Security

- Enforces **KYC validation** before asset interaction
- Prevents double voting and expired votes
- Limits asset values and durations to avoid abuse
- Handles Oracle price expiry and authorization
- Designed to comply with **regulatory frameworks** for asset-backed tokens

## Future Extensions

- Role-based access control (e.g., auditors, admins)
- On-chain asset liquidation logic
- Modular governance execution (e.g., fund allocation)
- Real-time streaming dividends
- Cross-chain bridges to Ethereum or Lightning Network

## Local Development

AssetFract is written in [Clarity](https://docs.stacks.co/guides-and-tutorials/clarity-crash-course), a decidable, predictable language for Stacks smart contracts.

### Dev Stack

- Language: Clarity (Stacks L2)
- Tooling: Clarinet (contract dev/test suite)
- Requirements: Stacks CLI, Clarinet, Clarity runtime

### Compile

```bash
clarinet check
```

## Authors & Maintainers

**AssetFract Protocol** was designed for tokenizing real-world assets in a compliant, decentralized way on Bitcoin L2. Maintained by a collective of builders in the Stacks ecosystem.