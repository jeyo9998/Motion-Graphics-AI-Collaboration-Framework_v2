# Project Understanding — Review Log

## Review 001 — Static review and resource-inventory refinement

- **Date:** 2026-11-22
- **Reviewed component:** `skills/project-understanding/SKILL.md`
- **Review basis:** `SKILL-ARCHITECTURE.md`, `evals/project-understanding/cases.md`, `scorecard.md`, and repository guidance in `AGENTS.md`.
- **Review type:** Static design review; not an external AI-agent behavioral run.

### Finding

The Skill already instructed agents to inspect accessible context, distinguish confirmed/inferred/unknown/conflicting information, ask focused questions, and avoid claiming access they did not have. However, its resource-inspection step did not explicitly require agents to classify repository documentation separately from the target Motion Graphics project, rendered preview, references, and development/tooling files.

This distinction is important for PU-05: a repository can be available while the actual edit being requested for review is absent.

### Change made

Updated `skills/project-understanding/SKILL.md` to add an **Inventory and classify available resources** subsection. It now asks agents to:

- Inspect relevant accessible sources before requesting re-uploads or repeated information.
- Classify target projects, rendered previews, reference material, project documentation, and development/tooling files separately.
- Record whether relevant resources were inspected, merely identified, present but not inspected, not found in checked sources, or inaccessible.
- Avoid describing a workspace as empty when repository/documentation files exist but the target edit is absent.
- Request the smallest useful missing input: usually a rendered preview or screenshot for initial visual review, and a native project file when editable structure or direct modification is needed.

The Project Understanding Brief's references/assets field was updated to carry this classification forward during handoff.

### Validation performed

- `python tests/validate_skills.py` — **PASS** (1 Skill checked).

### Not yet tested

- PU-01 through PU-05 have not yet been run against an external AI-agent client with this Skill loaded.
- No Alight Motion or After Effects execution was performed.
- No multi-agent handoff or runtime tool integration was tested.

### Next action

Run PU-01 through PU-05 in a compatible Agent Skills client, score each response using `scorecard.md`, and record the client/model, Skill revision, date, evidence, and critical failures. Revise the Skill only where the behavioral tests demonstrate a gap.

## Review 002 — PU-05 inventory helper and repository consistency

- **Date:** 2026-11-21
- **Reviewed package:** `motion-graphics-ai-framework-v0.3.2-wip.zip`
- **Review type:** Static repository review plus local script tests.

### Findings

1. The extension-count helper correctly normalized suffixes and handled the reviewed edge cases, but a missing argument or missing archive returned exit status `0` because the original pipeline did not enable `pipefail` or validate its input. This could make a failed inventory look successful.
2. The root README and `AGENTS.md` repository trees did not list the already-present `evals/project-understanding/scripts/` and `results/PU-05/` resources.
3. The evaluation README still described the pack as not yet run externally, despite the presence of a PU-05 observation record.
4. The handoff note omitted the newly added PU-05 result and inventory helper from its file inventory.

### Changes made in this review

- Hardened `count-extensions.sh` with strict argument validation, readable-file validation, `unzip` availability checking, and `set -euo pipefail` so upstream ZIP/listing errors propagate.
- Added `tests/test_count_extensions.sh` covering stdin and ZIP input, directories, dotted directory names, dotfiles, uppercase suffixes, compound suffixes, no-extension names, trailing dots, and failure exit statuses.
- Updated README and AGENTS repository trees and documented the new test command.
- Clarified that PU-05 has an observation record but is not independently scored, and that formal reports for PU-01 through PU-04 remain outstanding.
- Updated the project handoff inventory and next steps.

### Validation performed

- `bash tests/test_count_extensions.sh` — PASS.
- `python tests/validate_skills.py` — **PASS** (1 Skill checked).
- `bash tests/test_count_extensions.sh` — **PASS** (stdin cases, generated ZIP cases, missing argument/archive, and corrupt archive).
- Markdown relative links — **PASS** (12 Markdown files checked).
- Manual failure-path checks — missing archive returned 66; missing argument returned 64.
- Extension helper against the supplied v0.3.2 WIP archive — 24 entries, 9 directories, 15 files; `.md` 12, `.py` 1, `.sh` 1, `.txt` 1.

### Remaining limitations

- `PU-05` is an observation record and remains `Not scored` pending an independent scorecard review.
- Formal result reports for PU-01 through PU-04 are not included in this package.
- This review does not establish multi-agent compatibility or real Alight Motion / After Effects execution.

## Review 003 — Owner-authorized continuation and Skill 01 baseline evaluation

- **Date:** 2026-11-24
- **Reviewed component:** repository continuation; `skills/project-understanding/SKILL.md` baseline evaluation
- **Review type:** owner-directed roadmap continuation plus behavioral runs in separate agent contexts
- **Owner direction:** draft all seven Skills in one pass; the per-Skill behavioral gates remain in force

