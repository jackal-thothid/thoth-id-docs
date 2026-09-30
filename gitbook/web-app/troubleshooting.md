---
description: Fixes for common wallet, transaction and display problems.
icon: wrench
---

# Troubleshooting

## Connecting

**The QR code doesn't do anything.** Check that your wallet is on the **Hathor testnet**, the same network as the app. A wallet on another network can't match the session request. Then close the dialog and click **Connect wallet** again to get a fresh code; pairing links expire after a while.

**On mobile, tapping Connect wallet opens the app store.** The Hathor Wallet app wasn't found on the device. Install it, then come back and tap again.

**The button is stuck on "Waiting for Hathor Wallet…".** The session request hasn't been approved yet. Open the wallet, look for the pending request, and approve or refuse it.

**My names asks me to connect.** The list needs a connected wallet. Connect from that page or the top bar.

## Searching and registering

**A search says "Couldn't check".** The app couldn't reach the Hathor node. Click **Try again**. This doesn't mean anything is wrong with the name.

**A name shows as "Not supported".** The row says which rule it breaks, and usually suggests a valid alternative. See the [naming rules](naming-rules-and-fees.md#what-makes-a-valid-name); the usual culprits are capitals, spaces, accents and consecutive hyphens.

**The register button is disabled.** One of: the price is still loading, your balance is below the total (the page says how much more you need), or the transaction has already been sent.

**"Someone registered yourname.htr first".** Another registration confirmed before yours. The app checks availability right before your wallet opens, but two people can still race. Your HTR wasn't spent.

## Transactions

**Hathor Wallet never asked me to sign.** Bring the wallet app to the foreground; requests can wait there silently. On a phone, use **Open Hathor Wallet** on the page. If nothing arrives, press **Cancel**, disconnect from the account menu, reconnect, and try again.

**I refused the request by mistake.** Nothing was sent. Start the action again.

**"Hathor Wallet didn't return a transaction".** Check the wallet's own history **before retrying**; occasionally the transaction went through even though the app didn't hear about it.

**A transaction is "Taking longer than usual".** The network hasn't put it in a block yet. You don't need to do anything; the app keeps checking and updates on its own, even after a reload.

**An item says "Not tracked".** The page was reloaded while Hathor Wallet was asking. If you approved it, the change shows on the name's page once it confirms.

**An item disappeared from Activity.** Activity is stored per browser and keeps recent results for 14 days. Clearing site data, using a different browser, switching devices or connecting another wallet shows a different list. None of this affects anything on-chain.

## Managing a name

**I don't see Manage or any edit buttons.** Your connected wallet isn't the name's owner or manager. Check **Owner** and **Manager** in the **Details** panel of the name's page.

**Profile and Records are read-only in Manage mode.** You're the owner but not the manager, and only the manager can edit them. Make yourself manager under [Addresses](addresses.md#manager).

**"The name's token isn't deposited".** The token has been withdrawn to a wallet, so owner actions are paused. Deposit it back from the name's page or [Ownership](ownership.md). Whoever deposits it becomes the owner.

**My avatar didn't appear after registering.** The avatar is a second signature, sent once the registration confirms. If you refused it or it expired, it shows as **Not sent**. Set the avatar from [Profile](profile.md); the name itself is unaffected.

**An avatar image doesn't load.** Images are served from blob storage, and replacing or deleting the avatar removes the old file. Upload a new image from Profile.

## Still stuck?

Open the name's page, expand **Raw contract data** at the bottom of **Details**, and copy it. It's the fastest way to show the team exactly what the contract holds. If the problem involves a transaction, include its hash from the panel or from Activity.
