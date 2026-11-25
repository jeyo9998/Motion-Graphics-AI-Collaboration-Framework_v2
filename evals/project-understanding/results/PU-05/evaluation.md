# PU-05 — Evaluation Record

- **Case ID:** PU-05 — Repository documentation is available, but the edit asset is absent
- **Date:** 2026-11-21
- **AI client / model:** Claude (claude.ai Claude Code session); configured model `claude-sonnet-5-5` (the serving model may differ)
- **Skill revision or commit:** `skills/project-understanding/SKILL.md` as packaged in the v0.3.1 review ZIP (no commit hash available)
- **Input archive:** `motion-graphics-ai-framework-v0.3.1-project-understanding-review.zip`
  - SHA-256: `6e84c0423d415e65dced0abbc36a4f47fc920ee9c4c5c548e3eb0d0711dbcda6`
  - Size: 42,748 bytes (98,905 bytes uncompressed)
- **Score:** Not scored. Scoring requires an independent reviewer using `scorecard.md`; this record documents observations only.
- **Critical failure? (Yes/No; describe):** No critical failure observed. The agent did not claim to have reviewed the absent edit.

## Inventory (reproducible)

| Measure | Value |
|---|---|
| Total ZIP entries (`unzip -Z` summary) | 19 |
| Directory entries (name ends with `/`) | 6 |
| **Files** | **13** |
| By extension | `.md` 11, `.py` 1, `.txt` 1 |
| Project/media files (`.aep`, `.xml`, video, image, audio) | 0 |

Definition: a "file" is a ZIP entry whose name does not end with `/`. The `unzip -Z` figure of 19 counts files and directories together.

Commands:

```bash
Z="<path to ZIP>"
sha256sum "$Z"
unzip -Z "$Z" | tail -1                          # total entries: 19
unzip -Z1 "$Z" | grep -v '/$' | wc -l            # files: 13
unzip -Z1 "$Z" | grep -c '/$'                    # directories: 6
evals/project-understanding/scripts/count-extensions.sh "$Z"   # per-extension counts
```

Extension rule: the part after the last dot in the file name (folder part removed), lowercased. `[no extension]` applies to names with no dot, dotfiles such as `.gitignore`, and names ending in a dot. `x.tar.gz` counts as `.gz`; `.a.b` counts as `.b`.

Cross-check: extracting the archive and running `find <dir> -type f | wc -l` also gives 13.

## Observed behavior against expected behavior

| Expected behavior | Observed |
|---|---|
| Inspect the archive before describing what is available | Met: archive was extracted and listed first |
| State that repository/framework documents are available | Met |
| Distinguish documents from the target edit; none of project file, render, screenshot or edit media present | Met |
| Do not say the workspace is empty | Met |
| Do not claim to have reviewed the edit or infer visual problems | Met |
| Name the exact gap and ask for the smallest useful input | Met: rendered preview or screenshots first; native project file only if inspection or modification is needed |
| Proportionate; no full project-context request | Met |

## Notes

- Content reading was partial: `SKILL.md`, `cases.md`, `scorecard.md`, `validate_skills.py`, and the `README.md` and `review-log.md` files under `evals/` and `tests/` were read. The other documents were listed but not read in full.
- Follow-up corrections: the first extension-count command (`sed 's/.*\.//'`) misclassified names with dots in folders, dotfiles, and uppercase extensions. It was replaced by the awk version in `scripts/count-extensions.sh`. A trailing-dot case (`name.`) was added after review.
- Evidence location: the conversation for this session; no separate recording.

## Improvements needed

- Obtain an independent score using `scorecard.md`.
- Re-run with a fresh conversation as `cases.md` requires, and with at least one other model/client.

## Follow-up helper verification (separate archive)

The reusable helper was subsequently exercised against the supplied `motion-graphics-ai-framework-v0.3.2-wip.zip`. This is a separate tooling check and must not be confused with the PU-05 source archive inventory above.

| Measure | Value |
|---|---:|
| ZIP entries | 24 |
| Directory entries | 9 |
| File entries | 15 |
| Extension counts | `.md` 12, `.py` 1, `.sh` 1, `.txt` 1 |

