---
description: Sets the Hathor full-node URL.
icon: code
---

# setNodeUrl

## Description

A different node may be on a different network, so changing the node also clears the cached contract map. The SDK collects it again from the new node on the next call.

Use it to reach the **same network** through another node, such as a private one. It does not change the ThothNamer blueprints, so pointing a testnet instance at a mainnet node finds no domains. To change network, use [`setNetwork()`](setNetwork.md), then `setNodeUrl()` if you need a private node.

## Parameters

* `url` (string): The new Hathor full-node URL.

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

// Mainnet through a private node
const sdk = new ThothIdSDK({ network: "mainnet" });
sdk.setNodeUrl("https://my-mainnet-node.example.com/v1a/nano_contract/state");
```
