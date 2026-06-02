# Contributing to NorthernWidget

## Repository naming

| Type | Pattern | Examples |
|------|---------|---------|
| Hardware design | `Project-<Name>` | `Project-Margay`, `Project-Apis` |
| Arduino library (new) | match library name | `NW_BME280`, `Walrus_Library` |
| Arduino library (legacy) | `<Name>_Library` | `Margay_Library`, `MaxBotix_Library` |
| NW tools / specs | `NW-<Name>` | `NW-Device-Specification`, `NW-Provision` |

New library repos follow the Adafruit/SparkFun convention: the repository name matches the library name exactly, with no `_Library` suffix. Existing `_Library` repos retain their names.

## Arduino Library Manager naming

The `name=` field in `library.properties` follows separate rules from the repo name:

- Use the **generic chip or sensor name** if it is unclaimed in the Arduino Library Manager (no suffix, no prefix).
- Apply the **`NW_` prefix** only if the generic name is already taken.
- Never use a `_Library` suffix in `name=`.

Confirmed conflicts requiring `NW_` prefix: `NW_MCP3421`, `NW_BME280`.

Before finalizing any library name, check the [Arduino Library Manager](https://www.arduinolibraries.info/).

## Version numbering

See [version-numbering-standards](https://github.com/NorthernWidget/version-numbering-standards) for the NorthernWidget versioning scheme (covers combined hardware/firmware repos as well as code-only repos).
