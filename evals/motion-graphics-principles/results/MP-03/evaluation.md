# MP-03 — Evaluation Record

- **Case ID:** MP-03 — Cross-application parity
- **Date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/motion-graphics-principles/SKILL.md` at **rev. A** (before the Review 004 edits), 2026-11-24; no version field or commit
- **Input materials:** none
- **Score:** **93 / 100**
- **Critical failure? (Yes/No; describe):** No.
- **Raw response:** [`response.md`](response.md) · **Conditions:** [`prompt.md`](prompt.md)

## Evidence summary

- Produced **one** specification for both targets rather than two creative briefs; application work is explicitly deferred to a single implementation-stage hand-off.
- Carried "rotating exactly once" through as a *monotonic accumulation of 360°*, rejecting the start-value-equals-end-value formulation that produces no visible turn. This is the substantive trap in the case and it was handled.
- Expressed position in normalised composition coordinates, so the spec survives different canvas sizes and applications.
- Marked every unstated parameter (canvas, aspect ratio, frame rate, duration, background, colour, direction, shape proportions) as unknown or as a labelled proposal, and separated the three branching decisions as explicit choices.
- Stated that criteria 2 and 4 need per-application native confirmation, and that parity is not established by the document; nothing was marked as passing.
- No keyframe model, easing-control name, anchor-point or layer instruction appears anywhere in the response.

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent fidelity | 5 | 25 | 25 | Rounded rectangle, horizontal travel, exactly one revolution, dual-target parity all preserved as written. |
| Application neutrality | 5 | 20 | 20 | No app controls or formats; implementation deferred as a single named hand-off. |
| Specification quality | 5 | 20 | 20 | Timing table with units, exact/approx column, normalised coordinates, five observable criteria. |
| Evidence and uncertainty | 4 | 15 | 12 | Unknowns, proposals and choices are cleanly separated — but "a specification written as 'start and end look the same' will not produce visible turning in **either application**" is a cross-application behaviour claim stated as fact, not deferred. |
| Proportionality | 3 | 10 | 6 | Three branching choices with sub-options, a pre-hold, and corner-radius proportions go beyond what was asked; the answer is the longest of the three runs. |
| Handoff quality | 5 | 10 | 10 | Routes to `application-adaptation`, then `motion-graphics-execution` and `visual-evaluation`, with the acceptance criteria carried unchanged. |
| **Total** | | **100** | **93** | Strong (≥ 90). |

## Expected behavior checklist

- [x] Produces one application-neutral specification with shared duration, path, rotation, and acceptance criteria.
- [x] Keeps application-specific implementation out of the shared spec and hands it to application adaptation.
- [x] Does not claim that both applications can reproduce identical controls or that parity is already achieved.
- [x] Marks missing parameters (distance, duration, frame rate) as unknowns or clearly labelled proposals.
- [ ] Proportionate: the option tree and decorative parameters exceed the minimum.

## Critical failure review

- **Finding:** none.
- **Evidence:** no inspection or render claim; no parity claim; no user value altered; no application procedure presented as a principle.
- **Impact:** none.

## Improvements needed

- One cross-application behavioural assertion was presented as fact. The skill should require that *any* claim about how an application would interpret a construct be phrased as a question for application adaptation, not embedded in the shared spec.
- Trim the optional parameter proposals (corner radius, pre-hold, safe-area percentages) when the user has not asked for them, or collect them in one short "defaults I assumed" line.

## Retest

- Not required for the pass threshold. MP-03 was **not** re-run after the 2026-11-24 skill edit; this score applies only to the revision recorded above.
