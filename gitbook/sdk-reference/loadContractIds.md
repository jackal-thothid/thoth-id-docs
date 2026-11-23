---
description: >-
  Collects the map of domain suffixes (e.g., htr) and their nano contract IDs
  from the Hathor node.
icon: code
---

# loadContractIds

## Description

Every thoth.id domain is a nano contract created from a ThothNamer blueprint, and each one registers its domain when it is created. `loadContractIds()` lists those contracts on the Hathor node and builds the `domain suffix -> contract ID` map from them. The SDK needs this map to know which contract to ask about `example.htr`.

## How the map is built

* **Every ThothNamer version is searched.** A contract stays listed under the blueprint it was *created* from, even after it is upgraded. On mainnet, `.htr` was created from v1.0 and now runs v1.1, so the SDK lists the contracts of every blueprint in `blueprintIds`.
* **The first registry of a domain wins.** Anyone can create a registry for a domain that already exists. Across every version, the oldest one owns the domain and later ones are ignored.
* **The first registry must run a trusted blueprint.** Its creator can upgrade it to any code, so the SDK also checks the blueprint it runs now. If that blueprint is not in `blueprintIds`, the domain is [blocked](getBlockedDomains.md) instead of being handed to the next registry.
* **A contract that cannot be read fails the whole collection.** Skipping it could let the next registry for that domain take its place silently.

Names are not affected by upgrades: they live in the registry's state, which keeps its contract ID, so a name created on v1.0 still resolves after the upgrade to v1.1.

The map is collected once per instance:

* Later calls return the cached map without asking the node again, so calling it more than once costs nothing.
* Concurrent calls share a single collection.
* If the collection fails, nothing is cached, and the next call tries again.

To collect it again, use [`refreshContractIds()`](refreshContractIds.md).

## Why it is optional

Every method that needs a contract calls `loadContractIds()` for you if the map has not been collected yet. If you never call it, your first call, such as `resolveName()`, collects the map before doing its own work.

You don't need to call it when the instance already has what it needs:

* You passed a saved map with the `contractIds` option or [`setContractIds()`](setContractIds.md). It then returns that map without asking the node.
* You set a single contract with `contractId` or [`setContractId()`](setContractId.md). The map is not used at all.

## Why you may still want to call it

Collecting the map takes several requests to the node, sent one at a time because public nodes rate-limit to roughly one request per second: one per page of contracts for each blueprint, one per contract to read its domain, and one per domain to check its current blueprint. Calling `loadContractIds()` yourself lets you choose when that happens:

* **Pay the cost up front.** Call it at startup or behind a loading screen, so the first lookup a user makes is fast.
* **Fail early.** A wrong `nodeUrl`, a missing API key in `headers` or a node that is down shows up as an error at startup, not in the middle of a user action.
* **Read or save the map.** [`exportContractIds()`](exportContractIds.md), [`getDomains()`](getDomains.md) and [`getContractIdForDomain()`](getContractIdForDomain.md) only read the cached map and never collect it. Call `loadContractIds()` first, or they return an empty result.

That is why the examples in these docs call it right after creating the SDK. Each example works the same without that line.

## Parameters

None.

## Returns

* `Promise<Record<string, string>>`: The map of lower-case domain suffixes to contract IDs, e.g. `{ htr: "0000…" }`. Blocked domains are not in it; see [`getBlockedDomains()`](getBlockedDomains.md).

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ network: "mainnet" });

// Optional: collect the domain map now instead of on the first call
const contractIds = await sdk.loadContractIds();
console.log("Known domains:", Object.keys(contractIds)); // ["htr"]
console.log("Blocked:", sdk.getBlockedDomains());          // {}
```
