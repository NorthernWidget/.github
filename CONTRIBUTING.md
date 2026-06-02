# Contributing to NorthernWidget

## Repository naming

| Type | Pattern | Examples |
|------|---------|---------|
| Hardware design | `Project-<Name>` | `Project-Margay`, `Project-Apis` |
| Arduino library (new) | match library name | `NW_BME280`, `Walrus_Library` |
| Arduino library (legacy) | `<Name>_Library` | `Margay_Library`, `MaxBotix_Library` |
| NW tools / specs | `NW-<Name>` | `NW-Device-Specification`, `NW-Provision` |

New library repos follow the Adafruit/SparkFun convention: the repository name matches the library name exactly, with no `_Library` suffix. Existing `_Library` repos retain their names.

The `Project-` prefix for hardware design repos is a NorthernWidget convention — it has no direct equivalent at Adafruit or SparkFun, but clearly distinguishes hardware design repos from software at a glance.

## Arduino Library Manager naming

The `name=` field in `library.properties` follows separate rules from the repo name:

- Use the **generic chip or sensor name** if it is unclaimed in the Arduino Library Manager (no suffix, no prefix).
- Apply the **`NW_` prefix** only if the generic name is already taken.
- Never use a `_Library` suffix in `name=`.

Confirmed conflicts requiring `NW_` prefix: `NW_MCP3421`, `NW_BME280`.

Before finalizing any library name, check the [Arduino Library Manager](https://www.arduinolibraries.info/).

## Version numbering

See [version-numbering-standards](https://github.com/NorthernWidget/version-numbering-standards) for the NorthernWidget versioning scheme (covers combined hardware/firmware repos as well as code-only repos).

Hardware repos (`Project-*`) use a `HWmajor.HWminor.FWversion` scheme where `FWversion` tracks the firmware burned to the sensor's onboard MCU — not the Arduino library version, which is tracked separately in the corresponding `*_Library` repo.

## Releasing

- **Arduino libraries** — see [RELEASING.md § Arduino library](RELEASING.md)
- **Hardware design repos (`Project-*`)** — see [RELEASING.md § Hardware](RELEASING.md#releasing-nw-hardware-project-)