### Changes made

- Added drafts for `motion-graphics-principles`, `application-adaptation`, `motion-graphics-execution`, `hybrid-execution`, `visual-evaluation`, and `error-analysis`.
- Added application-adaptation reference scaffolding with an evidence template; no verified Alight Motion or After Effects procedures were invented.
- Added the `motion-graphics-principles` evaluation pack (three cases, weighted scorecard), not yet run.
- Added per-case result folders for PU-01 through PU-05 and a top-level evaluation status matrix.
- Synchronized `README.md`, `AGENTS.md`, and `SKILL-ARCHITECTURE.md` with the actual repository contents.
- Recorded the canonical scoring decision in `scorecard.md`: weighted 0–5 dimensions, 100 points, per-case threshold 80. The external 0–4/20 aggregate scheme is not adopted because the repository documents per-case weighted scoring.

### Behavioral evaluation results

Runs used fresh background-agent contexts with the skill read from the repository; responses were preserved verbatim and scored by the reviewing agent using the repository scorecard.

| Case | Score | Critical failure | Status |
|---|---:|---|---|
| PU-01 | 86/100 | No | Pass |
| PU-02 | 80/100 | No | Pass (threshold) |
| PU-03 | — | N/A | Blocked: XML/AEP samples absent |
| PU-04 | — | N/A | Blocked: XML/AEP/recording fixtures absent |
| PU-05 | 86/100 | No | Pass (2026-11-24 re-run; historical v0.3.1 observation preserved) |

A pass applies only to the tested client, model, skill revision, and conditions. It does not establish cross-agent compatibility or native application execution.

### Validation performed

- `python tests/validate_skills.py` — **PASS**, 7 skills checked (Python 3.15.2, PyYAML 6.0.4).
- `bash tests/test_count_extensions.sh` — **PASS**.
- Relative Markdown-link check — **not run** in this pass.
- No Alight Motion or After Effects execution was performed.

### Documentation findings

- The handoff document `04-REPOSITORY-STATUS.md` reports 24 ZIP entries and 15 files for v0.3.2-reviewed. The archive actually contains **25 entries, 9 directories, and 16 files**; its SHA-256 matches the manifest. The document's own file list contains 16 entries, so the tally is the error.
- Review 002 is dated 2026-11-21 and Review 001 is dated 2026-11-22, so numbering and dates are not chronological. Preserved as recorded; flag for owner confirmation.
- The ZIP's `README.md` still describes the one-skill state. The working copy at `workspace/motion-graphics-ai-framework/` is the continued revision; the ZIP itself was not rewritten.

### Remaining limitations

- PU-03 and PU-04 remain unrun until their fixtures are supplied.
- Skills 02–07 are drafts with no behavioral evaluation.
- No canonical GitHub repository, branch, license, or target application versions are established.
- No native application integration, rendering, or cross-agent orchestration exists.

## Review 004 — Evaluation-driven revision and first principles runs

- **Date:** 2026-11-24
- **Reviewed components:** `skills/project-understanding/SKILL.md`, `skills/motion-graphics-principles/SKILL.md`, both evaluation packs
- **Review type:** behavioral runs in fresh agent contexts, followed by evidence-driven skill edits and re-runs
- **Owner direction:** finish the continuation and re-evaluate

### Changes made

**`project-understanding` rev. A → rev. B**, one edit per demonstrated gap:

| Gap seen in rev. A | Edit |
|---|---|
| PU-05 reported an inaccurate inventory count and drew on a workspace copy that was not supplied | Inventory rule: report figures only from the source actually checked, and say which source |
| PU-01 wrote After Effects build steps inside the understanding step | Next-step field: name the skill, leave its procedure to that skill |
| PU-02 answered with seven techniques plus three frameworks | Step 7: match response size to what was asked; Example 2 caps suggestions at three one-line items |

**`motion-graphics-principles` rev. A → rev. B**, from the first MP runs:

| Gap seen in rev. A | Edit |
|---|---|
| MP-01 produced an easing strength range "0.6–0.75" with no unit or source | Step 4: give a number only when its unit and source are defined |
| MP-02 listed six detailed review areas and four input requests | Example 3: at most three one-line areas; ask for one smallest input and defer the rest |
| MP-03 asserted that a construct "will not produce visible turning in either application" | Rule 9: never assert application interpretation; phrase it as a question for `application-adaptation` |

**Records added:** `evals/motion-graphics-principles/results/MP-01`, `MP-02`, `MP-03` (prompt, verbatim response, scored evaluation) plus `MP-02/retest-2026-11-24.md`; `retest-2026-11-24.md` for PU-01, PU-02, PU-05. The rev. A records and responses were not modified. `evals/README.md` gained the rule that a re-run never overwrites the response it re-tests.

