---
description: Install the SDK and resolve your first name.
icon: rocket
---

# Quickstart

## Installation

The SDK is published on npm as [`thoth-id-sdk`](https://www.npmjs.com/package/thoth-id-sdk).

{% tabs %}
{% tab title="npm" %}
```bash
npm install thoth-id-sdk
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn add thoth-id-sdk
```
{% endtab %}
{% endtabs %}

The package ships its own TypeScript types, so there is nothing extra to install. It runs in the browser, in Electron and in Node.js 18 or later, and it is released under the MIT license. The source code is on [GitHub](https://github.com/jackal-thothid/thoth-id-sdk).

## Resolve your first name

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();

// Optional: collect the domain map now instead of on the first call
await sdk.loadContractIds();

const walletAddr = await sdk.resolveName("example.htr");
```

You do not have to configure a registry. The `loadContractIds()` line is optional: the code works the same without it. The sections below explain what it does.

## Choose a network

The SDK uses the **mainnet** unless told otherwise: the public mainnet node and the mainnet ThothNamer contracts. Pass `network: "testnet"` to use testnet:

{% tabs %}
{% tab title="Mainnet" %}
```typescript
import { ThothIdSDK } from "thoth-id-sdk";

// Mainnet is the default, so no option is needed
const sdk = new ThothIdSDK();

await sdk.resolveName("jackal.htr");      // "H93A2s655jatS1zfdMF5pwf6E4s5FHnUmh"
await sdk.checkNameStatus("jackal.htr");  // "active"
await sdk.isNameAvailable("jackal.htr");  // false

// Registration fee, in the token's smallest unit (100000 = 1,000.00 HTR)
await sdk.calculateFee("abcde.htr");      // 100000
await sdk.calculateFee("abc.htr");        // 2000000: short names cost more

// Reverse lookup: the primary name of an address on .htr
await sdk.getManagerPrimaryName("H93A2s655jatS1zfdMF5pwf6E4s5FHnUmh", "htr"); // "vulture"
```
{% endtab %}

{% tab title="Testnet" %}
```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ network: "testnet" });

await sdk.resolveName("jackal.htr");      // "WjcD1MGLi1TS8pH1JRcYzd9bJ1YPejVRtH"
await sdk.calculateFee("abcde.htr");      // 1
```
{% endtab %}
{% endtabs %}

Each network has its own registries: a name registered on testnet does not exist on mainnet. Mainnet addresses start with `H`, testnet ones with `W`. To switch an existing instance, use [`setNetwork()`](../sdk-reference/setNetwork.md).

## How the SDK finds each domain

Every thoth.id domain, such as `.htr`, is a nano contract created from a ThothNamer blueprint. Each one registers its domain when it is created. The SDK uses this to build the `domain suffix -> contract ID` map straight from the Hathor node:

* The map is collected on the **first call** that needs it, then reused for every later call on the same instance.
* Concurrent calls share a single collection, so the node is not asked twice.
* There is no registry endpoint to configure and nothing to keep in sync with the chain.
* Every version of the ThothNamer contract is searched, and when several registries claim the same domain, **the first one created wins**.
* A domain whose first registry was upgraded to code that is not a ThothNamer release is **blocked** instead of resolved. See [`getBlockedDomains()`](../sdk-reference/getBlockedDomains.md).

If you don't collect the map yourself, the first call that needs it does it for you. Calling [`loadContractIds()`](../sdk-reference/loadContractIds.md) right after creating the SDK lets you choose when that happens:

* **Pay the cost up front.** Collecting the map takes several requests to the node, so do it at startup or behind a loading screen, and the first lookup a user makes is fast.
* **Fail early.** A wrong node URL or a node that is down shows up as an error at startup, not in the middle of a user action.
* **Read or save the map.** Methods that only read the cached map, such as `exportContractIds()`, return an empty result until it has been collected.

That is why the examples in these docs call it right after creating the SDK.

## Cache the map between runs

Collecting the map takes a few requests to the node. Collect it once, save it, and pass it back in on later runs to skip discovery completely. A map belongs to one network, so key the cache by network:

```typescript
import { ThothIdSDK, Network } from "thoth-id-sdk";

async function getSdk(network: Network = "mainnet") {
  const cacheKey = `thoth-contract-ids:${network}`;
  const cached = localStorage.getItem(cacheKey);
  if (cached) {
    // Zero discovery requests
    return new ThothIdSDK({ network, contractIds: JSON.parse(cached) });
  }

  const sdk = new ThothIdSDK({ network });
  // Required here: exportContractIds() only reads the map, it never collects it
  await sdk.loadContractIds();
  localStorage.setItem(cacheKey, JSON.stringify(sdk.exportContractIds()));
  return sdk;
}

const sdk = await getSdk("mainnet");
```

A map passed in this way is trusted as is, without the blocked-domain check. If a domain was created after you saved it, calls for that domain throw an error until you call [`refreshContractIds()`](../sdk-reference/refreshContractIds.md) and save the new map. Refreshing now and then also catches a registry upgraded to an untrusted blueprint.

## Use a private node

Pass `headers` to authenticate against a node that needs it. They are sent with every request, discovery included. A header whose value is `undefined` is left out, so an unset environment variable sends nothing:

```typescript
const sdk = new ThothIdSDK({
  network: "testnet",
  nodeUrl: "https://node.testnet.dozer.finance/v1a/nano_contract/state",
  headers: { "X-API-Key": process.env.NODE_API_KEY },
});
```

`nodeUrl` only changes the node, not the network. A private **testnet** node needs `network: "testnet"` too, or the SDK looks for the mainnet ThothNamer blueprints on it. A private mainnet node only needs `nodeUrl`.

{% hint style="info" %}
In a browser, custom headers trigger a CORS preflight, so the node must allow them.
{% endhint %}

## Retries

Public nodes rate-limit to roughly one request per second. Every request, discovery and view calls alike, is retried on `429`, `502`, `503`, `504`, timeouts and dropped connections, with exponential backoff (1s, 2s, 4s, …). Set how many times with `retries` (default `3`, `0` to disable):

```typescript
const sdk = new ThothIdSDK({ retries: 5 });
```

## Use a specific contract (for testing)

For testing or development, you can point the SDK at one specific contract, such as one you deployed locally. Every call then goes to that contract, whatever the name's domain, and no discovery happens:

```typescript
const sdk = new ThothIdSDK({
  nodeUrl: "http://localhost:8080/",
  contractId: "YOUR_CONTRACT_ID", // Replace with your contract ID
});
```

See the [constructor](../sdk-reference/constructor.md) for every option. The next pages show common tasks.
