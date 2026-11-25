# Evaluation Fixtures

Motion Graphics project files used as test material for `evals/project-understanding/` (PU-03, PU-04) and `evals/motion-graphics-principles/`.

## Authorization and ownership

- Provided by the project owner on **2026-11-24** from `D:/Download/update`, and the owner directed that they be moved into this repository.
- **Copied, not moved:** the original files remain untouched at `D:/Download/update/XML/` and `D:/Download/update/aep/`. Re-verified on 2026-11-24 after inclusion: all seven originals hash identical to the repository copies. Delete them there only if the owner decides to.
- These are the owner's own work. They stay the owner's property; the repository's **MIT license (selected 2026-11-24) covers the framework's original work only, not these files** — inclusion here does not grant reuse or redistribution rights to anyone else (see `AGENTS.md` §11 and §13, and the scope note in the root `README.md`).
- No credentials, personal identifying data, or third-party licensed media are known to be embedded. Not yet verified: asset references inside the projects (fonts, footage, images) may point to files not included here.

## Integrity — SHA-256

Re-check with `sha256sum evals/fixtures/alight-motion/* evals/fixtures/after-effects/*` from the repository root.

| File | Size | SHA-256 |
|---|---:|---|
| `alight-motion/Motion_Graphics_unik.xml` | 276.954 B | `c31748fa2140a586446a77fd9091a6e508cabf777a6370d36ede3a928d879a32` |
| `alight-motion/movement_1.xml` | 3.115 B | `8d7010a8e8bf9e156210b147ec4e63687290f03378443b8d86a74d6c1467f1dc` |
| `alight-motion/movement_2.xml` | 1.940 B | `6c8083f1a814039d410903386a433600826104a89120a108fd2c4bb4db2f4dda` |
| `after-effects/Motion_Graphics_Unik.aep` | 25.704 B | `e790748e6d4ce01448b2e5a788ab301160c2f63ef524fa844fa4d418fd4d23f5` |
| `after-effects/Motion_Graphics_Unik_Camera.aep` | 203.068 B | `f6269372fd3a7bc894edd3b3b9d520a002e9a745be1d40b3226fde07d00f8e1c` |
| `after-effects/movement_1.aep` | 45.416 B | `7067f17d5c7064a126a53aa2ee3aff1098fa4c2b7acb862862ac753cddca0da6` |
| `after-effects/movement_2.aep` | 197.708 B | `6279b42b92f8f167ec3ededdae92cb28386cfcc677a9b4e765260e9b467a1866` |

All seven matched the source files at copy time.

## What each fixture is for

| File | Application | Verified properties | Supports |
|---|---|---|---|
| `alight-motion/movement_1.xml` | Alight Motion | 1920×1080, 120 fps, 19 keyframes; `.roundrect` layer "Persegi Panjang Bulat 1" travels x 0 → 795,378052 (t 0,051819 → 0,624813) with `cubicBezier 0.86685157 0.0 0.43377253 1.0` | PU-03, MP-03 comparison |
| `alight-motion/movement_2.xml` | Alight Motion | 1920×1080, 120 fps, 8 keyframes, 1 shape, 2 `rotation` | PU-03 |
| `alight-motion/Motion_Graphics_unik.xml` | Alight Motion | 1440×1080, 20 fps, 345 keyframes, 182 `shape`, 304 `transform`, 164 `effect`, 1011 `property` | PU-03 (complex case), **PU-04** (camera objects) |
| `after-effects/movement_1.aep` / `movement_2.aep` | After Effects | binary `.aep`, XMP `application/vnd.adobe.aftereffects.project` | PU-03 |
| `after-effects/Motion_Graphics_Unik.aep` | After Effects | binary `.aep`, same XMP marker | PU-03 |
| `after-effects/Motion_Graphics_Unik_Camera.aep` | After Effects | binary `.aep`; byte strings `Camera 1`, `(ADBE Camera Options Group`, `(ADBE Camera Zoom` | **PU-04** (camera capability) |

## Camera content, verified in the Alight Motion XML

Read from the repository copy as text; no application was opened.

`alight-motion/Motion_Graphics_unik.xml` declares two `<camera>` elements, both labelled `Kamera 1`:

```xml
<camera id="102424590" label="Kamera 1" startTime="0" endTime="18549"
        mediaFillMode="fill" parent="102424591" type="perspective">
  <transform><location value="0.000000,0.000000,-1247.076660" /></transform>
  <fov value="60.000000" />
  <focus-blur enabled="false"> … </focus-blur>
  <fog enabled="false"> … </fog>
</camera>
```

- `type="perspective"` and `fov` are explicit attributes; `focus-blur` and `fog` are present but **disabled**.
- Each camera's `parent` id resolves to a separate `<nullobj label="Nol 1">`. In this format a camera and a null object are **different element types**, not the same object under a different name.
- Status: **Observed in sample** for Alight Motion `5.0.273.1028425`. It says nothing about how the application displays these in the Camera Options UI, and nothing about After Effects.

