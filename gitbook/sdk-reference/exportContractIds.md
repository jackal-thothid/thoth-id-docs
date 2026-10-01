---
description: Returns a copy of the cached contract map, safe to save and pass back in later.
icon: code
---

# exportContractIds

## Description

Returns a snapshot of the `domain suffix -> contract ID` map the instance has collected. Save it and pass it back through the `contractIds` option or [`setContractIds()`](setContractIds.md) on a later run to skip discovery.

It does not start a collection. If the map has not been collected yet, it returns an empty object, so call [`loadContractIds()`](loadContractIds.md) first.

## Parameters

None.

## Returns

* `Record<string, string>`: A copy of the map of domain suffixes to contract IDs.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
// Required here: exportContractIds() only reads the map, it never collects it
await sdk.loadContractIds();

localStorage.setItem("thoth-contract-ids", JSON.stringify(sdk.exportContractIds()));
```
