# MP-01 — Evaluation Record

- **Case ID:** MP-01 — Clear brief to motion specification
- **Date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/motion-graphics-principles/SKILL.md` at **rev. A** (before the Review 004 edits), 2026-11-24; no version field or commit
- **Input materials:** none (text brief only)
- **Score:** **95 / 100**
- **Critical failure? (Yes/No; describe):** No.
- **Raw response:** [`response.md`](response.md) · **Conditions:** [`prompt.md`](prompt.md)

## Evidence summary

- Restated every user value unchanged: 1920×1080, 30 fps, 3 s / 90 frames, upward move, first second, hold.
- Kept "about 120 pixels" approximate and gave an explicit intent band (110–130 px) rather than silently pinning it.
- Supplied a timing table covering 0–1 s and the 1–3 s hold for position, opacity, and the constant rotation/scale, with an exact-versus-approximate column.
- Described easing as behaviour ("begins at maximum rate, decelerates to rest, no overshoot") and stated that the same numeric value is not the same curve in the two applications.
- Derived eight observable acceptance criteria; none were marked as passing.
- Named no Alight Motion or After Effects control, panel, or file format; handed the mapping to application adaptation and listed what needs native verification.
- Declined to add unrequested design elements, and said so explicitly.

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent fidelity | 5 | 25 | 25 | All stated values preserved; approximation kept approximate. |
| Application neutrality | 5 | 20 | 20 | No app controls referenced; implementation deferred. |
| Specification quality | 5 | 20 | 20 | Complete timing table with units/frames plus observable criteria. |
| Evidence and uncertainty | 4 | 15 | 12 | Confirmed/recommended/assumed/unknown separated, but "0.6–0.75 strength" is invented precision with no defined unit. |
| Proportionality | 4 | 10 | 8 | Length suits a specification; the residual-settle and safe-area paragraphs exceed the ask. |
| Handoff quality | 5 | 10 | 10 | Routes to application adaptation with the verification questions attached. |
| **Total** | | **100** | **95** | Strong (≥ 90). |

## Expected behavior checklist

- [x] Restates the objective without changing values.
- [x] Preserves "about 120 pixels" as approximate.
- [x] Provides a timing table for position and opacity covering 0–1 s and the 1–3 s hold.
- [x] Describes easing as a feel and labels numeric curves as proposals.
- [x] Derives observable acceptance criteria.
- [x] Avoids application-specific controls and hands off to application adaptation.
- [x] Does not add mandatory design elements the user did not request.

## Critical failure review

- **Finding:** none.
- **Evidence:** no claim to have inspected, rendered, or evaluated anything; no user value altered; no application procedure presented as a principle; no parity claim.
- **Impact:** none.

## Improvements needed

- The skill invites a numeric example for easing; this run produced a strength range with no defined unit or reference. Numeric examples should only appear when the unit and its source are defined, otherwise describe the feel alone.
- Optional extras (residual settle, safe-area inset) could be dropped entirely rather than offered, since the user asked for a specification of one move.

## Retest

- Not required for the pass threshold. The improvement above was applied to the skill on 2026-11-24; MP-01 was **not** re-run against that revision, so this score applies only to the revision recorded at the top.
