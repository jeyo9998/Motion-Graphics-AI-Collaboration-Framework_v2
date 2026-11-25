# Project Understanding — Evaluation Pack

**Status:** At skill **rev. B** (2026-11-24 runs): PU-01 **88/100 pass**, PU-02 **85/100 pass**, PU-03 **90/100 pass — the project owner's independent score, which governs** (reviewer A 83, reviewer B 90), PU-04 **80/100 pass — the project owner's independent score, which governs** (reviewer A 83, reviewer B 87; both agent scores carry the same-model limitation), PU-05 **94/100 pass**. At rev. A the PU-01/02/05 cases scored 86/80/86; those records are preserved. PU-03 and PU-04 were re-run against **rev. C** on 2026-11-24, each recorded in its own `retest-2026-11-24-revC.md` beside the preserved original response (PU-03 89/100, PU-04 88/100, reviewer A, no critical failure in either). Results apply only to the recorded client/conditions; no native application execution was tested.

This pack tests whether `skills/project-understanding/SKILL.md` can convert user requests and available project evidence into reliable, proportionate briefs and handoffs.

## How to run

1. Open the target AI-agent client that supports the repository's Agent Skills format.
2. Make sure `project-understanding` is available to the agent.
3. Run each case in a fresh conversation, providing only the materials named in that case.
4. Save the agent's response as evidence. Do not coach the agent during the first run.
5. Score the response using `scorecard.md`.
6. Record the client/model, date, exact skill revision or commit, score, failures, and evidence in `results/PU-XX/evaluation.md`. Preserve the raw prompt and response when practical.
7. Keep observed behavior separate from reviewer scores. A run record may be complete while its score remains explicitly `Not scored` until an independent reviewer applies `scorecard.md`.

Do not mark a case as passed just because the response sounds plausible. Check whether it followed the expected behavior and accurately represented the supplied evidence.

## Cases

See [`cases.md`](cases.md).

Reusable inventory helper: [`scripts/count-extensions.sh`](scripts/count-extensions.sh). Its regression test is [`../../tests/test_count_extensions.sh`](../../tests/test_count_extensions.sh).

Recorded runs: [`results/`](results/) — PU-01, PU-02, PU-05 scored at rev. A and re-scored at rev. B in `retest-2026-11-24.md`; PU-03 ran at rev. B on the in-repo fixtures (83 reviewer A / 90 reviewer B); PU-04 ran at rev. B on the in-repo fixtures plus the owner's screen recordings (80 owner / 83 reviewer A / 87 reviewer B), and both were re-run at rev. C in `retest-2026-11-24-revC.md` (PU-03 89 / PU-04 88, reviewer A). Both PU-03 and PU-04 record their fixture history and run conditions in their `prompt.md`/`evaluation.md`. Running a further independent review is described in [`independent-review-brief.md`](independent-review-brief.md).

## Passing rule

For the first baseline, a case passes when it scores at least 80/100 and has no critical failure. Critical failures include inventing inspected evidence, treating assumptions as confirmed, overlooking an important conflict, or proceeding with a consequential/destructive action without appropriate authorization.

A passing result only applies to the tested agent/client configuration. It does not establish universal compatibility.
