---
description: Lists the domains the SDK refuses to resolve because their registry runs an untrusted blueprint.
icon: code
---

# getBlockedDomains

## Description

Anyone can create a registry from a ThothNamer blueprint, and whoever creates one can later upgrade it to **any** code. Being *created* from a ThothNamer blueprint is therefore not enough to trust a registry.

During discovery, the SDK checks the blueprint that the **first** registry of each domain runs now:

* If it is one of the trusted blueprints (`blueprintIds`), the domain resolves to that registry as usual.
* If it is not, the domain is **blocked**. Calls for names under it throw an error instead of resolving, and the domain is **not** handed to the next registry that claimed it: the first registry still owns the domain.

`getBlockedDomains()` returns the blocked domains, with the registry and the blueprint that caused each block. It only reads what the last discovery found. It does not start a collection, so call [`loadContractIds()`](loadContractIds.md) first.

The SDK only checks the first registry of each domain, so this costs one extra request per domain, not per contract.

{% hint style="warning" %}
A map you saved and passed back with `contractIds` or [`setContractIds()`](setContractIds.md) skips discovery, and with it this check. Call [`refreshContractIds()`](refreshContractIds.md) now and then so a registry upgraded to an untrusted blueprint is caught.
{% endhint %}

### When a domain is blocked by mistake

A registry upgraded to a **new ThothNamer release** that your version of the SDK does not know yet is also blocked. Update the SDK, or add the new blueprint yourself with the `blueprintIds` option or [`setBlueprintIds()`](setBlueprintIds.md).

## Parameters

None.

## Returns

* `Record<string, BlockedDomain>`: A copy of the blocked domains, keyed by lower-case domain suffix. Empty when nothing is blocked.

| Property      | Type     | Description                                |
| ------------- | -------- | ------------------------------------------ |
| `contractId`  | `string` | The domain's first registry.               |
| `blueprintId` | `string` | The blueprint that registry runs now.      |

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ network: "mainnet" });
// Required here: getBlockedDomains() only reads what discovery found
await sdk.loadContractIds();

console.log(sdk.getBlockedDomains()); // {} when every domain is trusted

// For a blocked domain:
// { xyz: { contractId: "0000…", blueprintId: "<blueprint it runs now>" } }
```

Resolving a name under a blocked domain throws:

```
Refusing to resolve "alice.xyz": the ".xyz" domain is registered by contract 0000…,
which now runs blueprint 0000… — not a trusted ThothNamer version on mainnet (…).
If that blueprint is a new ThothNamer release, update the Sdk or add it to blueprintIds.
```

*Added in v3.2.*
