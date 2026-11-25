# MP-01 — Raw Response

Captured verbatim from the 2026-11-24 background-agent run. See [`prompt.md`](prompt.md) for conditions.

---

## Motion Principles Specification

**Objective**
Produce one portable motion design for a 3-second title so that Alight Motion and After Effects can each implement the same observable result from the same numbers.

**User requirements (verbatim intent)**
- Composition: 1920×1080, 30 fps, 3 seconds total (90 frames).
- The title fades in.
- The title moves upward by *about* 120 pixels.
- Both happen during the first second.
- After that, the title holds still for the rest of the composition.

**Recommendations (clearly labelled as mine, not your brief)**
- Easing character: soft **ease-out** on both properties — fastest at the start, settling into place. This reads as a calm arrival and matches an upward fade-in. Alternatives: *ease-in-out* feels more gentle/weighted but slightly slower to register; *linear* looks mechanical for a title arrival. Proposal, not a universal best.
- Start offset: place the title about 120 px below its resting position at t=0, and animate up to the resting position. This keeps the final frame on your intended layout rather than leaving the title displaced.
- Synchronise opacity and position on the same interval so they land together.
- Optional, only if you want it: a small residual settle (a few px) after the main move. Not included below because you did not ask for it.

**Subject and role**
Single element: the title layer. It is the primary — apparently sole — focal element, so nothing else needs to be sequenced against it.

**Spatial path**
Purely vertical, upward, no horizontal drift. Distance approximately 120 px, which is roughly 11% of the 1080 px frame height. Direction and distance are relative to the composition, not to any specific origin, so both applications can express it as an offset from the resting position.

**Rotation / scale / opacity**
- Rotation: none — hold at 0 throughout.
- Scale: none — hold at 100% throughout.
- Opacity: 0% → 100% over the first second, then hold at 100%.
- Fully transparent at t=0 means the title is invisible at the start; that is a consequence of your fade-in, not an added requirement.

**Timing table**

| Property | Start | End (s) | End (frames) | Start value | End value | Exact/approx | Notes |
|---|---|---|---|---|---|---|---|
| Position (vertical) | 0 s (f0) | 1.0 s | f30 | resting + about 120 px below | resting position | Distance **approximate**; times **exact** | Move upward; no horizontal change |
| Opacity | 0 s (f0) | 1.0 s | f30 | 0% | 100% | Exact at the endpoints; ramp shape is a recommendation | Linear-in-time ramp unless ease-out is adopted |
| Position (hold) | 1.0 s (f30) | 3.0 s (f90) | f90 | resting | resting | Exact | No change |
| Opacity (hold) | 1.0 s (f30) | 3.0 s (f90) | f90 | 100% | 100% | Exact | Fully opaque |
| Rotation / Scale | 0 s | 3.0 s | f90 | 0 / 100% | 0 / 100% | Exact | Constant, specified so both apps agree nothing moves |

Composition duration is exact at 3.0 s / 90 frames. "About 120 px" stays approximate — treat 110–130 px as within intent unless you want it pinned to a number.

**Easing character**
Describe it as behaviour, not as a control: both properties begin at their maximum rate of change and decelerate to rest at 1.0 s, arriving without a jolt and without overshoot past the resting position. If you want a numeric curve, a candidate is an output-decelerating curve in the range of roughly 0.6–0.75 strength — labelled as a **proposal only**, because the same numeric value does not mean the same curve in the two applications. Match the *feel*, not the number.

**Composition and hierarchy**
- Canvas 1920×1080, 16:9, 30 fps.
- Safe area: keep the title's final bounding box inside a centre region inset by about 5% horizontally and vertically (roughly 96 px / 54 px), so the 120 px travel does not end near an edge. Recommendation.
- Reading order: single title, so the title is the sole entry point. Its resting placement was not specified — treat as unknown.
- Typography: role is primary headline; weight and scale unspecified. I have not invented a font, size, or resting position.
- Colour: no palette supplied. Intent should be high contrast between title and background so the 0→100% fade stays legible throughout the first second.

**Transitions**
No transitions requested. One inbound appearance (fade/rise) at the start, one static hold to the end, and no exit. The composition ends with the title fully opaque and at rest at f90.

**Acceptance criteria**
1. Title moves upward, not downward or diagonally.
2. Total vertical travel is approximately 120 px (110–130 px within intent).
3. Movement begins at f0 and is complete by 1.0 s / f30, holding still from f30 to f90.
4. Opacity reaches 100% no later than 1.0 s / f30 and stays there.
5. At the first frame the title is absent or near-absent; at the last frame it is fully opaque and stationary.
6. No rotation, no scale change, no overshoot past the resting position.
7. Final title position matches the intended layout position, and text stays legible and inside the safe area.
8. Total duration 3.0 s / 90 frames at 30 fps in 1920×1080.

**Dependencies and unknowns**
- Unknown: background content/colour behind the title.
- Unknown: font, size, weight, and the intended resting placement.
- Unknown: whether the title is one layer or split into words/lines. The 120 px travel and one-second fade are written for a single solid block; a per-word stagger would need a separate stagger specification.
- Assumption: the 120 px is in composition pixels at 1920×1080. If either application is working in a scaled or pre-composed space, convert before keyframing.
- Assumption: "hold still" means no motion of any kind, including no continuous drift.

**Verification required in native application**
- Exact interpolation produced by each application's easing, and whether the perceived settle matches after export and playback at real frame rate.
- Pixel distance, confirm by measurement in the composition at 1920×1080.
- Opacity endpoint behaviour (whether the fade reads as complete at f30 in the render).
- Whether a layer's anchor/origin setup affects the vertical offset in your project.

These are generic expectations, not verified behaviour of either application — no native-app testing has been done here. Next step is the application adaptation, which maps this specification separately to Alight Motion and After Effects rather than forcing identical controls. If you would like a different easing feel, or the 120 px pinned to an exact value, say which and I will revise the specification.
