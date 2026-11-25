---
name: motion-graphics-principles
description: Converts an approved Motion Graphics brief into an application-neutral creative and motion specification covering composition, hierarchy, typography, color, timing, easing, and transitions. Use when a task needs design or animation reasoning before application-specific procedures are chosen.
---

# Motion Graphics Principles

## Purpose

Translate the user's approved intent into a reusable, application-neutral creative specification. This skill owns *what the motion should look and feel like*; it does not own how a specific application implements it.

The output must be portable: another agent should be able to implement it in Alight Motion or After Effects without this skill choosing one application's controls.

## Use When

- A brief exists and requires composition, timing, motion, or transition reasoning.
- The user asks for creative direction or animation advice.
- A plan needs shared creative parameters before application adaptation.
- Two applications must reach the same creative outcome.

## Don't Use When

- The user only needs application-specific procedures (use `application-adaptation`).
- The task is a concrete file/UI operation (use `hybrid-execution`).
- The result already exists and must be judged (use `visual-evaluation`).
- Intent is still unclear or conflicting (return to `project-understanding`).

## Inputs

- The understanding brief, especially objective, intended outcome, constraints, and acceptance criteria.
- Any supplied references, with their classification and inspection status.
- Target applications, only to avoid non-portable assumptions; do not design around one app's controls.

## Workflow

### 1. Restate the intent without changing it

Summarize the creative goal in one or two sentences. Clearly separate the user's requirements from your recommendations. If the brief is missing or stale, stop and hand back to `project-understanding`.

### 2. Define the motion concept

Describe, in application-neutral terms:

- **Subject and role:** what moves, and why it matters in the composition.
- **Narrative beat:** what the motion should communicate (arrival, emphasis, transition, exit).
- **Spatial path:** direction, distance, and relation to composition bounds.
- **Rotation/scale/opacity behavior:** only the dimensions the concept needs.
- **Interaction with other elements:** sequencing, overlap, continuity.

Do not invent mandatory elements that the user did not request.

### 3. Build a timing specification

Express timing in seconds, frames, or percentages of the composition duration. For each animated property, state:

- Start and end time.
- Start and end value, with units.
- Whether the value is exact or approximate; preserve the user's wording (for example, "about 120 px" stays approximate).
- Hold periods and total duration.

Use a table when more than one property is animated.

### 4. Specify easing as a feel, not a control

Describe easing by observable character: linear, ease-in, ease-out, ease-in-out, snappy, soft, overshoot, stepped. Give a number only when its unit and source are defined; otherwise a strength range with no reference is invented precision. Always note that the application's implementation may differ. Do not name controls from one application as if they were universal.

### 5. Specify composition and hierarchy

Where relevant, state:

- Canvas, aspect ratio, and safe areas.
- Visual hierarchy and reading order.
- Alignment and spacing rules.
- Typography role, weight, and relative scale (avoid inventing exact fonts unless supplied).
- Color roles and contrast intent.

### 6. Define transitions and continuity

Specify what enters, exits, or transforms, and at which boundaries. Note overlap and continuity requirements. Mark any transition that depends on unavailable material as unknown.

### 7. Derive observable acceptance criteria

Convert the specification into checks a reviewer can observe in a preview or render, for example:

- Direction, distance, and duration match the specification within the stated tolerance.
- Rotation completes exactly once during the stated interval.
- Text remains legible and within safe areas.
- The result remains editable if required.

Label criteria that need native-app validation.

### 8. Hand off

Produce a **Motion Principles Specification** and pass it to the relevant skills:

- `application-adaptation` to map it to each target application.
- `motion-graphics-execution` to sequence the work.
- `visual-evaluation` later, with the same acceptance criteria.

## Output Format

```markdown
## Motion Principles Specification
- Objective:
- User requirements (verbatim intent):
- Recommendations (clearly labelled):
- Subject and role:
- Spatial path:
- Rotation / scale / opacity:
- Timing table: property | start | end | value | exact/approx | notes
- Easing character:
- Composition and hierarchy:
- Transitions:
- Acceptance criteria:
- Dependencies and unknowns:
- Verification required in native application:
```

Omit sections that do not apply. Keep the specification proportional to the task.

## Rules

1. Never rewrite user requirements as if they were your recommendations.
2. Never force Alight Motion and After Effects into identical controls or terminology.
3. Do not add speculative application procedures; this skill stays application-neutral.
4. Mark proposals, inferences, and unknowns explicitly.
5. Preserve approximate values as approximate.
6. Do not claim a criterion passes before evaluation.
7. Keep exact specifications where the user gave exact values; avoid inventing precision.
8. If a creative decision could materially change the outcome, present it as a choice for the user rather than silently deciding.
9. Never assert how Alight Motion or After Effects will interpret something. Phrase it as a question for `application-adaptation`.
10. Propose optional parameters only when they change the observable result; collect the rest into one labelled defaults line.

## Examples

### Example 1: Clear title animation

User intent: fade in while moving up about 120 px during the first second of a 3-second, 1920×1080, 30 fps composition, then hold.

Output: subject = title layer; path = vertical, approximately 120 px upward; opacity 0→100%; timing 0–1 s, hold 1–3 s; easing described as soft ease-out (proposal); acceptance criteria include direction, approximate distance, one-second duration, and legibility.

### Example 2: Cross-application movement

User intent: a rounded rectangle travels horizontally and rotates once.

Output: one shared specification (path, one full rotation, duration, proportions) with application-neutral easing character. Hand off to `application-adaptation` for separate implementations; do not prescribe one application's keyframe model.

### Example 3: Ambiguous "more premium"

If no visual material is available, do not invent specific flaws. Ask for one smallest input — a preview or a few frames — and hold the remaining questions until it arrives. Offer at most three review areas, one line each, labelled as possibilities. State that the specification follows `project-understanding` once material exists.

## Edge Cases

- **Missing duration or canvas:** mark unknown; propose a default only if it is low-risk and label it as a proposal.
- **Conflicting references:** describe the conflict and ask which reference takes priority.
- **Effect that depends on unavailable plugins/assets:** mark the dependency and avoid assuming availability.
- **User asks for "the best" easing:** explain trade-offs and propose, rather than asserting a universal best.

## References

- [Agent Skills specification](https://agentskills.io/specification)
- [Project specification](../../PROJECT-SPECIFICATION.md)
- [Skill architecture](../../SKILL-ARCHITECTURE.md)
