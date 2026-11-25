# PU-03 — Re-run 2026-11-24 (rev. C skill)

- **Case:** PU-03 — Cross-application movement task with supplied samples (verbatim from `../../cases.md`)
- **Run date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/project-understanding/SKILL.md` at **rev. C** — the 2026-11-24 edits recorded in Review 008 (Technical evidence discipline: derived values show their derivation, binary values cite chunk/offset, generalizations scoped to what was inspected, changing recording values cite a frame timestamp). 231 lines; no version field in the file; the revision is also identifiable as commit `9fff40c`. The 83/100 (reviewer A), 90/100 (reviewer B) and **90/100 (project owner, governing)** records cover rev. B.
- **Materials supplied:** the four movement fixtures only — `alight-motion/movement_1.xml`, `alight-motion/movement_2.xml`, `after-effects/movement_1.aep`, `after-effects/movement_2.aep`
- **Procedure:** fresh agent context; the skill was read from the repository path; the agent was told not to open `cases.md`, `scorecard.md`, `review-log.md`, `independent-review-brief.md`, `evals/fixtures/README.md` or any `results/` folder; it was told to disregard any score arriving with its working context; the exact prompt below was submitted; no coaching and no follow-up occurred.
- **Score:** **89 / 100** (previous revision: **90/100 owner — governing** / 90 reviewer B / 83 reviewer A). The owner's 90 was set against rev. B and is unchanged; this rev. C number is reviewer A's dimensional assessment, added alongside it, not substituted for it.
- **Critical failure:** **No**

### Protocol note — one discarded attempt

A first rev. C attempt was started and then **discarded without being scored**. Two protocol deviations made it unusable: the prompt had been paraphrased instead of quoted verbatim from `cases.md`, and the prompt itself restated the evidence-discipline rules that the case was supposed to test, which counts as coaching. Neither the prompt nor the response of that attempt is preserved, because a run that violates the protocol produces no admissible evidence. The run recorded below was executed from scratch under the standard conditions.

## User prompt

> I want a rounded rectangle to travel horizontally across the composition while rotating once. Make the creative result comparable in Alight Motion and After Effects. I have supplied two Alight Motion XML movement samples and two After Effects AEP movement samples. Study them and prepare a plan for implementing the same motion in both applications. Do not modify the originals.

## Raw response

# Project Understanding Brief — "Sweep-and-Spin" Rounded Rectangle (Alight Motion + After Effects)

## 1. Objective and intended outcome

**Objective.** Build the same motion — *a rounded rectangle travelling horizontally across the composition while rotating exactly once* — as two separate, comparable builds: one in **Alight Motion**, one in **Adobe After Effects**, using the four supplied samples as the motion reference.

**Intended outcome.** Two editable native projects that a viewer could not distinguish in motion terms: the same subject (rounded rectangle), the same trajectory (straight horizontal line, constant height), the same total spin (one full 360° turn), the same start/end times for travel and rotation, and the same normalised ease curve — even though the two applications express each of these differently.

**Target applications.** Both, each with its own implementation path. Alight Motion version observed in the samples: `5.0.273.1028425` (Android export) — see `evals/fixtures/alight-motion/movement_1.xml` header comment. After Effects version: **unknown** (not recorded in the `.aep` files in a form I could verify).

---

## 2. Materials: inventory and inspection status

Inspected read-only. **No supplied file was modified**; analysis scripts were written to a system temp directory, not into the repository.

| File | Size | Status | What it yielded |
|---|---|---|---|
| `evals/fixtures/alight-motion/movement_1.xml` | 3,115 B | **Inspected** (plain-text XML, full read) | Scene "Proyek Baru 94", 1920×1080, `fps="120"`, `totalTime="3448"`, `bgcolor="#ff000000"`; layers: shape `300071272` "Persegi Panjang Bulat 1" (rounded rectangle) parented to null `300071273` "Nol 1"; shape `300071274` "Lingkaran 1" (circle) |
| `evals/fixtures/alight-motion/movement_2.xml` | 1,940 B | **Inspected** (full read) | Scene "Proyek Baru 95", 1920×1080, `fps="120"`, `totalTime="2090"`; shape `300071275` "Persegi Panjang Bulat 1" parented to null `300071276` "Nol 1" |
| `evals/fixtures/after-effects/movement_1.aep` | 45,416 B | **Inspected** with an *unofficial* Python RIFX chunk reader (no After Effects available) | Comp `Comp 1`; layers `Null 1`, `Shape Layer 2` (ellipse), `Shape Layer 1` (rect); keyframed `ADBE Position`, `ADBE Rotate Z`, `ADBE Scale` |
| `evals/fixtures/after-effects/movement_2.aep` | 197,708 B | **Inspected** with the same reader | Comps `matahari` (Shape Layer 7/9/8/6) and `SUB-1` (Null 1–5, Shape Layer 1–5); 8-keyframe bouncing Position path on `Shape Layer 4`; 13-keyframe non-uniform Scale |
| `evals/fixtures/alight-motion/Motion_Graphics_unik.xml`, `after-effects/Motion_Graphics_Unik.aep`, `…_Camera.aep` | — | **Present, not inspected** (outside the scope you gave) | — |
| `skills/application-adaptation/references/{alight-motion,after-effects}/README.md` | — | **Inspected** | Both state: *"No verified application procedures are recorded here yet"*; `.aep` must not be treated as XML/text; parser output must be labelled unofficial |

Classification: the four supplied files are **reference material** (movement samples), not the target project. No editable target project for this motion exists yet in either application.

---

## 3. What the Alight Motion samples actually encode (authoritative source)

The XML is fully readable, so it is the reliable reference. All values below are read directly from the file.

### 3.1 A time model, derived and then verified

`startTime` / `endTime` / `totalTime` are **frames at the scene's `fps`** (120), and a keyframe's `t` is a **fraction of that layer's own lifetime** (`endTime − startTime`), not a scene-absolute time.

Derivation (shown for one keyframe, then confirmed on all 12 keyframes in the two files):

- `movement_2.xml`, shape `300071275`: lifetime = 2090 − 0 = 2090 frames.
 `t = 0.001914` → 0.001914 × 2090 = **4.0003 → frame 4**; `t = 0.958852` → 0.958852 × 2090 = **2004.0007 → frame 2004**.
- `movement_1.xml`, null `300071273`: lifetime = 2448 − 291 = 2157 frames.
 `t = 0.001854` → 3.9991 → **frame 295**; `t = 0.484933` → 1046.0005 → **frame 1337**.
- `movement_1.xml`, shape `300071272`: lifetime = 2007 frames → **frames 104 → 1254** (`0.051819`, `0.624813`).
- `movement_2.xml`, null `300071276`: lifetime = 1382 frames → **frames 712 → 1546** (`0.002894`, `0.606368`).
- `movement_1.xml`, circle `300071274`: lifetime = 2007 frames → frames 1704, 2337, 2837, 3420 (listed out of order in the file: 0.131041, 0.986049, 0.695566, 0.446437 → 1704, 3420, 2837, 2337).

Every one of the 12 keyframe times lands on an integer frame to within 0.001 frame — that consistency is what supports the model. *Status: Observed in sample + arithmetic derivation (not vendor documentation).*

### 3.2 The two movement samples

**`movement_1.xml` — "translate the shape, rotate the parent null"** (this is the closest match to the brief):

| Element | Value |
|---|---|
| Rounded rectangle `Persegi Panjang Bulat 1` | size `100.000000,100.000000`, `cornerRadius 25.000000`, fill `#ff4a82b9` (=#4A82B9), no stroke |
| Its `location` | `0.000000,0.000000,0.000000` @ frame 104 → `795.378052,0.000000,0.000000` @ frame 1254, ease `cubicBezier 0.86685157 0.0 0.43377253 1.0` |
| Parent null `Nol 1` (type `perspective`) | location fixed at `960.000000,540.000000,0.000000` = frame centre |
| Null `rotation` | `0.000000` @ frame 295 → `360.000000` @ frame 1337, ease `cubicBezier 1.0 0.0 0.26 1.0` → **one full turn** |
| Null `scale` | `1.000000,1.000000` → `0.000000,0.000000` over the same two frames, ease `cubicBezier 0.42 0.0 0.58 1.0` → shrink-out |
| Second element `Lingkaran 1` (circle) | present frames 1441–3448; vertical bounce 540 → 997.35 → 78.81 → 540 with a size morph |

