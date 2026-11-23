---
description: Sets the ThothNamer blueprint IDs that discovery searches and trusts.
icon: code
---

# setBlueprintIds

## Description

Sets the list of ThothNamer blueprint IDs, one per released version of the contract. The list is used twice during discovery:

* **To find registries.** The SDK lists the contracts created from each blueprint. A contract stays listed under the blueprint it was *created* from even after it is upgraded, so every version has to be in the list.
* **To trust them.** The first registry of each domain must run one of these blueprints *now*, or the domain is [blocked](getBlockedDomains.md).

Changing the list changes which domains exist and which are trusted, so it also clears the cached contract map and the blocked domains. The SDK collects them again on the next call.

You rarely need this method: the `network` option already sets the right list. Use it to trust a new ThothNamer release before the SDK ships with it, or to test against your own blueprint.

## Parameters

* `ids` (string\[]): The blueprint IDs. Duplicates are ignored. It throws if the list is empty.

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK, MAINNET_BLUEPRINT_IDS } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ network: "mainnet" });

// Trust a new ThothNamer release before the SDK ships with it
sdk.setBlueprintIds([...MAINNET_BLUEPRINT_IDS, "NEW_BLUEPRINT_ID"]);
```

*Added in v3.2.*
