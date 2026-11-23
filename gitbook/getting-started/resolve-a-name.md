---
description: Resolve a thoth.id name to its wallet address with the SDK.
icon: magnifying-glass
---

# Resolve a Name

This example shows how to resolve a thoth.id name to its associated wallet address.

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

async function resolveName() {
  try {
    const sdk = new ThothIdSDK();
    // Optional: collect the domain map now instead of on the first call
    await sdk.loadContractIds();

    const walletAddress = await sdk.resolveName("example.htr");
    console.log(`The address for example.htr is:`, walletAddress);

  } catch (error) {
    console.error("Error resolving name:", error);
  }
}

resolveName();
```

On mainnet, pass the `network` option. Everything else is the same:

```typescript
import { ThothIdSDK } from "thoth-id-sdk";

const sdk = new ThothIdSDK({ network: "mainnet" });

const walletAddr = await sdk.resolveName("jackal.htr");
console.log(walletAddr); // "H93A2s655jatS1zfdMF5pwf6E4s5FHnUmh"
```

Or in a simple way:

```typescript

import { ThothIdSDK } from "thoth-id-sdk";

async function main() {
    const sdk = new ThothIdSDK();
    // Optional: collect the domain map now instead of on the first call
    await sdk.loadContractIds();

    const walletAddr = await sdk.resolveName("example.htr");
}

main();
```
