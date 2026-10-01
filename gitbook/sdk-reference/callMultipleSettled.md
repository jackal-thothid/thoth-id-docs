---
description: >-
  Makes multiple view calls in a single request and returns each call's own
  outcome.
icon: code
---

# callMultipleSettled

## Description

Sends the same single request as [`callMultiple`](callMultiple.md), but a failing call does not fail the whole batch. Each call gets its own result, in the order given, like `Promise.allSettled`. One invalid address only fails its own entry.

The promise is rejected only if the request itself fails, after retries.

## Parameters

* `calls` (Array<{ method: string; params?: any\[] }>): The calls to make. Each object has a `method` with the contract method name and an optional `params` array.
* `domainSuffix` (string): The domain suffix (e.g., `htr`).

## Returns

* `Promise<CallResult[]>`: One result per call, either `{ ok: true, value }` or `{ ok: false, error }`, where `error` is the message from the contract.

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();

const results = await sdk.callMultipleSettled(
  addresses.map((address) => ({ method: "get_manager_primary_name", params: [address] })),
  "htr"
);

for (const result of results) {
  if (result.ok) console.log(result.value);
  else console.warn(result.error); // e.g. "InvalidAddress('Invalid checksum of address')"
}
```
