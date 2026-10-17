# entry-1 — attestation

- **SHA-256** (prediction file): `036c4c5d4bc71793569e67f0b1697663cfc42211c467304a16e14756512a82d6` (see `SHA256SUMS`)
- **OpenTimestamps**: `prediction_2026-08-20.csv.ots` (this directory). The owner runs
  `ots upgrade prediction_2026-08-20.csv.ots` once the Bitcoin attestation is available,
  and re-commits the upgraded proof — the stamp's validity is independently checkable with
  `ots verify` against the CSV named in SHA256SUMS.
- **Zenodo**: version DOI `10.5281/zenodo.23049053` · concept DOI `10.5281/zenodo.23049052`
- The prediction file itself publishes in full on grading day (window closes **2028-02-20**),
  per the two-phase promise in `LEDGER.md`.
