# One IRBIS OEM database for all supported vehicles

**Architecture approved 2026-11-12.**

There is **one versioned, signed OEM reference package** distributed publicly at
`releases/oem-reference.bundle` (when source reviews, licences, signing and QA
are complete). It may contain manufacturer-approved references for multiple
makes, models, engines and model years. The user must **not** download a separate
file for each car.

## Selection on the device

1. IRBIS reads the vehicle identification available from the diagnostic ECU,
   and may attempt VIN decoding.
2. Any missing or ambiguous make/model, engine code or model year must be
   confirmed by the user or another trustworthy source. VIN alone does not
   prove all engine/ECU variants.
3. IRBIS searches its **locally installed unified package** using the exact
   make, model, engine code, model year, OBD PID, and verified operating
   condition.
4. Only a unique, source-verified record may be displayed as a manufacturer
   reference. A wrong engine, year, PID or operating condition yields
   **no OEM reference available**, not a guessed range.
5. The real value still comes from the connected ECU, independently of OEM
   references. Database download does not require an ELM327 connection.

## Update policy

- The package is downloaded via HTTPS from the pinned public source.
- Its IRBIS digital signature, schema, entries and increasing version number
  are checked before atomic local replacement.
- The database remains available offline after installation.
- OEM values are updated independently of the Android APK.
- Download availability, consent and network policy are separate from
  identification of the currently connected vehicle.

## Current limits

The Android code supports a single signed package and strict reference lookup.
Live PID display is **not yet connected to the selected vehicle's verified
make/model/engine/year and operating condition**. Until that integration is
complete, the user interface must show no verified OEM norms.

The 2026-11-12 seed database contains **zero** approved manufacturer
references. Do not publish a fake package to make the update button appear
functional.

Future scale: the initial signed JSON schema caps packages at 3,000 records and
512 KiB. Larger datasets require a reviewed schema, chunking or compression
plan before expanding this limit; never silently truncate or split the
public contract.
