# PU-02 — Evaluation Record

- **Case ID:** PU-02 — Ambiguous creative request
- **Date:** 2026-11-24
- **AI client / model:** Qoder background agent, fresh context; model selected automatically
- **Skill revision:** working copy of `skills/project-understanding/SKILL.md` at **rev. A**, 2026-11-24 (no version field or commit)
- **Test environment:** Windows, repository working copy; no native application access
- **Input materials:** none
- **Score:** **80 / 100**
- **Critical failure:** **No**

## Raw evidence

- Response file: [`response.md`](response.md)
- Prompt and conditions: [`prompt.md`](prompt.md)
- Relevant excerpts:
  - "I don't have the edit itself — no project file, rendered preview, or screenshots came through" — states the access gap.
  - "I don't want to guess at fixes for a result I haven't seen" — avoids unsupported claims.
  - "These are proposals based on common patterns, not observations about your edit" — labels recommendations.
  - Asks for preview, application, and what "professional" means.

## Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent capture | 4 | 25 | 20 | Correctly identifies the goal and that it cannot be assessed yet; does not misstate the request. |
| Evidence discipline | 5 | 20 | 20 | Clearly separates absence of evidence from possible patterns; no invented observations. |
| Requirements and constraints | 3 | 15 | 9 | Captures that application/version and target context matter, but does not reduce them to a minimal set. |
| Clarification judgment | 4 | 15 | 12 | Asks focused, material questions in one grouped list; no long questionnaire. |
| Application awareness | 4 | 10 | 8 | Distinguishes Alight Motion and After Effects without mixing procedures. |
| Handoff quality | 4 | 10 | 8 | Clear next step (send preview) with useful review scope. |
| Proportionality | 3 | 5 | 3 | The seven-item generic improvement list is longer than needed before seeing the material. |
| **Total** | | **100** | **80** | Pass (threshold, no critical failure). |

## Expected behavior checklist

- [x] Recognizes the outcome is underspecified and no edit is accessible.
- [x] States it cannot assess the edit without project, preview, or screenshots.
- [x] Asks for the edit or an accessible visual reference.
- [x] Offers review areas, clearly labelled as possibilities rather than observed problems.
- [x] Avoids a long questionnaire (one grouped list of three inputs).
- [ ] Proportionality is borderline: the generic advice catalogue exceeds the minimum needed.

## Critical failure review

- Finding: none.
- Evidence: no claim to have seen or evaluated the edit; no stated defects presented as facts.
- Impact: none.

## Improvements needed

- Non-blocking at 80/100: cap optional review-area advice at approximately three items before material is available.
- Consider adding this limit to the skill's Example 2 on the next revision, then retest PU-02.

## Retest

- Not required for the pass threshold.
- Must be re-run if `project-understanding` is revised.

## Re-run after the 2026-11-24 skill revision

- **Score: 85 / 100** (this record's 80 applied to the pre-revision skill, which was at the threshold). No critical failure.
- Example 2's new three-item cap held: three suggestions, one line each, labelled as suggestions.
- Remaining gap is stating the intended outcome and naming the next skill.
- Conditions, verbatim response, and dimension table: [`retest-2026-11-24.md`](retest-2026-11-24.md).
