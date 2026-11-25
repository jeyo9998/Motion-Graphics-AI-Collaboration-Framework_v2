# PU-04 — Prompt and Run Conditions

- **Case:** PU-04 — Camera research and evidence boundaries (verbatim from `../../cases.md`)
- **Run date:** 2026-11-24 (completed)
- **AI client:** fresh general-purpose agent context (one run; the preserved answer is in [`response.md`](response.md))
- **Skill revision:** rev. B of `skills/project-understanding/SKILL.md`
- **Status:** **Run and scored** — see [`evaluation.md`](evaluation.md)

## User prompt (verbatim, as issued to the run)

> Review my Alight Motion XML camera sample, my After Effects camera AEP, and the screen recording of the After Effects Camera Options. Explain what we can safely document for the two application adapters. I also want to know whether the After Effects camera is One-Node or Two-Node.

## Required materials (per case file)

| Role | Path | Present |
|---|---|---|
| Alight Motion XML with camera elements | `../../../fixtures/alight-motion/Motion_Graphics_unik.xml` | Yes |
| After Effects `.aep` camera sample | `../../../fixtures/after-effects/Motion_Graphics_Unik_Camera.aep` | Yes |
| Screen recording of the Camera Options state | `D:/Download/rekam kamera/Recording 2026-11-24 070641.mp4` (plus two phone recordings in the same folder) | Yes |

Fixture SHA-256 values, sizes, read-only rules, and copy-not-move provenance are recorded in [`../../../fixtures/README.md`](../../../fixtures/README.md); the recordings are deliberately kept **outside** the repository (540 MB of private capture) and are referenced by path and hash in that README's recordings section.

## Run conditions

1. **Fresh context.** The run agent had no prior exposure to this case, the scorecard, or the expected answers.
2. **Answer key withheld.** The agent was pointed at exactly the two fixture files and the recordings folder and was forbidden to read anything else under `evals/` (`cases.md`, rubrics, other results, review log).
3. **Verbatim prompt.** The case prompt above was issued unchanged; no hints about what the recordings contain or which file is which.
4. **No applications opened.** Neither Alight Motion nor After Effects was available; the XML and `.aep` were parsed as text/bytes and the recordings were consumed via frame extraction with a bundled ffmpeg binary (the agent located and ran the extraction itself). **Documented deviation:** the recordings were therefore examined as frame sets, not played back; audio tracks were not examined.
5. **No coaching.** The reviewer did not intervene during the run.
6. **Same-agent scoring limitation (SR-05 carry-over).** The reviewer is the same agent family as the run client. Scores carry that limitation until per-dimension human re-scoring happens.

## Availability history

- 2026-11-24 (earlier): **Blocked** — none of the three fixtures existed in the handoff package; any run would have tested invention, not understanding. That blocked state is preserved in the status history of [`evaluation.md`](evaluation.md).
- 2026-11-24: XML and `.aep` supplied by the owner and copied into `evals/fixtures/` — case still blocked on the recording.
- 2026-11-24: owner supplied the screen recordings at `D:\Download\rekam kamera`; materials complete, run executed the same day.
