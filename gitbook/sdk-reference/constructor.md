---
description: Creates a new instance of the SDK.
icon: code
---

# constructor()

## Parameters

* `opts` (ThothSDKOptions): An optional object to configure the SDK instance.

### ThothSDKOptions Schema

The `opts` parameter is an object of type `ThothSDKOptions` with the following properties:

| Property       | Type                                  | Description                                                                                                                                                                                         | Default                                                              |
| -------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `network`      | `"testnet" \| "mainnet"`              | The Hathor network to use. It sets the default `nodeUrl` and `blueprintIds`; both can still be overridden. See [Networks](#networks). *(v3.2)*                                                    | `"testnet"`                                                          |
| `nodeUrl`      | `string`                              | URL of the Hathor full-node to connect to. Either the `/v1a/nano_contract/state` endpoint or the bare node root works.                                                                              | The network's public node                                            |
| `contractIds` | `Record<string, string>`              | A `domain suffix -> contract ID` map you collected earlier, for example with [`exportContractIds()`](exportContractIds.md). Passing it skips discovery entirely.                                  | —                                                                    |
| `contractId`  | `string \| null`                      | A specific contract ID to use for all calls, whatever the name's domain. Mainly for testing against a local or test contract.                                                                      | `null`                                                               |
| `blueprintIds` | `string[]`                            | IDs of the ThothNamer blueprints, one per contract version. Discovery lists the contracts created from each one, and the first registry of a domain must run one of them now or the domain is [blocked](getBlockedDomains.md). *(v3.2)* | The network's blueprints                                             |
| `blueprintId`  | `string`                              | Shorthand for `blueprintIds` with a single blueprint, kept for v3.0 and v3.1 code. Ignored when `blueprintIds` is set. Change it only to test against your own blueprint.                         | —                                                                    |
| `headers`     | `Record<string, string \| undefined>` | Headers sent with every request to the node, for example an API key for a private node. Entries whose value is `undefined` are left out. In a browser, the node must allow them through CORS. | —                                                                    |
| `retries`     | `number`                              | How many times a request is retried after a `429`, `502`, `503` or `504`, a timeout or a dropped connection, with exponential backoff (1s, 2s, 4s, …). `0` disables retries.                        | `3`                                                                  |
| `timeoutMs`   | `number`                              | The timeout in milliseconds for each request to the Hathor node.                                                                                                                                    | `15000`                                                              |

It throws if `network` is not `"testnet"` or `"mainnet"`, or if `blueprintIds` is empty.

### Networks

| Network             | Default node                   | Default blueprints                                                                                                                         |
| ------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `testnet` (default) | `node1.testnet.hathor.network` | `000000009108a3ab3c24297df5e33679177fb8a051c133bcad467a8a23bf0dd3`                                                                         |
| `mainnet`           | `node1.mainnet.hathor.network` | v1.0 `000000420ca7b70e522da7765c8c11ecc89a9e8a79d70eee49d5bdff4db03e92`, v1.1 `00000020324712abca4e3de7f25c05825808b9a3dd9aeb5b7cfe89a892203183` |

These defaults are exported as `NETWORKS`, `MAINNET_NODE_URL`, `MAINNET_BLUEPRINT_IDS`, `DEFAULT_NODE_URL` and `DEFAULT_BLUEPRINT_ID`. To switch an existing instance, use [`setNetwork()`](setNetwork.md).

## Returns

* `ThothIdSDK`: A new instance of the thoth.id SDK.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

// Default settings: the public Hathor testnet node
const sdk = new ThothIdSDK();

// Mainnet: the public mainnet node and every mainnet ThothNamer blueprint
const mainnetSdk = new ThothIdSDK({ network: "mainnet" });

// Or a private node, with a previously saved contract map
const customSdk = new ThothIdSDK({
  nodeUrl: "https://node.testnet.dozer.finance/v1a/nano_contract/state",
  headers: { "X-API-Key": process.env.NODE_API_KEY },
  contractIds: JSON.parse(localStorage.getItem("thoth-contract-ids:testnet") ?? "{}"),
  retries: 5,
  timeoutMs: 10000,
});
```
