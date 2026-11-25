# PU-03 — Prompt and Run Conditions

- **Case:** PU-03 — Cross-application movement task with supplied samples (verbatim from `../../cases.md`)
- **Run date:** 2026-11-24 — **executed**
- **AI client / model:** Qoder CLI, `general-purpose` subagent in a fresh context. Underlying model name not reported by the client; session model tier was owner-set to "Efficient".
- **Skill revision:** rev. B of `skills/project-understanding/SKILL.md`
- **Materials supplied to the run:** the four movement fixtures only
- **Status:** **Run and scored — 93/100 pass.** See [`evaluation.md`](evaluation.md) and the verbatim [`response.md`](response.md).

## User prompt

> I want a rounded rectangle to travel horizontally across the composition while rotating once. Make the creative result comparable in Alight Motion and After Effects. I have supplied two Alight Motion XML movement samples and two After Effects AEP movement samples. Study them and prepare a plan for implementing the same motion in both applications. Do not modify the originals.

## Materials given (absolute paths withheld from the run as `.../evals/fixtures/`)

- `alight-motion/movement_1.xml` — SHA-256 `8d7010a8e8bf9e156210b147ec4e63687290f03378443b8d86a74d6c1467f1dc`
- `alight-motion/movement_2.xml` — SHA-256 `6c8083f1a814039d410903386a433600826104a89120a108fd2c4bb4db2f4dda`
- `after-effects/movement_1.aep` — SHA-256 `7067f17d5c7064a126a53aa2ee3aff1098fa4c2b7acb862862ac753cddca0da6`
- `after-effects/movement_2.aep` — SHA-256 `6279b42b92f8f167ec3ededdae92cb28386cfcc677a9b4e765260e9b467a1866`

## Run conditions

1. Fresh agent context; the skill file was the only instruction surface.
2. The agent was told **not** to read `cases.md`, `scorecard.md`, `review-log.md`, or `evals/fixtures/README.md`, so the answer key could not leak into the run. It was allowed the four named fixture files.
3. No coaching during the run. The raw response was preserved verbatim.
4. No application access: nothing was opened, rendered, or executed in Alight Motion or After Effects, and no `.aep` parser was installed.
5. Scoring was done by the same agent family that authored the skill, after independently re-deriving the response's factual claims from the fixtures. This is the known SR-05 limitation.

## Availability history

- 2026-11-24, first assessment: no `.xml`, `.aep`, video, image, or audio fixtures existed in the handoff package, the reference repository, or the reviewed archive; the case was recorded as blocked rather than simulated. The PU-05 record of the same day independently documents `0` project/media files in the archive it inspected.
- 2026-11-24, Review 006: the owner supplied the application files and directed their inclusion; the case became runnable and was then run.
