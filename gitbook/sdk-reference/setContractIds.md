---
description: Seeds the instance with a contract map you collected earlier.
icon: code
---

# setContractIds

## Description

Sets the `domain suffix -> contract ID` map directly, so the instance skips discovery entirely. Domain suffixes are stored in lower case.

It does the same as passing `contractIds` to the [constructor](constructor.md), for when the map becomes available after the SDK was created.

## Parameters

* `contractIds` (Record\<string, string>): A map of domain suffixes to contract IDs, such as the one returned by [`exportContractIds()`](exportContractIds.md).

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();

const cached = localStorage.getItem("thoth-contract-ids");
if (cached) {
  sdk.setContractIds(JSON.parse(cached));
}
```
