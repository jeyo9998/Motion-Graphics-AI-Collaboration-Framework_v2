# PU-04 — Raw Response (preserved verbatim)

- **Case:** PU-04 — Camera research and evidence boundaries
- **Run date:** 2026-11-24
- **Client:** fresh general-purpose agent context (no access to `evals/` beyond the two listed fixtures; answer key withheld)
- **Skill revision:** rev. B of `skills/project-understanding/SKILL.md`
- **Materials supplied:** `fixtures/alight-motion/Motion_Graphics_unik.xml`, `fixtures/after-effects/Motion_Graphics_Unik_Camera.aep`, and the owner's three screen recordings at `D:/Download/rekam kamera/`
- **Note:** the text below is the run's final message, unedited. Spelling, values, and claims are preserved exactly as produced; the reviewer's assessment of them is in [`evaluation.md`](evaluation.md).

---

# Camera findings: Alight Motion XML, After Effects AEP, and the recordings

## 1. The Alight Motion XML — `Motion_Graphics_unik.xml` (verified by parsing the file bytes)

Exported by Alight Motion 5.0.273.1028425 on Android (`am="com.alightcreative.motion/5.0.273.1028425"`, `amplatform="android"`, build `2d5c0f8 (20 Mei 2026)`), comp **1440×1080 @ 20 fps, 18.549 s** (root `<scene>` attributes, verified in bytes).

It contains **exactly two `<camera>` elements** (both direct children of the root `<scene>`, appearing late in the layer list):

| | Camera 1 | Camera 1 (second) |
|---|---|---|
| id / label | `102424590` / `"Kamera 1"` | `102424504` / `"Kamera 1"` |
| time window | `startTime=0` `endTime=18549` | `startTime=6150` `endTime=7649` |
| `parent` | `102424591` | `102424505` |
| `type` | `"perspective"` | `"perspective"` |
| `<transform><location>` | `value="0.000000,0.000000,-1247.076660"` (static, no keyframes) | identical |
| `<fov>` | `value="60.000000"` | identical |
| `<focus-blur enabled="false">` | `strength="0.500000"`, `depth-of-field="124.707664"`, `distance="1247.076660"` | identical |
| `<fog enabled="false">` | `near-z="1247.076660"`, `far-z="2494.153320"` | identical |

Both camera `<transform>` blocks contain **only `<location>`** — no `<rotation>`, no `<scale>` (verified with an XML parser; the tag census of the whole file is `camera×2, fov×2, focus-blur×2, fog×2` and nothing else camera-related). All the camera motion lives on **parented null objects** (`<nullobj>`, all `type="perspective"`, 6 of them):

- Camera 1 → `102424591` "Nol 1": location keyframed `(720.499756,1044.499756,1207.500000) → (720.499756,540.499756,0.000000)` with `e="cubicBezier 0.0 0.58235294 0.0 1.0"`; note the null's window is only `0–3199 ms`, much shorter than the camera's `0–18549 ms`.
- Camera 2 → a **three-deep chain**: `102424505 "Nol 1"` → `102424506 "Nol 1 Copy"` → `102424510 "Nol 1 Copy 2" (hidden="true")`, each with keyframed location only.

Keyframe format observed throughout the file: `<kf t="…" v="…" e="cubicBezier x1 y1 x2 y2"/>`, with `t` normalized 0–1 inside the element's start/end window (inferred: first keys land at ~25 ms of each window, e.g. `t=0.007815` × 3199 ms ≈ 25 ms). Easing values can overshoot, e.g. `cubicBezier 0.86333334 -0.5029412 0.14333332 1.425` (verified in bytes).

**Formula checks (inferred from the numbers):** default camera distance = `(comp_width/2)/tan(fov/2)` = `720/tan(30°)` = **1247.0766** — exactly the camera's `location.z` and the `focus-blur distance`; `depth-of-field = distance/10` (124.707664); `fog near-z = distance`, `fog far-z = 2×distance` (2494.153320). So AM's camera defaults are all derived from comp width + FOV 60°.

## 2. The After Effects .aep — `Motion_Graphics_Unik_Camera.aep` (verified by parsing the RIFX bytes)

RIFX/OMF container, form type `Egg!` (After Effects project), uncompressed, 203,068 bytes. Three project items: comp **"matahari"** (4 shape layers, no camera), one footage item, and comp **"SUB-1"** — the comp with the camera. SUB-1: **1920×1080, 30 fps** (comp `cdta` chunk: u16 1920 @140, 1080 @142, 30 @156). Renderer for both comps: `prin` chunk = `ADBE Escher` / **"Classic 3D"**.

**Exactly one camera layer in the entire project**: layer "Camera 1" (index 56) in SUB-1. Its serialized property tree (match names read from `tdmn` chunks, in file order):

```
ADBE Transform Group
  ADBE Anchor Point, ADBE Position (+ ADBE Position_0/_1/_2), ADBE Scale,
  ADBE Rotate Z, ADBE Opacity, ADBE Envir Appear in Reflect
ADBE Camera Options Group
  ADBE Camera Zoom, ADBE Camera Depth of Field, ADBE Camera Focus Distance,
  ADBE Camera Aperture, ADBE Camera Blur Level
```

