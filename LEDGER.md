# THE SAMUDRA LEDGER
**Samudra Intelligence · Florida Commercial Real Estate · Samudra LLC, Sarasota, Florida**

This document is the public protocol of record for Samudra Intelligence's prediction ledger. It states what we freeze, how we prove when we froze it, and how anyone can grade us later. It is published so that no claim we make about our own accuracy ever has to be taken on trust.

---

## THE PROTOCOL

**1. Predict.** Samudra Intelligence produces seller-propensity predictions for Florida commercial real estate parcels, built exclusively on public records (Florida DOR assessment rolls, recorded deeds, Sunbiz corporate filings, and other government sources).

**2. Freeze.** On a stated origin date, the complete prediction book is written to a single CSV file and never altered. One file, every prediction, no substitutions, no deletions.

**3. Hash.** The frozen file's SHA-256 digest is computed and published. The digest commits to every byte of the book: change one character of one prediction and the digest changes completely.

**4. Timestamp.** The digest is anchored outside our control:
- **OpenTimestamps** — the digest is committed into the Bitcoin blockchain (cryptographic proof of existence);
- **Zenodo** — this ledger and the timestamp proof are deposited under a DOI (institutional, citable record);
- **GitHub** — the same record is published as a public release (browsable convenience copy).

From Entry #2 onward, the external timestamp is created on the origin date itself. Entry #1 was timestamped after its freeze date; both dates are stated below, because the timestamp proves existence *no later than* its own date — nothing earlier.

**5. Grade.** Each prediction concerns whether a parcel records a qualified arm's-length deed (DOR qualification codes 01/02) within a stated forward window from the origin date. When the window closes, the frozen book is opened and graded against the deeds actually recorded — public records anyone can pull. Results are published: hits, misses, and rates, each with its numerator, denominator, and window.

**6. Pending doctrine.** Until a book grades, no score numbers are published — only ranks and deciles. A prediction that has not yet met reality is labeled PENDING, never presented as validated.

**Revision policy:** frozen files are never revised. Anything else we publish (indices, monitors, analytics) follows publish-first: errors are corrected openly and every revision is logged.

---

## THE LEDGER

### Entry #1 — The Founding Book
| Field | Value |
|---|---|
| File | `prediction_2026-08-20.csv` |
| Predictions | 323,522 |
| Coverage | 11 Florida counties (Charlotte, Collier, Duval, Hillsborough, Lee, Manatee, Miami-Dade, Orange, Palm Beach, Pinellas, Sarasota) |
| SHA-256 | `036c4c5d4bc71793569e67f0b1697663cfc42211c467304a16e14756512a82d6` |
| Frozen | 2026-08-20 |
| Independently timestamped | 2026-09-29 (OpenTimestamps; proof file: `prediction_2026-08-20.csv.ots`) |
| Window | 18 months from origin |
| Grades | on/after 2028-02-20, against recorded deeds |
| Status | **PENDING** |
| Zenodo (this entry) | version DOI `10.5281/zenodo.23049053` |

### Entry #2 — Statewide
| Field | Value |
|---|---|
| File | `prediction_2026-10-18.csv` |
| Predictions | 617,943 |
| Coverage | **all 67 Florida counties** |
| SHA-256 | `246c32420bb5c07f8a2723d98d1402b7ab2bc2c5c09940f234306c013b0a1f42` |
| Frozen | 2026-10-18 |
| Independently timestamped | **2026-10-18 — the same day it froze** (OpenTimestamps; proof file: `prediction_2026-10-18.csv.ots`) |
| Window | 18 months from origin |
| Grades | on/after 2028-04-18, against recorded deeds |
| Roll vintage | 2026P (preliminary), uniform across all 67 — see below |
| Zenodo (this entry) | version DOI `10.5281/zenodo.23460579` |
| Status | **PENDING** |

