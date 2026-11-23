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
| [`network`](constructor.md) option, [`setNetwork()`](setNetwork.md) | Mainnet support. Testnet stays the default. *(v3.2)* |
| [`blueprintIds`](constructor.md) option, [`setBlueprintIds()`](setBlueprintIds.md) | Discovery across every ThothNamer version. *(v3.2)* |
| [`getBlockedDomains()`](getBlockedDomains.md) | Domains whose registry was upgraded to an untrusted blueprint are blocked instead of resolved. *(v3.2)* |
| Mainnet by default | `new ThothIdSDK()` uses mainnet; pass `network: "testnet"` for testnet. *(v3.3)* |

`setNodeUrl()` now also clears the cached map, because a different node may be on a different network.

## Upgrading to v3.2

v3.2 adds mainnet and changes nothing for testnet code: in v3.2, `new ThothIdSDK()` still uses the public testnet node. (v3.3 makes mainnet the default; see below.) Two things are worth checking:

* **Saved maps.** If your app will use more than one network, key the saved map by network, for example `thoth-contract-ids:mainnet`. A testnet map passed to a mainnet instance resolves against the wrong contracts.
* **Blocked domains.** A domain whose first registry now runs a blueprint outside the trusted list throws instead of resolving. See [`getBlockedDomains()`](getBlockedDomains.md). This only affects registries upgraded to code that is not a ThothNamer release.

`blueprintId` and `setBlueprintId()` keep working, as shorthand for a single-entry `blueprintIds`.

## Upgrading to v3.3

{% hint style="warning" %}
**The default network is now mainnet.** In v3.3, `new ThothIdSDK()` connects to the public mainnet node instead of testnet. Nothing throws: code that relied on the default to reach testnet silently reads mainnet instead.
{% endhint %}

If your app uses testnet, pass the network explicitly everywhere you create the SDK:

```typescript
// v3.2: testnet was the default
const sdk = new ThothIdSDK();

// v3.3
const sdk = new ThothIdSDK({ network: "testnet" });
```

Check these too:

* **Saved maps.** A testnet map passed through `contractIds` without `network: "testnet"` is used against the mainnet node. Add the option wherever you seed a saved map.
* **Private nodes.** `nodeUrl` only changes the node, not the network. A private testnet node needs `network: "testnet"` as well, or the SDK looks for the mainnet blueprints on it.
* **Constants.** `DEFAULT_NODE_URL` and `DEFAULT_BLUEPRINT_ID` keep their testnet values and are deprecated. Use `TESTNET_NODE_URL` and `TESTNET_BLUEPRINT_IDS`, or `NETWORKS[DEFAULT_NETWORK]` for the current default.
