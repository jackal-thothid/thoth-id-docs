---
description: >-
  Human-readable names for the Hathor Network. Register one in the web app, or
  read them from your own application with the SDK.
icon: house
cover: .gitbook/assets/docs-cover.jpg
coverY: 0
---

# thoth.id Docs

{% hint style="warning" %}
**Project status: testnet**

thoth.id is under active development and currently runs on the **Hathor testnet**. Names you register, fees you pay and NFTs you receive there are testnet assets.

The SDK is provided for **testing and integration**, against a local development environment or the testnet contract. The contract API lives at `domains.thoth.id`; at mainnet launch it will be served from two endpoints, `mainnet.domains.thoth.id` (the default) and `testnet.domains.thoth.id`.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><strong>Use the Web App</strong></td><td>Connect your wallet, search for a name, register it, and manage its profile, records and ownership.</td><td><a href="web-app.md">web-app.md</a></td><td><a href=".gitbook/assets/card-web-app.jpg">card-web-app.jpg</a></td></tr><tr><td><strong>Build with the SDK</strong></td><td>Resolve names, check availability and read profile data from your own TypeScript application.</td><td><a href="sdk-reference.md">sdk-reference.md</a></td><td><a href=".gitbook/assets/card-sdk.jpg">card-sdk.jpg</a></td></tr></tbody></table>

## About this Documentation

This documentation covers thoth.id from two angles:

* [**Web App**](https://docs.thoth.id/web-app): the user guide. How to connect your wallet, search for a name, register it, and manage your profile, records and ownership. Start here if you want to _use_ thoth.id.
* [**SDK Reference**](https://docs.thoth.id/sdk-reference): the developer guide. How to read thoth.id data from your own application. Start here if you want to _build on_ thoth.id.

The SDK documentation will guide you through the process of integrating the thoth.id SDK into your applications. Whether you're building a new decentralized application (dApp) or integrating with an existing one, this SDK provides all the tools you need to interact with the thoth.id naming system on the Hathor Network.

You can find the source code for this SDK on [GitHub](https://github.com/jackal-thothid/thoth-id-sdk).

## What is thoth.id?

thoth.id is a decentralized naming service built on the Hathor Network. It allows you to map human-readable names (e.g., `username.htr`) to wallet addresses, effectively creating a digital identity on the blockchain. This simplifies the process of sending and receiving cryptocurrencies and interacting with dApps, as you no longer need to use long and complex wallet addresses.

With thoth.id, you can:

* **Create a unique digital identity:** Register a human-readable name that represents you on the Hathor Network.
* **Simplify transactions:** Send and receive funds using your thoth.id instead of a long wallet address.
* **Build a reputation:** Your thoth.id name can be used across multiple dApps, allowing you to build a consistent reputation within the ecosystem.

## What is the Hathor Network?

The Hathor Network is a scalable and easy-to-use blockchain platform designed for real-world use cases. It features a unique hybrid architecture that combines a Directed Acyclic Graph (DAG) of transactions with a blockchain of blocks. This design allows Hathor to be highly scalable and to process a large number of transactions per second with no fees.

Key features of the Hathor Network include:

* **Scalability:** A novel architecture that can handle a high volume of transactions.
* **Ease of Use:** Simplified token creation and nano contract deployment.
* **Security:** A secure and reliable network for decentralized applications.

## The Purpose of this SDK

The thoth.id SDK is a TypeScript library that simplifies interaction with the thoth.id nano contracts. It provides a set of easy-to-use methods that allow you to:

* Resolve thoth.id names to wallet addresses.
* Check if a thoth.id is available.
* And more!

By using this SDK, you can easily integrate thoth.id functionalities into your applications without having to worry about the low-level details of interacting with the nano contracts.
