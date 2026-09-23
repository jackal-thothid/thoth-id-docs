---
description: >-
  Updates the contractApiUrl of the SDK, so you can switch between contract API
  endpoints.
icon: code
---

# setContractApiUrl

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
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK();
sdk.setContractApiUrl("https://my-custom-api.com/contract-ids");
```
