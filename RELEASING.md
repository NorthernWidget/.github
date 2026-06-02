# Releasing an NW Arduino Library

This checklist applies to every versioned release of a NorthernWidget Arduino sensor library. Work through the items in order; make one commit per item.

**Physical hardware testing is required before any release.** A complete checklist does not mean the library is ready to release.

## Required files

Every library must have:

| File | Requirements |
|------|-------------|
| `library.properties` | `version=` at release semver; `paragraph=` filled in |
| `LICENSE` | GPL-3.0 |
| `README.md` | Zenodo DOI badge (concept DOI); basic usage example |
| `CITATION.cff` | cff-version 1.2.0; all authors with ORCIDs; concept DOI; `date-released`; `license: GPL-3.0` |
| `.zenodo.json` | `upload_type: software`; `license: {id: GPL-3.0-only}`; same authors and keywords |
| `keywords.txt` | KEYWORD1 = class/enum types; KEYWORD2 = public methods; LITERAL1 = constants/enum values |
| `doxygen_NW.cfg` | `OPTIMIZE_OUTPUT_FOR_C = NO`; no `MDFILE_AS_MAINPAGE`; `EXCLUDE = examples` |
| `src/` | Source in `src/`, not flat layout |
| `examples/LibraryName_Demo/` | Minimal sketch: `begin()` error check; `getHeader()` in setup; `getString()` in loop with `delay(1000)` |
| `.github/workflows/docs.yml` | Thin wrapper: `uses: NorthernWidget/.github/.github/workflows/deploy-docs.yml@main` |

## Pre-release checklist

One commit per item.

### Schema 0 baseline (all releases)

Complete these before any versioned release, regardless of schema:

1. **Version** — assess git history since last tag; choose semver bump; `0.x` → `1.0.0` for first stable release
2. **`library.properties`** — bump `version=`; fill `paragraph=` if empty
3. **DOI badge** — replace any deprecated `latestdoi`/`GITHUB_REPO_ID` format; use concept DOI (ask maintainer; never guess)
4. **`CITATION.cff`** — create or update; cff-version 1.2.0; all authors with ORCIDs
5. **`.zenodo.json`** — create or update; `upload_type: software`; `license: {id: GPL-3.0-only}`
6. **`keywords.txt`** — create or update
7. **`examples/LibraryName_Demo`** — create or update minimal demo sketch
8. **`doxygen_NW.cfg`** — fix known bad settings (`OPTIMIZE_OUTPUT_FOR_C = NO`; remove `MDFILE_AS_MAINPAGE`; `EXCLUDE = examples`)
9. **Return types** — `begin()` must return `bool`; update Doxygen tags and examples
10. **`.github/workflows/docs.yml`** — add if missing

Tag a Schema 0 snapshot release once items 1–10 are complete and the library has been tested on physical hardware. This snapshot preserves the last known-good register map before any breaking Schema 1 changes.

### Schema 1 migration (sensor libraries only)

Complete these when migrating to [NW-Device-Specification](https://github.com/NorthernWidget/NW-Device-Specification) Schema 1. Do not begin until the spec is stable and a Schema 0 snapshot tag exists.

11. **Schema 1 compliance** — implement the full Schema 1 register map per the device appendix in NW-Device-Specification:
    - **Page 0 (0x00–0x1F, EEPROM-backed identity):** schema byte `0x01` at `0x00`; 7-byte name at `0x01–0x07`; HW/FW version at `0x08–0x0A`; serial number block at `0x10–0x17`; magic byte `0x4E` at `0x1D`; CRC-8/SMBUS at `0x1E`; I²C address at `0x1F`
    - **Page 1 (0x20–0x3F, SRAM sensor data):** status byte at `0x20` (bit 0 = ready, bit 7 = pan-fault); extended fault byte at `0x21`; sensor data from `0x22` onward per device appendix
    - **Page 2 (0x40–0x5F, calibration, if applicable):** per device appendix
    - Update default I²C address to the Schema 1 value from the address registry
    - `begin()` reads schema byte; rejects non-`0x01` values

Controllers (Margay, Okapi) are not sensors and do not implement the sensor register map; their Schema 1 entries are identity-only.

## Code conventions

- `begin()` returns `bool`; checks I²C ACK; stubs return `false`
- No build artifacts committed (no `_docs/`, no downloaded binaries)
- DOI badge uses concept DOI (permanent, not per-version)

## Authors

Known authors for citation files:

| Name | ORCID | Affiliation |
|------|-------|-------------|
| Andrew D. Wickert | 0000-0002-9545-3365 | University of Minnesota, Department of Earth & Environmental Sciences |
| Bobby Schulz | 0000-0002-9272-4756 | Northern Widget LLC |

Confirm full author list from `library.properties` and `git log` before writing `CITATION.cff` or `.zenodo.json`.

## Reference libraries

- **[Apis_Library](https://github.com/NorthernWidget/Apis_Library)** — reference for `CITATION.cff`, `keywords.txt`, `.github/workflows/docs.yml`, code conventions
- **[Walrus_Library](https://github.com/NorthernWidget/Walrus_Library)** — reference for `.zenodo.json`
- **[NW_BME280](https://github.com/NorthernWidget/NW_BME280)** — alternate reference for `CITATION.cff`
