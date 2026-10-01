---
description: Discards the cached contract map and collects it from the node again.
icon: code
---

# refreshContractIds

## Description

The contract map is collected once per instance. If a new domain was created on chain after that, or you seeded the instance with a saved map that is now out of date, call `refreshContractIds()` to collect the map again.

## Parameters

None.

## Returns

* `Promise<Record<string, string>>`: The freshly collected map of domain suffixes to contract IDs.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const CACHE_KEY = "thoth-contract-ids";
const sdk = new ThothIdSDK({ contractIds: JSON.parse(localStorage.getItem(CACHE_KEY) ?? "{}") });

// A new domain went live since the map was saved
const contractIds = await sdk.refreshContractIds();
localStorage.setItem(CACHE_KEY, JSON.stringify(contractIds));
```
