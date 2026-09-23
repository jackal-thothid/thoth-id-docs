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

The search box lowercases and trims what you type, so `Satoshi` is treated as `satoshi`. Anything that still breaks a rule comes back as [**Not supported**](search.md#-not-supported).

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

Both the base fee and the multipliers are stored in the nano contract and can be changed by the contract's developer address, so this documentation deliberately doesn't quote figures. **The number you see in the app is read live from the contract** — it's on the [registration page](register.md) and in the [extend dialog](renew.md), and it's the one that will be charged.

Developers can read the same values with [`getFeeInfo`](../sdk-reference/getFeeInfo.md), [`calculateFee`](../sdk-reference/calculateFee.md) and [`getFeeStructure`](../sdk-reference/getFeeStructure.md).

### Terms

You can pay for **1 to 10 years** at a time, both when registering and when renewing. There's no discount for buying more years — the total is simply the yearly fee multiplied by the term.

## Expiry and the grace period

| Phase            | What it means                                                                                    |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| **Active**       | Everything works normally                                                                        |
| **Grace period** | The name has expired. It's still yours to renew, and nobody else can take it. Lasts **30 days**. |
| **Available**    | The grace period is over. The name is released and anyone can register it.                       |

See [Renew a Domain](renew.md) for how to extend before that happens.

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
| NFT token symbol          | First **5** characters of the name, uppercased      |

The record limits are covered in more detail on the [Records](records.md) page.