## Screen recordings (supplied 2026-11-24, kept outside the repository)

The owner pointed to `D:/Download/rekam kamera/` for PU-04's recording fixture. Three MP4s exist there. They are **not copied into the repository**: together they are ~540 MB, and they capture the owner's desktop and phone screens. `AGENTS.md` §11 forbids committing private recordings without explicit permission and a licensing basis, so they are referenced by path and hash instead.

| File | Size | Duration | Resolution / fps | Content verified from extracted frames |
|---|---:|---|---|---|
| `Recording 2026-11-24 070641.mp4` | 368.534.467 B | 00:05:59.40 | 1918×994, 30 fps, h264 Main + aac | **After Effects desktop session** — the PU-04 recording fixture |
| `screen-20261124-215814.mp4` | 129.381.205 B | 00:07:03.65 | 720×1612 portrait, ~42,7 fps | **Alight Motion on Android** — layer stack, `Tambahkan` menu, `Move & Transform`, bezier editor |
| `screen-20261124-220101.mp4` | 43.576.575 B | 00:02:18.48 | 720×1612 portrait, ~45,3 fps | **Alight Motion on Android** — `Kamera 1` track, easing curves, numeric entry |

SHA-256 (re-check with `sha256sum "/d/Download/rekam kamera"/*.mp4`):

```text
3b0e82b8e0ab31ef79a5af87656c285869d35fc2bc3c750e11410878a2ba3b33  Recording 2026-11-24 070641.mp4
f4507a6920d00993f9e7b5cc05c7da52c7854e13f138e40dce7a61f2527fbd89  screen-20261124-215814.mp4
ce6f252b98427e2a33c81fda854bb82f6c1dc76947448f69926e57c0c40f127b  screen-20261124-220101.mp4
```

Duration, resolution, and codec were read from the MP4 `mvhd`/`tkhd`/`stsd` boxes and confirmed with a decoder. The portrait recordings are the reason the two phone files were not mistaken for the After Effects evidence.

### What the After Effects recording actually shows

Frames were sampled across the full 5:59 (every 25 s for the property panel, every 10 s for the whole UI) and read as images.

- A camera layer `Camera 1` is selected. Its timeline group **Transform** lists `Point of Interest`, `Position`, `Orientation`, `X/Y/Z Rotation`; a second group **Camera Options** lists `Zoom`, `Depth of Field`, `Focus Distance`, `Aperture`, `Blur Level`, `Iris Shape` (`Fast Rectangle`).
- Values seen include `Point of Interest 1025.3, 540.0, 0.0` → `848.6, 1792.0, 0.0`; `Position 960.0, 540.0, -1422.0 / -2582.7 / -2666.7`; `Zoom 3420.7 → 7353.3 → 6400.7`; `Focus Distance 2666.7`; `Aperture 25.3`; `Blur Level 100.0 %`. Comps `SUB-1`, `matahari`, `Comp 3` at 30.00 fps. A second camera labelled `cx Camera 1` appears later.
- **The Camera Settings dialog never appears in any sampled frame**, and no One-Node/Two-Node control is visible anywhere in the recording. The Graph Editor is shown several times; a Playback Settings panel appears in some frames.

That last point is the evidence boundary PU-04 was written to test, and it is now observable rather than assumed.

### Frame evidence location

Extracted frames used as the inspection surface for the runs are staged **outside the repository** at
`…/motion-graphics-ai-handoff-v1.0/evidence/recording-frames/` (`ae_01.jpg`, `ae_06.jpg`, `sheet_01.jpg`, `full_ae.jpg`, `phone2.jpg`, `phone3.jpg`, ~900 KB total). They show owner application UI, so they are likewise not committed. Regenerate with any decoder, e.g.

```bash
ffmpeg -i "D:/Download/rekam kamera/Recording 2026-11-24 070641.mp4" \
  -vf "fps=1/25,crop=1000:300:0:694,scale=500:150,tile=2x7" -frames:v 1 sheet.jpg
```

## Rules for using these fixtures

1. **Read-only.** Do not edit, re-save, or "clean up" a fixture. If a run needs a modified copy, create it outside the repository and say so in the record.
2. **`.aep` is not XML.** Treat After Effects files as binary; do not parse them as interchange XML and do not present unofficial parser output as Adobe documentation (`AGENTS.md` §6).
3. Evidence from these files is **Observed in sample** — never generalize it to every version of the application.
4. Record the application and version when a claim depends on them: these XML exports came from Alight Motion `5.0.273.1028425` on Android.
5. No claim that a project opened, rendered, or executed may be recorded — the test environment has no access to either application.
