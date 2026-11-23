---
description: Sets the ThothNamer blueprint ID used to discover domain contracts.
icon: code
---

# setBlueprintId

## Description

This method is intended for **testing and development**, for example against a blueprint you deployed yourself.

It is shorthand for [`setBlueprintIds([id])`](setBlueprintIds.md): it **replaces** the whole list with this one blueprint. On mainnet that drops the other ThothNamer versions, so registries created from them are no longer found. To add a blueprint instead, use `setBlueprintIds()`.

The SDK finds every domain by listing the contracts created from the blueprint. Changing it changes which domains exist, so it also clears the cached contract map. The SDK collects it again on the next call.

## Parameters

* `id` (string): The blueprint ID.

## Returns

* `void`

## Example

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ nodeUrl: "http://localhost:8080/" });
sdk.setBlueprintId("YOUR_BLUEPRINT_ID");
```