**`movement_2.xml` — "the shape does both"** (travel *and* spin locked to the same interval):

| Element | Value |
|---|---|
| Rounded rectangle `Persegi Panjang Bulat 1` | size `100.000000,100.000000`; `cornerRadius` **animated 0 → 180** (square→circle morph), ease `cubicBezier 0.42 0.0 0.0 1.0`; fill `#ff464dfe` (=#464DFE); white stroke, `size 12.500000`, centred |
| Its `location` | `-726.712280,0.000000,0.000000` @ frame 4 → `773.965210,0.000000,0.000000` @ frame 2004, ease `cubicBezier 0.42 0.0 0.0 1.0` |
| Its `rotation` | `-0.058411` → `359.941589` over the **same two frames**, same ease → **one full turn, synchronised with the travel** |
| Parent null `Nol 1` | at `960,540`; `rotation` `0` @ frame 712 → `180` @ frame 1546, ease `cubicBezier 1.0 0.0 0.26067954 1.0` (a *second*, counter-spin — **excluded from the shared spec**, see §5) |

Derived world-space travel of `movement_2` (null at 960 + local X): **233.288 px → 1733.965 px**, i.e. **12.15 % → 90.31 %** of a 1920-wide frame; total travel 1500.677 px = 78.16 % of frame width.

---

## 4. What the After Effects samples encode (unofficial parse)

The `.aep` files are RIFX (big-endian) chunked binaries; names live in UTF-8 chunks (`Utf8`) and property names in `tdmn` chunks; keyframe data in `ldat` chunks preceded by `lhd3`. Everything in this section is **Observed in sample via an unofficial parser**, not vendor documentation.

**`movement_1.aep`, comp `Comp 1`:**

- Layers: `Null 1`, `Shape Layer 2` (`ADBE Vector Shape - Ellipse`, `ADBE Vector Ellipse Size` = 200, 200), `Shape Layer 1` (`ADBE Vector Shape - Rect`, `ADBE Vector Rect Size` = 200, 200.0223). Both shapes carry `ADBE Vector Graphic - Fill` with `ADBE Vector Fill Color` = (255, 63.75, 140.25, 255) → normalised (1.00, 0.25, 0.55, 1.00) = **#FF408C** *(derivation: divide each stored component by 255)*.
- Keyframed properties: `ADBE Position`, `ADBE Rotate Z`, `ADBE Scale`. Static: `ADBE Rotate X`/`Y` = 0, `ADBE Anchor Point`, `ADBE Time Remapping` present on `Null 1`.
- Decoded keyframe values (the value triplet sits at doubles 6–8 of a 15-double record for 3-D properties and the value is the first double of a 5-double record for 1-D properties — a rule that is self-consistent across every record inspected in both files, but is **not** a confirmed format description):

| Layer / property | From → to |
|---|---|
| `Null 1` Position | (960, 540) → (238.667, 540) — ΔX −721.333 |
| `Null 1` Rotate Z | 0° → **360°** |
| `Shape Layer 2` (ellipse) Position | (−669.333, 50) → (52.000, 50) — ΔX +721.333 |
| `Shape Layer 1` (rect) Position | (189.893, 514.915) → (1761.227, 514.915) — ΔX +1571.334 |
| `Shape Layer 1` Scale | (100 %, 100 %, 100 %) → (0 %, 0 %, 100 %) — shrink-out, mirroring AM `movement_1` |

- Spatial interpolation is present on every Position record (tangent magnitudes ±120.222 / ±261.889 paired on X and Y) — i.e. **the AE samples move along a curved spatial path**, not a straight line.
- Ease/influence numbers appear in the records (0.333333 = 1/3, 0.166667 = 1/6, 0.8, 0.65, 0.36, 0.34, 0.694444), swapping between consecutive keyframe records in the pattern "outgoing influence of key *i* ↔ incoming influence of key *i+1*". Consistent with AE's influence model; exact field semantics **not confirmed**.
- **Keyframe times were not decoded.** Each record starts with a 32-bit header word; observed values in `movement_1.aep`: 0, 49152, 61440, 76800, 81920, 116736 (= 1024 × 0, 48, 60, 75, 80, 114). Neither a 16.16 fixed-point-seconds reading (0 / 0.75 / 0.9375 / 1.171875 / 1.25 / 1.78125 s) nor a frames×1024 reading could be confirmed. **Consequence: the AE timing in the plan is authored explicitly, not copied from the sample.**

**`movement_2.aep`:** comps `matahari` (four ellipse layers) and `SUB-1` (Null 1–5, Shape Layer 1–5). `Shape Layer 4` Position has **8 keyframes** forming a horizontal bounce with constant Y = 174.667: 595.562 → 1340.9 → −184.438 → 595.562 → 595.562 → 539.562 → 539.562 → (−225.771, 50.667). Its Scale has 13 keyframes with non-uniform values such as (2.8, 2.8, 1) and (3.64, 2.8, 1). `Null 5` Rotate Z 0 → 15.667°, `Null 4` Rotate Z 0 → 17°.

**Two things the AE samples do *not* contain:** no rounded-rectangle primitive and no round-corners effect (`ADBE Round Corner` absent; only `Rect` and `Ellipse` shapes appear), and no straight-line X travel (all Position animation is spatial). Both are the parity traps addressed in §7.

---

## 5. The shared motion specification ("the contract")

Application-neutral, so each app authors it in its own terms. Values marked *(derived)* are computed from the samples above.

| # | Specification item | Value | Source |
|---|---|---|---|
| S1 | Canvas | 1920 × 1080, black background | AM scenes (`width/height/bgcolor`) |
| S2 | Subject | One rounded rectangle, 100 × 100 px, corner radius 25 px, solid fill **#464DFE** (alt. #4A82B9), no stroke | AM `movement_1`/`movement_2` |
| S3 | Trajectory | Straight horizontal; **Y constant**; centre X from **12.15 % → 90.31 %** of frame width (233.288 → 1733.965 px) | AM `movement_2`, world space *(derived)* |
| S4 | Rotation | Exactly **+360°**, starting at 0°, ending at 360° (one turn) | AM `movement_2` (`-0.058411° → 359.941589°`) and `movement_1` null (`0 → 360`) |
| S5 | Coupling | Travel and rotation share **identical start and end times** and the **identical ease curve** | AM `movement_2` (same `t` values, same `e` on both properties) |
| S6 | Ease (temporal only) | cubic Bézier control points **(0.42, 0, 0, 1)**, applied to both travel and rotation | AM `movement_2` `e="cubicBezier 0.42 0.0 0.0 1.0"` *(read as CSS-style x1,y1,x2,y2 — inferred)* |
| S7 | Path shape | **Straight** — no spatial curvature, no overshoot | Deliberate divergence from the AE samples (see §4) |
| S8 | Interval | Free parameter, identical in both apps. Samples used 1150 frames (9.58 s) and 2000 frames (16.67 s) at 120 fps. **Proposal:** 4.0 s | AM samples *(proposal)* |
| S9 | Excluded in v1 | AM `movement_2` parent-null 180° counter-spin (would make 540° total); corner-radius morph 0→180; 12.5 px stroke; AM `movement_1` shrink-out (scale 1→0); second bouncing circle | Required to satisfy "rotating once" |

**Reference progress values for S6** (cubic Bézier (0.42,0,0,1), solved numerically — these are the numbers both builds must hit):

| Normalised time u | 0.00 | 0.25 | 0.50 | 0.75 | 1.00 |
|---|---|---|---|---|---|
| Progress | 0.000000 | 0.371894 | 0.859549 | 0.974293 | 1.000000 |
| X (px) | 233.288 | 791.381 | 1523.194 | 1695.387 | 1733.965 |
| Angle (°) | 0.000 | 133.882 | 309.438 | 350.745 | 360.000 |

---

## 6. Alight Motion implementation plan

**Preconditions:** Alight Motion 5.0.273.x (version observed in the sample export); new project, 1920 × 1080; fps 30 or 120 (both fine — S5/S6 are time-based); no assets needed.

1. **Project setup.** New composition, 1920 × 1080, background black, duration = S8 (proposal 4 s). Keep the supplied `movement_*.xml` files untouched; work in a new project.
2. **Subject.** Add a **rounded rectangle** layer (sample label "Persegi Panjang Bulat" = *rounded rectangle*): size 100 × 100, corner radius 25, solid fill #464DFE, no stroke.
3. **Pivot.** Add a **Null** layer ("Nol"), place it at (960, 540) — the frame centre, as in both samples — and set the rounded rectangle's **Parent** to it. The null carries no animation of its own in v1 (S9 excludes its counter-spin).
4. **Travel.** On the rectangle's **Location**, keyframe X from **−726.712** to **+773.965** (local to the null) with Y = 0 at both keys. These are the sample's own local values; they place the subject at 233.288 → 1733.965 px in frame space (S3).
5. **Rotation.** On the same layer's **Rotation**, keyframe **0° → 360°** at the *same two times* (S4, S5).
6. **Timing inside Alight Motion's model.** Keyframe `t` is a fraction of the layer's own lifetime (§3.1). For a 4 s layer at 30 fps (120 frames) use `t = 0` at the first key and `t = 1` at the last; for a 480-frame layer at 120 fps use `t = 0` and `t = 1` as well, or keep the sample's proportions by scaling (`t = start/(end−start)`, `t = end/(end−start)`). Do not copy the samples' raw `t` values into a different-length layer.
7. **Ease.** On the *earlier* keyframe of each pair, set the interpolation to the custom curve **cubic Bézier (0.42, 0, 0, 1)** — in the sample this is the `e="cubicBezier …"` attribute on the first of the two keyframe elements. Apply the same curve to Location and Rotation so the two stay phase-locked.
8. **Self-check in-app.** Scrub: X strictly monotonic with no overshoot; Y constant; total rotation exactly 360°; corner radius still 25; no scaling inherited from the null.
9. **Delivery.** Keep the project editable; export a short preview for the parity check in §8. Do not export over the sample files.

---

## 7. After Effects implementation plan

**Preconditions:** After Effects version **unknown** — version-sensitive steps below are marked *Unverified* and must be confirmed in the app. No AE is installed in this environment, so this plan is authoring instructions, not an executed edit. AEP files are proprietary binaries: **do not attempt to write them programmatically**; author in the UI.

1. **Composition.** New comp, 1920 × 1080, 30 fps, 4 s (S8), black solid background to match AM's `#ff000000`.
2. **Subject (capability difference — the main trap).** After Effects has **no rounded-rectangle primitive** (the supplied AEPs contain only `ADBE Vector Shape - Rect` and `- Ellipse`). Build it as: Shape Layer → Rectangle, Size **100 × 100**, then **Round Corners** effect with radius **25 px** (*Unverified — no round-corner effect appears in the supplied AEPs*). Fallback if the effect is unavailable: draw a custom path with four Bezier corner points at radius 25.
3. **Fill.** Solid fill **#464DFE** (R 0.275, G 0.302, B 0.996) — note the AE samples' stored colour (255, 63.75, 140.25, 255) is a *different* pink, #FF408C, so the colour is a deliberate spec choice, not a copy.
4. **Pivot.** Add a **Null Object** "Control" at (960, 540) and parent the shape layer to it (*Inferred*: AE 2-D parenting offsets the child's Position by the parent's position, the same relationship the AM sample uses; confirm visually).
5. **Travel.** With the parent null at (960, 540), keyframe the shape layer's **Position X** from **−726.712** to **+773.965** (child-local, so it lands at 233.288 → 1733.965 px in frame space), Y constant at 0. This reproduces the AM local-space convention exactly.
6. **Straight-path guarantee (second trap).** The supplied AE samples move along **spatial (curved) paths** — their Position records carry spatial tangents. To match AM's straight horizontal travel, keep the motion 1-D: either animate only X with Y static, or in the Graph Editor select the Position **spatial path dimension** and set it to linear. Verify there is no X overshoot and that Y never changes.
7. **Rotation.** On the same shape layer, keyframe **Rotation 0° → 360°** at the same two times. Put the spin on the shape layer (as AM `movement_2` does), **not** on the null, so the total turn is one revolution.
8. **Ease.** Set both keyframe pairs to **Bezier** interpolation (not Hold, not Linear) and shape the speed-graph handles to reproduce cubic Bézier (0.42, 0, 0, 1). AE's influence model is not a documented 1:1 match for the AM/CSS control points — the mapping is *Unverified*; validate numerically against the §5 reference table (U = 0.25/0.50/0.75) before declaring parity.
9. **Self-check in-app.** X monotonic, Y constant, rotation = 360.000°, corner radius visually 25 px, no scale inherited from the null.
10. **Delivery.** Save the .aep as a new file (do not overwrite the supplied fixtures); render a preview for the parity check.

---

## 8. Parity verification and acceptance criteria

**Method:** render/inspect both builds and compare at the same *normalised* times u = (t − t₀)/(t₁ − t₀) — necessary because the two apps may run at different frame rates. Sample u = 0.00, 0.25, 0.50, 0.75, 1.00 (five frames each).

**Acceptance criteria (observable):**

1. Subject centre travels a **straight horizontal line**: Y deviation 0 px at all sampled frames, X strictly monotonic (no overshoot) in both apps.
2. **Travel endpoints identical** in both apps: X = 233.288 px and 1733.965 px at 1920 width (12.15 % → 90.31 %); tolerance ≤ 1 px.
3. **Total rotation exactly 360°** in both apps (start 0° ± 0.2°, end 360° ± 0.5°), with rotation start/end times equal to travel start/end times.
4. **Normalised progress matches the S6 curve** at every sample: X within ±1 px and angle within ±0.5° of the §5 table (u = 0.25 → 791.381 px / 133.882°, u = 0.50 → 1523.194 px / 309.438°, u = 0.75 → 1695.387 px / 350.745°).
5. **Subject identical in both builds:** 100 × 100 px, corner radius 25 px, fill #464DFE.
6. In the After Effects build, the Position **spatial path is linear** (explicitly verified in the Graph Editor) — a deviation from the supplied AE samples, which use curved spatial paths, is intentional and required for parity with Alight Motion.
7. Both projects remain **editable** (native layer/property structure, no baked raster), and the supplied sample files are unchanged.

---

## 9. Uncertainties, inferences, conflicts

| Item | Classification | Note / how to close |
|---|---|---|
| AM keyframe `t` = fraction of the layer's own lifetime | **Observed + derived** (12/12 keyframes land on integer frames) | Confirm against AM's own documentation or a new project before relying on it for other lengths |
| AM `cubicBezier a b c d` = CSS-style control points | **Inferred** | Confirm on-device by drawing a known curve and exporting the XML |
| AM sample durations in seconds (9.58 s / 16.67 s) | **Derived** from `fps=120` and frame counts | — |
| AE keyframe time encoding | **Unresolved** | Header words observed (0, 49152, 61440, 76800, 81920, 116736 …); unit not established. AE timing is therefore *authored*, not copied |
| AE `ldat` record field semantics (value position, influence fields, spatial tangents) | **Inferred** from an unofficial parser | Rules used were self-consistent across every record in both files, but are not vendor-documented; label any reuse as unofficial |
| AE comp frame rate, duration, and dimensions | **Unverified** | `cdta` chunk contains 600/1200/120/30-type values, but their meaning was not established. Use an explicit new comp instead of inheriting from the samples |
| Whether AE 2-D parenting offsets the child's Position by the parent's | **Inferred** | Verify in-app with a 2-keyframe null + child |
| AM cubic-Bézier ↔ AE keyframe-influence mapping | **Unverified** | Close by the numeric comparison in §8, criterion 4 |
| "Comparable in both applications" | **Confirmed as the goal**; definition of comparable = shared S1–S9 + acceptance criteria | — |
| Whether the extra sample elements (corner morph, stroke, shrink-out, second circle, 180° counter-spin) belong in scope | **Unknown** | Needs one decision from you; v1 excludes them (S9) |

---

## 10. Constraints and dependencies

- **No Alight Motion and no After Effects in this environment.** Nothing here can be executed, rendered, or visually confirmed; every application step above is an instruction to be performed in-app, and each is labelled with its evidence status.
- **The repository's application references are empty by design** (`skills/application-adaptation/references/*/README.md`: *"No verified application procedures are recorded here yet"*). The steps in §6–§7 are therefore hypotheses to be validated on-device and then recorded via `references/EVIDENCE-TEMPLATE.md` — they must not be presented as verified procedures.
- **No automation route is established.** No scripting/API interface is verified for either application in this repository; plan for manual authoring, and treat any scripted route as unverified until a source is confirmed.
- **File preservation:** the four supplied samples are the owner's work; they were read only and are unchanged. Any experiment (including in-app rebuilds) should use new files.
- **Cross-application rule in force:** the shared creative outcome is authoritative; the two apps' keyframe models, terminology, and file formats stay separate — no parameter, ease, or layer structure is to be "copied" between them as if the constructs were equivalent.

---

## 11. Approvals needed before execution

1. **Interval length and frame rate** for the canonical build (proposal: 4.0 s; 30 fps in AE, 120 fps in AM or both 30 fps).
2. **Colour and finish**: #464DFE flat (proposal, from `movement_2`) versus #4A82B9 (from `movement_1`); stroke on/off; corner-radius morph on/off.
3. **Confirm exclusion** of the 180° parent-null counter-spin, the shrink-out, and the second circle — otherwise "rotating once" no longer holds.
4. **Who executes the builds** (no app access in this environment) and whether AE authoring should be manual or scripted.
5. Permission to record verified in-app findings into `skills/application-adaptation/references/` once they exist.

---

## 12. Recommended next step

Run **application-adaptation** on the shared specification in §5, one application at a time, to convert S1–S9 into ordered, evidence-labelled procedures for Alight Motion and for After Effects (and to record the two capability traps: no native rounded rectangle in AE; straight-line vs spatial-path travel). Then hand off to **motion-graphics-execution** for sequencing and **hybrid-execution** for the concrete method of each build, and to **visual-evaluation** for the §8 comparison, once renders exist. `motion-graphics-principles` is needed only if the ease profile itself is re-designed; `error-analysis` is not indicated — no failure has occurred.

**Smallest useful next input from you:** answer the five approvals in §11 (or just approve the proposed defaults), and confirm who will execute the two builds in the applications.

## Reviewer verification

Every checkable claim was re-derived independently from the fixture bytes and files, not accepted from the response.

| # | Claim in the response | Verdict | Reviewer note |
|---|---|---|---|
| 1 | File sizes 3,115 / 1,940 / 45,416 / 197,708 B | **Reproduced** | `os.path.getsize` on the four fixtures |
| 2 | AM `movement_1.xml`: scene "Proyek Baru 94", 1920×1080, `fps="120"`, `totalTime="3448"`, `bgcolor="#ff000000"`, version `5.0.273.1028425` (Android) | **Reproduced** | XML header read |
| 3 | AM `movement_2.xml`: scene "Proyek Baru 95", `totalTime="2090"`, `fps="120"` | **Reproduced** | XML header read |
| 4 | Rect `300071272` parented to null `300071273` "Nol 1"; circle `300071274` "Lingkaran 1"; null type `perspective` | **Reproduced** | Element/attribute read |
| 5 | Rect location `0,0,0` → `795.378052,0,0`; size 100×100; `cornerRadius 25`; fill `#ff4a82b9`; no stroke | **Reproduced** | `<location>`, `<property>`, `<fillColor value="#ff4a82b9"/>`; no stroke element in the file |
| 6 | Null location fixed at `960,540`; null rotation `0` → `360` with ease `cubicBezier 1.0 0.0 0.26 1.0`; null scale `1,1` → `0,0` with ease `cubicBezier 0.42 0.0 0.58 1.0` | **Reproduced** | Element read; the scale ease is stated correctly (the rev. B record left it unspecified) |
| 7 | Circle bounce `540 → 997.35 → 78.81 → 540` with a size morph, frames 1441–3448 | **Reproduced** | `<kf>` values `540`, `997.349976`, `78.812500`, `540`; size keyframes `100,100` ↔ `76,100` ↔ `100,76` |
| 8 | `movement_2`: shape `300071275` → null `300071276`; location `−726.712280` → `773.965210`; rotation `−0.058411` → `359.941589`; cornerRadius `0 → 180`; fill `#ff464dfe`; white stroke size 12.5 centred; null rotation `0` → `180` | **Reproduced** | Element read; stroke is `<path-stroke direction="centered">` with `<color value="#ffffffff"/>` and `<size value="12.500000"/>` |
| 9 | The 12 derived frame numbers (4, 2004, 295, 1337, 104, 1254, 712, 1546, 1704, 3420, 2837, 2337) | **Reproduced** | `t × lifetime` recomputed: max deviation 0.0009 frame, so "within 0.001 frame" holds |
| 10 | World-space travel `233.288 → 1733.965 px` = `12.15 % → 90.31 %`, total `1500.677 px` = `78.16 %` | **Reproduced** | `960 ± local X`; percentages recomputed (12.1504 %, 90.3107 %, 78.1603 %) |
| 11 | S6 progress table `0.371894 / 0.859549 / 0.974293` and the derived X and angle rows | **Reproduced** | CSS cubic-bezier(0.42,0,0,1) solved numerically: progress, X (791.381 / 1523.194 / 1695.387) and angle (133.882 / 309.438 / 350.745) all match to 3 decimals |
| 12 | `#464DFE` → R 0.275 / G 0.302 / B 0.996; AE stored colour (255, 63.75, 140.25, 255) → `#FF408C` | **Reproduced** | Arithmetic recomputed |
| 13 | AE chunks: `Utf8`, `tdmn`, `ldat`, `lhd3`, `svap`, `adfr`, `prin`; RIFX big-endian | **Reproduced** | Substring counts (184 / 209 / 7 / 24 / 1 / 1 / 1); magic `RIFX` |
| 14 | `movement_1.aep`: `ADBE Vector Shape - Rect` ×1, `- Ellipse` ×1, `ADBE Round Corner` ×0, `Roundness` ×0, `Round` ×0 | **Reproduced** | Substring counts |
| 15 | Ellipse size 200 × 200; rect size 200 × 200.0223 | **Reproduced** | Doubles at offsets 7724 (200, 200) and 20808 (200.02233938) |
| 16 | Fill colour components 63.75 and 140.25 | **Reproduced** | Doubles at 8220 / 8228 and 21296 / 21304 |
| 17 | `Null 1` Position `(960,540) → (238.667,540)`; `Shape Layer 2` Position `(−669.333,50) → (52.000,50)`; `Shape Layer 1` Position `(189.893,514.915) → (1761.227,514.915)` | **Reproduced** | Doubles at 2428, 9240, 9368, 22316/22324, 22444/22452 (128 bytes apart, identical Y) |
| 18 | Spatial tangents ±120.222 / ±261.889 | **Reproduced** | Doubles at 2324 / 2452 / 9288 and 22364 / 22492 |
| 19 | Keyframe-time header words 49152, 61440, 76800, 81920, 116736 in `movement_1.aep` | **Reproduced** | Big-endian uint32 counts (2 / 1 / 4 / 1 / 7); absent from `movement_2.aep`; the "× 1024" reading is presented by the response as unconfirmed |
| 20 | `movement_2.aep` comps `matahari` and `SUB-1`; `Shape Layer 4` Position values 595.562 / 1340.9 / −184.438 / 539.562 / −225.771 with constant Y 174.667; `Null 5` 15.667°; `Null 4` 17°; scale values 2.8 and 3.64 | **Reproduced** | Doubles at 76302 / 76430 / 76558 / 76942 / 77198 / 76310 (Y) / 71744 (15.66667) / 92686 (16.99998) / 78324 (2.8) / 78580 (3.64). The exact keyframe *counts* (8 and 13) were not re-derived |
| 21 | Influence-like fractions `0.333333 = 1/3`, `0.166667 = 1/6`, `0.8`, `0.65`, `0.36`, `0.34`, `0.694444` cited under `movement_1.aep` | **Does not reproduce as cited** | `0.33333333` occurs 0× and `0.8` occurs 0× in `movement_1.aep`; both occur in `movement_2.aep` (73× and 255×). The other five do occur in `movement_1.aep`. The values are real; the file attribution is wrong |
| 22 | `Shape Layer 1` Scale `(100 %, 100 %, 100 %) → (0 %, 0 %, 100 %)` | **Does not reproduce** | Exhaustive big-endian double scan of `movement_1.aep`: no triple (100,100,100) and no triple (0,0,100); float32 scan likewise empty. 28 doubles equal to exactly 100.0 and many zeros are present in the layer region, so a scale keyframe exists, but the stated values and their order cannot be confirmed from the bytes |
| 23 | `ADBE Time Remapping` on `Null 1`; `ADBE Rotate X`/`Y` = 0; `ADBE Anchor Point` present | **Reproduced** | Substring counts (1 / 3 / 3 / 1) |
| 24 | `skills/application-adaptation/references/*/README.md` states "No verified application procedures are recorded here yet" | **Reproduced** | Both files quoted verbatim |
| 25 | The three camera fixtures are present but out of scope | **Reproduced** | Files exist in `evals/fixtures/` |
| 26 | The four supplied samples were not modified | **Reproduced** | SHA-256 after the run identical to the fixture inventory: `8d7010a8…`, `6c8083f1…`, `7067f17d…`, `6279b42b…` |

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent capture | 5 | 25 | 25 | Shared intent identified exactly as asked (horizontal travel + one full turn), both representations treated as different, plan produced, originals preserved, and the shared contract written application-neutral before any procedure. |
| Evidence discipline | 4 | 20 | 16 | The AM time model is *derived and shown*, not asserted; XML values cite element and attribute; AE values cite chunk and property names; official/unofficial is stated repeatedly; the AE keyframe-time encoding is explicitly left unresolved. Two citation defects remain: the influence-fraction list is attributed to the wrong `.aep` (row 21) and the Scale triple is presented as a decoded value without reproducing from the bytes (row 22). No file offset is cited for any AE double. |
| Requirements and constraints | 5 | 15 | 15 | Every supplied value, the no-modify rule, editability, the absence of applications, the empty reference scaffolding and the absence of an automation route are captured; every invented parameter (interval, colour, exclusions) is labelled a proposal or an exclusion with the reason. |
| Clarification judgment | 4 | 15 | 12 | Five approvals, each with a proposed default, and a single "smallest useful next input" line. Deducted because the list mixes genuine build blockers with scheduling questions ("who executes the builds", "permission to record findings") that belong to the execution stage, and no item is marked as the one blocking question. |
| Application awareness | 5 | 10 | 10 | The two parity traps are identified from the samples themselves (no rounded-rectangle primitive in the AE files; spatial vs straight path travel), the counter-spin exclusion is reasoned from the rotation requirement, and the AE ease mapping is marked Unverified with a numeric closure test. |
| Handoff quality | 4 | 10 | 8 | Routing is correct and selective — `application-adaptation` first, then execution, hybrid execution and visual evaluation, with `motion-graphics-principles` conditional and `error-analysis` explicitly not indicated. Deducted because the response itself writes the per-application procedures (§6, §7), which is the receiving skill's job. |
| Proportionality | 3 | 5 | 3 | Twelve sections including two full application build plans, a nine-item contract, a derivation table, a ten-row uncertainty table and a five-item approval list for a task whose output should be an understanding plus a plan and a short question set. |
| **Total** | | **100** | **89** | Pass (80–89). |

## Expected behavior checklist

- [x] Identify the common creative intent: horizontal movement plus one full rotation.
- [x] Treat Alight Motion XML and After Effects AEP as different project representations.
- [x] Recognize that the supplied samples may inform structure and animation approaches but do not automatically prove that the same exact settings or visual result can be transferred.
- [x] Preserve the originals and propose copies or separate working files before any modifications.
- [x] Identify any missing visual acceptance criteria or asset dependencies only when they materially affect the implementation.
- [x] Hand off to motion principles, application adaptation, and execution; use hybrid execution only when choosing an actual technical method.
- [x] State what needs native-app preview/render validation.

## Critical failure review

- **Finding:** none.
- **Evidence:** no claim to have opened, rendered, or executed either application — the AE plan is explicitly "authoring instructions, not an executed edit"; the `.aep` files are treated as binaries and never as XML; the four fixtures hash identically to the inventory after the run; no user requirement was altered (the additions are labelled proposals and exclusions with reasons); no destructive or externally visible action was taken.
- **Impact:** none. Row 22 was checked against the scorecard's critical-failure test — "presents assumptions or unsupported technical interpretations as confirmed facts" — and was judged not to meet it: the scale keyframe exists in the file (28 doubles equal to 100.0 in the layer region), the response stated the record rule it used, and the discrepancy is a citation the reviewer could not confirm rather than a value the reviewer showed to be absent. The defect is recorded as a deduction, not a failure.

## Improvements needed

1. **Cite a byte offset for every binary value.** The rev. C rule asks for chunk, offset, or property block; this run used chunk and property names but no offsets, so several values could not be re-checked by a reviewer without re-deriving the whole record layout.
2. **Check which file a value came from before citing it.** The influence-fraction list mixes values from `movement_2.aep` into the `movement_1.aep` paragraph.
3. **Do not tabulate a value that does not survive a byte check.** The Scale triple is presented as decoded; a value the run could not confirm should have been marked Unverified in the same table where the other decoded values sit.
4. **Stop at the shared contract.** Sections 6 and 7 belong to `application-adaptation`; the understanding step can name the two capability traps without writing the numbered build procedures.
5. **Ask one blocking question, not five.** Separate "what must be decided before a build" from "who schedules the build".

## Retest

- Not required for the pass threshold. This run supersedes the rev. B record for PU-03 at the current skill revision; the earlier record and its [`response.md`](response.md) remain in place as the evidence for rev. B.
- The project owner's score for rev. C has not been given. The owner's rev. B score (**90/100 — governing**) remains the human score for PU-03 until they score this revision.
- Any further independent score for this response is **added, not substituted**. The owner reconciles it against the initial assessment; no governing score changes automatically.
