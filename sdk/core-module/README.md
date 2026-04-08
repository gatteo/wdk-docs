---
title: WDK Core
description: Overview of the @tetherto/wdk-core module
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

# @tetherto/wdk-core

 This package serves as the main entry point and **orchestrator for all WDK wallet and protocol modules**, allowing you to register and manage different blockchain wallets through a single, unified interface.

```mermaid
graph LR
    subgraph Core["@tetherto/wdk (Core)"]
        RW["registerWallet()"]
        RP["registerProtocol()"]
        GA["getAccount()"]
        EP["executeProtocol()"]
    end

    RW --> BTC["wdk-wallet-btc"]
    RW --> EVM["wdk-wallet-evm"]
    RW --> EVM43["wdk-wallet-evm\n-erc4337"]
    RW --> SOL["wdk-wallet-solana"]
    RW --> SPARK["wdk-wallet-spark"]
    RW --> TON["wdk-wallet-ton"]
    RW --> TRON["wdk-wallet-tron"]

    RP --> SWAP["swap-velora-evm"]
    RP --> BRIDGE["bridge-usdt0-evm"]
    RP --> LEND["lending-aave-evm"]
    RP --> FIAT["fiat-moonpay"]

    style Core fill:#0f3460,stroke:#e94560,color:#fff
    style BTC fill:#f7931a,stroke:#c16800,color:#fff
    style EVM fill:#627eea,stroke:#3c3c3d,color:#fff
    style EVM43 fill:#627eea,stroke:#3c3c3d,color:#fff
    style SOL fill:#9945ff,stroke:#6b2fd6,color:#fff
    style SPARK fill:#e94560,stroke:#c73550,color:#fff
    style TON fill:#0088cc,stroke:#006699,color:#fff
    style TRON fill:#ff0013,stroke:#cc0010,color:#fff
    style SWAP fill:#533483,stroke:#e94560,color:#fff
    style BRIDGE fill:#533483,stroke:#e94560,color:#fff
    style LEND fill:#533483,stroke:#e94560,color:#fff
    style FIAT fill:#533483,stroke:#e94560,color:#fff
```

## Next Steps

<table data-card-size="large" data-view="cards">
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th data-hidden data-card-target data-type="content-ref"></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
				<i class="fa-code">:code:</i>
			</td>
			<td>
				<strong>Node.js Quickstart</strong>
			</td>
			<td>Get started with WDK in a Node.js environment</td>
			<td>
				<a href="../../start-building/nodejs-bare-quickstart.md">nodejs-quickstart.md</a>
			</td>
		</tr>
        <tr>
			<td>
				<i class="fa-code">:code:</i>
			</td>
			<td>
				<strong>WDK Core Configuration</strong>
			</td>
			<td>Get started with WDK's configuration</td>
			<td>
				<a href="./configuration.md">WDK Core Configuration</a>
			</td>
		</tr>
        <tr>
			<td>
				<i class="fa-code">:code:</i>
			</td>
			<td>
				<strong>WDK Core API</strong>
			</td>
			<td>Get started with WDK's API</td>
			<td>
				<a href="./api-reference.md">WDK Core API</a>
			</td>
		</tr>
        <tr>
			<td>
				<i class="fa-code">:code:</i>
			</td>
			<td>
				<strong>WDK Core Usage</strong>
			</td>
			<td>Get started with WDK's usage</td>
			<td>
				<a href="./usage.md">WDK Core Usage</a>
			</td>
		</tr>
	</tbody>
</table>

***

### Need Help?

{% include "../../.gitbook/includes/support-cards.md" %}
