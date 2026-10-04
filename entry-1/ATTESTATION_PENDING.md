# entry-1 — attestation steps still outstanding

Two artifacts named in LEDGER.md are **not yet in this directory**, because
neither can be fabricated and both require credentials this machine does not
hold. They are listed here so the gap is visible rather than implied.

Until both land, entry-1 is published but **not independently attested**.

## 1. `prediction_2026-08-20.csv.ots` — OpenTimestamps proof

Not generated. No `ots` client is installed, and creating the proof requires
calling the public calendar servers. A fabricated `.ots` would be worse than
none at all.

```bash
pip install opentimestamps-client            # or: brew install opentimestamps
cd <engine>/ledger
ots stamp prediction_2026-08-20.csv          # -> prediction_2026-08-20.csv.ots
# the calendars need ~an hour to fold it into a Bitcoin block
ots upgrade prediction_2026-08-20.csv.ots
ots verify  prediction_2026-08-20.csv.ots    # must report the digest below
cp prediction_2026-08-20.csv.ots <this repo>/entry-1/
```

Must attest exactly:
`036c4c5d4bc71793569e67f0b1697663cfc42211c467304a16e14756512a82d6`

Note `ots stamp` reads the CSV to compute its digest, but the resulting `.ots`
contains only the digest and the path to the Bitcoin block — publishing the
`.ots` does **not** publish the file. That is what makes phase 1 possible.

## 2. Zenodo DOI

Not deposited. Requires a Zenodo account and token.

Deposit **the digest and the metadata, not the CSV** while the entry is in
phase 1. Title it so the phase is unambiguous, e.g.
*"Samudra Ledger Entry #1 — frozen prediction file digest (2026-08-20)"*.
Record the DOI in `LEDGER.md` and in the release notes once minted.

## 3. Then cut the release

```bash
gh release create entry-1 \
  --repo Samudra-Intelligence/samudra-ledger \
  --title "Ledger entry #1 — frozen 2026-08-20" \
  --notes-file entry-1/RELEASE_NOTES.md \
  entry-1/SHA256SUMS entry-1/prediction_2026-08-20.meta.json \
  entry-1/prediction_2026-08-20.csv.ots
```

Delete this file once 1 and 2 are done.
