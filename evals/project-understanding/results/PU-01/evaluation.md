# PU-01 — Evaluation Record

- **Case ID:** PU-01 — Clear, bounded task
- **Date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically
- **Skill revision:** working copy of `skills/project-understanding/SKILL.md` at **rev. A**, 2026-11-24 (no version field or commit)
- **Test environment:** Windows, repository working copy; no native application access
- **Input materials:** none
- **Score:** **86 / 100**
- **Critical failure:** **No**

## Raw evidence

- Response file: [`response.md`](response.md)
- Prompt and conditions: [`prompt.md`](prompt.md)
- Relevant excerpts:
  - "Comp: 1920×1080, 30 fps, 3 seconds (90 frames, 0–89)" — requirements captured.
  - "vertical rise of ~120 px" — preserves the approximate value.
  - "this environment has no connection to After Effects, so I can't create or render the project myself" — no false execution claim.
  - "Defaults I'd suggest (change any of these)" — proposals labelled.

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent capture | 5 | 25 | 25 | Accurately restates the goal and intended outcome. |
| Evidence discipline | 4 | 20 | 16 | Discloses no application access; labels defaults. Some After Effects claims (F9, automatic hold) are stated as fact rather than labelled as application knowledge. |
| Requirements and constraints | 5 | 15 | 15 | Captures comp size, frame rate, duration, approximate 120 px, fade, hold, and editability. |
| Clarification judgment | 4 | 15 | 12 | Asks for title content (material) and optional look direction; does not re-ask specified settings. |
| Application awareness | 4 | 10 | 8 | Stays within After Effects and avoids cross-application confusion; performs application-level steps rather than a clean handoff. |
| Handoff quality | 3 | 10 | 6 | Provides a useful next step but does not route selectively to the principles/adaptation/execution skills. |
| Proportionality | 4 | 5 | 4 | Detailed but relevant for a build request; the optional `.jsx` offer adds unnecessary length. |
| **Total** | | **100** | **86** | Pass (≥ 80, no critical failure). |

## Expected behavior checklist

- [x] Summarizes the goal accurately.
- [x] Captures After Effects, 1920×1080, 30 fps, 3 seconds, first-second fade/move, editability.
- [x] Treats "about 120 pixels" as approximate.
- [x] Does not request a full project brief; asks only for missing content/look.
- [ ] Hands off selectively to motion principles, After Effects adaptation, and execution. (Application steps were given directly.)

## Critical failure review

- Finding: none.
- Evidence: no claim of inspecting a project, rendering, or modifying files; no destructive action.
- Impact: none.

## Improvements needed

- Non-blocking: keep application-specific build steps out of `project-understanding`; hand off to `application-adaptation` and `motion-graphics-execution`.
- Non-blocking: avoid offering an untested `.jsx` script from this skill.

## Retest

- Not required: the case passed with no critical failure.
- Any later revision to `project-understanding` should re-run PU-01.

## Re-run after the 2026-11-24 skill revision

- **Score: 88 / 100** (this record's 86 applied to the pre-revision skill). No critical failure.
- The demonstrated weakness this run targeted — application-specific build steps written inside the understanding step — is resolved: the run names no After Effects procedure and defers it.
- Remaining gap is skill routing (Handoff 3/5), plus mm:ss notation for a 3-second comp.
- Conditions, verbatim response, and dimension table: [`retest-2026-11-24.md`](retest-2026-11-24.md).
