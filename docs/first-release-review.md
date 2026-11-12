# First OEM reference release: source review queue

Status: **NOT APPROVED FOR PUBLICATION**. No numerical OEM norms in the public repository.

Target vehicle: Chevrolet Cruze 1.6 / F16D3 / 2013.

Before each reference can be included in a signed IRBIS OEM package, verify:
- exact engine code **F16D3**, rather than LUJ/LUW/F16D4/other 1.6 engines;
- actual manufacturer/service documentation ID, revision and page/section;
- the applicable vehicle market/year and ECU calibration if stated;
- conditions (cold vs warmed, closed loop, idle/rpm/load, A/C on/off);
- that the displayed OBD PID and converted unit correspond to the documented parameter;
- explicit redistribution rights for inclusion in a commercial app;
- a reviewer sign-off, and a compatible licensed method to distribute the data.

## Initial source research (unverified candidates only)

- 2013 F16D3 engine identification: a parts catalog indicates F16D3 / LXT, but **parts catalog data is not scan-data OEM normative values**: https://partsouq.com/en/catalog/genuine/vehicle
- A diagnostic forum presents individual F16D3 live measurements (e.g. one specific vehicle in 2011). **Do not treat those measurements as factory limits**: https://forum.adact.ru/topic/40183-chevrolet-cruze-2011-f16d3-16lxt-metki-grm/
- Various Chevrolet Cruze service datasets contain expected scan-tool ranges, but some target 1.4 LUJ or LUW rather than F16D3. **Do not cross-apply them** without explicit manufacturer applicability.

Outcome: **0 approved OEM reference records.** The signed release path
`releases/oem-reference.bundle` must remain absent, and the app's OEM update
source must remain disabled until reviewed authorized data exists.

## Private signing workflow (not yet executed)

The release builder and its QA tests now live in the **private** IRBIS source
repository under `tools/oem/build_release.py` and
`tools/oem/test_build_release.py`. Nothing is signed or published automatically.

Before building a real package, a reviewer must approve the source documents,
technical values and rights to redistribute. Compute SHA-256 of the exact
approved schema-2 JSON; then use the private builder with the approved hash
and an external private signing key. The signing key must never be copied to
this public repository.

After signing, independently verify the bundle against the **public key
embedded in the Android application**, test a successful update and rejection
of a modified payload, then publish the resulting
`releases/oem-reference.bundle`. Until then there are **zero** approved OEM
entries and the update channel stays disabled.
