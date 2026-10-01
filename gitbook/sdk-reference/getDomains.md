---
description: Lists the domain suffixes the instance currently knows about.
icon: code
---

# getDomains

## Description

Returns the domain suffixes in the cached contract map. It does not start a collection, so it returns an empty array until the map has been collected or seeded.

## Parameters

None.

## Returns

* `string[]`: The known domain suffixes, e.g. `["htr", "tst"]`.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
// Required here: getDomains() only reads the map, it never collects it
await sdk.loadContractIds();

console.log(sdk.getDomains()); // ["htr", ...]
```
