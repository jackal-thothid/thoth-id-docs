---
description: Which names are valid, what they cost per year and how expiry works.
icon: ruler
---

# Naming Rules & Fees

## What makes a valid name

A thoth.id name must be:

* Between **3 and 80 characters** long.
* Made up of **lowercase letters `a–z`, digits `0–9`, and hyphens `-`**.
* **ASCII only** — no accents, emoji or other Unicode. This is deliberate: it stops names that look identical from being different names.

And it must not:

* **Start or end with a hyphen** — `-name` and `name-` are rejected.
* Contain **two hyphens in a row** — `my--name` is rejected, `my-name` is fine.

The search box lowercases and trims what you type, so `Satoshi` is treated as `satoshi`. Anything that still breaks a rule comes back as [**Not supported**](search.md#not-supported), with the reason and, when possible, a valid suggestion.

| Name        | Valid? | Why                                 |
| ----------- | ------ | ----------------------------------- |
| `satoshi`   | Yes    |                                     |
| `my-name`   | Yes    | Single hyphen in the middle is fine |
| `web3-2026` | Yes    | Digits are fine                     |
| `ab`        | No     | Shorter than 3 characters           |
| `my--name`  | No     | Consecutive hyphens                 |
| `-name`     | No     | Leading hyphen                      |
| `café`      | No     | Non-ASCII character                 |

## What a name costs

The fee is **per year**, paid in **HTR**, and depends on the **length of the name**:

```
fee per year = base fee × length multiplier
```

There are three tiers of multiplier — for **3-character**, **4-character**, and **5-or-more-character** names. Shorter names are scarcer, so they carry the bigger multiplier: a 3-letter name costs more per year than a 10-letter one.

Both the base fee and the multipliers are stored in the nano contract and can be changed by the contract's developer address, so this documentation deliberately doesn't quote figures. **The number you see in the app is read live from the contract**: in search results, on the [registration page](register.md), on the landing page's price table and in the [Renew dialog](renew.md). It's the one that will be charged. There are no network fees on Hathor on top of it.

Developers can read the same values with [`getFeeInfo`](../sdk-reference/getFeeInfo.md), [`calculateFee`](../sdk-reference/calculateFee.md) and [`getFeeStructure`](../sdk-reference/getFeeStructure.md).

### Terms

You can pay for **1 to 10 years** at a time, both when registering and when renewing. There's no discount for buying more years — the total is simply the yearly fee multiplied by the term.

## Expiry and the renewal window

| Phase            | What it means                                                                                    |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| **Active**       | Everything works normally                                                                        |
| **Renewal window** | The name has expired and no longer resolves. It can still be renewed, and nobody else can register it. Lasts **30 days**. |
| **Available**    | The renewal window is over. The name is released and anyone can register it.                     |

See [Renew a Name](renew.md) for how to extend before that happens.

## Other limits

Set by the nano contract:

| Limit                     | Value                                               |
| ------------------------- | --------------------------------------------------- |
| Names managed per address | **100**                                             |
| Records per name          | **20**                                              |
| Record key length         | 1–**50** characters (letters, numbers, underscores) |
| Record value length       | 1–**200** characters                                |
| Total size of all records | 10,000 bytes                                        |
| Avatar image upload       | **5 MB**                                            |
| Name token symbol         | First **5** characters of the name, uppercased      |

The record limits are covered in more detail on the [Records](records.md) page. The contract calls the renewal window its _grace period_; SDK methods such as [`getGracePeriodDays`](../sdk-reference/getGracePeriodDays.md) use that name.
