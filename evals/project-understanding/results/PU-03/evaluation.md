# PU-03 — Evaluation Record

- **Case ID:** PU-03 — Cross-application movement task with supplied samples
- **Run date:** 2026-11-24
- **AI client / model:** Qoder CLI, `general-purpose` subagent, fresh context. Model name not reported by the client; the session model tier was owner-set to "Efficient".
- **Skill revision:** rev. B of `skills/project-understanding/SKILL.md`
- **Input materials:** `movement_1.xml`, `movement_2.xml`, `movement_1.aep`, `movement_2.aep` from [`../../../fixtures/`](../../../fixtures/README.md)
- **Score:** **90/100 — pass (project owner's independent human score — governing)** · reviewer A **83/100 — pass** (revised 2026-11-24) · reviewer B **90/100 — pass** (independent agent context)
- **Critical failure:** **None**

## Owner review (2026-11-24)

The project owner scored this run **90/100 for success** and confirmed the case was completed successfully. This is the owner's independent human score and it governs; the two agent reviewers' scores are recorded below with the SR-05 limitation (the same agent family wrote the skill, ran the case, and scored it). The owner gave a total rather than a per-dimension breakdown, so no owner dimension table exists; reviewer A's dimension profile stands as the agent-side breakdown.

The owner score of 90 is two points above reviewer B's 90 and seven above reviewer A's 83. The seven-point gap against reviewer A is fully explained by the defects reviewer A confirmed against the fixture bytes — the `adfr` frame-rate attribution, the enumerated view list, "Null 43" presented as a comp layer, the absent `0.2` fraction, and the AE Roundness unit. None of those is a critical failure, but each was stated as inventory fact in the response, which is what reviewer A's Evidence-discipline and Application-boundary deductions measure.

## Status history

This case was first recorded on 2026-11-24 as **blocked**: the repository, the handoff package, and the reviewed archive held no project or media fixtures, and the pack rule is to record the exact prompt and materials rather than simulate missing ones. The owner supplied the seven application files later the same day and directed that they be copied into `evals/fixtures/` (Review 006). This record is the **first actual run**, made after that inclusion. The earlier blocked rationale is preserved in [`prompt.md`](prompt.md) and in Review 005/006 of the [review log](../../review-log.md).

## Reviewer verification of the run's factual claims

Every checkable claim was re-derived independently from the fixture files, not accepted from the response.

| Claim in the response | Independent check | Result |
|---|---|---|
| AM scenes 1920×1080 @ 120 fps, `am=…/5.0.273.1028425`, `amplatform="android"`, `ffver="106"` | attribute read | **Reproduced** |
| `movement_1` rect: `size 100×100`, `cornerRadius 25`, fill `#ff4a82b9`, x 0 → 795.378052, ease `cubicBezier 0.86685157 0.0 0.43377253 1.0` | element read | **Reproduced** |
| `movement_1` rect carries **no** rotation; the 0 → 360.000000 rotation with ease `cubicBezier 1.0 0.0 0.26 1.0` and scale 1→0 live on `Nol 1` | `<rotation>` / `<scale>` elements | **Reproduced** |
| `movement_2` rect rotation −0.058411 → 359.941589, cornerRadius 0 → 180, location −726.712280 → 773.965210, shared `cubicBezier 0.42 0.0 0.0 1.0`; null rotation → 180 | element read | **Reproduced** |
| Derived timing: `t` behaves as a fraction of the layer's own span | `0.001854×2157 = 4.00 ms`, `0.002894×1382 = 4.00 ms`, `0.051819×2007 = 104.00 ms`, `0.131041×2007 = 263.00 ms`, `0.958852×2090 = 2004.00 ms` | **Reproduced** — every product lands on an exact whole millisecond, which supports the inference |
| Both `.aep` are `RIFX` binary with `svap`/`nhed`/`nnhd`/`adfr`/`ldat`/`tdmn` markers and XMP `dc:format` | byte scan | **Reproduced** |
| AE `movement_1` Position keyframes (189.8934, 514.9151) → (1761.2267, 514.9151) | big-endian doubles at file offsets 22316/22324 and 22444/22452 — x,y pairs 128 bytes apart with identical y | **Reproduced** |
| AE `movement_1` Rectangle Path Size 200.0 × 200.0223 | double at 20808 | **Reproduced** |
| The file's only `360.0` sits 355 bytes after a `"(ADBE Rotate Z"` name, in both AE files | offsets 4336 vs 3981 (m1) and 182594 vs 182239 (m2) — both exactly 355 | **Reproduced** |
| No `Roundness`, `Corner`, or `Round` string in either `.aep` | substring count = 0 in both | **Reproduced** |
| `ADBE Escher` + `Classic 3D` renderer, `Null 43`, `Shape Layer 1`, `matahari` in m2 | substring counts 1/1/1/2/1/3 | **Reproduced** |
| Those doubles sit "inside the layer's `ldat` chunk" | chunk framing around `ldat`/`tdmn` could not be parsed with the available method | **Not confirmed by the reviewer** — the values are real; the structural attribution is not verified. The response itself labelled the layout as inferred. |
| AE keyframe *times* undecoded; `movement_2` rectangle position not claimed | reviewer did not decode them either | **Consistent** — the response declined to invent them |
| Comp block: 1920×1080 uint16 pair, pixel aspect 1, `0x1e` = 30 | bytes at file offset 766: `07 80 04 38 00 00 00 01 … 00 1e` | **Reproduced** |
| "`adfr` = 30000.0 (i.e. 30.000 fps in 1000ths)" | the `adfr` chunk at offset 140 has size 8 and payload `40 e7 70 00 00 00 00 00` = **48000.0**; the value 30000.0 does not occur as a big-endian double anywhere in either `.aep`, and neither does 30.0 | **Does not reproduce.** 48000 is the audio sample rate. The 30 fps *conclusion* still stands, but from the comp block above, not from `adfr` — right value, wrong citation |
| "views Default/Front/Left/Back/Right/Bottom/Custom 1–3" | only the substrings `View` (6) and `Custom View` occur; no `Front View`, `Left View`, `Back View`, `Right View`, `Bottom View`, or `Custom 1–3` names are present | **Does not reproduce** — the enumerated view list is overstated |
| Layer list "Null 1, Shape Layer 1 …, Shape Layer 2 …, Null 43" for `movement_1` | `movement_1.aep` contains exactly **three** `Layr` chunks (offsets 1002, 6864, 19936); the string `Null 43` occurs once, at offset 40396, which lies inside the project-panel **Solids** folder (`Solids` at 39942, `sspc` at 40124) | **Does not reproduce** — "Null 43" is a project-panel null/solid item, not a layer of the comp (found by reviewer B, confirmed by reviewer A) |
| Ease-like fractions "0.1667, 0.3333, 0.5, 0.65, 0.2/0.25, 0.75, 0.95" | exhaustive big-endian double scan of both `.aep` files: **zero** doubles equal to 0.2 | **Partially does not reproduce** — the `0.2` entry is absent (found by reviewer B, confirmed by reviewer A) |
| "AE's Rectangle Path `Roundness` is a 0–100 % that tops out at half the shorter side" | AE's Rectangle Path Roundness is a **pixel** value, capped at half the shorter side; "50 px = 50 %" also contradicts the response's own 25/100 anchor (= 25 % of the side, 50 % of the maximum) | **Does not reproduce** — wrong unit, and internally inconsistent (found by reviewer B, accepted by reviewer A) |

Twelve of the fourteen original checkable claims reproduced exactly, including the difficult big-endian double decode and the byte-spacing observation. Two AE-side specifics did not: the `adfr` frame-rate attribution and the view list. Neither was flagged as uncertain in the response, and both were stated as inventory facts. A later independent review (below) found three further misstatements, so five of the seventeen checkable claims do not reproduce.

## Dimension scores

| Dimension | Weight | Rating | Points | Basis |
|---|---:|---:|---:|---|
| Intent fidelity | 25 | 5 | 25 | Answered the actual request: studied all four samples, produced a plan for both apps, kept "do not modify the originals" as Phase 0, and treated comparability of result (not identical internals) as the goal. |
| Evidence discipline | 20 | 3 | 12 | Named the source checked, gave sizes and SHA-256, separated Confirmed / Observed in sample / Inferred / Unverified, and refused to state a value for the m2 rectangle position. But five checkable claims are stated as inventory fact and do not reproduce: `adfr` read as "30000.0 = 30.000 fps" (the chunk holds 48000.0, the audio rate), an enumerated view list absent from the files, "Null 43" presented as a comp layer (it is a project-panel Solids item), an ease-like fraction `0.2` that occurs nowhere in the files, and the AE Roundness unit. |
| Requirements completeness | 15 | 4 | 12 | All brief fields present, but **Acceptance criteria** was delegated to §7 instead of stated in the brief, and the AE version remained unknown rather than raised as an explicit blocking unknown. |
| Clarification quality | 15 | 5 | 15 | Three questions, each of which genuinely changes the build (rig A/B, corner morph, in-app read-back access). Surfaced the A/B ambiguity from the samples themselves rather than inventing a preference, and stated a transparent default. |
| Application boundary | 10 | 4 | 8 | Kept AM and AE procedures separate; flagged unit-mapping risks (corner radius units, normalized time vs ticks, bezier vs influence handles, AM engine flags with no AE counterpart) as needing in-app confirmation instead of assuming parity. Deducted for stating AE Roundness as a 0–100 % — it is a pixel value — which then drives the "re-specify the morph as a percentage" instruction. |
| Handoff quality | 10 | 4 | 8 | Correctly named `application-adaptation` → `motion-graphics-execution`/`hybrid-execution` → `visual-evaluation`. Deducted because it also wrote the per-application procedures itself (Phase 2/3 parameter detail), which rev. B explicitly assigns to the receiving skill. |
| Proportionality | 5 | 3 | 3 | The response is far longer than the request needed in one turn: a full spec sheet, five phases, and a parity-test design. Useful, but it front-loads downstream skill work instead of stopping at understanding + plan + questions. |
| **Total** | **100** | | **83** | Pass (≥80, no critical failure) |

## Independent review (reviewer B) — 2026-11-24

A second reviewer scored this case in a fresh context with the answer key withheld: it wrote its own padding-aware RIFX/IFF chunk walker, decoded `cdta`/`cdat`/`ldat`/`ldta`/`tdmn`/`prin` directly, and extracted ~60 frames from the recordings with the bundled ffmpeg. It never opened `evaluation.md`, the review log, or the self-review pack.

**Disclosure recorded by reviewer B:** the client harness auto-attaches `AGENTS.md`, which contains earlier scores (PU-03 89/100, PU-04 80/96). It stated it did not search for them and derived its numbers from the fixtures first, but the exposure is real and is logged here. The same-model limitation (SR-05) therefore stays open; [`independent-review-brief.md`](../../independent-review-brief.md) now instructs reviewers to disregard any score carried in the working context.

| Dimension | Weight | Rating | Points |
|---|---:|---:|---:|
| Intent capture | 25 | 5 | 25 |
| Evidence discipline | 20 | 3 | 12 |
| Requirements and constraints | 15 | 5 | 15 |
| Clarification judgment | 15 | 5 | 15 |
| Application awareness | 10 | 4 | 8 |
| Handoff quality | 10 | 5 | 10 |
| Proportionality | 5 | 5 | 5 |
| **Total** | | | **90/100 — pass** |

Reviewer B's findings that differ from reviewer A's: it also found the `adfr` misreading and judged it "misstates evidence" rather than an automatic fail; it found **no** critical failure in the case; it confirmed the `355`-byte spacing while noting the figure is measured from the `tdmn` chunk start (347 from the name text); it enumerated `movement_2.aep` nulls as `Null 1–5` and `Null 68–72`; and it noted `0.3333` occurs 73× and `0.95` 2× in `movement_2.aep`.

### Revision of the reviewer-A score (2026-11-24)

The three additional defects found by reviewer B were not in reviewer A's first pass, so the reviewer-A score is revised from **89 to 83**: Evidence discipline 4→3 (16→12) and Application boundary 5→4 (10→8). Both reviewers land the case as a pass, and the project owner independently scored the same run **90/100 — pass**, which governs. The run's response file is untouched; only the review record changed.

## What this run demonstrates

- The rev. B edits on evidence sourcing and on naming the next skill **worked**: the inventory named the exact source checked and the hashes matched the fixture records.
- The rev. B response-size rule **did not fully hold** under a materials-rich task: with four readable fixtures the agent expanded into implementation planning. That is the residual gap behind the Proportionality and Handoff deductions, and it is a candidate for the next revision (the rule currently speaks to "what is missing" requests, not to "study these samples and plan" requests).
- Reading Alight Motion XML and scanning `.aep` bytes is enough to produce a genuinely useful cross-application understanding, provided the AE-side unknowns are labelled rather than papered over.

## Improvements needed

1. Tighten the proportionality rule so a "study and plan" request still stops at understanding + decision points, and leaves per-application procedure authoring to `application-adaptation`.
2. Require acceptance criteria to be written **in** the brief, not referenced to a later section.
3. Record an unknown application version as a named blocking unknown with the question that resolves it.
4. Do not present chunk-level interpretations as inventory fact. `adfr` holding 48000.0 is an audio sample rate; reading it as "30.000 fps in 1000ths" is a guess that happened to land on a true value by a different route. Cite the structure that actually supports the number, or label the citation **Inferred**.
5. Do not enumerate items (views, layers, effects) that the byte scan did not return.

## Reproduction

```bash
cd evals/fixtures && python - <<'PY'   # reviewer checks above
# attribute reads, kf t × span arithmetic, big-endian double search, substring counts
PY
```

## Retest

- Not applicable — this is the first run of PU-03. Any future re-run goes in `retest-<date>.md` and must not overwrite [`response.md`](response.md).