**On the 2026P vintage, stated plainly.** Florida DOR deletes preliminary rolls
from its portal once Final is posted. At freeze time 2026 Final existed for only
48 of 67 counties — and not for Miami-Dade or Broward — so the only way to freeze
a uniform statewide book was the preliminary vintage, which the source has since
withdrawn. A verifier therefore cannot re-download our inputs. So we hashed them
instead: every one of the 134 input files is listed with its SHA-256 in
`INPUTS_SHA256SUMS`, archived under object-lock, and verified 134/134 by
re-downloading and re-hashing. Per-county vintage is recorded in the entry's
metadata. We would rather publish the awkward fact than a book you cannot check.

**On what this book can and cannot claim.** Deed history is not uniform across
Florida. Thirteen counties have records back to 2015; the other 54 begin
2025-01-01. Backtest folds before 2024 are therefore observable in only those 13
counties, and any lift quoted from them is a 13-county figure, not a statewide
one. The first substantially statewide fold is 2025-01-01, at 17 of 18 months
observable. This book is the first statewide freeze; it has not been graded, and
nothing here is a result.

### Entry #3 — Statewide, corrected sales history
| Field | Value |
|---|---|
| File | `prediction_2026-10-19.csv` |
| Predictions | 617,943 |
| Coverage | **all 67 Florida counties** |
| SHA-256 | `3a64c3b1fe0a7c9e2d2d30e6a66de642dfeda7ed161cdcb85206f5ecf00fac9a` |
| Frozen | 2026-10-19 |
| Independently timestamped | **2026-10-19 — the same day it froze** (OpenTimestamps; proof file: `prediction_2026-10-19.csv.ots`) |
| Window | 18 months from origin |
| Grades | on/after 2028-04-19, against recorded deeds |
| Roll vintage | 2026P (preliminary), uniform across all 67 — same corpus as Entry #2 |
| Zenodo (this entry) | version DOI pending — recorded on publication |
| Status | **PENDING** |

**Why this entry exists.** Entry #2, frozen the day before, was built on a sales
history that double-counted sales appearing in more than one annual vintage —
recorded in ERRATA E-1 below. Entry #2 is not withdrawn and not revised: it is
published, hashed and timestamped, and it will be graded as it stands. Entry #3
is the same universe, the same inputs and the same 2026P roll vintage, recomputed
on a corrected merge. The input manifest is byte-identical to Entry #2's
(`INPUTS_SHA256SUMS`, self-digest `f26fb53b…`), because the defect was in how the
inputs were combined, not in the inputs themselves.

**What changed, measured.** Across the thirteen counties assembled from multiple
vintages, the corrected merge removes the duplicates the old one kept — Broward
1,518,315 rows to 940,286, Charlotte 541,499 to 356,737. Statewide the walk-forward
top-decile lift at the 2019 origin moves from 3.87x to 3.57x, and every graded fold
stays under the leakage rail (highest AUC 0.822 against a 0.85 limit). Corrections
ran in both directions, which is what a genuine de-duplication looks like.

**What is still true of both entries.** Deed history is not uniform across Florida:
thirteen counties reach back to 2015, the other fifty-four begin 2025-01-01.
Backtest folds before 2024 are observable only in those thirteen, so any lift
quoted from them is a thirteen-county figure, not a statewide one. Neither entry
has been graded. Nothing here is a result.

*Further entries are appended here as they freeze. Entries are append-only; no entry is ever edited or removed.*

---

## ERRATA

Appended, never substituted. An entry's own block above is never edited; defects
found after publication are recorded here, under the date they were found.

### E-1 · 2026-10-18 — cross-vintage sale duplication in the merged sales history

**What was wrong.** Each annual Florida DOR sales file (SDF) carries roughly two
years of sales, so adjacent vintages list the same sale twice. The copies differ
in their assessment-year field, so the merge step's whole-row de-duplication kept
both. The per-parcel count of prior qualified sales — a model input, and the
trigger for the "trades often" signal — was therefore inflated wherever a county's
history was assembled from more than one vintage.

