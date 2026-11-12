# IRBIS OEM Reference Database — package format

**Documentation only. This file does not contain verified OEM data.**

The Android IRBIS v4.0 QA application expects a single binary package named
`releases/oem-reference.bundle`, containing an RSA-SHA256-signed UTF-8 JSON
payload in the existing IRBIS binary bundle container. Only the application
verifies the signature; HTTPS alone is not enough.

## Signed JSON schema 2

The signed JSON object contains:
- `schema`: integer 2
- `version`: increasing `YYYY.M.D.N`, e.g. `2026.11.12.1`
- `references`: 1 to 3000 fully reviewed OEM reference entries.

Each reference entry must contain:
- `vehicle`: `make`, `model`, `engineCode`, `modelYear`
- `pid`: integer OBD PID 0..255
- `lower`, `upper`: finite, ordered numerical bounds in raw metric units
- `unit`: physical measurement unit
- `condition`: `id` and `description` for the precise operating conditions
- `source`: `publisher`, `documentTitle`, `documentId`,
  `revision`, `pageOrSection` for traceability
- `verified`: `true` only after editorial verification.

The application rejects wrong schema, malformed version, missing sources,
unverified records, duplicate vehicle/PID/condition entries, and invalid
bounds. The package must carry a valid signature from the offline-held IRBIS
signing key. Do not store signing keys or access tokens in this repository.

Even a signed record with `verified: true` requires real technical document
verification and appropriate redistribution rights. Sample diagnostic values
are not OEM specifications.

## Deployment checklist

1. Source and license review.
2. Inspect vehicle, engine, applicability and operating condition.
3. Validate schema and data quality.
4. Sign the exact JSON bytes with an offline private key.
5. Produce the signed binary bundle and upload at the reserved path.
6. Test download, signature verification, installation and failure cases.
7. Enable the pinned source in the **private QA branch** only after success.

**At present no OEM bundle is published and the Android download channel
must remain disabled.**
