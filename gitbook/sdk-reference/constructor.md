---
description: Creates a new instance of the SDK.
icon: code
---

# constructor()

## Parameters

* `opts` (ThothSDKOptions): An optional object to configure the SDK instance.

### ThothSDKOptions Schema

The `opts` parameter is an object of type `ThothSDKOptions` with the following properties:

| Property      | Type                                  | Description                                                                                                                                                                                         | Default                                                              |
| ------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `nodeUrl`     | `string`                              | URL of the Hathor full-node to connect to. Either the `/v1a/nano_contract/state` endpoint or the bare node root works.                                                                              | `"https://node1.testnet.hathor.network/v1a/nano_contract/state"`     |
| `contractIds` | `Record<string, string>`              | A `domain suffix -> contract ID` map you collected earlier, for example with [`exportContractIds()`](exportContractIds.md). Passing it skips discovery entirely.                                  | —                                                                    |
| `contractId`  | `string \| null`                      | A specific contract ID to use for all calls, whatever the name's domain. Mainly for testing against a local or test contract.                                                                      | `null`                                                               |
| `blueprintId` | `string`                              | ID of the ThothNamer blueprint. Every contract created from it is a domain registry, which is how the SDK discovers the map. Change it only to test against your own blueprint.                    | `"000000009108a3ab3c24297df5e33679177fb8a051c133bcad467a8a23bf0dd3"` |
| `headers`     | `Record<string, string \| undefined>` | Headers sent with every request to the node, for example an API key for a private node. Entries whose value is `undefined` are left out. In a browser, the node must allow them through CORS. | —                                                                    |
| `retries`     | `number`                              | How many times a request is retried after a `429`, `502`, `503` or `504`, a timeout or a dropped connection, with exponential backoff (1s, 2s, 4s, …). `0` disables retries.                        | `3`                                                                  |
| `timeoutMs`   | `number`                              | The timeout in milliseconds for each request to the Hathor node.                                                                                                                                    | `15000`                                                              |

## Returns

* `ThothIdSDK`: A new instance of the thoth.id SDK.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

// Default settings: the public Hathor testnet node
const sdk = new ThothIdSDK();

// Or a private node, with a previously saved contract map
const customSdk = new ThothIdSDK({
  nodeUrl: "https://node.testnet.dozer.finance/v1a/nano_contract/state",
  headers: { "X-API-Key": process.env.NODE_API_KEY },
  contractIds: JSON.parse(localStorage.getItem("thoth-contract-ids") ?? "{}"),
  retries: 5,
  timeoutMs: 10000,
});
```