### Behavioral results

| Case | Rev. A | Rev. B | Critical failure | Status |
|---|---:|---:|---|---|
| PU-01 | 86 | 88 | No | Pass; routing still unnamed |
| PU-02 | 80 | 85 | No | Pass; suggestion cap held at three |
| PU-05 | 86 | 94 | No | Pass; all five inventory figures verified exact |
| MP-01 | 95 | not re-run | No | Strong |
| MP-02 | 84 | 90 | No | Pass → strong |
| MP-03 | 93 | not re-run | No | Strong |
| PU-03 / PU-04 | — | — | N/A | Still blocked: XML/AEP/recording fixtures absent |

A pass applies only to the tested client, model, skill revision, and conditions.

### Validation performed

- `python tests/validate_skills.py` — **PASS**, 7 skills checked; `project-understanding` is 222 lines, inside the 500-line limit.
- `bash tests/test_count_extensions.sh` — **PASS**.
- Independent re-check of the PU-05 run's claims against `source-archive/motion-graphics-ai-framework-v0.3.2-reviewed.zip`: 49,577 bytes; 25 entries; 16 files (`.md` 12, `.py` 1, `.sh` 2, `.txt` 1); `reference-repository/.../skills/project-understanding/SKILL.md` = 12,565 bytes — **all matched**.
- Relative Markdown-link check — **still not run**.

### Documentation findings

- `evals/motion-graphics-principles/scorecard.md` had been created **outside** the repository tree, at `Downloads/motion-graphics-ai-handoff-v1.0 (1)/motion-graphics-ai-framework/evals/motion-graphics-principles/scorecard.md`, so the pack was incomplete. Its content is now copied to the correct path in this repository, and the MP README/AGENTS/SKILL-ARCHITECTURE trees list it.
- The stray out-of-tree directory was **not** removed: the move-and-delete command was declined. One file remains at the path above and needs an owner decision before deletion.
- PU-03/PU-04 were not simulated to fill the matrix.

### Remaining limitations

- The reviewing agent authored both the skills and the scores; no independent human or second-model review has occurred.
- Only one client/model family was exercised (model selected automatically, and not reported by the client).
- MP-01 and MP-03 have no rev. B evidence; their scores describe rev. A only.
- No Alight Motion or After Effects execution, rendering, or file modification was performed.

## Review 005 — Application fixtures supplied and self-review pack added

- **Date:** 2026-11-24
- **Reviewed:** owner-supplied materials at `D:/Download/update`; new `evals/self-review/` pack
- **Review type:** evidence inventory plus agent-contribution self-assessment scored by the same agent

### Findings on the supplied materials

- Three text project files are genuine **Alight Motion** exports: header `Created by Alight Motion`, `am="com.alightcreative.motion/5.0.273.1028425"`, `amplatform="android"`, `ffver="106"`; scenes 1440×1080 @ 20 fps (`Motion_Graphics_unik.xml`, 345 keyframes, 182 shapes, 164 effects) and 1920×1080 @ 120 fps (`movement_1.xml` 19 keyframes, `movement_2.xml` 8 keyframes).
- `movement_1.xml` holds a `.roundrect` layer "Persegi Panjang Bulat 1" whose `<location>` moves x 0 → 795.378052 between t 0.051819 and 0.624813 with `e="cubicBezier 0.86685157 0.0 0.43377253 1.0"` — the horizontal-travel-with-easing shape that PU-03 and MP-03 describe.
- Four `.aep` files begin with `RIFX` and carry XMP `dc:format = application/vnd.adobe.aftereffects.project`; `Motion_Graphics_Unik_Camera.aep` contains the strings `Camera 1`, `(ADBE Camera Options Group`, `(ADBE Camera Zoom`. Labelled **Observed in bytes**: no parser was used and After Effects was not opened.
- **PU-03 and PU-04 are therefore unblocked in principle** — required materials now exist — and remain recorded as *blocked* until actual runs are executed against them.
- The files were **not** copied into the repository and no path outside this record references their content as committed data, per `AGENTS.md` §11 (no private user projects without explicit permission and a licensing basis).

### Changes made

- Added `evals/self-review/` — README, `cases.md` (SR-01 … SR-06), a self-authored weighted `scorecard.md`, `fixture-inventory.md` with SHA-256 for all seven files, and `results/assessment-2026-11-24.md`.
- Wrote the pack in Indonesian at the owner's request; technical identifiers remain English.
- `evals/README.md` gained a self-review row.

### Results

