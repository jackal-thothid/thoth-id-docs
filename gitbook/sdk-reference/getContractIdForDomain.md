---
description: Returns the cached contract ID of a domain suffix.
icon: code
---

# getContractIdForDomain

## Description

Looks up a domain suffix in the cached contract map. The lookup is case-insensitive and does not start a collection.

## Parameters

* `domainSuffix` (string): The domain suffix, without the dot (e.g., `htr`).

## Returns

* `string | undefined`: The contract ID, or `undefined` if the domain is not in the cached map.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
// Required here: getContractIdForDomain() only reads the map, it never collects it
await sdk.loadContractIds();

const htrContractId = sdk.getContractIdForDomain("htr");
```
