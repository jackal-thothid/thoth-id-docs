---
description: Register a name end to end, in five steps and one signature.
icon: rocket
---

# Register Your First Name

Five steps, one signature, about two minutes. This page is the happy path; each step links to the full detail if you want it.

**Before you start** you need [Hathor Wallet](connect-wallet.md#what-you-need) with WalletConnect support and enough **HTR** to cover the first year.

## 1 · Find a name that's free

Type the name you want in the search box on the landing page, on the search page, or in the top bar. The result appears as you type. You can leave the `.htr` off.

![A search result showing an available name](../.gitbook/assets/search-available.jpg)

**Available** means it's yours to take: the row shows the price per year. **Registered** means someone got there first. **Not supported** means the name breaks the [naming rules](naming-rules-and-fees.md#what-makes-a-valid-name); the row says why and usually suggests a valid alternative.

Click **Register**.

→ [Search for a Name](search.md)

## 2 · Choose your term

Pick how many years you want, from **1 to 10**. The price per year depends on how long the name is (shorter names cost more), and the **Total** is shown at the bottom.

![The registration page](../.gitbook/assets/register-page.jpg)

You can add an avatar here too, but it's optional and easy to do later.

→ [Register a Name](register.md)

## 3 · Connect your wallet

If you haven't yet, the button reads **Connect wallet**. On desktop, scan the QR code with Hathor Wallet and approve the session. On a phone, the button opens Hathor Wallet directly.

![The WalletConnect dialog](../.gitbook/assets/connect-wallet-modal.jpg)

Connecting only shares your address. It never lets thoth.id spend anything on its own: every transaction comes back to your wallet for you to approve.

Once you're connected, your **Balance** appears next to the total, so you can see whether you can cover it.

→ [Connect Your Wallet](connect-wallet.md)

## 4 · Approve the transaction

Click **Register yourname.htr** and approve the transaction in Hathor Wallet.

The name isn't yours until that transaction confirms on-chain, which usually takes about 30 seconds. The page shows **Confirming** with a timer, then **yourname.htr is yours**. You can leave the page meanwhile; the bell in the top bar keeps tracking it.

→ [Transactions & Activity](notifications.md)

## 5 · You're done

Click **View yourname.htr** to open your name's public page. Your new name is also in **My names**, marked with a star: your first name automatically becomes your **primary name**, the one thoth.id shows instead of your address.

![My names](../.gitbook/assets/my-names.jpg)

→ [My Names](dashboard.md)

***

## Using your name

Your name resolves to your wallet address, so anyone can send you funds using `yourname.htr` instead of a long string of characters. Your name's page also has a QR code and a shareable link.

This works in **Hathor wallets** to begin with, and then in any other wallet or application that integrates thoth.id. Support depends on the app you're using having built it in; where it hasn't, your plain address still works exactly as before.

Developers can resolve names in their own applications with the [SDK](../sdk-reference/resolveName.md).

## Two things worth knowing

{% hint style="warning" %}
**Your wallet controls your names.**

There is no thoth.id account and no password reset. Whoever controls the address controls the names registered to it, so if you lose access to your wallet, you lose the names with it. Your wallet's seed phrase backup is the only way back in. Back it up, and never share it with anyone, including anyone claiming to be from thoth.id.
{% endhint %}

{% hint style="info" %}
**Names expire.**

You bought a term, not a permanent right. thoth.id warns you as the date approaches, and there's a 30-day renewal window after it passes during which the name can still be renewed. Once that ends, anyone can register it. See [Renew a Name](renew.md).
{% endhint %}

## Where to next

* Add an avatar and a bio → [Profile](profile.md)
* Publish links, socials or anything else on-chain → [Records](records.md)
* Understand owner vs manager, and how to sell a name → [Ownership](ownership.md)
* Something went wrong → [Troubleshooting](troubleshooting.md)
