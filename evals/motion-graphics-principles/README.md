# Motion Graphics Principles — Evaluation Pack

**Status:** Run 2026-11-24 in fresh agent contexts. MP-01 **95/100**, MP-02 **84/100** (rev. A) → **90/100** (rev. B re-run), MP-03 **93/100**. No critical failures. Scores apply only to the recorded client, model, and skill revision; no native application execution was involved.

This pack tests whether `skills/motion-graphics-principles/SKILL.md` converts an approved brief into a portable, application-neutral specification without inventing user requirements or claiming untested application behavior.

## How to run

1. Use a fresh agent context with the skill loaded.
2. Provide only the materials named in each case.
3. Submit the exact prompt from [`cases.md`](cases.md).
4. Preserve the raw response in `results/MP-XX/response.md`.
5. Score with [`scorecard.md`](scorecard.md); record the client/model, date, and skill revision.
6. Do not coach the agent during the first run.

A passing score requires at least 80/100 and no critical failure, for the tested configuration only.

## Cases

| Case | Focus | Score |
|---|---|---|
| MP-01 | Clear brief → complete application-neutral motion specification | 95/100 |
| MP-02 | Ambiguous creative direction with no material → proportionate response | 84/100 rev. A; 90/100 rev. B |
| MP-03 | Cross-application parity → one shared spec, no app-specific controls | 93/100 |

Recorded runs: [`results/`](results/) — each case folder holds `prompt.md`, `response.md`, `evaluation.md`; MP-02 also holds `retest-2026-11-24.md`.

## Related

- [`../../skills/motion-graphics-principles/SKILL.md`](../../skills/motion-graphics-principles/SKILL.md)
- [Skill architecture](../../SKILL-ARCHITECTURE.md)