**Measured, not estimated.** On Manatee across ten vintages: 582,215 raw rows,
of which **46.8% were cross-vintage duplicates that the old merge removed none
of**. Prior-qualified-sale counts were inflated on **87.7%** of parcels (mean
2.572 against a true 1.305). The "trades often" signal fired on 98,060 parcels
where it should have fired on 29,290 — **68,770 false positives, 68,621 of them
parcels that had sold exactly once**.

**What it touches.**

- **Entry #2** (statewide, 67 counties). Thirteen counties are assembled from
  multiple vintages. **62.1% of the entry's 617,943 rows, and 81.7% of its top
  decile, come from those thirteen.** The freeze log records all thirteen merging
  at "0 dropped", which is the defect's signature.
- **Entry #1** (founding book, 11 counties). Its eleven counties are *exactly* the
  eleven for which a ten-vintage history was assembled, and the merge code
  predates the freeze by thirteen days. **Entry #1's book and the eleven-county
  Backtest Atlas are affected too.** Every validation figure drawn from that
  Atlas — including the top-decile lift range quoted publicly — is suspect until
  reproduced on corrected data.

**What we are not doing.** We are not revising either frozen file, and not
withdrawing either entry. Both are published, hashed and externally timestamped;
a frozen book is a record of what we predicted, including when we predicted it
with a defect we had not yet found. The 2028 grades will measure these books as
they stand. That is the protocol working, not a loophole in it.

**What we are doing.** The defect is fixed in the pipeline
([samudra-engine PR #5](https://github.com/Samudra-Intelligence/samudra-engine/pull/5),
merged 2026-10-18, the same day Entry #2 published). The Backtest Atlas is being
reproduced on corrected data and the corrected figures will be published with the
old-versus-new difference shown per fold, not quietly swapped. The next entry
freezes on corrected data. Any figure sourced from the affected Atlas should be
treated as provisional until that reproduction is published.

Found and disclosed the same day Entry #2 published.



---

## HOW TO VERIFY US

1. **Today:** confirm the timestamp. Take `prediction_2026-08-20.csv.ots` from this deposit and check it at opentimestamps.org (or with the open-source `ots` client). It proves a file with the digest above existed no later than the stamped date.
2. **On grading day:** we publish the frozen CSV. Run `shasum -a 256` on it. If the digest does not match this ledger exactly, we altered the book — discard everything we have ever claimed.
3. **Any day:** pull the recorded deeds from the county clerks — they are public records — and grade any published book yourself. You do not need our permission or our software.

*No rate without its numerator, denominator, and window.*

---

## WHERE THIS IS PUBLISHED

Entry #1 went public **2026-10-18**. Three independent anchors, any one of which
can be checked without our cooperation:

| anchor | locator |
|---|---|
| GitHub (browsable) | `github.com/Samudra-Intelligence/samudra-ledger` — public; release tag `entry-1` |
| OpenTimestamps (Bitcoin) | `entry-1/prediction_2026-08-20.csv.ots` (654 bytes), stamped 2026-09-29 |
| Zenodo (citable) | concept DOI `10.5281/zenodo.23049052` (always resolves to the current version) · entry-1 `10.5281/zenodo.23049053` · entry-2 `10.5281/zenodo.23460579` |

What is published now, and what is not: the digest, the metadata, the timestamp
proof and this protocol are public today. **The frozen CSV itself is withheld
until grading day (2028-02-20)** — it contains raw propensity values, and a live
book is product. On grading day the full CSV is published verbatim, propensity
column included, and any reader must be able to reproduce
`036c4c5d…512a82d6` from it. A graded, expired book is evidence, not product.

Reproduce the published digest yourself, no account needed:

```
curl -s https://raw.githubusercontent.com/Samudra-Intelligence/samudra-ledger/main/entry-1/SHA256SUMS
```

**Contact:** Samudra LLC, Sarasota, Florida · Cite as: "Samudra Intelligence Ledger, Zenodo, DOI 10.5281/zenodo.23049052" (concept DOI — always resolves to the current version; Entry #1's own version DOI is 10.5281/zenodo.23049053)
