---
description: >-
  The user guide. Search for a name, register it, and manage everything attached
  to it.
icon: browser
---

# Web App

{% hint style="warning" %}
**Project status: testnet**

The thoth.id web app currently runs against the **Hathor testnet**. Names you register, fees you pay and NFTs you receive are testnet assets. Screenshots in this section were taken on the testnet build.
{% endhint %}

The thoth.id web app is where you search for a name, register it, and manage everything attached to it — your avatar, your records, who controls the name, and when it expires.

This section is the **user guide**. If you are a developer looking to read thoth.id data from your own application, see the [Sdk Reference](sdk-reference.md) instead.

![The thoth.id landing page](.gitbook/assets/landing-hero.jpg)

## What you can do

| Task                                            | Where                                                    |
| ----------------------------------------------- | -------------------------------------------------------- |
| **Get started — register a name end to end**    | [**Register Your First Name**](web-app/quickstart.md)    |
| Connect your Hathor wallet                      | [Connect Your Wallet](web-app/connect-wallet.md)         |
| Find out whether a name is free                 | [Search for a Name](web-app/search.md)                   |
| Register a name and set an avatar               | [Register a Domain](web-app/register.md)                 |
| See every name you control                      | [Your Dashboard](web-app/dashboard.md)                   |
| Inspect or edit a single name                   | [The Domain Page](web-app/domain-page.md)                |
| Add years before a name expires                 | [Renew a Domain](web-app/renew.md)                       |
| Follow a transaction to confirmation            | [Transactions & Notifications](web-app/notifications.md) |
| Check what names are allowed and what they cost | [Naming Rules & Fees](web-app/naming-rules-and-fees.md)  |
| Fix a problem                                   | [Troubleshooting](web-app/troubleshooting.md)            |

## How it works, in one paragraph

Every thoth.id name is a **nano contract entry on the Hathor Network**, and registering one also mints an **NFT token** that represents it. The web app never holds your keys and never stores your names — it reads the contract through the [thoth.id Sdk](sdk-reference.md), and every change you make is a transaction that **you sign in your own wallet**. Nothing changes until that transaction confirms on-chain.

The one exception is avatar images. An image is too big to live on-chain, so the app uploads it to blob storage and writes only the resulting **URL** into your on-chain profile.

## Before you start

You need:

* A **Hathor wallet** that supports WalletConnect — the mobile app, or the desktop wallet.
* Some **HTR** in that wallet to pay the registration fee and, later, renewals.

That's it. There is no thoth.id account, no password, and no sign-up. Your wallet _is_ your identity.

## Not ready to register?

The landing page has a **Join the waitlist** button. Leave your email — and optionally the name you'd like to reserve — and you'll hear from the team at launch.

![The waitlist dialog](.gitbook/assets/waitlist-dialog.jpg)