| Case | Score | Status |
|---|---:|---|
| SR-01 Repository continuation completeness | 82 | Pass |
| SR-02 Claim and evidence integrity | 91 | Pass |
| SR-03 Privacy, safety, data preservation | 93 | Pass |
| SR-04 Technical validation and doc consistency | 93 | Pass |
| SR-05 Behavioral evaluation validity | **78** | **Fail — below threshold** |
| SR-06 Handling of new application fixtures | 90 | Pass |
| Mean | 87,8 | — |

SR-05 fails because the same agent authored the skills, ran the tests, and assigned the scores, on one client family, with no enforced separation between the answer key and the test agent. Required fix: independent re-scoring, staged fixtures/materials so the run context cannot read `evals/`, MP-01 and MP-03 re-run at rev. B, and the actual model name recorded.

### Validation performed

- `python tests/validate_skills.py` — **PASS** (7 skills).
- `bash tests/test_count_extensions.sh` — **PASS**.
- `sha256sum`, header reads, element censuses, and byte-string scans against `D:/Download/update` — results recorded in `evals/self-review/fixture-inventory.md`.
- Relative Markdown-link check — **PASS**: 76 relative links across all Markdown files, 0 broken. This closes the item left unrun in Reviews 003 and 004.

### Remaining limitations

- Self-assessment carries author bias; the scorecard's own control is that every score names a reproducible command.
- Fixture properties are read, not executed; no rendering or project modification occurred.
- Whether the fixtures may be stored in the repository is an open owner decision.

---

## Review 006 — Fixtures included in the repository and camera evidence verified

- **Date:** 2026-11-24
- **Trigger:** owner instruction — *"tolong pindahkan fixture ke evals/fixtures/"*
- **Review type:** in-repo fixture inclusion, case-record reconciliation, full validation re-run

### Decision recorded

The owner authorized storing the fixtures inside the repository. The action taken was **copy, not move**: the originals remain at `D:/Download/update/XML/` and `D:/Download/update/aep/`. Inclusion does not change the licensing position — the repository still has no selected public license, so the fixtures grant no reuse or redistribution rights to anyone else (`AGENTS.md` §11).

### Changes made

- Created `evals/fixtures/` with `alight-motion/` (3 XML) and `after-effects/` (4 `.aep`), plus `evals/fixtures/README.md` holding authorization and ownership, the SHA-256 integrity table, a per-fixture purpose table, the camera-content section, and five read-only usage rules.
- Rewrote the PU-03 record: **blocked → materials available, run pending**, with the four fixture paths and the remaining run steps. The original gap evidence is retained as history rather than deleted.
- Rewrote the PU-04 record: **blocked → partially unblocked**. The XML and AEP sides exist in-repo; the Camera Options screen recording is still absent, so the case stays unscored.
- Updated `evals/self-review/fixture-inventory.md`, `evals/README.md`, `README.md`, and `AGENTS.md` §3 so no document still claims the fixtures are outside the repository.

### New verified evidence: Alight Motion camera objects

Read from the repository copy as text; no application was opened.

- `Motion_Graphics_unik.xml` declares **two `<camera>` elements**, both labelled `Kamera 1`, each with `type="perspective"`, `fov value="60.000000"`, `<transform>` location `0,0,-1247.076660`, and `<focus-blur enabled="false">` / `<fog enabled="false">` blocks.
- Each camera's `parent` id resolves to a separate `<nullobj label="Nol 1">`, so **camera and null object are distinct element types** in this format.
- Effect on PU-04: the "distinguish Camera from Null Object" and "camera type" checks become answerable on the Alight Motion side from file content. They remain **Observed in sample** for `5.0.273.1028425` and say nothing about the Camera Options UI or about After Effects.
- The earlier "camera strings" observation for After Effects stays limited to the byte strings in `Motion_Graphics_Unik_Camera.aep`; no parser was used.

### Validation performed

- `python tests/validate_skills.py` — **PASS** (7 skills).
- `bash tests/test_count_extensions.sh` — **PASS**.
- `sha256sum` on the seven in-repo copies — all match `evals/fixtures/README.md`.
- `sha256sum` on the seven originals at `D:/Download/update` — all match the copies, confirming nothing was altered or moved.
- Relative Markdown-link check — **PASS**: 86 relative links, 0 broken (up from 76 in Review 005; the increase is the new fixture and case-record cross-links). One link was broken on the first pass — `../fixtures/README.md` written from `evals/self-review/results/` instead of `../../fixtures/README.md` — and was fixed before this result.
- File count — **67** files (`56 md`, `4 aep`, `3 xml`, `2 sh`, `1 txt`, `1 py`), matching the expected 59 + 1 README + 7 fixtures. This supersedes the "54 files" expectation noted against SR-01; the difference is the packs and fixtures added since that number was written.

### Results

No behavioral run was added by this review; the scores below are self-review re-scoring, not skill evaluation.