Decoded values (big-endian doubles from `cdat` chunks):

- Anchor Point **(960.0, 540.0, 0.0)**; Scale (1,1,1); Rotate Z 0; Opacity 100%
- **Position is keyframed** — the keyframe list header records **2 keyframes**; decoded doubles: time ≈ 0.1667 s → value **(960.0, 898.000031, −2666.666667)**, time ≈ 0.7 s → value **(960.0, 540.0, −2666.666667)**, with spatial tangents ±59.6667 (keyframe record layout partially inferred)
- **Camera Zoom = 2666.6666666666665** (static, no keyframes); **Depth of Field = 0.0 (off)**; **Focus Distance = 2666.6666666666665**; **Aperture = 25.3**; **Blur Level = 100.0**
- **Parent & Link = None** (layer `ldta` parent field = 0; the five nulls "Null 1…Null 5" parent the *shape* layers, not the camera)

**What is definitively NOT in the file** (byte search, 0 hits): `Point of Interest` / `Interest`, `One-Node`, `Two-Node`, `Auto-Orienteer`, `Angle of View`, `Focal Length`, `Iris`, `bokeh`. Inside the camera layer's block there is also no `ADBE Orientation`, `ADBE Rotate X`, `ADBE Rotate Y` (those strings exist only in other layers' blocks, e.g. the `matahari` layer and the nulls). The camera block therefore contains **neither a Point of Interest nor an Orientation/X-Y-rotation set** — I cannot fully explain this serialization, and I flag it as an open discrepancy below.

Formula checks (inferred): Zoom 2666.6667 = 50 mm focal × 1920 px ÷ 36 mm film width → consistent with AE's default **50 mm** camera preset; horizontal AoV = 2·atan(18/50) ≈ **39.6°**. Camera z = −2666.6667 = −Zoom, i.e. the default camera sits exactly one "Zoom" behind the comp plane, and Focus Distance = |camera z| (distance to the z=0 plane) — all three coincide only in the default state.

## 3. The recordings

**`Recording 2026-11-24 070641.mp4`** (desktop, 1918×994, 30 fps, 5:59, with audio) — this is the "After Effects Camera Options" recording. It shows AE with project items **Comp 3, matahari, SUB-1**, timeline on **SUB-1**, layer **Camera 1, Parent & Link "None"**; Info panel: Duration 00:00:10:00, Out 0:00:09:29.

What it shows (video timestamps cited):

- **@20 s (and throughout 0–355 s):** the camera's Transform rows are **Point of Interest `1025.3, 540.0, 0.0` · Position `960.0, 540.0, -2666.7` (keyframed) · Orientation `0.0, 0.0, 0.0` · X/Y/Z Rotation `0x+0.0°`**, then a **Camera Options** group.
- **@70–78 s:** Camera Options expanded: **Zoom 3420.7 · Depth of Field (checkbox, unticked) · Focus Distance 2666.7 · Aperture 25.3 · Blur Level 100.0% · Iris Shape "Fast Rectangle" (popup) · Iris Rotation 0x+0.0° · Iris Roundness 0.0% · Iris Aspect Ratio 1.00 · Iris Diffraction Fringe 0.0 · Highlight Gain 0.0 · Highlight Threshold 255.0 · Highlight Saturation 0.0** (@76 s).
- The user animates during the session: Position/POI values change (POI → `848.6, 540.0, 0.0` @160 s → `848.6, 1792.0, 0.0` @220 s, with a keyframe context menu open @220 s); X Rotation is set to `0x+40.3°` @100 s; Zoom is keyframed (3420.7 → 5727.7 → **6400.7** @320 s → 3825.9); Graph Editor used ~187–200 s and ~290–310 s; auto-save toast "Auto-saved SUB-1-….aep" ~305 s.
- **It never shows the Camera Settings / New Camera dialog** (the one containing the literal `Type: One-Node/Two-Node` popup). I sampled 72 frames at 5 s steps over the full 359 s, 33 frames at 2 s steps over 112–178 s, and the frames at the only large scene changes (124.6, 125.8, 182.8, 197.6, 283.9, 287.4 s) — no modal dialog anywhere.
- **The recorded project is not byte-equal to the .aep:** the video's Zoom is keyframed (3420.7/6400.7) vs. static 2666.6667 in the file; the video animates Point of Interest, which doesn't exist in the file; "Comp 3" exists in the video's Project panel but the string is absent from the .aep. Same comp name, same matahari item, same Focus Distance 2666.7, same Position z −2666.7, same 1920×1080@30fps/10 s — so it is clearly the same project family at a different save state. The recording's audio track was not examined.

