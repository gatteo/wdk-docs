---
title: Lending Modules Overview
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

# Lending Modules Overview

The Wallet Development Kit (WDK) provides a set of modules that support connection with lending protocols on different blockchain networks. All modules share a common interface, ensuring consistent behavior across different blockchain implementations.

```mermaid
flowchart LR
    App["Your App"] --> WDK["WDK Core"] --> Lending["Lending Module"] --> Pool["Aave V3 Pool"]

    style App fill:#080201,stroke:#FF4E00,color:#fff
    style WDK fill:#2d1a0a,stroke:#FF4E00,color:#fff
    style Lending fill:#331a00,stroke:#FF4E00,color:#fff
    style Pool fill:#FF4E00,stroke:#cc3e00,color:#fff
```

## Lending & Borrowing Protocol Modules

DeFi lending functionality for different lending & borrowing protocols

| Module | Route | Status | Documentation |
|--------|-------|--------|---------------|
| [`@tetherto/wdk-protocol-lending-aave-evm`](https://github.com/tetherto/wdk-protocol-lending-aave-evm) | EVM | ✅ Ready | [Documentation](./lending-aave-evm/README.md) |


## Next Steps

To get started with WDK modules, follow these steps:

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
				<i class="fa-mobile-alt">:mobile-alt:</i>
			</td>
			<td>
				<strong>React Native Quickstart</strong>
			</td>
			<td>Build mobile wallets with React Native Expo</td>
			<td>
				<a href="../../start-building/react-native-quickstart.md">react-native-quickstart.md</a>
			</td>
		</tr>
        <tr>
			<td>
				<i class="fa-mobile-alt">:mobile-alt:</i>
			</td>
			<td>
				<strong>WDK Core Module</strong>
			</td>
			<td>Manage wallet and protocol modules</td>
			<td>
				<a href="../core-module/README.md">WDK Core</a>
			</td>
		</tr>
	</tbody>
</table>

***

### Need Help?

{% include "../../.gitbook/includes/support-cards.md" %}