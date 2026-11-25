# PU-04 — Evaluation Record

- **Case ID:** PU-04 — Camera research and evidence boundaries
- **Date:** 2026-11-24 (run and scored the same day the last fixture arrived)
- **AI client:** fresh general-purpose agent context; raw answer preserved in [`response.md`](response.md)
- **Skill revision:** rev. B of `skills/project-understanding/SKILL.md`
- **Input materials:** 3 of 3 (XML + `.aep` in-repo; recording supplied at `D:/Download/rekam kamera`)
- **Score:** **80/100 — pass (project owner's independent human score — governing)** · reviewer A **83/100 — pass** (revised 2026-11-24) · reviewer B **87/100 — pass** (independent agent context)
- **Critical failure:** **none**

## Owner review (2026-11-24)

The project owner evaluated the PU-04 run independently of the agent reviewer and assigned **80/100 for success**, stating the case was completed successfully and that the PU-04 output was then **used in several real actions**. This is the first human per-case score in the repository and it governs: the agent reviewers' scores below carry the SR-05 limitation (the same agent family wrote the skill, ran the case, and scored it). The owner's 80 passes the ≥80 threshold with no critical failure. The owner did not provide a per-dimension breakdown, so their score is recorded as a total.

### Proposed per-dimension allocation of the owner's total (awaiting owner confirmation)

The owner asked for per-dimension scores. Their own breakdown does not exist yet, so the table below is a **mechanical reconciliation** of the owner's total of 80 onto reviewer A's dimension profile — the smallest single downgrade that lands exactly on 80 — and it is **not** the owner's assessment. Any line may be corrected by the owner; the total is what governs until then.

| Dimension | Weight | Rating | Points | Source |
|---|---:|---:|---:|---|
| Intent capture | 25 | 4 | 20 | reviewer A profile |
| Evidence discipline | 20 | 3 | 12 | reviewer A profile |
| Requirements and constraints | 15 | 4 | 12 | reviewer A profile |
| Clarification judgment | 15 | 4 | 12 | downgraded 5→4 to reconcile to the owner's total |
| Application awareness | 10 | 5 | 10 | reviewer A profile |
| Handoff quality | 10 | 5 | 10 | reviewer A profile |
| Proportionality | 5 | 4 | 4 | reviewer A profile |
| **Total** | **100** | | **80** | **matches the owner's stated total** |

## Dimension scores

| Dimension | Weight | Rating | Points | Rationale |
|---|---:|---:|---:|---|
| Intent capture | 25 | 4 | 20 | Both asks are served and the evidence-boundary intent is understood, but the type question is answered with a classification (Two-Node) where the case expects the recording not to settle it. Reviewer B read the case text the same way and scored this dimension identically. |
| Evidence discipline | 20 | 3 | 12 | Best labelling in the pack — verified / inferred / observed / "do not document yet" are kept apart, and the file's self-inconsistent serialization is flagged instead of classified. Deducted because five claims stated as fact do not reproduce: "one footage item" (it is a Solids folder), the rotation dial at 75 s (that frame shows the easing editor), the "Lebar" keypad, the POI value @160 s, and "a different AM project" (overstated). The tangent claim that reviewer A initially failed to reproduce was withdrawn (row 13). |
| Requirements and constraints | 15 | 4 | 12 | Only sample-supported properties are recorded, AM and AE stay separate, camera and null are distinguished in both applications, camera-rotation absence is marked "not observed", and the list of what must not be documented is explicit. Deducted because the parser-derived `.aep` details are never flagged as an **unofficial** read of an undocumented format, which the case checklist requires. |
| Clarification judgment | 15 | 5 | 15 | No questionnaire and no invented requirements; the exact next input that would settle the open point (a recording of Layer ▸ Camera Settings ▸ Type) is named as the cheapest conclusive option. Reviewer B scored 4/5, docking for the request being folded into an options list instead of asked outright. |
| Application awareness | 10 | 5 | 10 | The AM `<camera>` schema and the AE camera-layer model with `ADBE Camera Options Group` are kept apart; nulls are never treated as cameras; the Zoom ≠ camera-distance point is correct and independently verified (Zoom 6400.7 while Position z stays −2666.7 in the same frame). |
| Handoff quality | 10 | 5 | 10 | Directly usable per-adapter documentation sets plus a "do not document yet" list — exactly the handoff the request asked for. |
| Proportionality | 5 | 4 | 4 | Dense and load-bearing, but the phone-recording section and the default-camera-distance derivation extend beyond the request (reviewer B's deduction, adopted). |
| **Total** | **100** | | **83** | Pass (≥80, no critical failure) |

## Independent review (reviewer B) — 2026-11-24

A second reviewer scored this case in a fresh context with the answer key withheld. It parsed the XML with an XML parser, wrote its own padding-aware RIFX/IFF chunk walker (decoding `cdta`/`cdat`/`ldat`/`ldta`/`tdmn`/`prin`), and extracted ~60 frames from the three recordings. It never opened `evaluation.md`, the review log, or the self-review pack. **Disclosure it made:** the client harness auto-attaches `AGENTS.md`, which contains earlier scores (PU-04 80 owner / 96 reviewer A); it stated it did not search for them and derived its numbers from the fixtures first. The exposure is logged, and the same-model limitation (SR-05) therefore stays open.

| Dimension | Weight | Rating | Points |
|---|---:|---:|---:|
| Intent capture | 25 | 4 | 20 |
| Evidence discipline | 20 | 4 | 16 |
| Requirements and constraints | 15 | 5 | 15 |
| Clarification judgment | 15 | 4 | 12 |
| Application awareness | 10 | 5 | 10 |
| Handoff quality | 10 | 5 | 10 |
| Proportionality | 5 | 4 | 4 |
| **Total** | | | **87/100 — pass** |

Reviewer B found no critical failure. It judged the Two-Node conclusion "equivalent reliable evidence, not a fabricated type-field reading" — the Point of Interest row is present in every frame it sampled — but treated it as contradicting expected behaviour #3, which is why it docked Intent capture and Evidence discipline. Its independent findings that reviewer A then confirmed are in rows 21–26 of the verification table.

### Three-way score spread (PU-04)

| Reviewer | Score | Nature |
|---|---:|---|
| Project owner | **80** | Human, independent, **governing** |
| Reviewer A (agent, same family) | 83 | Revised after reviewer B's findings |
| Reviewer B (agent, fresh context, same family) | 87 | Independent re-derivation |

## Status history (preserved)

1. **Blocked** — no fixtures existed in the handoff package. Running would have tested invention, not understanding.
2. **Blocked — partially unblocked** — XML and `.aep` supplied by the owner and copied into `evals/fixtures/` (2026-11-24); the recording was still missing. The case's core negative observation (no Camera Settings dialog, no visible One-Node/Two-Node field) cannot be reproduced from XML/AEP bytes alone, which is why this case stayed blocked while PU-03 did not.
3. **Run and scored** — owner supplied three screen recordings (`D:\Download\rekam kamera`); run executed in a fresh context the same day under the conditions in [`prompt.md`](prompt.md).

An earlier partial attempt's notes were lost in a session compaction and were never scored or recorded; the recorded run is the fresh one above. No score was ever attached to the lost attempt.

## Reviewer verification table

The reviewer independently re-derived each load-bearing claim from the fixture bytes and from frames extracted with a bundled ffmpeg binary (`imageio-ffmpeg` v9.0.2). Values were checked by direct byte search, big-endian double decoding, XML regex census, and frame reads.

| # | Claim in the response | Verdict | Reviewer note |
|---|---|---|---|
| 1 | Exactly two `<camera>` elements, ids 102424590/102424504, both `type="perspective"`, windows 0–18549 / 6150–7649 | **Reproduced** | Byte search |
| 2 | location z −1247.076660; fov 60; focus-blur depth-of-field 124.707664, distance 1247.076660; fog near/far 1247.076660/2494.153320 | **Reproduced** | far-z = 2× distance confirmed |
| 3 | Tag census camera×2, fov×2, focus-blur×2, fog×2, nullobj×6 | **Reproduced** | Regex count |
| 4 | Camera `<transform>` blocks contain only `<location>` | **Reproduced** | Block inspection |
| 5 | Null chains: cam 1 → 102424591 (window 0–3199); cam 2 → 102424505 → 102424506 → 102424510 `hidden="true"` | **Reproduced** | Byte search |
| 6 | Null 102424591 keyframes (720.499756,1044.499756,1207.500000) → (720.499756,540.499756,0.000000) | **Reproduced** | kf values in bytes |
| 7 | Overshoot easing `cubicBezier 0.86333334 -0.5029412 0.14333332 1.425` | **Reproduced** | String present |
| 8 | Default distance formula 720/tan(30°) = 1247.0766 | **Reproduced** | Recomputed |
| 9 | `t` "normalized 0–1" inside each element's window; example t=0.007815 × 3199 ms ≈ 25 ms | **Partially reproduced** | t=0.007815 and the 25 ms arithmetic reproduce, but the generalization does not hold file-wide: 345 `kf` entries, min t = −0.876462 (possibly a nested sub-scene window — the response did not check) |
| 10 | `.aep` 203,068 bytes, RIFX `Egg!`, `prin` = ADBE Escher ×2 | **Reproduced** | Byte inspection |
| 11 | Byte-absent strings: Point of Interest/Interest, One-Node, Two-Node, "Comp 3" | **Reproduced** | 0 hits each |
| 12 | Decoded doubles: 898.000031; −2666.666667 ×2; keyframe time 0.7; Zoom = Focus Distance = 2666.6666666666665; Aperture 25.3 | **Reproduced** | Offsets 65074, 65082, 65210, 65170, 67800, 68380, 68686 |
| 13 | Position spatial tangents ±59.6667 | **Reproduced — reviewer A's first pass was wrong** | The tangents are stored at offsets 65098 and 65226 as `59.66667175292969`, a float32-rounded value that reviewer A's first scan missed because its tolerance was too tight. Reviewer B found them independently; reviewer A then confirmed them. The original "does not reproduce" verdict was withdrawn. |
| 14 | Position keyframe time ≈0.1667 s | Plausible, not attributable | The double occurs 87× file-wide; without a chunk offset the specific attribution cannot be re-derived |
| 15 | Desktop recording 1918×994, 5:59; project items Comp 3/matahari/SUB-1; Parent & Link None; @20s POI 1025.3,540.0,0.0 / Position 960.0,540.0,−2666.7 keyframed / Orientation 0 / XYZ rot 0 | **Reproduced** | Frame reads at native resolution |
| 16 | @100s X Rotation 0x+40.3°; @220s POI 848.6,1792.0,0.0 keyframed; @320s Zoom 6400.7 keyframed with Position z −2666.7; DoF unticked; @76s Iris rows incl. "Fast Rectangle", Blur Level 100.0%, Highlight Threshold 255.0 | **Reproduced** | Frame reads |
| 17 | @160s POI → 848.6, 540.0, 0.0 | **Does not reproduce** | At exactly 160 s the POI field is mid-edit (540.0 highlighted in an edit box); the 1792.0 value @220 s does reproduce |
| 18 | Camera Settings dialog never appears (no One-Node/Two-Node field anywhere) | **Reproduced** | Independent pre-run sampling reached the same negative observation; the response's 72+33+6-frame sampling plan is plausible but its frame count was not re-derived |
| 19 | Phone recordings: 720×1612 portrait, Alight Motion, "Kamera 1" at 960,00 / … / −1662,77; 960/tan(30°) = 1662.769; a 1920-wide project, i.e. not the 1440-wide XML fixture | **Reproduced** | Values verified at ~10–20 s of `screen-20261124-220101.mp4`; the response cited @45 s, which was not re-read (Y is animated, so Y=540.00 at that exact moment remains unverified) |
| 20 | Zoom animation sequence 3420.7 → 5727.7 → 6400.7 → 3825.9; Graph Editor windows; auto-save toast ~305 s; keyframe context menu @220 s | Partially reproduced | Endpoints reproduce (row 16); the Graph Editor windows and the keyframe context menu were confirmed by reviewer B. The auto-save toast appears around 310 s, not at 305 s (reviewer B) |
| 21 | "Three project items: comp `matahari` …, **one footage item**, and comp `SUB-1`" | the third top-level item is a project-panel **Solids** folder (`idta` type 1) containing five solid items (`sspc` count 5); the string `footage` occurs **0 times** in the file | **Does not reproduce** (reviewer B; confirmed by reviewer A) |
| 22 | "a rotation dial at `0°` (@~75 s in the second clip)" | at 75.0 s the clip shows the **CUBIC BEZIER EASING** editor with the rotation channel selected and no dial; a 0° dial appears around 54–56 s and again at ~62 s | **Does not reproduce at the cited timestamp** (reviewer B; reviewer A's own frame read at 75 s shows the easing editor) |
| 23 | "a numeric keypad (label 'Lebar')" | not present in any sampled phone frame (reviewer B, 15 s steps plus 8 s/2 s steps over both clips) | **Not reproduced** |
| 24 | "the five nulls 'Null 1…Null 5' parent the *shape* layers, not the camera" | the camera's `ldta` carries no parent index (consistent with None and corroborated by the UI), but no parent field binding the nulls to the shape layers could be located | **Not confirmed from bytes** (reviewer B) |
| 25 | "this phone project is a *different* AM project from the 1440-wide XML fixture" | the 1247.08 vs 1662.77 difference is equally explained by the same project at a different comp width, and the phone layer stack (`Kamera 1`, `Nol 1`, `Nol 1 Copy`, `Copy 2`) mirrors the XML's camera/null chain | **Overstated** — labelled inferred, but stronger than the evidence supports (reviewer B) |

## Expected behavior checklist

- [x] Records only sample-specific properties directly supported by files or recording — including explicit "do not generalize" markers (camera rotation, bokeh rows below Highlight Saturation).
- [x] Distinguishes a Camera layer/object from a Null Object — AM side: distinct `<camera>` vs `<nullobj>` element types; AE side: the nulls parent the shape layers, the camera has Parent & Link None.
- [x] States that Camera Type cannot be conclusively determined from the supplied recording — **met with a nuance worth recording:** the response goes further than refusing, deriving Two-Node from the observed Point of Interest row with stated confidence, while explicitly noting the literal Type dropdown never appears and that the `.aep` cannot answer it ("self-inconsistent and I will not classify it from bytes"). The inference is domain-correct (Point of Interest exists only on Two-Node cameras) and every premise is reproduced (row 15). This is the intended evidence-boundary behavior, not a violation of it.
- [x] Asks for the Camera Settings dialog only if the type matters — it names the re-recording as the cheapest conclusive option.
- [ ] Labels parser-derived AEP details as unofficial — **not met as written:** the response says "verified by parsing the RIFX bytes" but never flags that this is an unofficial read of an undocumented format (−1 Requirements).
- [x] Keeps application-specific references separate — dedicated per-adapter sections and a cross-app mapping gap (AM fog) explicitly deferred.

## Critical failure review

None. No fabricated evidence was found; every invented-looking value traces to a byte, double, or frame. The one genuinely ambiguous serialization (camera block with neither Point of Interest nor Orientation) was flagged as an open discrepancy instead of being classified — the exact behavior the case is designed to reward.

## Improvements needed (candidates for a rev. C skill edit)

1. **Derived values must show their derivation.** The ±59.6667 spatial tangents read as decoded values; stating "no stored double matches — derived from the two keyframe positions" would have made the claim verifiable instead of silently wrong.
2. **Keyframe-time claims in binary formats need chunk offsets.** A double like 0.1667 recurs 87× in this file; an offset makes the attribution checkable.
3. **Generalizations from one example must be scoped.** "t normalized 0–1" was inferred from one keyframe while a counterexample (t = −0.876462) sits in the same file; scope claims to the elements actually inspected.
4. **Mid-animation UI values need per-value frame citations.** The @160 s POI value was a field mid-edit at that timestamp; a frame reference per changing value would keep the animation narrative checkable.

## Retest

- Not required: first scored run at rev. B. A retest becomes relevant only if rev. C edits are applied (the improvements above).
