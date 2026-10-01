---
description: >-
  Removed in v3. Updated the contractApiUrl of the SDK, so you could switch
  between contract API endpoints.
icon: code
---

# setContractApiUrl

{% hint style="danger" %}
**Removed in v3.** This method, and the `contractApiUrl` option it changed, no longer exist. Calling it on v3 throws `sdk.setContractApiUrl is not a function`.

In v2, the SDK downloaded its `domain suffix -> contract ID` map from a contract API (`https://domains.thoth.id/contract-ids` by default), and this method pointed it at a different one. In v3, the SDK builds the map itself from the Hathor node, so there is no API to point at. See [`loadContractIds`](loadContractIds.md) for how that works.

**What to use instead:**

* To use a map you already have, pass it to the [constructor](constructor.md) as `contractIds`, or call [`setContractIds()`](setContractIds.md).
* To test against a single contract, use [`setContractId()`](setContractId.md).
* To test against your own blueprint, use [`setBlueprintId()`](setBlueprintId.md).

See [Migrating from v2](migrating-from-v2.md) for every change.
{% endhint %}

The reference below applies to **v2 only**.

## Signature

```typescript
setContractApiUrl(url: string): void
```

## Parameters

### url

The new URL for the contract API.

* Type: `string`
* Required: `true`

## Returns

`void`

## Example

```typescript
// v2 only
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
sdk.setContractApiUrl("https://my-custom-api.com/contract-ids");
```
