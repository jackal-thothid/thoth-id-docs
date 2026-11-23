---
description: >-
  Install the thoth.id SDK and make your first calls against the thoth.id nano
  contracts.
icon: play
---

# Getting Started

{% hint style="warning" %}
**Project status: testnet**

The SDK is provided for **testing and integration**. It uses the **testnet** contracts by default; pass `network: "mainnet"` to read the **mainnet** contracts, or point it at a **local development environment**. See the project status on the home page for the current endpoints.
{% endhint %}

These guides walk you through the thoth.id SDK step by step, with practical examples to help you get started quickly.

Install it from [npm](https://www.npmjs.com/package/thoth-id-sdk):

```bash
npm install thoth-id-sdk
```

The [Quickstart](getting-started/quickstart.md) also covers yarn, mainnet, caching and private nodes.

{% content-ref url="getting-started/quickstart.md" %}
[quickstart.md](getting-started/quickstart.md)
{% endcontent-ref %}

{% content-ref url="getting-started/resolve-a-name.md" %}
[resolve-a-name.md](getting-started/resolve-a-name.md)
{% endcontent-ref %}

{% content-ref url="getting-started/check-name-availability.md" %}
[check-name-availability.md](getting-started/check-name-availability.md)
{% endcontent-ref %}

{% content-ref url="getting-started/check-name-status.md" %}
[check-name-status.md](getting-started/check-name-status.md)
{% endcontent-ref %}
