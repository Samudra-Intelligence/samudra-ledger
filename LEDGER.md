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

*Further entries are appended here as they freeze. Entries are append-only; no entry is ever edited or removed.*

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
| Zenodo (citable) | concept DOI `10.5281/zenodo.23049052` · entry-1 version DOI `10.5281/zenodo.23049053` |

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

**Contact:** Samudra LLC, Sarasota, Florida · Cite as: "Samudra Intelligence Ledger, Zenodo, DOI 10.5281/zenodo.23049053"
