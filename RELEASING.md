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

One commit per item:

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
11. **Schema 1 compliance** — implement per [NW-Device-Specification](https://github.com/NorthernWidget/NW-Device-Specification) once the spec is stable (sensor libraries only; controllers follow a different path)

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
