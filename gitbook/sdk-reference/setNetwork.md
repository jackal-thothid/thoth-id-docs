---
description: Switches the instance to another Hathor network's node and ThothNamer blueprints.
icon: code
---

# setNetwork

## Description

Points an existing instance at another network, as if it had been created with that `network` option: it sets the node URL and the trusted ThothNamer blueprints to that network's defaults.

Each network has its own registries, so it also clears the cached contract map and any [blocked domains](getBlockedDomains.md). The SDK collects the new network's map on the next call.

To start on a network instead of switching later, pass `network` to the [constructor](constructor.md).

{% hint style="info" %}
`setNetwork()` replaces any custom `nodeUrl` or `blueprintIds` with the network's defaults. To keep a private node, call [`setNodeUrl()`](setNodeUrl.md) after it.
{% endhint %}

## Parameters

* `network` (`"testnet" | "mainnet"`): The network to switch to.

| Network   | Node                           | ThothNamer blueprints                                                                                                                  |
| --------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `mainnet` (default) | `node1.mainnet.hathor.network` | v1.0 `000000420ca7b70e522da7765c8c11ecc89a9e8a79d70eee49d5bdff4db03e92`, v1.1 `00000020324712abca4e3de7f25c05825808b9a3dd9aeb5b7cfe89a892203183` |
| `testnet`           | `node1.testnet.hathor.network` | `000000009108a3ab3c24297df5e33679177fb8a051c133bcad467a8a23bf0dd3`                                                                     |

It throws `Unknown network "<name>"` for any other value.

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK(); // mainnet

// Drops the mainnet map; the testnet one is collected on the next call
sdk.setNetwork("testnet");

const address = await sdk.resolveName("jackal.htr"); // "WjcD1MGLi1TS8pH1JRcYzd9bJ1YPejVRtH"
```

*Added in v3.2.*
