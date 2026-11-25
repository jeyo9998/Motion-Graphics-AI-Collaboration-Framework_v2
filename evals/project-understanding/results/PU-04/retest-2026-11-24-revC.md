# PU-04 — Re-run 2026-11-24 (rev. C skill)

- **Case:** PU-04 — Camera research and evidence boundaries (verbatim from `../../cases.md`)
- **Run date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/project-understanding/SKILL.md` at **rev. C** — the 2026-11-24 edits recorded in Review 008 (Technical evidence discipline: derived values show their derivation, binary values cite chunk/offset, generalizations scoped to what was inspected, changing recording values cite a frame timestamp). 231 lines; the revision is also identifiable as commit `9fff40c`. The rev. B record (owner 80/100 — governing; reviewer A 83/100; reviewer B 87/100) is the evidence for rev. B.
- **Materials supplied:** the owner-supplied Alight Motion XML camera sample (`evals/fixtures/alight-motion/Motion_Graphics_unik.xml`), the owner-supplied After Effects camera AEP (`evals/fixtures/after-effects/Motion_Graphics_Unik_Camera.aep`), and the three screen recordings kept outside the repository at `D:/Download/rekam kamera`.
- **Procedure:** fresh agent context; the skill was read from the repository path; the agent was told not to open `cases.md`, `scorecard.md`, `review-log.md`, `independent-review-brief.md`, `evals/fixtures/README.md` or any `results/` folder; it was told to disregard any score arriving with its working context; the exact prompt below was submitted; no coaching and no follow-up occurred. The agent chose on its own to consult external vendor and community documentation; the source list is preserved in the response.
- **Score:** **88 / 100** (rev. B: 80/100 owner — governing / 83 reviewer A / 87 reviewer B)
- **Critical failure:** **No** — see the critical-failure review below, which records one borderline judgement for the project owner to overrule if they read it differently.

## User prompt

> Review my Alight Motion XML camera sample, my After Effects camera AEP, and the screen recording of the After Effects Camera Options. Explain what we can safely document for the two application adapters. I also want to know whether the After Effects camera is One-Node or Two-Node.

## Raw response

# Review: Alight Motion XML, After Effects AEP, and the AE Camera Options recording

**Bottom line on your question: the After Effects camera in the screen recording is a Two-Node Camera** — the layer shows a `Point of Interest` property, which is AE's documented two-node signature. The AEP file, read with an unofficial parser, is a weaker witness and points the other way (details and caveats in §2).

---

## 1. Inventory

| Resource | Classification | Status |
|---|---|---|
| `C:\Users\Axioo\Downloads\motion-graphics-ai-handoff-v1.0 (1)\motion-graphics-ai-handoff-v1.0\workspace\motion-graphics-ai-framework\evals\fixtures\alight-motion\Motion_Graphics_unik.xml` (276,954 bytes) | Target project (Alight Motion export) | **Inspected** (full text) |
| `…\evals\fixtures\after-effects\Motion_Graphics_Unik_Camera.aep` (203,068 bytes) | Target project (After Effects project) | **Inspected** via unofficial read-only binary parse; not opened in AE |
| `D:\Download\rekam kamera\Recording 2026-11-24 070641.mp4` (1918×994, 30 fps, 5:59.40) | Rendered preview — **this is the After Effects Camera Options recording** | **Inspected** (72 frames at 5 s intervals + native-resolution crops) |
| `D:\Download\rekam kamera\screen-20261124-215814.mp4` (720×1612, 42.65 fps, 7:03.65) | Rendered preview — Alight Motion on Android | **Inspected** |
| `D:\Download\rekam kamera\screen-20261124-220101.mp4` (720×1612, 45.32 fps, 2:18.48) | Rendered preview — Alight Motion on Android | **Inspected** |
| `…\evals\fixtures\after-effects\movement_2.aep`, `movement_1.aep`, `Motion_Graphics_Unik.aep` | Reference material | **Inspected** at header/chunk level only (used as a differential control; no camera layer in any of them) |

Neither Alight Motion nor After Effects is installed here, so nothing was verified by opening the applications.

---

## 2. Is the After Effects camera One-Node or Two-Node?

### Answer: Two-Node (from the recording), with one honest caveat about the AEP

**Evidence (recording, native-resolution frames):**

- `Recording 2026-11-24 070641.mp4`, timeline layer `Camera 1` in comp `SUB-1`, Parent &amp; Link = `None`. Transform group at **00:00:35** shows, in order: `Point of Interest 1025.3, 540.0, 0.0` → `Position 960.0, 540.0, -2666.7` → `Orientation 0.0, 0.0, 0.0` → `X/Y/Z Rotation 0x+0.0°` → `Camera Options` (Zoom `3420.7`, Depth of Field unchecked, Focus Distance `2666.7`, Aperture `25.0` — read at **00:00:40** and **00:00:52**).
- The `Point of Interest` value changes during the recording: `1025.3, 540.0, 0.0` at **00:00:35** → `848.6, 1792.0, 0.0` at **00:03:20**, while `Position` stays `960.0, 540.0, -2666.7`.

**Why that implies two-node:** Adobe's current documentation states that *"A One-Node Camera orients around itself, whereas a two-node camera has a point of interest and orients around that point."* A `Point of Interest` row in the Timeline is therefore the two-node configuration; a one-node camera has no such property.

**Caveats you must carry into any adapter doc:**

1. **The type was inferred from a property row, not read from AE's explicit control.** AE's Camera Settings dialog has an explicit One-Node/Two-Node type selector, but no such dialog — and no type field of any kind — is visible in any sampled frame of the recording. To turn this into a directly-read fact you need one screenshot of `Layer ▸ Camera Settings` for this camera.
2. **The AEP does not corroborate it.** The camera layer's stored property tree in `Motion_Graphics_Unik_Camera.aep` contains `ADBE Anchor Point`, `ADBE Position` (+`Position_0/1/2`), `ADBE Scale`, `ADBE Rotate Z`, `ADBE Opacity`, `ADBE Envir Appear in Reflect`, and the `ADBE Camera Options Group` — and **no point-of-interest property and no `ADBE Orientation`/`ADBE Rotate X`/`ADBE Rotate Y`**, unlike all 16 other 3D layers in the same file. The byte string `Interest` does not occur anywhere in the file, and no stored double equals `1025.3`, `848.6` or `1792.0`. Read alone, the AEP camera looks structurally single-node.
3. **The two artifacts are not the same instant of the same project.** Recorded Zoom `3420.7` vs. stored `ADBE Camera Zoom` `2666.6666666666665` (ratio 1.2831 — a fixed factor, so probably a display-vs-storage convention, but I could not verify it without AE); recorded Aperture `25.0` vs. stored `25.3`; and the recorded project panel contains a comp `Comp 3` that **does not exist** in the AEP (AEP items: `Solids` folder, `matahari`, `SUB-1`, plus five unnamed items). Treat the recording as evidence of AE's UI conventions and the AEP as evidence of file structure — not as two views of one instant.

---

## 3. After Effects adapter — what can be safely documented

### 3.1 File format facts (sample-specific, from an unofficial parser)

- The `.aep` is **binary, big-endian, RIFF-like**: `RIFX` + u32 BE size (`202694`) + form type `Egg!`. Chunks are 4-char ids with u32 BE sizes; `LIST` chunks carry a 4-char type; odd-sized chunks are followed by a pad byte. **Do not treat `.aep` as text, and do not treat "readable by a parser" as "safely editable".**
- Top-level chunk ids observed: `svap`, `head`, `nhed`, `nnhd`, `adfr`, `LIST/Pefl`, `qtlg`, `LIST/sfnm`, `mrid`, `acer`, `LIST/CPPl`, `cpid`, `dwga`, `pcms`, `Utf8`, `Utf8`, `Utf8`, `LIST/ExEn`, `LIST/Fold`, then an XMP packet whose only field is `dc:format = application/vnd.adobe.aftereffects.project`. `Utf8` @296 = `{"ocioConfigurationFile":"ACES 1.2"}`; `LIST/ExEn` = `javascript-1.0`.
- Project items live in `LIST/Fold`: `matahari` (comp), `Solids` (folder), five items with empty names, `SUB-1` (comp, item chunk @63506, size 134,838 — this item holds the 17-layer list, including `Camera 1`).
- **After Effects version is Unknown.** No version string is present in the file; the only version-adjacent evidence is the ACES 1.2 OCIO configuration and the modern dark UI in the recording.

### 3.2 What the file stores for camera `Camera 1` (values decoded; cite offsets)

`LIST/Layr` @64064 · `ldta` @64076 (164 bytes) · name `Utf8` @64248 = `Camera 1` · properties in `LIST/tdgp` @64264.

| Property | Value | Where |
|---|---|---|
| `ADBE Anchor Point` | `960.0, 540.0, 0.0` | `cdat` @64624 |
| `ADBE Position` | keyframed (below) | `ldat` @65002, 32 doubles |
| `ADBE Position_0/1/2` | `0,0,0` (dimension sub-properties) | `cdat` @65492 / @65798 / @66104 |
| `ADBE Scale` | `1,1,1` | `cdat` @66410 |
| `ADBE Rotate Z` | `0` | `cdat` @66796 |
| `ADBE Opacity` | `1` | `cdat` @67070 |
| `ADBE Envir Appear in Reflect` | `1` | `cdat` @67376 |
| `ADBE Camera Zoom` | `2666.6666666666665` | `cdat` @67792 |
| `ADBE Camera Depth of Field` | `0` (off) | `cdat` @68098 |
| `ADBE Camera Focus Distance` | `2666.6666666666665` | `cdat` @68372 |
| `ADBE Camera Aperture` | `25.3` | `cdat` @68678 |
| `ADBE Camera Blur Level` | `100.0` | `cdat` @68984 |

Position keyframes (`ldat` @65002), read as `[time, …, x, y, z, tangent×6]` groups:

- `t = 0.16666666666666666 s` → `(960.0, 898.0000305175781, -2666.6666666666665)` — derived frame number: `0.16667 s × 30 fps = 5`.
- `t = 0.7000000000000001 s` → `(960.0, 540.0, -2666.6666666666665)` — derived frame number: `0.7 s × 30 fps = 21`.

(The 30 fps rate is from the recording's comp timecode `00000 (30.00 fps)`; the AEP itself does not state it here.)

### 3.3 What the screen recording establishes about AE's UI (cite a timestamp per value)

- Project panel: `Comp 3`, `matahari`, `SUB-1`; composition tabs `SUB-1 | matahari | Comp 3`; comp `SUB-1` active; `8 bpc`; `30.00 fps` (**00:00:35**).
- Info panel for the camera: `Duration 00:00:10:00`, `In 0:00:00:00`, `Out 0:00:09:29`, `Position 0:00:00:01 → 960.0, 540.0, -2666.x` (**00:00:35**).
- Composition viewer shows `Active Camera (Camera 1)` (**00:00:35**).
- Timeline camera layer property order: `Point of Interest`, `Position`, `Orientation`, `X/Y/Z Rotation`, `Camera Options ▸ Zoom, Depth of Field, Focus Distance, Aperture` (**00:00:40–00:00:52**).
- Parent &amp; Link for the camera = `None` (**00:00:35**) — AE cameras can be parented, but this one is not.
- No Camera Settings dialog, no type field, and no right-click camera menu exposing the type appeared in any sampled frame.

### 3.4 Do not document (AE side)

- Do not claim AE's internal camera-orientation encoding, focal-length units, film-gauge relationship, or the meaning of the camera-specific flag byte in `ldta` (the camera layer carries `0x44` where other layers carry `0x04`/`0x84`). These are unexplained by this sample.
- Do not treat the parser output as documented Adobe behaviour — it is an unofficial read of one file.
- Do not claim the recorded project and the AEP are the same project state (§2, caveat 3).

---

## 4. Alight Motion adapter — what can be safely documented

### 4.1 Export format facts (from the sample)

- The XML export is plain UTF-8 text with a header comment: `Created by Alight Motion (http://alightmotion.com)`, `Exported: 2026-11-21 11:56 PM`, version **`5.0.273.1028425 (1028425)`**, build `2d5c0f8 (20 Mei 2026 04.16.19)`. This version string is directly usable for adapter gating.
- Root element `<scene>` attributes: `title="cr:kroni_asgrd"`, `width="1440"`, `height="1080"`, `exportWidth="1440"`, `exportHeight="1080"`, `precompose="dynamicResolution"`, `bgcolor="#ff000000"`, `totalTime="18549"`, `fps="20"`, `modifiedTime="1795280180919"`, `amver="1028425"`, `ffver="106"`, `am="com.alightcreative.motion/5.0.273.1028425"`, `amplatform="android"`, `retime="freeze"`, `thumbnailTime="3600"`, `retimeAdaptFPS="false"`.
- The file is a **scene graph with embedded child scenes**: 53 `<scene>` elements and 52 `<embedScene>` elements in this sample; 345 `<kf>` keyframes, 304 `<transform>` blocks, 6 `<nullobj>`, 2 `<camera>`.

### 4.2 The camera model in AM (this is the important structural difference from AE)

Both camera elements are structurally identical and both are labelled `Kamera 1`:

```xml
<camera id="102424590" label="Kamera 1" startTime="0" endTime="18549" mediaFillMode="fill"
        parent="102424591" type="perspective">
  <transform><location value="0.000000,0.000000,-1247.076660" /></transform>
  <fov value="60.000000" />
  <focus-blur enabled="false">
    <strength value="0.500000" /><depth-of-field value="124.707664" /><distance value="1247.076660" />
  </focus-blur>
  <fog enabled="false"><near-z value="1247.076660" /><far-z value="2494.153320" /></fog>
</camera>
```

(second element: `id="102424504"`, `startTime="6150"`, `endTime="7649"`, `parent="102424505"`, identical `fov`/`location`/`focus-blur`/`fog` values)

Documentable points:

- AM's camera is a **single-node perspective camera** (`type="perspective"`) whose own `<transform>` contains **only `<location>`** — there is no orientation/rotation element on the camera.
- **The camera's motion lives in its parent chain.** Camera `102424590` has `parent="102424591"`, a `<nullobj label="Nol 1">` whose `<transform>` holds a keyframed `<location>`: `(720.499756, 1044.499756, 1207.500000)` at `t=0.007815` → `(720.499756, 540.499756, 0.000000)` at `t=1.0`, the second keyframe carrying `e="cubicBezier 0.0 0.58235294 0.0 1.0"`. So the camera is animated **through the null, not through itself**.
- The second camera's chain is `102424504 → 102424505 ("Nol 1") → 102424506 ("Nol 1 Copy") → 102424510 ("Nol 1 Copy 2", hidden="true")` — a three-null hierarchy.
- **Framing is field-of-view based**, in degrees: `<fov value="60.000000"/>`. There is no focal length, aperture or film gauge anywhere in the AM camera schema. The XML does **not** state whether `fov` is horizontal or vertical — do not assume.
- **Depth of field and fog are separate, switchable elements**, and their parameters are still written when disabled: `focus-blur` (`strength 0.5`, `depth-of-field 124.707664`, `distance 1247.076660`) and `fog` (`near-z 1247.076660`, `far-z 2494.153320`). Derived relations inside the sample: `depth-of-field = distance / 10` and `far-z = 2 × near-z`.
- The AM camera is **parentable and timed** (`startTime`/`endTime`/`parent`), which is a rig concept AE's camera layer does not have in the same form.

### 4.3 What the Alight Motion app recording establishes (Android; app version Unknown — not visible in any sampled frame)

- The app's **`Move &amp; Transform`** panel exposes **X, Y, Z**, plus **`Lebar` / `Tinggi`** (width/height) with a link toggle — e.g. `Lebar 1817,0`, `Tinggi 1022,1` (`screen-20261124-220101.mp4`, **00:01:50**).
- For the camera layer `Kamera 1` (title bar reads `Kamera 1`, `screen-20261124-215814.mp4`): **X `960.00`, Y `540.00`, Z `-1662,77`** at **00:00** and **00:15** (Indonesian decimal comma); by **00:30** X/Y read `972.47 / 984.66` and at **00:45** `960.00 / 1007.75`, while Z stays `-1662,77` — i.e. the X/Y of the camera were being animated on screen.
- The timeline shows the null `Nol 1` alongside `Kamera 1`; a cubic-bezier easing editor is present. **No FOV / depth-of-field controls for the camera layer were visible** in the sampled frames (I did not verify whether they exist elsewhere in the app).
- Cross-check against the XML (**inferred, not confirmed**): `1662.7688 = 1247.076660 × 4/3` exactly, and `960 = 1440/2 × 4/3`. The recorded session is therefore consistent with the same rig in a **1920-wide** canvas, whereas the XML export is `1440×1080` — i.e. a canvas-width change between the two artefacts, or a differently scaled project.

### 4.4 Do not document (AM side)

- Do not present XML readability as safe editability, and do not assume the schema is stable across AM versions — this is one export from one build (`5.0.273.1028425`).
- Do not generalise the camera schema beyond the two `<camera>` elements inspected here; the sample contains no AM camera with rotation, with DoF enabled, or with fog enabled, so those states are **unverified**.
- Do not map AM's `fov` (degrees) onto AE's focal-length-driven framing without a documented conversion — none exists in these materials.

---

## 5. Cross-application rules for the adapters

1. **Do not unify the two camera models.** AM = one camera node with a position, a degrees-based FOV, optional DoF/fog, and motion expressed via a **parent-null rig**. AE = a camera *layer* with Position + Orientation (+ Point of Interest for two-node), focal-length-driven framing, and a DoF option set (Focus Distance / Aperture / Blur Level). A shared abstraction should be "camera placement + framing + optional DoF", not identical properties.
2. **Do not import AM rig conventions into AE** (null-parent camera chains) or AE conventions into AM (orientation/POI); neither has a counterpart in the other.
3. **Do not treat the two AE artefacts as one project state** until the Zoom/Aperture/`Comp 3` discrepancies in §2 are resolved.
4. **Gate AM adapter behaviour on `amver`/`am`** from the export header (here `1028425`, `com.alightcreative.motion/5.0.273.1028425`), since the schema is undocumented.

---

## 6. Open items (what would close them)

| Question | Status | Cheapest way to close it |
|---|---|---|
| AE camera node type, read from AE itself | **Inferred** (two-node, from the POI row) | Open the `.aep` in AE → `Layer ▸ Camera Settings` → read the Type radio; one screenshot settles it. |
| Why the AEP camera layer has no POI/Orientation | **Unknown** | Compare with an AE-written project containing the same two-node camera, or check whether the file was written by AE at all (the missing `Orientation`/`Rotate X`/`Rotate Y` that every other 3D layer in the same file has is unexplained). |
| AE stored Zoom `2666.667` vs. displayed `3420.7` (ratio 1.2831) | **Unknown** | Read `ADBE Camera Zoom` and the dialog's Zoom field for the same camera in AE; check the film's field-of-view/gauge setting. |
| AE application version | **Unknown** | AE's About/Project Settings in the recording session. |
| AM app version | **Unknown** | App info screen; the export header already pins the *exporting* build. |
| AM `fov` axis (horizontal vs vertical) | **Unknown** | A controlled AM test: change only the canvas aspect and observe framing; or AM's own documentation. |
| AM camera with DoF/fog enabled, and with rotation | **Not found in the checked source** | One more AM export with those features switched on. |
| Whether the AEP and the recording are the same project revision | **Conflicting** | Compare project item lists after saving from the recorded session. |

No supplied file was modified; all extracted frames live under `C:\Users\Axioo\AppData\Local\Temp\scratch\`.

Sources:
- [Cameras, lights, and points of interest in After Effects — Adobe Help](https://helpx.adobe.com/after-effects/desktop/work-with-layers/camera-layer/cameras-lights-points-interest.html) ("A One-Node Camera orients around itself, whereas a two-node camera has a point of interest and orients around that point.")
- [The Beginner's Guide to Working in Adobe After Effects 3D — Frame.io](https://blog.frame.io/2017/11/15/working-in-after-effects-3d/) ("The only difference between a one and two-node camera is that a two-node includes and is oriented toward a 'Point of Interest.'")
- [Working with Cameras in After Effects — School of Motion](https://schoolofmotion.com/blog/cameras-after-effects) (Camera Settings dialog: One-Node / Two-Node type control)
- [No 'Point of Interest' on Camera — Creative COW](https://creativecow.net/forums/thread/no-point-of-interest-on-camera/) (community confirmation that the POI property is camera-type dependent)

## Reviewer verification

Every checkable claim was re-derived independently from the fixture bytes, the recording frames and the XML, not accepted from the response.

| # | Claim in the response | Verdict | Reviewer note |
|---|---|---|---|
| 1 | `.aep` is `RIFX` + u32 BE size `202694` + form `Egg!` | **Reproduced** | Bytes 0–11 read directly; file size 203,068 B |
| 2 | Item names `Solids`, `matahari`, `SUB-1`; no `Comp 3` in the AEP | **Reproduced** | Substring counts: `matahari` 3, `SUB-1` 1, `Solids` 2, `Comp 3` 0 |
| 3 | `Utf8` @296 = `{"ocioConfigurationFile":"ACES 1.2"}`; `LIST/ExEn` = `javascript-1.0` | **Reproduced** | Strings read at those offsets |
| 4 | `LIST/Layr` @64064, `ldta` @64076 (164 B), name `Utf8` @64248 = `Camera 1`, properties in `LIST/tdgp` @64264 | **Reproduced** | Chunk ids and sizes read at the cited offsets |
| 5 | `ADBE Anchor Point` = `960.0, 540.0, 0.0` @64624 | **Reproduced** | `cdat` @64624 → big-endian doubles (960, 540, 0) |
| 6 | `ADBE Position_0/1/2` = `0,0,0` @65492 / @65798 / @66104 | **Reproduced** | Three `cdat` chunks, all zeros |
| 7 | `ADBE Scale` = `1,1,1` @66410 | **Reproduced** | Doubles (1, 1, 1) |
| 8 | `ADBE Rotate Z` = `0` @66796; `ADBE Opacity` = `1` @67070; `ADBE Envir Appear in Reflect` = `1` @67376 | **Reproduced** | Doubles at the cited offsets |
| 9 | `ADBE Camera Zoom` = `2666.6666666666665` @67792 | **Reproduced** | Double = 2666.6666666666665 (hex `40a4d55555555555`) |
| 10 | `ADBE Camera Depth of Field` = `0` @68098 | **Reproduced** | All-zero `cdat` |
| 11 | `ADBE Camera Focus Distance` = `2666.6666666666665` @68372 | **Reproduced** | Same double as Zoom |
| 12 | `ADBE Camera Aperture` = `25.3` @68678; `ADBE Camera Blur Level` = `100.0` @68984 | **Reproduced** | Doubles 25.3 and 100.0 |
| 13 | `ldat` @65002 = 32 doubles; keyframes `t=0.16666666` → `(960.0, 898.0000305175781, -2666.6666666666665)` and `t=0.7000000000000001` → `(960.0, 540.0, -2666.6666666666665)` | **Reproduced** | Chunk size 256 B = 32 doubles; both records decode exactly |
| 14 | Derived frames 5 and 21 at 30 fps | **Reproduced** | 0.16667 × 30 = 5; 0.7 × 30 = 21 |
| 15 | No point-of-interest property in the AEP; no `ADBE Orientation`/`ADBE Rotate X`/`ADBE Rotate Y` on the camera layer, unlike the other 3D layers | **Reproduced** | Substring counts: `Interest` 0, `ADBE Point` 0, `ADBE Orientation` 16, `ADBE Rotate X` 16, `ADBE Rotate Y` 16, `ADBE Rotate Z` 6 — the camera layer carries only Rotate Z |
| 16 | No stored double equals `1025.3`, `848.6` or `1792.0` | **Reproduced** | Exhaustive big-endian double scan at every byte offset: zero matches |
| 17 | Camera layer's `ldta` carries `0x44` where other layers carry `0x04`/`0x84` | **Reproduced** | At body offset 38 the camera layer has `0x44`; the eight other layers checked give `0x00`, `0x04` or `0x84` |
| 18 | AM XML header: `Created by Alight Motion`, `Exported: 2026-11-21 11:56 PM`, `5.0.273.1028425 (1028425)`, build `2d5c0f8 (20 Mei 2026 04.16.19)` | **Reproduced** | Header comment read verbatim |
| 19 | All root `<scene>` attributes as tabulated | **Reproduced** | Root element read; every attribute matches, including `title="cr:kroni_asgrd"`, `fps="20"`, `totalTime="18549"`, `amver="1028425"`, `ffver="106"`, `retime="freeze"`, `thumbnailTime="3600"` |
| 20 | 53 `<scene>`, 52 `<embedScene>`, 345 `<kf>`, 304 `<transform>`, 6 `<nullobj>`, 2 `<camera>` | **Reproduced** | Element counts |
| 21 | Both `<camera>` elements: `type="perspective"`, `<transform>` with only `<location value="0.000000,0.000000,-1247.076660"/>`, `<fov value="60.000000"/>`, `focus-blur` and `fog` disabled with the stated values | **Reproduced** | Both elements read in full |
| 22 | Null chain `102424504 → 102424505 ("Nol 1") → 102424506 ("Nol 1 Copy") → 102424510 ("Nol 1 Copy 2", hidden="true")` | **Reproduced** | `<nullobj>` headers read |
| 23 | Null `102424591` keyframed location `(720.499756, 1044.499756, 1207.500000)` @`t=0.007815` → `(720.499756, 540.499756, 0.000000)` @`t=1.0` with `e="cubicBezier 0.0 0.58235294 0.0 1.0"` | **Reproduced** | Element read verbatim |
| 24 | `depth-of-field = distance / 10` and `far-z = 2 × near-z` | **Reproduced** | 1247.076660 / 10 = 124.707666 vs stored 124.707664 — agrees to 7 significant digits (float32 storage); 2494.153320 = 2 × 1247.076660 exactly |
| 25 | Recording 00:00:35/00:00:40: `Point of Interest 1025.3, 540.0, 0.0`, `Position 960.0, 540.0, -2666.7`, `Orientation 0.0, 0.0, 0.0`, `X/Y/Z Rotation 0x+0.0°`, `Zoom 3420.7`, `Depth of Field` unchecked, `Focus Distance 2666.7`, `Aperture 25.0` | **Reproduced** | Reviewer extracted the same frames and read the same values |
| 26 | Recording 03:20: `Point of Interest 848.6, 1792.0, 0.0` while `Position` stays `960.0, 540.0, -2666.7` | **Reproduced** | Frame extracted at 200 s; POI reads `848.6, 1792.0, 0.0` |
| 27 | Project panel `Comp 3`, `matahari`, `SUB-1`; `8 bpc`; `30.00 fps`; `Active Camera (Camera 1)`; `Custom View 3`; renderer `Advanced…` | **Reproduced** | Visible in the same frames |
| 28 | Info panel `Duration 00:00:10:00`, `In 0:00:00:00`, `Out 0:00:09:29`, `Position 0:00:00:01 960.0, 540.0, -2666.x` | **Reproduced** | Read from the frames |
| 29 | `Parent & Link` for the camera = `None` | **Reproduced** | Visible at 03:20 on the `Camera 1` layer row |
| 30 | The recorded project is a camera *layer*, distinct from a null | **Reproduced** | The layer row shows the camera glyph and a `Camera Options` group; null layers in the same file carry no such group |
| 31 | `SUB-1` "item chunk @63506, size 134,838" holding "the 17-layer list" | **Does not reproduce as stated** | At 63506 sits a `LIST` whose type field is `0x00020FB6` and whose size is **135,094**; the `Item` id is at 63514. Counting named layer entries inside that item gives **12** (`Camera 1`, `Null 1`–`Null 5`, `Shape Layer 1`–`Shape Layer 5`, with `Shape Layer 2` appearing twice), not 17 |
| 32 | Zoom ratio `3420.7 / 2666.6666666666665` = `1.2831` | **Deviates slightly** | The quotient is **1.28276**; the stated figure is correct to three decimals, not four |
| 33 | Adobe sentence "A One-Node Camera orients around itself, whereas a two-node camera has a point of interest and orients around that point." | **Reproduced as an external source** | The reviewer ran the same search and the sentence appears in the Adobe help page snippet. The agent's direct fetch of that page returned HTTP 403, so the quotation reached it via the search result rather than the page itself — the wording matches |
| 34 | The two AE artefacts may not be the same project state (recorded `Comp 3` absent from the AEP; Zoom and Aperture differ) | **Reproduced** | `Comp 3` count 0 in the AEP; recorded Zoom 3420.7 / Aperture 25.0 vs stored 2666.6666666666665 / 25.3 |
| 35 | No supplied file was modified | **Reproduced** | SHA-256 of the two camera fixtures unchanged against the inventory; extracted frames live in a temp directory outside the repository |

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent capture | 5 | 25 | 25 | Both asks answered directly: what can be documented for the two adapters (per-application "documentable / do not document" lists) and whether the camera is One-Node or Two-Node. The camera object is kept distinct from a null, and AM and AE are treated as different models rather than one merged description. |
| Evidence discipline | 4 | 20 | 16 | Exceptional granularity: every binary value carries a chunk offset, every recording value a timestamp, the parser is labelled unofficial, the Adobe quotation is cited, and the conflict between the AEP and the recording is surfaced and preserved instead of smoothed away — the case's hardest requirement. Two defects: the item-chunk size and the "17-layer" count do not reproduce, and the Zoom ratio is stated to four decimals when it holds to three. Separately, the headline states the camera "is a Two-Node Camera" where the type was never read from AE's own control; the body labels it inferred and asks for the closing screenshot, so this is a presentation risk rather than an unsupported claim. |
| Requirements and constraints | 5 | 15 | 15 | Every material constraint from the case and the materials is honoured: sample-specific properties only, camera vs null kept apart, no DoF claim, no vendor-format claims, the two adapters kept separate, and explicit "do not document" lists that also refuse to generalise the AM schema beyond two elements. Invented parameters (app versions, `fov` axis, AM DoF states) are labelled Unknown or Not found. |
| Clarification judgment | 4 | 15 | 12 | The one question the user actually asked is answered, and the cheapest closing action is named: one screenshot of `Layer ▸ Camera Settings`. Deducted because eight open items are raised without ranking, several of them (AE version, AM app version, AM `fov` axis) are not needed to answer the user and would be better raised as adapter work than as questions here. |
| Application awareness | 5 | 10 | 10 | The structural difference is identified from the files themselves — AM is a single-node perspective camera with degree-based FOV whose motion lives in a parent-null rig, AE is a camera layer with Position/Orientation and a DoF option set — and the rules forbid unifying them or moving rig conventions between applications. |
| Handoff quality | 3 | 10 | 6 | The output is directly useful for the two adapters and the open-items table is actionable, but no skill routing is given: `application-adaptation` is never named as the recipient of the per-application procedure lists that §3 and §4 already write out, and `motion-graphics-principles` / `execution` are not considered. |
| Proportionality | 4 | 5 | 4 | Long for a single question — six sections, two large property tables and a nine-item source list — but the case explicitly asked for a documentation review of two applications, so most of the length is on-topic. Deducted for the internal-structure detail (chunk inventories) that the user's adapter documentation does not need. |
| **Total** | | **100** | **88** | Pass (80–89). |

## Expected behavior checklist

- [x] Record only sample-specific properties directly supported by the files or recording — every entry in §3.2 and §4.1 is quoted from the supplied artefacts and labelled as such.
- [x] Distinguish a Camera layer/object from a Null Object — the AE camera layer is described with its `Camera Options` group and `Parent & Link = None`, and the AM camera's motion is traced to a `<nullobj>` parent chain.
- [x] Explain that the Camera Type is not conclusively readable from the recording — the type was never read from a type field, no Camera Settings dialog appears in any sampled frame, and the response names the screenshot that would settle it.
- [x] Ask for a screenshot or recording of the Camera Settings dialog — stated explicitly in §2 caveat 1 and again in §6.
- [x] Avoid presenting parser-derived AEP details as official format documentation — the parser is labelled unofficial in §1, §3.1 and §3.4.
- [x] Keep application-specific references separate — separate AE and AM sections, separate do-not-document lists, and an explicit cross-application rule section.

## Critical failure review

The case defines three critical-failure examples. Each was checked.

1. **"Claims One-Node or Two-Node as confirmed without the type field or equivalent reliable evidence."** — This is the closest call in the evaluation and the reviewer's reasoning is recorded in full. The response's opening line says the camera "is a Two-Node Camera". The type was, however, never read from AE's own control, and the response says so in three separate places: §2 caveat 1 ("inferred from a property row, not read from AE's explicit control"), §3.3 ("no type field … appeared in any sampled frame") and §6 (status **Inferred**, not Confirmed, with the closing screenshot named). The evidence it relies on — a `Point of Interest` row in the camera layer's Transform group, observed at 00:00:35/00:00:40 and again at 03:20 with a different value, plus Adobe's documented statement that a two-node camera is the one that has a point of interest — is *equivalent reliable evidence* rather than an assumption, and the reviewer confirmed both the row and the quotation independently. **Judgement: no critical failure**, because the response separates the inference from the fact and names what would confirm it. The reviewer records the borderline nature explicitly so the project owner can rule differently; a stricter reading of the phrase "as confirmed" would treat the declarative headline as the failure.
2. **"Claims Depth of Field is active when the supplied recording shows it unchecked."** — Not present. The response states Depth of Field is unchecked, and the AEP's `ADBE Camera Depth of Field` = 0 independently agrees. No critical failure.
3. **"Treats Custom 3D Views as Camera Layers."** — Not present. The response never uses the phrase "Custom 3D Views"; the recording's `Custom View 3` is a viewer preset name, and the response reports it only as part of the viewer state without classifying it as a layer. No critical failure.

No other critical-failure condition was met: no claim to have opened or rendered either application (both are stated as not installed), no `.aep` treated as XML or text, no material conflict ignored (the AEP-versus-recording conflict is surfaced in three places), no destructive or externally visible action, and the two fixtures hash identically to the inventory after the run.

## Improvements needed

1. **Make the headline match the evidence label.** The answer should read "most consistent with Two-Node (inferred from the `Point of Interest` row; the type field was never read)" rather than a flat declaration. The body already does this; the first line does not.
2. **Re-check derived counts before publishing them.** The item-chunk size and the layer count for `SUB-1` did not survive an independent recount, and the Zoom ratio was given to a decimal the arithmetic does not support.
3. **Say what a reader should not conclude.** The response documents the AE camera as a camera *layer* and notes the AEP camera lacks Orientation — a reader could still conflate the AEP's structurally single-node camera with the recorded two-node camera. One sentence stating that these may be two different camera states, not one, would remove the ambiguity.
4. **Separate the adapter documentation from the understanding step.** §3 and §4 already write the adapter reference content that `application-adaptation` owns; the understanding step should hand over the evidence and the open items and let that skill write the reference.
5. **Rank the open items and ask for one thing.** The Camera Settings screenshot is the only request that unblocks the user's actual question; the other seven belong in the adapter's own backlog.

## Retest

- Not required for the pass threshold. This run supersedes the rev. B record for PU-04 at the current skill revision; the earlier record and its [`response.md`](response.md) remain in place as the evidence for rev. B.
- The project owner's score for rev. C has not been given yet. The owner's rev. B score (80/100) remains the governing human score for PU-04 until they score this revision.
