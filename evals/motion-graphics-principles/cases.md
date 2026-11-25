# Motion Graphics Principles — Test Cases

Use a fresh conversation for each case. Do not rewrite these prompts when running the official evaluation.

## MP-01 — Clear brief to motion specification

**Purpose:** Verify complete, application-neutral timing and motion specification.

**User prompt:**

> I'm building a 3-second title in a 1920×1080, 30 fps composition. The title should fade in while moving upward by about 120 pixels during the first second, then hold still for the rest of the composition. Give me an application-neutral motion specification I can implement in either Alight Motion or After Effects.

**Expected behavior:**

- Restates the objective without changing values.
- Preserves "about 120 pixels" as approximate.
- Provides a timing table for position and opacity covering 0–1 s and the 1–3 s hold.
- Describes easing as a feel (for example, soft ease-out) and labels numeric curves as proposals.
- Derives observable acceptance criteria.
- Avoids application-specific controls and hands off to application adaptation.
- Does not add mandatory design elements the user did not request.

**Critical failures:**

- Changes duration, direction, distance, or frame rate.
- Prescribes one application's controls as universal.
- Claims a criterion has passed without evaluation.

## MP-02 — Ambiguous creative direction

**Purpose:** Verify proportionate handling when there is no material to inspect.

**User prompt:**

> Make my logo reveal feel more premium.

No project file, preview, or reference is supplied.

**Expected behavior:**

- States that the reveal cannot be assessed without project or visual material.
- Asks for the smallest useful input (preview or screenshots).
- Optionally offers a short set of review areas, clearly labelled as possibilities.
- Does not invent specific flaws or a full redesign.
- Does not claim the material was inspected.

**Critical failures:**

- Claims to have seen or evaluated the reveal.
- States specific defects without evidence.
- Rewrites the request as a mandatory redesign.

## MP-03 — Cross-application parity

**Purpose:** Verify that shared intent is separated from application implementation.

**User prompt:**

> Create a specification for a rounded rectangle that travels horizontally across the frame while rotating exactly once. It must work equally well in Alight Motion and After Effects.

**Expected behavior:**

- Produces one application-neutral specification with shared duration, path, rotation, and acceptance criteria.
- Keeps application-specific implementation out of the shared spec and hands it to application adaptation.
- Does not claim that both applications can reproduce identical controls or that parity is already achieved.
- Marks missing parameters (distance, duration, frame rate) as unknowns or clearly labelled proposals.

**Critical failures:**

- Produces two conflicting creative specifications.
- Assumes identical keyframe/easing representations.
- Claims native-app parity without evidence.

## Result template

```markdown
# MP-XX — Evaluation Record

- Case ID:
- Date:
- AI client / model:
- Skill revision:
- Input materials:
- Score: Not scored / XX out of 100
- Critical failure: Yes / No

## Raw evidence
- Response file:
- Relevant excerpts:

## Dimension scores
| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |

## Expected behavior checklist
- [ ] ...

## Critical failure review
- Finding:
- Evidence:
- Impact:

## Improvements needed
- ...

## Retest
- Skill revision:
- Result:
```
