---
title: Concepts & Definitions
description: Key concepts and definitions used throughout the Wallet Development Kit
---

## Account Abstraction

Account Abstraction is a blockchain technology that separates the concept of a user account from the mechanism of transaction validation and fee payment. In traditional blockchain systems, users must pay transaction fees in the native token of the blockchain (like ETH on Ethereum). Account Abstraction allows users to pay fees in other tokens or have fees sponsored by third parties, enabling gasless transactions and enhanced user experiences.

### WDK Implementation

WDK provides Account Abstraction support through specialized wallet modules:

- `@tetherto/wdk-wallet-evm-erc4337` - EVM chains with ERC-4337 standard
- `@tetherto/wdk-wallet-ton-gasless` - TON blockchain with gasless transactions
- `@tetherto/wdk-wallet-tron-gasfree` - TRON blockchain with gas-free transactions

These modules allow developers to implement gasless transaction flows where users can pay fees in tokens like USD₮ or XAU₮ instead of native blockchain tokens.

## ERC-4337

ERC-4337 is an Ethereum standard that enables Account Abstraction without requiring changes to the Ethereum protocol itself. It introduces a new transaction type called "UserOperation" that allows smart contract wallets to handle transaction validation and fee payment logic through components like EntryPoint contracts, Bundlers, and Paymasters.

```mermaid
flowchart LR
    User["👤 User"] --> UO["UserOperation"]
    UO --> Bundler["Bundler"]
    Bundler --> EP["EntryPoint\n(on-chain)"]
    EP --> Paymaster["Paymaster\n(sponsors gas)"]
    EP --> Wallet["Smart Contract\nWallet"]
    Wallet --> Chain["Blockchain"]

    style User fill:#080201,stroke:#FF4E00,color:#fff
    style UO fill:#1a0e06,stroke:#FF4E00,color:#fff
    style Bundler fill:#1a0e06,stroke:#FF4E00,color:#fff
    style EP fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style Paymaster fill:#331a00,stroke:#FF4E00,color:#fff
    style Wallet fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style Chain fill:#080201,stroke:#FF4E00,color:#fff
```

## Gasless Transactions

Gasless transactions allow users to perform blockchain operations without holding native tokens for gas fees. Instead, transaction fees are paid by third-party services or in alternative tokens, enabling new user onboarding, cross-chain operations, and corporate applications where companies can sponsor employee transactions.

## Paymaster Services

Paymaster services are third-party providers that sponsor transaction fees on behalf of users. They accept payment in various tokens and handle the conversion and payment of gas fees to the blockchain network, providing fee estimation, gas optimization, and high transaction success rates.

## Safe Accounts

Safe Accounts are smart contract wallets built on the Safe protocol that provide enhanced security features and multi-signature capabilities. In the context of ERC-4337, Safe Accounts can be used as the underlying wallet implementation, combining the security benefits of multi-signature with the flexibility of Account Abstraction for enterprise, family, and institutional use cases.

## BIP Standards

BIP (Bitcoin Improvement Proposal) standards define common practices for Bitcoin and other blockchain wallets. WDK modules implement several key BIP standards for consistent wallet behavior across different blockchains.

### BIP-39 (Mnemonic Seed Phrases)

BIP-39 defines a standard for generating mnemonic seed phrases from random entropy. These phrases are human-readable and can be used to recover wallet private keys. WDK modules use BIP-39 for secure seed phrase generation and validation.

### BIP-44 (Multi-Account Hierarchy)

BIP-44 defines a hierarchical deterministic wallet structure that allows creating multiple accounts from a single seed phrase. The derivation path format is `m/purpose'/coin_type'/account'/change/address_index`, where each module uses its specific coin type (e.g., 60 for Ethereum, 998 for Spark).

```mermaid
graph TD
    Seed["🔑 Seed Phrase\n(BIP-39 mnemonic)"] --> M["m"]
    M --> P44["44' (purpose)"]
    M --> P84["84' (purpose)"]

    P44 --> BTC["0' (Bitcoin)"]
    P44 --> ETH["60' (Ethereum)"]
    P44 --> SOL["501' (Solana)"]
    P44 --> SPARK["998' (Spark)"]

    P84 --> BTC84["0' (Bitcoin\nSegWit)"]

    BTC --> BTCA0["Account 0"]
    ETH --> ETHA0["Account 0"]
    SOL --> SOLA0["Account 0"]
    SPARK --> SPKA0["Account 0"]
    BTC84 --> BTC84A0["Account 0"]

    BTCA0 --> BTCAddr["bc1q..."]
    ETHA0 --> ETHAddr["0x..."]
    SOLA0 --> SOLAddr["So1..."]
    SPKA0 --> SPKAddr["sp1..."]
    BTC84A0 --> BTC84Addr["bc1q..."]

    style Seed fill:#080201,stroke:#FF4E00,color:#fff
    style M fill:#1a0e06,stroke:#FF4E00,color:#fff
    style P44 fill:#1a0e06,stroke:#FF4E00,color:#fff
    style P84 fill:#1a0e06,stroke:#FF4E00,color:#fff
    style BTC fill:#FF4E00,stroke:#cc3e00,color:#fff
    style ETH fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style SOL fill:#1a0e06,stroke:#FF4E00,color:#fff
    style SPARK fill:#FF4E00,stroke:#cc3e00,color:#fff
    style BTC84 fill:#FF4E00,stroke:#cc3e00,color:#fff
```

