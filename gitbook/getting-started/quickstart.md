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

You do not have to configure a registry. The `loadContractIds()` line is optional: the code works the same without it. The next section explains what it does.

## How the SDK finds each domain

Every thoth.id domain, such as `.htr`, is a nano contract created from the ThothNamer blueprint. Each one registers its domain when it is created. The SDK uses this to build the `domain suffix -> contract ID` map straight from the Hathor node:

* The map is collected on the **first call** that needs it, then reused for every later call on the same instance.
* Concurrent calls share a single collection, so the node is not asked twice.
* There is no registry endpoint to configure and nothing to keep in sync with the chain.

If you don't collect the map yourself, the first call that needs it does it for you. Calling [`loadContractIds()`](../sdk-reference/loadContractIds.md) right after creating the SDK lets you choose when that happens:

* **Pay the cost up front.** Collecting the map takes several requests to the node, so do it at startup or behind a loading screen, and the first lookup a user makes is fast.
* **Fail early.** A wrong node URL or a node that is down shows up as an error at startup, not in the middle of a user action.
* **Read or save the map.** Methods that only read the cached map, such as `exportContractIds()`, return an empty result until it has been collected.

That is why the examples in these docs call it right after creating the SDK.

## Cache the map between runs

Collecting the map takes a few requests to the node. Collect it once, save it, and pass it back in on later runs to skip discovery completely:

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const CACHE_KEY = "thoth-contract-ids";

async function getSdk() {
  const cached = localStorage.getItem(CACHE_KEY);
  if (cached) {
    // Zero discovery requests
    return new ThothIdSDK({ contractIds: JSON.parse(cached) });
  }

  const sdk = new ThothIdSDK();
  // Required here: exportContractIds() only reads the map, it never collects it
  await sdk.loadContractIds();
  localStorage.setItem(CACHE_KEY, JSON.stringify(sdk.exportContractIds()));
  return sdk;
}
```

A map passed in this way is trusted as is. If a domain was created after you saved it, calls for that domain throw an error until you call [`refreshContractIds()`](../sdk-reference/refreshContractIds.md) and save the new map.

## Use a private node

Pass `headers` to authenticate against a node that needs it. They are sent with every request, discovery included. A header whose value is `undefined` is left out, so an unset environment variable sends nothing:

```typescript
const sdk = new ThothIdSDK({
  nodeUrl: "https://node.testnet.dozer.finance/v1a/nano_contract/state",
  headers: { "X-API-Key": process.env.NODE_API_KEY },
});
```

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
