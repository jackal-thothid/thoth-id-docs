---
description: Sets the Hathor full-node URL.
icon: code
---

# setNodeUrl

## Description

A different node may be on a different network, so changing the node also clears the cached contract map. The SDK collects it again from the new node on the next call.

## Parameters

* `url` (string): The new Hathor full-node URL.

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
sdk.setNodeUrl("https://node1.mainnet.hathor.network/v1a/nano_contract/state");
```