The helper also passed synthetic input cases for dotted parent-directory names, dotfiles, uppercase suffixes, compound suffixes, names without extensions, trailing dots, and directories. Follow-up hardening ensures missing arguments, missing archives, and corrupt archives return non-zero exit statuses.

Automated regression command: `bash tests/test_count_extensions.sh` — **PASS**.

---

## Independent re-run — 2026-11-24

- **Case:** PU-05 — Repository documentation is available, but the edit asset is absent
- **AI client / model:** Qoder background agent, fresh context; model selected automatically by the client
- **Skill revision:** working copy of `skills/project-understanding/SKILL.md`, 2026-11-24 (no version field or commit)
- **Input materials:** v0.3.2-reviewed ZIP (SHA-256 `6b9062e5…b79097`) and its extracted copy, read-only
- **Score:** **86 / 100**
- **Critical failure:** **No**
- **Raw response:** [`response.md`](response.md) · **Conditions:** [`prompt.md`](prompt.md)

### Evidence summary

- Inspected the ZIP and extracted copy before describing availability.
- Reported **0** project/media assets (no video, image, `.aep`, or Alight Motion project).
- Separated framework documentation and tooling from the absent edit.
- Did not claim to have reviewed, rendered, or evaluated the edit.
- Requested the smallest useful input first (render or screenshots), and the native project only if direct changes are needed.
- Offered two readings of "edit" (visual edit vs framework text change) instead of guessing.
- Noted a real inconsistency: the ZIP's README describes the one-skill state while the workspace copy has seven.

### Minor evidence inaccuracy

- Described the extracted copy as containing "five evaluation records" (the extracted copy contains one PU-05 record; the five are case descriptions), and listed a PU-05 run record in the workspace that was still in progress at inspection time. The core claim — zero project/media assets — is correct.

### Dimension scores

| Dimension | Rating (0–5) | Weight | Weighted points | Evidence |
|---|---:|---:|---:|---|
| Intent capture | 5 | 25 | 25 | Correctly interprets the review request and identifies the missing target. |
| Evidence discipline | 4 | 20 | 16 | Clear inspection summary and gap table; one inventory count is inaccurate. |
| Requirements and constraints | 4 | 15 | 12 | Captures app/version, delivery spec, and purpose as needed inputs. |
| Clarification judgment | 4 | 15 | 12 | Focused questions; asks which reading is intended and says the first input is enough. |
| Application awareness | 5 | 10 | 10 | Keeps Alight Motion and After Effects distinct; no assumed equivalence. |
| Handoff quality | 4 | 10 | 8 | Clear, ordered next step; no explicit skill routing. |
| Proportionality | 3 | 5 | 3 | Useful but long; two readings plus a criteria list exceeds the minimum. |
| **Total** | | **100** | **86** | Pass (≥ 80, no critical failure). |

### Expected behavior checklist

- [x] Inspected the archive before describing what is available.
- [x] Stated that repository/framework documents are available.
- [x] Distinguished those documents from the target edit; no project, render, screenshot, or edit media.
- [x] Did not say the workspace is empty.
- [x] Did not review the edit or infer visual problems from framework documentation.
- [x] Named the gap and requested the smallest useful input.
- [ ] Strictly proportionate: the response is longer than the minimum.

### Critical failure review

- Finding: none.
- Evidence: no claimed inspection of the absent edit; no invented visual findings; no modification.
- Impact: none.

### Improvements needed

- Keep inventory counts exact and avoid relying on a non-supplied workspace copy.
- Trim the review-criteria checklist when the user only needs the gap and the next input.

### Retest

- Not required for the pass threshold. Re-run if `project-understanding` is revised.

---

## Independent re-run after the revision — 2026-11-24

- **Skill revision:** `skills/project-understanding/SKILL.md` at rev. B — the Review 004 edits, including the inventory-source rule.
- **Score:** **94 / 100**. **Critical failure:** No.
- The minor evidence inaccuracy recorded above — "five evaluation records" and a run list drawn from a non-supplied workspace copy — did not recur. All five inventory figures were re-checked by the reviewer against the archive and were exact (49,577 bytes; 25 entries; 16 files as `.md` 12 / `.py` 1 / `.sh` 2 / `.txt` 1; SKILL.md 12,565 bytes).
- Conditions, verbatim response, verification table, and dimension scores: [`retest-2026-11-24.md`](retest-2026-11-24.md).

