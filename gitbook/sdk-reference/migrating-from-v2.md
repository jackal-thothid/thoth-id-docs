---
description: What changed in thoth-id-sdk v3 and how to update your code.
icon: arrow-up
---

# Migrating from v2

In v3, the SDK finds each domain's contract straight from the Hathor node instead of from the `domains.thoth.id` contract API. Most apps only need to delete code.

## Upgrade

```bash
npm install thoth-id-sdk@^3
```

## Breaking changes

### `contractApiUrl` and `setContractApiUrl()` are removed

The contract map is now built from the nano contracts created from the ThothNamer blueprint, so there is no registry endpoint to configure. Remove the option and any call to [`setContractApiUrl()`](setContractApiUrl.md):

```typescript
// v2
const sdk = new ThothIdSDK({
  nodeUrl: "https://node1.testnet.hathor.network/v1a/nano_contract/state",
  contractApiUrl: "https://domains.thoth.id/contract-ids",
});

// v3
const sdk = new ThothIdSDK({
  nodeUrl: "https://node1.testnet.hathor.network/v1a/nano_contract/state",
});
```

If you ran your own contract API for testing, either pass the map directly with the `contractIds` option, or use `blueprintId` to point discovery at your own blueprint.

### `loadContractIds()` is optional and takes no URL

In v2 you had to call it before anything else. In v3, the first call that needs the map collects it for you, so your code works without it.

Keeping your `await sdk.loadContractIds()` calls is still a good idea: they collect the map at startup instead of during the first user action, and they surface node errors early. See [`loadContractIds`](loadContractIds.md) for when to call it.

Two things changed in the method itself: it no longer takes a `url` argument, and it now returns the map instead of `void`.

## New in v3

| Feature | What it does |
| --- | --- |
| [`contractIds`](constructor.md) option, [`exportContractIds()`](exportContractIds.md), [`setContractIds()`](setContractIds.md) | Save the collected map and reuse it on later runs to skip discovery. |
| [`refreshContractIds()`](refreshContractIds.md) | Collect the map again, for example after a new domain goes live. |
| [`getDomains()`](getDomains.md), [`getContractIdForDomain()`](getContractIdForDomain.md) | Inspect the cached map. |
| [`blueprintId`](constructor.md) option, [`setBlueprintId()`](setBlueprintId.md) | Discover domains from a different blueprint, for testing. |
| [`headers`](constructor.md) option | Authenticate against a private node. *(v3.1)* |
| [`retries`](constructor.md) option | Automatic retries with exponential backoff on rate limits and transient errors. *(v3.1)* |
| [`callMultipleSettled()`](callMultipleSettled.md) | Batch view calls without one failure sinking the rest. *(v3.1)* |

`setNodeUrl()` now also clears the cached map, because a different node may be on a different network.
