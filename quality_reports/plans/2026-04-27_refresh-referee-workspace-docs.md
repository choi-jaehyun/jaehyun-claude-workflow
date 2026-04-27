# Plan: Refresh referee workspace docs
**Date:** 2026-04-27

## Goal
Update the repository guides so they describe the expanded contents and purpose of
`quality_reports/referee_workspace/`, which now includes broader writing and presentation
reference material alongside referee templates.

## Files
- README.md
- AGENTS.md
- CLAUDE.md

## Order
1. Review the current `referee_workspace/` filenames and identify how the folder purpose has broadened.
2. Update the shared docs to describe the workspace as tracked guidance for review, writing, and presentation work.
3. Refresh session-memory sections in `AGENTS.md` and `CLAUDE.md`, then verify the diff and repo status.

## Risks
- The folder name still says `referee_workspace`, so the wording needs to broaden its purpose without implying a rename.
- `AGENTS.md` should keep only the three most recent session entries.

## Verification
- Re-read the changed markdown content in diff form.
- Confirm `git status --short` shows only the expected doc edits, plan file, and the newly added reference PDFs.
