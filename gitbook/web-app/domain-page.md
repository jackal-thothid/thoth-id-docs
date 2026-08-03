# The Domain Page 🏷️

Every registered name has a page at **/domain/&lt;name&gt;.htr**. It is **public** — anyone can open it, with or without a wallet, and see who holds the name, what's in its profile and when it expires.

![The domain page, Profile tab](../assets/web-app/domain-profile.jpg)

## The header

* The name in full, with a **copy** button next to it.
* An **Extend** button, which opens the renewal dialog. See [Renew a Domain](renew.md).

## The four tabs

| Tab | What's on it |
| --- | --- |
| [**Profile**](profile.md) | Avatar, expiry, description, and the primary-name switch |
| [**Records**](records.md) | Every key/value entry stored on-chain for this name |
| [**Ownership**](ownership.md) | Manager and owner addresses, the NFT, and the resolver |
| [**Info**](info.md) | The raw contract record, as JSON |

The active tab is part of the URL (`?tab=records`), so you can link somebody directly to it.

## Your role decides what you can edit

When you open the page with a wallet connected, the app compares your address against the record and gives you one of three roles:

| Role | You are… | You can… |
| --- | --- | --- |
| **Owner** | the address that holds the name NFT | transfer ownership, change the resolver, deposit/withdraw the NFT, and everything a manager can do |
| **Manager** | the address in charge of day-to-day use | edit the profile and records, set the name as primary, change the manager |
| **Visitor** | anyone else | view only |

Edit controls simply don't appear for visitors. The exact rules for changing roles — including why the NFT sometimes has to be *deposited* first — are on the [Ownership](ownership.md) page.

## Live updates

The page reloads its data by itself whenever one of your queued transactions succeeds, so after signing an edit you'll see the new value appear without touching the browser.