### BIP-84 (Native SegWit)

BIP-84 defines the derivation path for native SegWit addresses (P2WPKH) in Bitcoin wallets. This standard provides better security and lower transaction fees compared to legacy Bitcoin addresses.

## Lightning Network

The Lightning Network is a second-layer payment protocol built on top of Bitcoin that enables instant, low-fee transactions. It works by creating payment channels between parties, allowing them to transact without broadcasting every transaction to the Bitcoin blockchain.

### Key Features

- **Instant Payments**: Transactions settle immediately within payment channels
- **Low Fees**: Minimal fees compared to on-chain Bitcoin transactions
- **Scalability**: Can handle millions of transactions per second
- **BOLT11 Invoices**: Standard format for Lightning payment requests

### WDK Integration

The Spark wallet module integrates Lightning Network functionality, allowing users to create and pay Lightning invoices directly from their Spark wallets.

## Layer 2 Solutions

Layer 2 solutions are protocols built on top of existing blockchains to improve scalability, reduce fees, and enhance transaction speed. They process transactions off the main blockchain and periodically settle to the base layer.

### Types of Layer 2

```mermaid
graph TD
    L2["Layer 2 Solutions"] --> Rollups["Rollups"]
    L2 --> SC["State Channels"]
    L2 --> Side["Sidechains"]

    Rollups --> Opt["Optimistic\n(Arbitrum, Optimism)"]
    Rollups --> ZK["ZK Rollups"]

    SC --> LN["Lightning Network"]

    subgraph WDK["WDK Module Support"]
        direction LR
        WDK_EVM["wdk-wallet-evm\n(EVM Rollups)"]
        WDK_SPARK["wdk-wallet-spark\n(Lightning / Spark)"]
    end

    Opt -.-> WDK_EVM
    LN -.-> WDK_SPARK

    style L2 fill:#080201,stroke:#FF4E00,color:#fff
    style Rollups fill:#1a0e06,stroke:#FF4E00,color:#fff
    style SC fill:#1a0e06,stroke:#FF4E00,color:#fff
    style Side fill:#1a0e06,stroke:#FF4E00,color:#fff
    style Opt fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style ZK fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style LN fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style WDK fill:#FF4E00,stroke:#cc3e00,color:#fff
    style WDK_EVM fill:#FF4E00,stroke:#cc3e00,color:#fff
    style WDK_SPARK fill:#FF4E00,stroke:#cc3e00,color:#fff
```

- **Rollups**: Bundle multiple transactions and submit them as a single transaction to the main chain
- **State Channels**: Allow parties to transact off-chain and settle periodically
- **Sidechains**: Independent blockchains that connect to the main chain via bridges

### WDK Support

WDK modules support various Layer 2 solutions:
- **Spark**: Bitcoin Layer 2 with Lightning Network integration
- **EVM Rollups**: Support for Arbitrum, Optimism, and other EVM-compatible rollups

## EVM (Ethereum Virtual Machine)

The Ethereum Virtual Machine is a runtime environment that executes smart contracts on Ethereum and other EVM-compatible blockchains. It provides a standardized way to run decentralized applications across different networks.

### EVM-Compatible Chains

Many blockchains are EVM-compatible, meaning they can run the same smart contracts and use the same tools as Ethereum:
- **Polygon**: Layer 2 scaling solution for Ethereum
- **BSC**: Binance Smart Chain
- **Arbitrum**: Optimistic rollup for Ethereum
- **Optimism**: Layer 2 scaling solution

### WDK EVM Support

The `@tetherto/wdk-wallet-evm` module works with any EVM-compatible blockchain, providing unified access to multiple networks through a single API.

## UTXO (Unspent Transaction Output)

UTXO is a fundamental concept in Bitcoin and other UTXO-based blockchains. Each transaction consumes previous UTXOs and creates new ones, forming a chain of ownership.

### How UTXOs Work

