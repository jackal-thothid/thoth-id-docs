---
description: Register a name end to end, in five steps and one signature.
icon: rocket
---

# Register Your First Name

Five steps, one signature, about two minutes. This page is the happy path — each step links to the full detail if you want it.

**Before you start** you need a [Hathor wallet](connect-wallet.md#what-you-need) with WalletConnect support and enough **HTR** to cover the first year.

## 1 · Connect your wallet

Click **Connect Wallet** in the top-right corner.

On desktop, scan the QR code with your Hathor wallet and approve the session. On a phone, the button opens the Hathor Wallet app directly.

![The WalletConnect dialog](../.gitbook/assets/connect-wallet-modal.jpg)

Approving the session lets thoth.id _ask_ for signatures — it never lets it spend anything on its own. Every transaction still comes back to your wallet for you to approve.

→ [Connect Your Wallet](connect-wallet.md)

## 2 · Find a name that's free

Type the name you want and press **Enter**. You can leave the `.htr` off.

![A search result showing an available name](../.gitbook/assets/search-available.jpg)

**Available** means it's yours to take — click the row to continue. **Registered** means someone got there first. **Not supported** means the name breaks the [naming rules](naming-rules-and-fees.md#what-makes-a-valid-name); the usual causes are being under 3 characters, using capitals or accents, or doubling up a hyphen.

→ [Search for a Name](search.md)

## 3 · Choose your term

Pick how many years you want, from **1 to 10**. The fee per year depends on how long the name is — shorter names cost more — and the **Total** and your **Balance** are shown side by side so you can see whether you can cover it.

![The registration page](../.gitbook/assets/register-page.jpg)

You can add an avatar here too, but it's optional and easy to do later.

→ [Register a Domain](register.md)

## 4 · Sign the transaction

Click **Register Domain** and approve the transaction in your wallet.

The name isn't yours until that transaction confirms on-chain, which usually takes a few seconds. Watch it under the notification bell — you'll see it go from _pending_ to _success_.

→ [Transactions & Notifications](notifications.md)

## 5 · You're done

Your new name appears on your dashboard, tagged **PRIMARY** and **MANAGER** — your first name automatically becomes the one thoth.id shows for your address everywhere.

![The dashboard](../.gitbook/assets/dashboard.jpg)

→ [Your Dashboard](dashboard.md)

***

## Using your name

Your name resolves to a wallet address, so anyone can send you funds using `yourname.htr` instead of a long string of characters.

This works in **Hathor wallets** to begin with, and then in any other wallet or application that integrates the thoth.id platform. Support depends on the app you're using having built it in — where it hasn't, your plain address still works exactly as before.

Developers can resolve names in their own applications with the [SDK](https://docs.thoth.id/sdk-reference/name-methods/resolvename).

## Two things worth knowing

{% hint style="warning" %}
**Your wallet controls your names.**

There is no thoth.id account and no password reset. Whoever controls the address controls the names registered to it — so if you lose access to your wallet, you lose the names with it. Your wallet's seed phrase backup is the only way back in. Back it up, and never share it with anyone, including anyone claiming to be from thoth.id.
{% endhint %}

{% hint style="info" %}
**Names expire.**

You bought a term, not a permanent right. thoth.id warns you as the date approaches, and there's a 30-day grace period after it passes during which the name is still yours to renew — but once that ends, anyone can register it. See [Renew a Domain](https://docs.thoth.id/web-app/renew).
{% endhint %}

## Where to next

* Add an avatar and a description → [Profile Tab](profile.md)
* Publish links, socials or anything else on-chain → [Records Tab](records.md)
* Understand owner vs manager, and how to sell a name → [Ownership & Roles](ownership.md)
* Something went wrong → [Troubleshooting](troubleshooting.md)
