# Independent Reviewer Brief — PU-03 / PU-04

A copy-paste brief for a reviewer that is **not** the agent that wrote the skill, ran the cases, or scored them first (for example Claude, another model, or a human). Its purpose is to produce per-dimension scores with the answer key withheld until after verification.

## What the reviewer needs

- The repository working copy, read-only.
- These two response files, and nothing else from `results/`:
  - `evals/project-understanding/results/PU-03/response.md`
  - `evals/project-understanding/results/PU-04/response.md`
- The rubric `evals/project-understanding/scorecard.md` and the case definitions in `evals/project-understanding/cases.md`.
- Fixtures under `evals/fixtures/`; recordings at `D:/Download/rekam kamera/` (owner machine only — substitute another path if reviewing elsewhere).
- **Must not read:** any `evaluation.md`, `review-log.md`, `evals/README.md`, or `evals/self-review/` content. Those hold prior scores. If a score is seen accidentally, say so.
- **Working-context warning:** the client harness auto-attaches `AGENTS.md` to every agent session, and `AGENTS.md` contains earlier scores. Instruct the reviewer to disregard any score that arrives with the working context, and to record that the exposure occurred (as the 2026-11-24 reviewer B did) rather than omitting it.

## Prompt to give the reviewer

> You are an independent evaluation reviewer. Score each case response per dimension using the repository's weighted scorecard. Verify the response's load-bearing claims against the fixture files and recordings yourself before scoring; do not accept the response's own citations as proof. For each case, produce: a table of Dimension | Weight | Score 0–5 | Weighted points | one-sentence rationale; a total /100 with pass/fail against the threshold; a list of claims you reproduced; a list of claims you could not reproduce, with what you found instead; and any critical failure (fabricated evidence, claimed inspection that did not occur), or "none". Be adversarial; do not inflate. Do not read any existing evaluation record or score.

## How the result is recorded

- Save the returned tables verbatim in the relevant `evaluation.md` under "Independent review (reviewer B)" with the reviewer's name and date.
- Reviewer B's score does not overwrite the existing scores; it is added. The project owner's score remains governing.
- A reviewer-B score from the same model family as the original run (for example, another instance of the same agent) is labelled as such and does **not** close the SR-05 same-agent limitation. Only a different model or a human reviewer can do that.
