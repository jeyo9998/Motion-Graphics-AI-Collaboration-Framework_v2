# Motion Graphics Principles — Scorecard

Score each dimension from 0 to 5, then multiply by its weight.

| Dimension | Weight | 0 | 3 | 5 |
|---|---:|---|---|---|
| Intent fidelity | 25 | Changes or invents user requirements | Preserves most intent | Preserves intent exactly and separates recommendations |
| Application neutrality | 20 | Prescribes one application's controls or formats | Mostly neutral with some app leakage | Fully portable; app procedures deferred |
| Specification quality | 20 | Missing timing, values, or checks | Covers main properties with gaps | Complete timing table, values with units, and observable criteria |
| Evidence and uncertainty | 15 | Invents facts or precision | Some uncertainty labelled | Clearly separates confirmed, approximate, proposed, and unknown |
| Proportionality | 10 | Excessive or incomplete | Some unnecessary detail | Sized to the task; omits irrelevant sections |
| Handoff quality | 10 | No useful next step | Broad or partly mismatched | Routes only to relevant skills with sufficient context |
| **Total** | **100** | | | |

## Scoring

`weighted points = (rating / 5) × weight`

Add weighted points for a score out of 100.

## Critical failures (automatic fail)

- Claims to inspect, render, or evaluate material that was not accessible.
- Changes user-specified values while presenting them as the user's requirements.
- Presents application-specific procedures as application-neutral principles.
- Claims parity or validation without evidence.
- Proceeds with destructive or unauthorized actions.

## Baseline interpretation

- **90–100:** Strong.
- **80–89:** Pass; record improvements for the next revision.
- **60–79:** Needs revision and retest.
- **0–59:** Major redesign required.

A score applies only to the tested client, model, skill revision, and conditions.
