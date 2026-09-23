---
description: Fixes for common wallet, transaction and display problems.
icon: wrench
---

# Troubleshooting

## Connecting

**The QR code doesn't do anything.** Check that your wallet is on the **Hathor testnet**, the same network the app is pinned to. A wallet on a different network can't match the session request. Then close the dialog, click **Connect Wallet** again to get a fresh code — pairing URIs expire after a short while.

**On mobile, tapping Connect Wallet opens the app store.** That means the Hathor Wallet app wasn't detected on the device. Install it, then come back and tap again.

**I get redirected to the landing page when I open /dashboard.** The dashboard needs a connected wallet. Connect first, then use **My Domains**.

**I connected, but the top bar still shows "Connect Wallet".** The session request was probably never approved in the wallet. Open the wallet, check for a pending request, and approve or dismiss it before retrying.

## Searching and registering

**A name I know is valid shows as "Not supported".** That status also appears when the availability check itself fails — usually a Hathor node that's slow or unreachable. Search again. If it persists, check the [naming rules](naming-rules-and-fees.md#what-makes-a-valid-name); the usual culprits are consecutive hyphens and non-ASCII characters.

**The register button is greyed out.** One of: the wallet isn't connected, the fee is still loading, your HTR balance is below the total, or the transaction has already been submitted. The summary bar shows which — an insufficient balance is called out in red.

**"Invalid name format. Please go back and try a different name."** The name reached the register page but the contract rejects it. Go back and pick one that follows the [naming rules](naming-rules-and-fees.md#what-makes-a-valid-name).

**Someone registered the name between my search and my registration.** Possible — availability is checked at search time, and the winner is whoever's transaction confirms first. The transaction will fail and no fee is charged.

## Transactions

**My wallet never asked me to sign.** Bring the wallet app to the foreground; requests can queue silently there. If nothing arrives, disconnect from the avatar menu, reconnect, and try again.

**"Transaction was rejected in your wallet."** The signature request was dismissed. Nothing happened on-chain and nothing was charged. Just retry.

**"No transaction hash received."** The wallet didn't return a hash. Check the wallet's own transaction history **before retrying** — occasionally the transaction went through even though the app didn't hear about it.

**A transaction has been pending for a long time.** The app polls every few seconds and will update on its own. Leave the tab open. The queue is saved in your browser, so a reload won't lose track of it.

**A notification disappeared.** Notifications are stored per browser. Clearing site data, using a different browser, or switching devices starts the list fresh — this has no effect on anything on-chain.

## Editing a name

**I don't see any edit buttons.** You're viewing the name as a **visitor**. Edit controls only appear for the owner or the manager of the name, and only while that wallet is connected. Check the [Ownership tab](ownership.md) to see which addresses hold those roles.

**"Token must be deposited to change the manager."** The name's NFT has been withdrawn to a wallet. Deposit it back from the [Ownership tab](ownership.md) and the role fields unlock. Note that whoever deposits the token becomes the owner.

**I can change the manager but not the owner.** Reassigning ownership requires you to be the **current owner** _and_ the token to be deposited. Managers can only pass on the manager role.

**My avatar didn't appear after registering.** The avatar is a second transaction that runs once the registration confirms — if the tab was closed before it asked for a signature, it never ran. Set the avatar from the [Profile tab](profile.md); the name itself is unaffected.

**An avatar image doesn't load.** Images are served from blob storage, and deleting or replacing the `avatar_link` [record](records.md) removes the old file. Upload a new image from the Profile tab.

## Data looks stale

**The dashboard doesn't show a change I just made.** The dashboard loads its list once, when the page opens. Reload it. [Domain pages](domain-page.md) refresh themselves when a transaction confirms.

**A page shows an old avatar or primary name.** Avatar and primary-name lookups are cached in memory for the life of the page. Reload to clear it.

## Still stuck?

Open the name's [Info tab](info.md) and copy the raw record — it's the fastest way to show the team exactly what the contract holds. Include the transaction hash from the notification centre if the problem involves a transaction.