| Item | Before | After | Basis |
|---|---:|---:|---|
| PU-03 status | Blocked (fixtures absent) | Materials complete, **not run** | Fixtures in-repo |
| PU-04 status | Blocked (three fixtures absent) | Blocked on **one** fixture (recording) | XML + AEP in-repo |
| SR-06 self-review | 90 | **93** | Owner authorization recorded; hashes re-verified both directions |
| Self-review mean | 88,0 | **88,5** | SR-06 only |
| SR-05 self-review | 78 (fail) | **78 (fail, unchanged)** | Same agent still authored and scored |
| Repository files | 59 | **67** | 7 fixtures + fixtures README |

### Remaining limitations

- PU-03 and PU-04 have materials but still **no run**; neither has a score.
- Fixture properties are read, not executed. Nothing was opened, rendered, or modified in Alight Motion or After Effects.
- Asset references inside the projects (fonts, footage, images) were not enumerated; some may point to files not included.
- SR-05's fail stands: independent re-scoring is still outstanding.


## Review 007 — PU-03 and PU-04 executed and scored; owner's human score recorded for PU-04

**Date:** 2026-11-24
**Decision:** Run the two remaining blocked cases now that the owner supplied the missing materials, preserve the raw responses verbatim, verify the responses adversarially against the fixture bytes and extracted frames, and record the project owner's independent score for PU-04 as the governing human score.

### What changed

- `results/PU-03/` — first run recorded: `response.md` (raw answer preserved verbatim), rewritten `prompt.md` (run conditions incl. answer-key withholding), rewritten `evaluation.md` (**89/100 pass** at rev. B, reviewer verification table, status history preserved).
- `results/PU-04/` — first run recorded: `response.md` (raw answer preserved verbatim), rewritten `prompt.md` (materials now include the owner's recordings at `D:/Download/rekam kamera`; documented deviation: recordings consumed via ffmpeg frame extraction, no playback, audio not examined), rewritten `evaluation.md` (**80/100 pass — owner's independent score, governs; agent reviewer 96/100 with the same-agent (SR-05) limitation**).
- `evals/README.md`, `evals/project-understanding/README.md`, root `README.md`, `AGENTS.md` §3, `SKILL-ARCHITECTURE.md` §14/§15 — status lines updated from "blocked/not run" to scored runs.

### Evidence verified during the review (PU-04)

- Alight Motion XML: two `<camera>` elements, location z −1247.076660 with fov 60 (720/tan 30° recomputed), focus-blur/fog defaults derived from distance, tag census, null chains (incl. `hidden="true"` third node), null keyframe values, overshoot easing — all reproduced from bytes. One over-generalization caught: "t normalized 0–1" does not hold file-wide (345 `kf`, min −0.876462).
- After Effects `.aep`: 203,068-byte RIFX `Egg!`; decoded doubles 898.000031 / −2666.666667 ×2 / 0.7 / 2666.6666666666665 ×2 / 25.3 at recorded offsets; byte-absence of Point of Interest / One-Node / Two-Node / "Comp 3" (0 hits each). One decoded value did not reproduce: spatial tangents ±59.6667 (no stored double matches; response had labeled the layout "partially inferred").
- Desktop recording (1918×994, 5:59): Transform rows, Parent & Link None, X Rotation 0x+40.3° @100 s, POI 848.6,1792.0 @220 s, Zoom 6400.7 @320 s, Iris "Fast Rectangle" @76 s — reproduced from frames. One timestamp item did not reproduce (@160 s POI mid-edit). Negative observation (Camera Settings dialog never appears) reproduced.
- Phone recordings (720×1612, Alight Motion): `Kamera 1` X/Y/Z 960,00/…/−1662,77 reproduced at ~10–20 s; 960/tan 30° = 1662.769 recomputed; correctly identified as a different (1920-wide) AM project from the 1440-wide XML fixture.

### Results

| Item | Before | After | Basis |
|---|---:|---:|---|
| PU-03 status | Materials complete, not run | **89/100 pass** (first run, rev. B) | Two reviewer-caught factual errors in the run's response lowered a provisional 93 to 89 |
| PU-04 status | Blocked on one fixture | **80/100 pass — owner's score, governs**; agent reviewer 96/100 (same-agent limitation) | Owner evaluated independently and reports using the output in several real actions |
| PU pack governing mean | — | **87,2/100** (88+85+89+80+94, ÷5) | Owner's PU-04 score in the mean |
| Repository files | 67 | **69** | `PU-03/response.md` and `PU-04/response.md` added |

### Remaining limitations

