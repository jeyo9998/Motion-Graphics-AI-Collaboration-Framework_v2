---
name: motion-graphics-execution
description: Coordinates approved Motion Graphics work from brief through checked completion, decomposing it into sequenced work items, approval gates, and evidence-backed status. Use when the user asks to create, modify, improve, or troubleshoot actual project work.
---

# Motion Graphics Execution

## Purpose

Own the *what, in what order, and how completion is judged* of an approved task. This skill sequences work and tracks status; it does not select the low-level technical method, and it does not decide whether the visual result is good.

## Use When

- The user asks to create, modify, improve, or troubleshoot actual project work.
- An approved brief and creative specification exist.
- Multiple operations must be ordered, gated, or tracked.

## Don't Use When

- There is no approved brief yet (use `project-understanding`).
- The shared creative specification is missing (use `motion-graphics-principles`).
- A concrete operation needs a technical route (use `hybrid-execution`).
- An existing result must be judged (use `visual-evaluation`).
- A known failure must be diagnosed (use `error-analysis`).

## Inputs

- Project Understanding Brief.
- Motion Principles Specification with acceptance criteria.
- Application Adaptation Plan, when an application is known.
- Permissions, backup status, and delivery constraints.

## Workflow

### 1. Verify the inputs

Check that objective, acceptance criteria, target application, and permissions are present. If a critical input is missing, state the blocker and hand back rather than inventing it.

### 2. Decompose into work items

Create the smallest set of work items that covers the task. Each item states:

- What changes.
- Which acceptance criterion it serves.
- Its dependencies and required inputs.
- Whether it is reversible and whether a backup exists.
- Which skill performs it (`hybrid-execution`, usually).

Avoid unnecessary steps. Do not add redesign work that the brief did not request.

### 3. Sequence and gate

Order items by dependency. Mark approval gates for destructive, irreversible, externally visible, or scope-changing actions. Define what must be true before each gate opens.

### 4. Delegate operations

For each work item, hand the concrete operation to `hybrid-execution` with enough context to act without re-deciding the creative brief. Execution must not silently broaden scope.

### 5. Track status precisely

Use these states consistently:

- `planned` — described, not attempted.
- `attempted` — started, completion not established.
- `completed` — operation finished, result not yet validated.
- `verified` — checked against a stated criterion with evidence.
- `blocked` — cannot proceed due to a named missing tool, permission, input, or dependency.

Never promote an item to `verified` without evidence.

### 6. Close through evaluation

When operations are complete, pass the result and the unchanged acceptance criteria to `visual-evaluation`. If evaluation reports a mismatch, route to `error-analysis`; do not guess a cause here.

### 7. Report

Produce an Execution Plan and Status Log. Record planned, attempted, completed, verified, and blocked work as separate facts.

## Output Format

```markdown
## Execution Plan
- Objective:
- Acceptance criteria:
- Target application / version:
- Backup / recovery status:
- Work items: id | action | criterion | depends on | reversible | status
- Approval gates:
- Open blockers:
- Next skill:
```

## Rules

1. Do not self-approve a gate the user must approve.
2. Do not change the creative brief or acceptance criteria; propose changes explicitly.
3. Do not claim a visual result is verified; that belongs to `visual-evaluation`.
4. Do not choose the technical method; that belongs to `hybrid-execution`.
5. Preserve originals and record recovery status before risky work.
6. Record every blocker with the exact missing dependency.
7. Keep the plan proportional; a single clear operation does not need a large plan.

## Examples

### Example 1: Single title animation

Work items: create composition, create text layer, animate position and opacity, verify structure, hand to visual evaluation. One gate: none, because the work is reversible and non-destructive. Status starts `planned`; the agent does not report `verified` until the result is checked.

### Example 2: Modifying a supplied project

Before any change, record that a backup or copy is required and obtain approval if the original would be overwritten. Work on the copy. The status log records the copy path and the original's untouched state.

### Example 3: Blocked operation

If no verified scripting interface exists for the target version, mark the scripted export item `blocked`, name the missing evidence, and propose a UI route or a verification step through `hybrid-execution`.

## Edge Cases

- **Conflicting user instructions:** stop and resolve through `project-understanding`.
- **Partial completion:** keep each item's own status; never mark the whole task done.
- **Unexpected side effects:** stop, record what happened, and request direction before continuing.
- **Delivery pressure:** do not skip evaluation gates to save time.

## References

- [Skill architecture](../../SKILL-ARCHITECTURE.md)
- [Project specification](../../PROJECT-SPECIFICATION.md)
