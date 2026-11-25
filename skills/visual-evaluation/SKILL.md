---
name: visual-evaluation
description: Judges a Motion Graphics result against approved acceptance criteria using available preview, render, screenshot, or project-state evidence, and reports pass, partial, fail, or not testable. Use when an output or project state exists and must be checked.
---

# Visual Evaluation

## Purpose

Determine whether an observed result meets the user-approved acceptance criteria. This skill identifies mismatches; it does not explain their cause. Evaluation is limited to the evidence actually available.

## Use When

- A preview, render, screenshot, project state, or other result can be inspected.
- A pass/partial/fail decision is required against agreed criteria.
- A correction needs re-evaluation against the same criteria.

## Don't Use When

- No result exists yet (the status is `not testable`; do not invent a verdict).
- The cause of a mismatch must be diagnosed (use `error-analysis`).
- The task is planning or execution (use the corresponding skill).

## Inputs

- Acceptance criteria from the brief or Motion Principles Specification.
- The result and its evidence location.
- Known limitations of the evidence (resolution, frame coverage, compression, inspection method).

## Workflow

### 1. Confirm the criteria

Restate the exact criteria being evaluated. Do not add new requirements and do not relax existing ones. If a criterion is ambiguous, mark it as requiring clarification rather than guessing.

### 2. Inventory the evidence

Classify each item:

- Native application preview or render.
- Exported video or image sequence.
- Screenshot supplied by the user.
- Project-file inspection (structure only).
- Third-party parser output (label as unofficial).

Record what was **actually inspected**, what was merely listed, and what was unavailable. Do not claim to have viewed frames or states you did not see.

### 3. Define observable checks

For each criterion, state:

- The observable property.
- The expected value or range, including tolerance.
- The evidence needed to judge it.
- Whether the available evidence can support a conclusion.

If the evidence cannot support a check, mark it `not testable` rather than passing or failing it.

### 4. Evaluate each check

Report one status per check: `pass`, `fail`, `partial`, or `not testable`, with the supporting evidence and its provenance. Keep observation separate from interpretation.

### 5. Summarize

Give an overall status using the weakest material result:

- `pass` — all material criteria pass with adequate evidence.
- `partial` — some criteria pass and some are unmet or unsupported.
- `fail` — a material criterion is demonstrably unmet.
- `not testable` — evidence is insufficient for a verdict.

### 6. Hand off

If the result is partial or fail, pass the mismatch and evidence to `error-analysis`. Do not propose a root cause here. After a correction, re-evaluate against the unchanged criteria.

## Output Format

```markdown
## Visual Evaluation Report
- Criteria source:
- Result / evidence location:
- Evidence classification: inspected | listed | unavailable
- Source limitations:
- Checks: criterion | expected | observed | status | evidence
- Overall status: pass / partial / fail / not testable
- What remains untested:
- Recommended next skill:
```

## Rules

1. Do not infer a cause from a mismatch; that belongs to `error-analysis`.
2. Do not claim to have inspected frames, states, or files that were not accessible.
3. Distinguish native-app preview from file/parser inspection.
4. Preserve original files; evaluate copies when possible.
5. Judgement applies only to the tested result, application version, and conditions.
6. Do not average away a failed material criterion.
7. Do not treat a plausible-looking output as a pass without checks.

## Examples

### Example 1: Title animation

Criteria: 1920×1080, 30 fps, 3 s, upward movement of approximately 120 px in the first second, full opacity by 1 s, then static. With a supplied render and project state, inspect frames at 0 s, 0.5 s, 1 s, and 2 s, record observed positions and opacity, and mark approximate distance within tolerance. Do not claim pixel-identical hold without frame-by-frame evidence.

### Example 2: Cross-application comparison

Evaluate each application's output separately against the same shared criteria. Do not penalize different internal controls. Do not declare parity without evidence from both outputs.

### Example 3: Project file only

If only the project structure is available and no render exists, structural checks (layer present, keyframes exist) can pass while visual criteria remain `not testable`. State this explicitly.

## Edge Cases

- **Compressed preview:** note artifacts that limit fine-detail judgement.
- **Partial frame coverage:** mark criteria outside the sampled range as not testable.
- **User-supplied screenshot:** record provenance and crop/scale limitations.
- **Conflicting criteria:** stop and resolve through `project-understanding`.

## References

- [Skill architecture](../../SKILL-ARCHITECTURE.md)
- [Project specification](../../PROJECT-SPECIFICATION.md)
