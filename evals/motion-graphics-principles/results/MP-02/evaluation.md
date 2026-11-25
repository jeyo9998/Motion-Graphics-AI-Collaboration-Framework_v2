# MP-02 — Evaluation Record

- **Case ID:** MP-02 — Ambiguous creative direction with no material to inspect
- **Date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/motion-graphics-principles/SKILL.md` at **rev. A** (before the Review 004 edits), 2026-11-24; no version field or commit
- **Input materials:** none (no project file, preview, screenshot, or reference)
- **Score:** **84 / 100**
- **Critical failure? (Yes/No; describe):** No.
- **Raw response:** [`response.md`](response.md) · **Conditions:** [`prompt.md`](prompt.md)

## Evidence summary

- Opened by stating that the project, preview, and reference are not visible, and refused to name defects in work it had not seen.
- Made no claim to have inspected, rendered, or evaluated the reveal; the offered areas are explicitly labelled "my recommendations, not your brief".
- Did not rewrite the request as a redesign; asked whether the reveal is allowed to change duration.
- Asked for the smallest useful input, but listed four input items plus two direction questions rather than the one that unblocks the work.
- Produced **six** multi-line review areas where the case allows "a short set", plus a preview of what the eventual spec will contain — the response is roughly three times the size the situation needs.
- Kept the whole answer free of application controls and named no Alight Motion or After Effects behaviour.

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent fidelity | 5 | 25 | 25 | "Premium" treated as an unresolved direction, not rewritten into a mandate. |
| Application neutrality | 5 | 20 | 20 | No application controls, formats, or procedures referenced. |
| Specification quality | 3 | 20 | 12 | No specification produced (appropriate without material), but the candidate areas stay qualitative — no timing or measurable form. |
| Evidence and uncertainty | 5 | 15 | 15 | Clear "I can't see it / I'd be guessing" framing; recommendations separated from requirements. |
| Proportionality | 3 | 10 | 6 | Six detailed areas, four input requests, and two decision questions for a one-line prompt with no evidence. |
| Handoff quality | 3 | 10 | 6 | Promises a future app-neutral spec but names no skill and no routing. |
| **Total** | | **100** | **84** | Pass (≥ 80, no critical failure). |

## Expected behavior checklist

- [x] States that the reveal cannot be assessed without project or visual material.
- [x] Asks for the smallest useful input (preview or screenshots).
- [x] Offers a set of review areas, clearly labelled as possibilities.
- [x] Does not invent specific flaws or a full redesign.
- [x] Does not claim the material was inspected.
- [ ] Proportionate: the offered set is six detailed areas, not a short one, and the input request lists four items plus two decisions.

## Critical failure review

- **Finding:** none.
- **Evidence:** no inspection claim; no invented defect presented as a finding; no mandatory redesign; no application-specific procedure.
- **Impact:** none.

## Improvements needed

- The skill allows a "short set of review areas" without a cap; the model produced six detailed ones. Replace the cap-with-no-number with an explicit limit of three areas, one line each, when no material is available.
- The skill does not say what to do about unblocking questions, so the run accumulated four input requests. It should ask for the single smallest input first and hold the rest until the material arrives.
- No skill routing was given; the principles skill should hand to `project-understanding` (missing context) or `application-adaptation` (implementation) by name.

## Retest

- **Skill revision:** edited on 2026-11-24 after this score (three-area cap, single smallest input, explicit routing).
- **Result:** see [`retest-2026-11-24.md`](retest-2026-11-24.md) — recorded separately; this score remains attached to the pre-edit revision.