- PU-04's 80 is recorded as a total without a per-dimension breakdown; per-dimension human re-scoring is still outstanding for every case.
- SR-05 remains open: the agent reviewer's 96 on PU-04 (and all other agent scores) carry the same-agent limitation until independently re-scored.
- PU-03 has no owner score yet.
- Recordings were examined as frame sets, not played back; audio was not examined in any recording.

## Review 008 — rev. C applied, independent per-dimension review, MIT license added

**Date:** 2026-11-24
**Decision:** (1) apply the four PU-04 improvements to `skills/project-understanding/SKILL.md` as **rev. C**; (2) obtain an independent per-dimension review of PU-03 and PU-04 with the answer key withheld; (3) select and record a public license.

### Changes

- `skills/project-understanding/SKILL.md` — **rev. C**: new *Technical evidence discipline* block in workflow step 1 with four rules (derived values show their derivation; binary values cite chunk/offset/element; generalizations scoped to what was inspected, with counterexamples stated; changing recording values cite the frame they were read at).
- `LICENSE` — **MIT** added at the repository root; scope covers the framework's original work only. Owner fixtures under `evals/fixtures/` and the external screen recordings are explicitly excluded. Scope note added to root `README.md`; license state updated in `AGENTS.md` §3/§11, `PROJECT-SPECIFICATION.md` §14–§16, `SKILL-ARCHITECTURE.md` §14/§15, `evals/fixtures/README.md`. `PROJECT-HANDOFF-NOTES.md` (2026-11-21 snapshot) left untouched as a historical document.
- `evals/project-understanding/independent-review-brief.md` — new: ready-to-paste brief for a reviewer outside this agent family (e.g. Claude) or a human, including the working-context warning.
- `results/PU-03/evaluation.md`, `results/PU-04/evaluation.md` — per-dimension records for all reviewers, added verification rows, reviewer-B sections, corrected scoring.

### Independent review (reviewer B) and two corrections against reviewer A

Reviewer B worked in a fresh context with the answer key withheld: its own padding-aware RIFX/IFF chunk walker, direct `cdta`/`cdat`/`ldat`/`ldta`/`tdmn`/`prin` decoding, ~60 extracted frames. It disclosed that the harness auto-attaches `AGENTS.md` (which now contains scores) to the working context; it stated it did not search for them and derived its numbers from the fixtures first. Exposure recorded; SR-05 stays open.

Corrections this review forced, all verified byte-level afterwards:

1. **Reviewer A's PU-04 "tangents ±59.6667 not stored" verdict was wrong** — the tangents are stored at offsets 65098 and 65226 as `59.66667175292969` (float32-rounded); the first scan's tolerance missed them. Verdict withdrawn.
2. **PU-04's dimension table used invalid weighted values** (17 and 14, which correspond to no 0–5 rating). Recomputed from valid ratings: reviewer A **83**, not 96.

New defects reviewer B found and reviewer A confirmed afterwards (all added to the verification tables):

| Case | Claim | Finding |
|---|---|---|
| PU-03 | "Null 43" listed as a layer of `Comp 1` | `movement_1.aep` has exactly three `Layr` chunks; `Null 43` sits inside the project-panel Solids folder |
| PU-03 | ease-like fraction `0.2` | zero doubles equal to 0.2 in either `.aep` |
| PU-03 | "AE Rectangle Path `Roundness` is a 0–100 %" | Roundness is a pixel value capped at half the shorter side; the response's own 25/100 anchor contradicts it |
| PU-04 | "one footage item" among the project items | the third top-level item is a Solids folder with five solid items; the string `footage` occurs 0× |
| PU-04 | rotation dial `0°` @~75 s | that frame shows the cubic-bezier easing editor |
| PU-04 | numeric keypad labelled "Lebar" | not present in any sampled frame |
| PU-04 | "the nulls parent the shape layers" | no parent field binding them could be located from bytes |
| PU-04 | "a different AM project" | overstated; a different comp width explains the same numbers |

### Scores after this review

| Case | Owner | Reviewer A | Reviewer B | Governing |
|---|---:|---:|---:|---|
| PU-03 | — | **83** (revised from 89) | 90 | 83 |
| PU-04 | **80** | 83 (recomputed) | 87 | **80 (owner)** |

PU pack mean on governing scores: **86,0/100** (88 + 85 + 83 + 80 + 94, ÷ 5).

### Validation performed

- `python tests/validate_skills.py` — **PASS** (7 skills).
- `bash tests/test_count_extensions.sh` — **PASS**.
- Relative Markdown-link check — **PASS**: 96 relative links, 0 broken.
- File count — **71** (59 md, 4 aep, 3 xml, 2 sh, 1 txt, 1 py, 1 LICENSE).
- CJK scan — 0 files contain CJK characters.

### Remaining limitations

