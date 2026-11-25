---
name: application-adaptation
description: Translates a shared Motion Graphics specification into verified, application-specific procedures for Alight Motion or Adobe After Effects, recording evidence status, version, and unknowns. Use when the target application is known and implementation details are needed.
---

# Application Adaptation

## Purpose

Map an application-neutral creative specification onto one target application without inventing capabilities. This skill supplies verified knowledge and procedures; it does not perform the operation and it does not assume that a documented tool or integration is installed.

## Use When

- The target application is known and implementation details are required.
- A shared specification must be implemented in Alight Motion and/or After Effects.
- The agent needs to explain application-specific terminology, structure, or dependencies.
- A procedure must be checked for version and platform applicability.

## Don't Use When

- The creative specification does not exist yet (use `motion-graphics-principles`).
- The target application is unknown and the choice affects implementation (return to `project-understanding`).
- A concrete operation must actually be carried out (use `hybrid-execution`).

## Inputs

- Motion Principles Specification with acceptance criteria.
- Target application and, where known, version and platform.
- Available references and their evidence status.
- User constraints on editability, assets, and delivery.

## Evidence Model

Every application-specific claim must carry one of these labels:

- **Official:** stated by the application vendor's documentation for the named version.
- **Observed in sample:** present in a supplied file or recording; not generalized.
- **Inferred:** reasoned from evidence but not confirmed.
- **Unverified:** no sufficient evidence.
- **Not tested:** no relevant test performed.

Never present an inferred or unofficial-parser observation as official documentation. Never transfer a procedure between applications because the names look similar.

## Workflow

### 1. Confirm the target context

Record the application, version, platform, and project format. If the version is unknown, state that version-sensitive procedures cannot be confirmed and identify what would confirm them.

### 2. Load the relevant reference

Read only the reference needed for the task:

- `references/alight-motion/` for Alight Motion.
- `references/after-effects/` for Adobe After Effects.
- `references/EVIDENCE-TEMPLATE.md` when adding new findings.

References are evidence records, not a promise that every procedure is available in every version.

### 3. Map shared concepts to application concepts

For each element of the creative specification, identify:

- The application construct that can express it.
- Required assets, fonts, effects, or plugins.
- Parameter ranges and units, with evidence status.
- Known version or platform differences.
- What cannot be reproduced faithfully.

If no verified mapping exists, say so and propose a verification step.

### 4. Produce an Application Adaptation Plan

For each application, provide an ordered plan with:

- Preconditions and dependencies.
- Constructs and parameters, each labelled with evidence status.
- Required checks before and after the operation.
- What must be validated in the native application.
- What remains unknown.

Do not present a plan as an implemented integration.

### 5. Hand off

Pass the plan to `motion-graphics-execution` for sequencing and to `hybrid-execution` when a concrete method must be chosen. The shared acceptance criteria remain authoritative; application parity is judged by the creative outcome, not identical controls.

## Output Format

```markdown
## Application Adaptation Plan
- Application / version / platform:
- Shared specification reference:
- Evidence sources:
- Construct mapping: intent | construct | parameters | evidence status | notes
- Ordered procedure:
- Dependencies and permissions:
- Native validation required:
- Unknowns / conflicts:
- Recommended next skill:
```

## Rules

1. Keep Alight Motion and After Effects references separate.
2. Do not claim an integration, plugin, script, or automation exists because a procedure is documented.
3. Do not invent parameter names, ranges, or default values.
4. Preserve original project files; any experiment uses a copy.
5. Record the application and version for every finding.
6. Label unofficial parsers and reverse-engineered format observations accordingly.
7. If application capabilities are insufficient for the creative intent, say so and propose an alternative.
8. Keep sample-specific observations separate from general behavior.

## Examples

### Example 1: Camera evidence

A recording shows a camera layer and an animated zoom value but does not show the camera type field. The plan records what is observed, states that the camera type cannot be conclusively determined from the recording, and identifies the specific dialog or field needed to confirm it.

### Example 2: Cross-application movement

The shared specification requires horizontal travel plus one full rotation. Produce two separate plans. Each plan records the application's own keyframe/easing model with evidence status; neither plan claims the other application's representation applies.

### Example 3: Unverified automation

The user asks for a scripted export. Record that no verified scripting interface for the target version is available in this repository, avoid inventing an API, and propose either a documented interface check or a UI-based route through `hybrid-execution`.

## Edge Cases

- **Unknown application version:** treat version-sensitive steps as unverified and say why.
- **Conflicting documentation:** preserve the conflict and ask which source is authoritative.
- **Missing plugin/asset:** mark the dependency; do not silently substitute.
- **User-supplied project file:** inspect a copy only, with authorization.

## References

- [Alight Motion reference](references/alight-motion/README.md)
- [After Effects reference](references/after-effects/README.md)
- [Evidence template](references/EVIDENCE-TEMPLATE.md)
- [Skill architecture](../../SKILL-ARCHITECTURE.md)
