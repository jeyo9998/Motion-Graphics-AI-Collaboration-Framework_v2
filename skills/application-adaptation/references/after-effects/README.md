# After Effects Reference — Status: Scaffolding Only

**No verified application procedures are recorded here yet.**

This directory is reserved for evidence-backed Adobe After Effects knowledge. Add records only from verified sources, using [`../EVIDENCE-TEMPLATE.md`](../EVIDENCE-TEMPLATE.md).

## Current state

- Application version: **unknown**
- Platform: **unknown** (Windows/macOS differences must be recorded separately)
- Scripting/API interface: **not verified in this repository**; do not claim ExtendScript or UXP support for a version without a source
- Project-file format: `.aep` is a binary project format and must **not** be treated as plain XML or text
- Unofficial parser observations: must be labelled as unofficial and sample-specific

## Known evidence boundary

PU-04 references an After Effects camera AEP inspected with an unofficial, read-only parser and a screen recording that does not show the Camera Settings dialog or a One-Node/Two-Node field. Those materials are not present here. Do not state a camera type from this repository's contents.

## Open questions

- Which After Effects version(s) are targeted for the first benchmark?
- Which scripting interface is available and documented for those versions?
- Which native preview/render checks can be performed in the available environment?
- Which project settings materially affect cross-application parity?

## Adding evidence

1. Copy a record from the evidence template.
2. State the exact version and build.
3. Identify the evidence type and source.
4. Keep parser-derived output labelled unofficial.
5. Never present an inferred capability as documented behavior.

## Related

- [`../../SKILL.md`](../../SKILL.md) — application adaptation workflow
- [`../alight-motion/README.md`](../alight-motion/README.md)