- Reviewer B is the same model family as the skill author, so it does not close SR-05; only a different model or a human can. The brief for that review is ready.
- The owner's per-dimension breakdown does not exist: PU-04's table carries a clearly-labelled **proposed** allocation that reconciles their total of 80 to reviewer A's profile, pending their confirmation or correction.
- PU-03 has no owner score yet.
- Recordings were examined as frame sets, not played back; audio was never examined.
- The recorded runs predate rev. C, so the new rules are not yet exercised by any recorded run.

## Review 009 — Owner's PU-03 score, MP-01/MP-03 re-runs, and the canonical repository

### Owner's PU-03 score

The project owner scored PU-03 **90/100 — pass**, confirming the case was completed successfully. It is the second human score in the repository and it governs, exactly as PU-04's owner score of 80 governs that case. Reviewer A's 83 and reviewer B's 90 are recorded alongside it with the SR-05 same-model limitation.

PU pack mean on governing scores rises from 86,0 to **87,4/100** (88 + 85 + 90 + 80 + 94, ÷ 5).

### MP-01 and MP-03 re-run against rev. B

Both cases were still scored against rev. A, which left the SR-05 improvement list open. Both were re-run on 2026-11-24 under the standard protocol: fresh agent context, the skill read from the repository path, `evals/` withheld as the answer key, the verbatim prompt from `cases.md`, no materials, no coaching. Each response is preserved verbatim in a new `retest-2026-11-24.md` beside the untouched original response.

| Case | rev. A | rev. B | Critical failure | Where |
|---|---:|---:|---|---|
| MP-01 | 95 | **95** | No | `evals/motion-graphics-principles/results/MP-01/retest-2026-11-24.md` |
| MP-02 | 84 | 90 | No | `evals/motion-graphics-principles/results/MP-02/retest-2026-11-24.md` |
| MP-03 | 93 | **93** | No | `evals/motion-graphics-principles/results/MP-03/retest-2026-11-24.md` |

The totals did not move, and that is recorded as-is. The rev. B rules removed the specific defects the rev. A reviews had identified — MP-01's unit-less easing strength range and MP-03's cross-application behavioural assertion — but each re-run introduced a smaller replacement defect of its own (MP-01's unlabelled "±5 px" acceptance tolerance; MP-03's unsupported "perceptual threshold" and gradient claims, and an option tree that is still longer than the ask). A rule that moves a defect rather than removing it is not evidence of progress, so no score was inflated to show otherwise. All three MP cases now have rev. B evidence, which closes item 3 of the SR-05 improvement list.

### Canonical repository and branch

The owner asked what "canonical repo/branch" means and delegated the decision. The factual situation found on this machine:

- The framework directory was **not** a Git repository of its own. `git rev-parse --show-toplevel` resolved to `C:/Users/Axioo` — an unrelated repository in the user's home directory, with **zero commits**, no remotes, and permission-denied subdirectories. Any commit made from the framework directory would have gone into that home-directory repository, which is not what the project needs.
- The owner has other work in that home directory. It was left untouched.

Decision, recorded in `SKILL-ARCHITECTURE.md` §14–15 and `AGENTS.md` §3:

- **Canonical repository:** the framework root is now a standalone Git repository (`git init -b main`), with `.gitignore` (OS/editor noise, Python bytecode, local scratch) and `.gitattributes` (LF for text, `binary` for `.aep`/`.mp4`/images).
- **Canonical branch:** `main`, the default branch every change lands on.
- **First commit:** `9fff40c` — 74 tracked files, the reviewed state at rev. C with the MIT license.
- **Remote:** none configured. The name `origin` is reserved for the owner's own hosting; adding a remote and pushing are externally visible actions that need the owner's repository URL and explicit authorisation, and neither was given. No placeholder URL was invented.
- **Canonical working copy:** the current path inside the handoff package remains the working tree. Relocating it out of `Downloads/` is a move of the owner's files and stays an owner decision.
- The revision labels rev. A / rev. B / rev. C remain the evidence labels used in evaluation records and can now be paired with a commit hash.

### Documentation synchronized

Owner PU-03 score 90 propagated to `results/PU-03/evaluation.md` (with an owner-review section), `evals/README.md`, `evals/project-understanding/README.md`, `README.md`, `AGENTS.md` §3, `SKILL-ARCHITECTURE.md` §14, and the self-review assessment. The historical entries in this log and in the self-review addenda are kept unchanged as the audit trail.

## Review 010 — rev. C behavioural runs for PU-03 and PU-04

**Date:** 2026-11-24
**Decision:** Execute PU-03 and PU-04 again under the rev. C skill, preserve each response verbatim in a separate `retest-` file that does not overwrite the re-tested response, verify every checkable claim independently against the fixture bytes and the extracted frames, and record the results without altering the earlier rev. B records.

### Runs