```mermaid
flowchart LR
    subgraph Inputs["Inputs (consumed)"]
        UTXO1["UTXO 0.5 BTC"]
        UTXO2["UTXO 0.3 BTC"]
    end

    subgraph TX["Transaction"]
        Process["Σ inputs = 0.8 BTC\n- fee: 0.0001 BTC"]
    end

    subgraph Outputs["Outputs (created)"]
        Out1["UTXO 0.6 BTC\n→ Recipient"]
        Out2["UTXO 0.1999 BTC\n→ Change (sender)"]
    end

    UTXO1 --> Process
    UTXO2 --> Process
    Process --> Out1
    Process --> Out2

    style Inputs fill:#080201,stroke:#FF4E00,color:#fff
    style TX fill:#1a0e06,stroke:#FF4E00,color:#fff
    style Outputs fill:#FF4E00,stroke:#cc3e00,color:#fff
    style UTXO1 fill:#331a00,stroke:#FF4E00,color:#fff
    style UTXO2 fill:#331a00,stroke:#FF4E00,color:#fff
    style Process fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style Out1 fill:#FF4E00,stroke:#cc3e00,color:#fff
    style Out2 fill:#FF4E00,stroke:#cc3e00,color:#fff
```

1. **Inputs**: References to previous UTXOs that are being spent
2. **Outputs**: New UTXOs created by the transaction
3. **Change**: Remaining value returned to the sender as a new UTXO

### WDK UTXO Management

The Bitcoin wallet module automatically handles UTXO selection and change address management, ensuring optimal transaction construction and fee calculation.

## Seed Phrases and Private Keys

Seed phrases and private keys are the foundation of wallet security in blockchain systems.

### Seed Phrases (BIP-39)

- **12-24 words**: Human-readable representation of wallet entropy
- **Deterministic**: Same seed phrase always generates the same keys
- **Recovery**: Can recover entire wallet from seed phrase
- **Security**: Must be kept secure and never shared

### Private Keys

- **256-bit numbers**: Cryptographic keys that control wallet funds
- **Derived from seed**: Generated deterministically from seed phrase
- **Signing**: Used to sign transactions and prove ownership
- **Memory safety**: WDK modules handle private keys securely with automatic cleanup

## Network Types

Blockchain networks come in different types for different use cases.

```mermaid
graph TD
    subgraph Mainnet["🟢 Mainnet (Production)"]
        M1["Real value transacted"]
        M2["Ethereum, Bitcoin, Spark"]
    end

    subgraph Testnet["🟡 Testnet (Development)"]
        T1["Test tokens, no real value"]
        T2["Sepolia, Bitcoin Testnet, Spark Testnet"]
    end

    subgraph Regtest["🔵 Regtest (Local)"]
        R1["Fully local, instant blocks"]
        R2["Private Ethereum, Bitcoin Regtest"]
    end

    Mainnet ~~~ Testnet
    Testnet ~~~ Regtest

    style Mainnet fill:#FF4E00,stroke:#cc3e00,color:#fff
    style Testnet fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style Regtest fill:#1a0e06,stroke:#FF4E00,color:#fff
```

### Mainnet

Production networks where real value is transacted:
- **Ethereum Mainnet**: Production Ethereum network
- **Bitcoin Mainnet**: Production Bitcoin network
- **Spark Mainnet**: Production Spark network

### Testnet

Development networks for testing without real value:
- **Goerli/Sepolia**: Ethereum test networks
- **Bitcoin Testnet**: Bitcoin test network
- **Spark Testnet**: Spark test network

### Regtest

Local networks for development and testing:
- **Local Ethereum**: Private Ethereum network
- **Bitcoin Regtest**: Local Bitcoin network
- **Spark Regtest**: Local Spark network

### Testnet Funds & Faucets

To test transactions without spending real assets, developers use "Testnets"—networks that mimic the main blockchain but use tokens with no monetary value. You can obtain these tokens for free from different publicly available "Faucets". Links to common "Faucets" are below.

{% hint style="warning" %}
The below faucets are for testnets. The USD₮ tokens and other tokens available at the links below are not real and do not entitle the holder to anything. In particular, they cannot be redeemed with Tether International, S.A. de C.V. ("Tether International") and are not Tether Tokens as described in [Tether International's Terms of Service](https://tether.to/en/legal). The USD₮ tokens available at the links below on various testnets are intended for testing WDK on the applicable testnet. The links below are links to third-party websites and are Third-Party Information as described in Tether Operations, S.A. de [C.V.'s Website Terms](https://tether.io/terms/).
{% endhint %}

#### Common Faucets
*   **USD₮ Test Tokens (Sepolia)**: [Pimlico Faucet](https://dashboard.pimlico.io/test-erc20-faucet)
*   **USD₮ Test Tokens (Sepolia)**: [Candide Faucet](https://dashboard.candide.dev/faucet)
*   **Ethereum (Sepolia)**: [Google Cloud Web3 Faucet](https://cloud.google.com/application/web3/faucet/ethereum/sepolia)
*   **Aave Test Tokens (Sepolia)**: [Aave Faucet](https://app.aave.com/faucet/) — get test USD₮, DAI and other tokens for DeFi testing
*   **TON Testnet**: [Testgiver Bot](https://t.me/testgiver_ton_bot)
*   **Bitcoin Testnet**: [CoinFaucet](https://coinfaucet.eu/en/btc-testnet/)
