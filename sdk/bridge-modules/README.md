---
title: Bridge Modules Overview
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: false
---

# Bridge Modules Overview

The Wallet Development Kit (WDK) provides a set of modules that support bridging between different blockchain networks. All modules share a common interface, ensuring consistent behavior across different blockchain implementations.

```mermaid
flowchart LR
    SRC["Source Chain\n(EVM)"] --> Bridge["Bridge Protocol\n(LayerZero)"] --> DST1["EVM Destination"]
    Bridge --> DST2["Non-EVM\n(Solana, TON, TRON)"]

    style SRC fill:#16213e,stroke:#0f3460,color:#fff
    style Bridge fill:#0f3460,stroke:#e94560,color:#fff
    style DST1 fill:#1a3a2a,stroke:#4ecca3,color:#fff
    style DST2 fill:#533483,stroke:#e94560,color:#fff
```

## Bridge Protocol Modules

Cross-chain bridge functionality for token transfers between blockchains:

| Module | Route | Status | Documentation |
|--------|-------|--------|---------------|
| [`@tetherto/wdk-protocol-bridge-usdt0-evm`](https://github.com/tetherto/wdk-protocol-bridge-usdt0-evm) | EVM → EVM + Non-EVM | ✅ Ready | [Documentation](./bridge-usdt0-evm/) |

## Next steps

To get started with WDK modules, follow these steps:

1. Get up and running quickly with our [Quick Start Guide](../../start-building/nodejs-bare-quickstart.md)
2. Choose the modules that best fit your needs from the tables above 
3. Check specific documentation for modules you wish to use

You can also:

- Learn about key concepts like [Account Abstraction](../../resources/concepts.md#account-abstraction) and other important definitions
- Use one of our ready-to-use examples to be production ready