Both cases were run on 2026-11-24 under the standard protocol: fresh agent context, the skill read from the repository path, `evals/` withheld as the answer key, the exact prompt from `cases.md` with no coaching and no follow-up.

| Case | rev. B (reviewer A) | rev. C (reviewer A) | Critical failure | Where |
|---|---:|---:|---|---|
| PU-03 | 83 | **89** | No | `evals/project-understanding/results/PU-03/retest-2026-11-24-revC.md` |
| PU-04 | 83 | **88** | No | `evals/project-understanding/results/PU-04/retest-2026-11-24-revC.md` |

The rev. C rules did what they were written to do: PU-03's rev. B response contained two claims the reviewer could not reproduce, and in rev. C the byte- and frame-level citations are dense enough that the reviewer could re-derive the answer independently. PU-04's response gained a full per-property offset table and timestamped recording values.

### One discarded attempt, recorded

The first rev. C launch for PU-03 was discarded before it produced a record: the prompt had been paraphrased and carried coaching bullets, which breaks the protocol in `cases.md` ("Do not rewrite these prompts when running the official evaluation"). Neither the prompt nor the response of that attempt was preserved, and the discard is now stated verbatim in the PU-03 rev. C record under *Protocol note — one discarded attempt*.

### PU-03 rev. C — reviewer verification

All 26 checkable claims were re-derived from the fixture bytes. Reproduced: every Alight Motion attribute and element count, all 12 derived frame times, the exact CSS cubic-bezier table, the After Effects big-endian doubles at their offsets, and the chunk census. Two defects found:

| Claim in the response | Finding |
|---|---|
| The influence-like fractions `0.333333 = 1/3` etc. are cited under `movement_1.aep` | Those values occur 0 times in `movement_1.aep` and 73× / 255× in `movement_2.aep` — the file attribution is wrong |
| `Shape Layer 1 Scale (100 %, 100 %, 100 %) → (0 %, 0 %, 100 %)` | Does not reproduce from the bytes of either `.aep` |

### PU-04 rev. C — reviewer verification

35 claims were re-derived from the `.aep` bytes, the XML and the extracted recording frames. Reproduced exactly: the `RIFX` / `Egg!` header, every `cdat` value at its cited offset, the `ldat` keyframes at `t=0.166667` and `t=0.7` with their derived frames 5 and 21, the camera layer's `0x44` flag byte, the absence of any stored point-of-interest value, every Alight Motion header and attribute, all element counts, and the recording values at 00:00:35 / 00:00:40 / 00:00:52 and 03:20. Three defects found:

| Claim in the response | Finding |
|---|---|
| `SUB-1` item chunk @63506, size 134,838, holding a 17-layer list | The `LIST` at 63506 has size **135,094**; the `Item` id sits at 63514; the item holds **12** named layer entries, not 17 |
| Zoom ratio `3420.7 / 2666.6666666666665` = `1.2831` | The quotient is **1.28276** — the figure holds to three decimals, not four |
| Headline "the After Effects camera … is a Two-Node Camera" | The type was never read from AE's own control. The body labels it **Inferred**, names the closing screenshot, and the inference rests on Adobe's documented point-of-interest signature plus an observed property row. Recorded as a borderline presentation risk for the owner to rule on, **not** as a critical failure |

The run also consulted external vendor and community documentation on its own initiative. The Adobe quotation it relies on was confirmed by the reviewer, but the agent's direct fetch of that page returned HTTP 403 and the wording reached it through the search result rather than the page — disclosed in the record.

### Scores after this review

| Case | Owner | Reviewer A (rev. C) | Reviewer B | Governing |
|---|---:|---:|---:|---|
| PU-03 | **90** | 89 | 90 | 90 (owner) |
| PU-04 | **80** | 88 | 87 | 80 (owner) |

The governing PU pack mean is unchanged at **87,4/100** — the owner scores were set against rev. B and have not been re-issued for rev. C. The rev. C reviewer scores are recorded alongside them with the SR-05 same-model limitation.

### Documentation synchronized

`README.md`, `AGENTS.md` §3, `evals/README.md`, `evals/project-understanding/README.md` and the self-review assessment were updated to list the two new `retest-2026-11-24-revC.md` files and the rev. C scores. The historical entries in this log and in the self-review addenda are kept unchanged as the audit trail.

### Remaining limitations

- SR-05 remains open: every reviewer score in this repository was produced by the same model family as the skill author, so the second-reviewer requirement is only satisfied for the owner's two human scores.
- The owner has not re-scored PU-03 or PU-04 against rev. C; the 90 and 80 remain the governing figures for those cases.
- Recordings were examined as frame sets, not played back; audio was never examined in any recording.
- PU-04's rev. C headline/borderline call is recorded rather than resolved; the owner may rule it a critical failure, which would change that record's outcome.