**`screen-20261124-215814.mp4` (7:04) and `screen-20261124-220101.mp4` (2:18)** — both are **Android 12 phone recordings (720×1612 portrait) of Alight Motion**, not After Effects. They show the AM "Move & Transform" screen for the layers **"Kamera 1"** (camera, with video-camera glyph) and **"Nol 1"** (null): X/Y/Z boxes `960,00 / 540,00 / -1662,77` for Kamera 1 (@45 s), keyframe diamonds on the timeline, cubic-bezier easing editor, a rotation dial at `0°` (@~75 s in the second clip), a numeric keypad (label "Lebar"). Formula check (inferred): `960/tan(30°) = 1662.769` — again the AM default camera distance, here for a 1920-wide comp, so this phone project is a *different* AM project from the 1440-wide XML fixture.

## 4. What can safely be documented per adapter

**Alight Motion adapter**
- *Verified (file bytes):* `<camera>` element schema — attributes `id, label, startTime, endTime, mediaFillMode, parent, type="perspective"`; children `<transform><location>`, `<fov>`, `<focus-blur enabled/strength/depth-of-field/distance>`, `<fog enabled/near-z/far-z>`; cameras are scene-level siblings of layers; a project may hold several cameras with independent time windows; keyframe `kf` syntax with normalized time and `cubicBezier` easing (overshoot allowed).
- *Verified for this sample, do not generalize yet:* cameras carry **no rotation/scale** — one sample cannot prove the format lacks camera rotation; mark it "not observed".
- *Verified pattern:* motion is carried by parented `<nullobj>` chains (1–3 deep, `type="perspective"`), while the camera itself holds a fixed z offset; parent windows may be shorter than the camera's. (Inheritance semantics = inferred from standard parenting, consistent with the sample.)
- *Inferred (formula, two independent confirmations — XML and phone recording):* default camera distance `(width/2)/tan(fov/2)`; focus distance defaults to that distance; DoF range = distance/10; fog near = distance, far = 2×distance; default FOV 60°.

**After Effects adapter**
- *Verified (bytes):* camera is a **layer** ("Camera 1") with `ADBE Transform Group` + `ADBE Camera Options Group`; serialized match names `ADBE Camera Zoom / Depth of Field / Focus Distance / Aperture / Blur Level`; comp 1920×1080 @30 fps; Classic 3D renderer; camera **not** parented to a null; Position is keyframeable (2 keys with spatial tangents).
- *Observed (frames of the desktop recording):* full UI property set — Transform: Point of Interest, Position, Orientation, X/Y/Z Rotation; Camera Options: Zoom, Depth of Field (checkbox), Focus Distance, Aperture, Blur Level, Iris Shape/Rotation/Roundness/Aspect Ratio, Iris Diffraction Fringe, Highlight Gain/Threshold/Saturation. POI, Position and Zoom are independently keyframeable. Do not document the bokeh rows below "Highlight Saturation" — the list was never scrolled further in the video.
- *Inferred (formula):* Zoom ↔ focal-length parameterization (Zoom = focal × width/film-width; AoV = 2·atan(w/2/Zoom)); default camera sits at z = −Zoom with Focus Distance = |z|. **Teach the adapter that Zoom is not the camera distance**: in the recording Zoom changes (3420.7→6400.7) while Position z stays −2666.7.
- *Observed defaults to document:* Zoom 2666.667 px (fresh 50 mm preset), Focus Distance 2666.7, Aperture 25.3, Blur Level 100%, DoF off, Iris Shape "Fast Rectangle", Iris Rotation 0°, Iris Roundness 0%, Iris Aspect Ratio 1.00, Iris Diffraction Fringe 0.0.

**Do not document yet:** AE version (not legible in the bytes I decoded, not shown in the video); AM camera rotation support; AM `type` values other than `"perspective"`; whether AE serializes `Point of Interest` for saved cameras at all (see discrepancy); the mapping AM `fog` → AE (no fog-like property appears in the observed AE camera list, but I only observed the camera, not effects).

## 5. One-Node or Two-Node?

**The camera shown in the screen recording is a Two-Node camera.** Evidence: at 20 s (and in every sampled frame across 0–355 s) the Camera 1 Transform contains a **Point of Interest** row together with Orientation and X/Y/Z Rotation. In After Effects the Point of Interest property exists only on Two-Node cameras; a One-Node camera has Position + Orientation/Rotation and **no** Point of Interest row. Confidence: high (directly observed), though the literal `Type` dropdown in the Camera Settings dialog is never shown in the video, and Point of Interest is animated during the session (1025.3→848.6, y 540→1792), which is the Two-Node workflow.

**The .aep file cannot answer the question by itself.** Its Camera 1 serializes neither `ADBE Point of Interest` nor `ADBE Orientation`/`Rotate X`/`Rotate Y`. The absence of Point of Interest alone looks like One-Node, but the same block also lacks the rotation properties a One-Node camera must have, so the byte evidence is self-inconsistent and I will not classify it from bytes. The file also demonstrably differs from the recorded session (Zoom and POI keyframes present in the video, absent in the file; "Comp 3" present in the video's project panel, absent in the file), so the .aep is a different save state. To resolve it from bytes you would need: (a) a reference .aep saved by the same AE version with a camera of known Type, or (b) the AE version number, or (c) a re-recording that opens Layer > Camera Settings… and shows the Type popup — the cheapest and most conclusive option.
