# Evaluation Packs

Status matrix for skill evaluation. A run applies only to the tested client, model, skill revision, and conditions.

| Pack | Cases | Status |
|---|---|---|
| [`project-understanding/`](project-understanding/README.md) | PU-01 – PU-05 | Rev. B (2026-11-24 runs): PU-01 **88/100 pass**; PU-02 **85/100 pass**; PU-03 **90/100 pass — the owner's score, governs** (reviewer A 83, reviewer B 90); PU-04 **80/100 pass — the owner's score, governs** (reviewer A 83, reviewer B 87, same-model limitation on both); PU-05 **94/100 pass**. Rev. A scores 86/80/86 remain in the same records |
| [`motion-graphics-principles/`](motion-graphics-principles/README.md) | MP-01 – MP-03 | MP-01 **95/100 pass**; MP-02 **84/100 pass** at rev. A → **90/100 pass** at rev. B; MP-03 **93/100 pass** |
| `application-adaptation/` | — | Planned; no pack yet |
| `motion-graphics-execution/` | — | Planned; no pack yet |
| `hybrid-execution/` | — | Planned; no pack yet |
| `visual-evaluation/` | — | Planned; no pack yet |
| `error-analysis/` | — | Planned; no pack yet |
| [`fixtures/`](fixtures/README.md) | — | Owner-supplied application material (2026-11-24), **copied into the repository** at the owner's direction: 3 Alight Motion XML exports (`5.0.273.1028425`, Android) and 4 After Effects `.aep` files, with SHA-256, read-only rules, and verified camera elements in `Motion_Graphics_unik.xml`. Originals at `D:/Download/update` remain, hash identical. Screen recordings (supplied 2026-11-24) are kept **outside** the repository, referenced by path and hash. PU-03 and PU-04 both ran on their fixtures |
| [`self-review/`](self-review/README.md) | SR-01 – SR-06 | Agent-contribution review (Indonesian), 2026-11-24: initial mean **88,0/100**, **88,5/100** after the Review 006 addendum; SR-01 82, SR-02 91, SR-03 93, SR-04 94, **SR-05 78 — fail threshold**, SR-06 90 → 93. Includes the verified fixture inventory and the in-repo fixture copies. Not a skill-behavior pack |

## Scoring standard

The repository uses weighted 0–5 dimension scorecards, totalling 100 points, with a pass threshold of 80/100 per case and no critical failure. An external handoff draft used a 0–4-per-scenario aggregate (20 points); that scheme is not adopted (see the note in `project-understanding/scorecard.md`).

## Evidence rules

- Do not run a case without its required fixtures; record it as blocked instead.
- Preserve the exact prompt, the raw response, and the review conditions.
- A re-run after a skill edit goes in a separate `retest-<date>.md`; never overwrite the response it re-tests.
- Do not claim a pass without a scored evaluation record.
- Record every reviewer separately: the project owner's human score governs, agent reviews are added alongside it, and a review by the same model family is labelled as such (see [`project-understanding/independent-review-brief.md`](project-understanding/independent-review-brief.md)).
- Do not treat structural validation or this status table as evidence of application execution.
