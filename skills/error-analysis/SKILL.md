---
name: error-analysis
description: Diagnoses a known Motion Graphics discrepancy or failure by separating observed symptoms from confirmed facts and hypotheses, testing causes, and verifying a correction. Use when evaluation or execution reports an unexpected result.
---

# Error Analysis

## Purpose

Investigate a specific, observed problem. Separate what is known from what is suspected, design minimal tests, and verify whether a correction actually fixes the issue. This skill does not judge the visual result and does not silently redesign the task.

## Use When

- `visual-evaluation` reports a partial/fail result.
- `hybrid-execution` or `motion-graphics-execution` hits an unexpected outcome.
- A user reports a reproducible problem with project material available.

## Don't Use When

- No concrete problem exists yet (use `visual-evaluation` to establish one).
- The issue is simply a missing input or permission (record the blocker instead).
- A creative direction change is being requested (return to `project-understanding`).

## Inputs

- The observed symptom, with evidence.
- The acceptance criterion that was not met.
- Environment: application/version/platform, tools, method used.
- Relevant logs, screenshots, project copies, and recent changes.

## Workflow

### 1. Record the symptom precisely

State what was observed, when, with which evidence, and what was expected. Avoid blame and avoid conclusions. Distinguish the symptom from the user's interpretation of it.

### 2. Establish confirmed facts

List only facts supported by evidence:

- Inputs and their hashes or names.
- Environment and version.
- Steps actually performed and their results.
- Error messages or logs, quoted exactly.
- What was not accessible.

### 3. Generate hypotheses

List plausible causes, including at minimum:

- Incorrect input or missing asset.
- Procedure or parameter error.
- Application/version limitation or difference.
- File-format or parser limitation.
- Environment/tool/permission problem.
- Requirement ambiguity.

Label each hypothesis `suspected` until tested.

### 4. Design minimal tests

Choose the smallest reversible test that distinguishes hypotheses. Record what each test would prove or disprove. Prefer copies and read-only checks; do not run destructive experiments.

### 5. Test and classify

Record results. Classify each cause as:

- `confirmed` — supported by direct evidence.
- `suspected` — consistent with evidence but not proven.
- `unknown` — no sufficient evidence.
- `ruled out` — contradicted by evidence.

Do not upgrade a hypothesis to confirmed without a test or reliable source.

### 6. Propose and verify a correction

Hand the correction to `motion-graphics-execution`/`hybrid-execution`. After the correction, have `visual-evaluation` re-check the same criteria. Report the verified resolution or leave the issue explicitly unresolved.

### 7. Record the lesson

If the cause and fix are verified, record a concise, reusable lesson with scope and version. Do not generalize a sample-specific observation into universal application behavior.

## Output Format

```markdown
## Error Analysis Report
- Symptom (observed):
- Expected:
- Confirmed facts:
- Environment:
- Hypotheses: cause | status | test | evidence
- Tests performed:
- Confirmed cause / suspected / unknown:
- Correction performed:
- Re-evaluation result:
- Remaining uncertainty:
- Lesson recorded:
```

## Rules

1. Never present a hypothesis as a confirmed cause.
2. Quote evidence exactly; do not paraphrase error messages into a diagnosis.
3. Preserve the failing artifact; do not overwrite the only evidence copy.
4. Do not change acceptance criteria to make a failure disappear.
5. Do not run destructive or irreversible tests without approval.
6. Distinguish application behavior from tooling/parser behavior.
7. If the cause remains unknown, say so and state what evidence would resolve it.

## Examples

### Example 1: Motion ends early

Symptom: the animation reaches its final position before the specified time. Confirmed facts: keyframe timestamps from the project copy and the rendered frame times. Hypotheses: wrong keyframe time, frame-rate mismatch, or easing overshoot. Test by comparing keyframe times against the target frame rate. Report the confirmed cause only after the comparison, then re-evaluate.

### Example 2: Text appears blurry

Symptom: text is soft in a preview. Confirmed facts: preview resolution and export settings. Hypotheses: source scaling, compression, or motion blur. Do not assert one cause from a compressed preview; request a higher-quality frame or inspect project settings.

### Example 3: Script fails

Record the exact error, script version, and application version. Test whether the failure is a missing dependency, an unsupported API for that version, or a script error. Do not claim the application lacks the capability until the version-specific test supports it.

## Edge Cases

- **Intermittent problem:** record conditions and attempt a reproducible case; do not claim a fix without reproduction.
- **User changed multiple things:** isolate variables with a copy.
- **Conflicting evidence:** preserve the conflict and test it.
- **External/third-party tool:** label its behavior as tool-specific.

## References

- [Skill architecture](../../SKILL-ARCHITECTURE.md)
- [Project specification](../../PROJECT-SPECIFICATION.md)
