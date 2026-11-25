# MP-03 — Raw Response

Captured verbatim from the 2026-11-24 background-agent run. See [`prompt.md`](prompt.md) for conditions.

---

## Motion Principles Specification

- **Objective:** Make a single rounded rectangle read as one continuous object crossing the frame while completing exactly one full turn, with a specification that both Alight Motion and After Effects can implement separately to the same visible outcome.

- **User requirements (verbatim intent):**
  1. The subject is a **rounded rectangle**.
  2. It **travels horizontally across the frame**.
  3. It **rotates exactly once** (one full revolution — exact, not approximate).
  4. The result must **work equally well in Alight Motion and After Effects**.

- **Recommendations (clearly labelled):** Everything below this line is mine, not yours. Duration, distance, size, proportions, easing, and direction are unspecified in your request, so I have proposed values that are labelled "proposal" and marked the ones that branch the outcome as **Choice**.

**Subject and role:** One shape layer, the sole moving element. The motion reads as an **arrival/positioning beat** (proposal): the shape enters, crosses, and comes to rest as a settled composition anchor. If you intended it as a pass-through or an exit instead, the end position and hold change.

**Spatial path:**
- Direction: left → right (proposal; you said "horizontally" without a direction — **Choice A**: left-to-right / right-to-left).
- Motion is strictly horizontal: the vertical centre stays constant at **50% of composition height** throughout. No vertical drift, no arc.
- Position is expressed in **normalised composition coordinates** so it is resolution- and app-independent: start centre x = **−10% of composition width** (fully off-frame), end centre x = **+50% of composition width** (horizontally centred). Total travel ≈ 60% of composition width.
- Shape proportions (approx, proposals): width ≈ **30% of composition width**, height ≈ **18% of composition height**, corner radius ≈ **12% of the shape's short side**.

**Rotation:** 0° → 360° about the **shape's centre** over the same interval. "Exactly once" is carried into the spec as: the rotation must be a **monotonic accumulation of 360° of angular displacement across the interval** — not a start/end pair that happens to be numerically equivalent. A specification written as "start and end look the same" will not produce visible turning in either application.

**Rotation-vs-travel coupling (Choice B — materially changes the feel):**
- **B1 — rotation linear, travel eased:** constant spin rate; the shape reads as mechanically turning.
- **B2 — rotation eased identically to travel:** turning rate tracks travel rate; the shape reads as one object settling (recommended default).
- **B3 — rolling look:** rotation rate is derived from distance travelled, so it reads like the shape rolls rather than spins. This requires the rotation amount to stay locked to the travel distance, and it is the option most likely to need compromise on one of the two targets — say so before implementation if you want it.

**Timing table:**

| property | start | end | value | exact/approx | notes |
|---|---|---|---|---|---|
| Position X | 0.30 s | 1.50 s | −10% → 50% of comp width | values approx; interval approx | proposal; horizontal only |
| Position Y | 0.00 s | end of comp | 50% of comp height | approx | constant |
| Rotation | 0.30 s | 1.50 s | 0° → 360° | **rotation exact**; interval approx | one revolution, monotonic, about centre |
| Hold (pre) | 0.00 s | 0.30 s | off-frame at start position | approx | static; drop if no lead-in wanted |
| Hold (post) | 1.50 s | end of comp | at rest, centred | approx | nothing animates |
| Opacity / Scale | — | — | unchanged | — | not part of your brief; not added |

Timing is stated in seconds against a **proposed 3.0 s composition**; convert to frames at whatever frame rate the project uses. Percentages of composition duration are equivalent: travel spans roughly **10%–50%** of the composition.

**Easing character:** travel = **ease-in-out, soft at both ends, no overshoot** (proposal). Overshoot is a **Choice C** — it reads livelier but the shape momentarily reverses direction and stops further right than specified, and the two applications will not reproduce the same overshoot shape from the same words. Describe any numeric curve you add as a suggestion, because a curve authored in one application is not a curve in the other.

**Composition and hierarchy:** Canvas, aspect ratio, frame rate, and background are **unknown**. The shape is the only element, so hierarchy and reading order are not applicable. Colour roles: unspecified — one high-contrast fill against the background, stroke optional and thin relative to the corner radius (proposal). No typography is requested, so none is added. Safe area: keep the resting position inside the central 90% of width and 80% of height so the shape is not crowded by edges after turning.

**Transitions:** Entry is off-frame at the left edge with no fade or scale — the shape becomes visible by crossing the boundary. Exit: none; the shape remains at rest. If you want it to leave the frame instead of parking, that replaces the post-move hold and changes Choice A's meaning.

**Acceptance criteria:**
1. The path is horizontal — vertical centre unchanged from start to rest, within the stated tolerance.
2. Rotation completes **exactly once** during the 0.30–1.50 s interval: no partial turn, no second turn, no frozen shape that merely starts and ends at the same angle.
3. Travel distance and duration match the specification within the stated tolerance; direction matches the chosen option.
4. One continuously visible object: no snapping, popping, jumps in angle, or discontinuity at the end of the turn.
5. The resting shape sits inside the stated safe area with the corner radius reading as a rounded rectangle rather than a near-circle or a hard-edged box.
6. Criteria 1–5 are checkable in a preview or render in either application. Criteria 2 and 4 additionally **require native-side confirmation per application**, because whether one revolution renders identically depends on how each application interprets angular interpolation — this is a hand-off question, not something this specification settles.
   None of these are marked as passing; nothing has been produced or reviewed yet.

**Dependencies and unknowns:**
- Unknown: composition size, aspect ratio, frame rate, total duration, background, fill colour, whether other elements exist.
- Open choices needing your call: **A** direction, **B** rotation/travel coupling (B1/B2/B3), **C** easing with or without overshoot, plus the actual duration and the arrival-vs-passthrough intent.
- Dependency: this spec deliberately contains no keyframe model, no easing-control names, and no layer or anchor-point instructions for either application.

**Verification required in native application:** how each application expresses a full accumulated revolution, how each one's pivot/anchor convention affects rotation about the shape's centre, whether rounded-corner geometry is authored equivalently, and whether the proposed easing character reproduces comparably. These belong to the next stage.

**Hand-off:** send this to `application-adaptation` to produce **two separate implementations** judged against the same criteria above, then to `motion-graphics-execution` for sequencing, and to `visual-evaluation` later with these acceptance criteria unchanged. Tell me your picks for A, B, and C (and a real duration and canvas if you have them) and I will tighten the numbers before that hand-off.
