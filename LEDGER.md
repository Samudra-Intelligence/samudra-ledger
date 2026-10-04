# The Samudra Ledger

A ledger entry is a file of predictions, frozen on a stated date, hashed, and
left alone until the window closes. Then the county's deeds grade it, and the
grades are published next to the misses.

This repository is the public, append-only record of those entries. It is
operated by Samudra LLC, Sarasota, Florida.

---

## The two-phase promise

Every entry lives through exactly two phases. This is the whole protocol.

### Phase 1 — FROZEN (from the freeze date until the window closes)

Published here: the **SHA-256 of the prediction file**, its `meta.json`, an
**OpenTimestamps** proof, and a **Zenodo DOI**.

**The prediction file itself is NOT published in this phase.** A live book is the
product; publishing it would hand over the scored book for every commercial
parcel in the covered counties. What is published is enough to make the file
*unforgeable later*: the digest is attested by Bitcoin timestamp and by an
independent archive, both dated before anyone knows the outcome.

### Phase 2 — GRADED (on grading day, when the window has closed)

Published here: **the full frozen CSV, verbatim, propensity column included** —
together with the grades, hits and misses in the same table.

Anyone can then run:

```
shasum -a 256 prediction_<date>.csv
```

and must get back the digest that was timestamped before the window opened. If
it does not match to the character, the entry is void and should be treated as
such. That check is the point of the whole exercise.

A graded, expired book is **evidence, not product**. Its predictive value is
spent; its evidentiary value is the only thing left, and that value is zero
unless the bytes are public and match.

---

## Entry #1 — the founding freeze

| | |
|---|---|
| file | `prediction_2026-08-20.csv` |
| frozen on | **2026-08-20** |
| rows | **323,522** |
| counties | 11 |
| horizon | 18 months |
| data through | 2026-06-01 |
| window closes | **2028-02-20** |
| top-k tracked | 250 |
| **SHA-256** | **`036c4c5d4bc71793569e67f0b1697663cfc42211c467304a16e14756512a82d6`** |
| phase | **1 — FROZEN.** CSV publishes on grading day. |

Also in `entry-1/`: `prediction_2026-08-20.meta.json` (the manifest written at
freeze time), `SHA256SUMS`, the OpenTimestamps proof, and the Zenodo DOI.

### Verifying entry #1 today, before the CSV exists here

1. `shasum -a 256 -c SHA256SUMS` fails for the CSV — correct, you do not have it.
   The `.meta.json` line must pass.
2. Verify the timestamp proof: `ots verify prediction_2026-08-20.csv.ots`. It
   attests the digest above, not the file, so it verifies without the file.
3. Check the Zenodo record resolves and carries the same digest.
4. On 2028-02-20 the CSV lands here and step 1 must pass completely.

If you were given a copy of the CSV privately — under NDA, in diligence, as a
customer — hash it and compare to the digest above. That is the same check the
public will run in 2028.

---

## Rules this repository keeps

1. **Append-only.** Entries are added, never revised. A correction is a new
   entry that cites the old one; the old one stays exactly as published.
2. **No silent edits.** Any change to a published file is a hash change and is
   therefore a lie. There is no mechanism here for touching a frozen entry.
3. **Misses print.** A grade publishes hits and misses in the same table. A
   miss is a top-decile parcel that did not transfer, or a transfer that sat in
   the bottom half. Both appear.
4. **Denominators print.** No rate is published without the count it came from.
5. **No accuracy claims before grading.** Everything published before an entry's
   window closes is a walk-forward backtest and is labelled as one. A backtest
   is not a ledger grade.

## What this is not

Decision support from public records. Not investment advice; Samudra LLC is not
an investment adviser, and nothing here is an offer to buy or sell real estate
or any instrument. Source data is the Florida Department of Revenue assessment
rolls and sale data files, published under chapter 119, Florida Statutes.
