# Plan: Document referee workspace
**Date:** 2026-04-24

## Goal
Update the repository guides so they describe the new `quality_reports/referee_workspace/`
folder and its role in the template, then commit and push the changes.

## Files
- README.md
- AGENTS.md
- CLAUDE.md

## Order
1. Add the referee workspace to the documented repo structure and quality report guidance.
2. Refresh session-memory sections in `AGENTS.md` and `CLAUDE.md` as needed for the template.
3. Review the wording for consistency, then stage, commit, and push.

## Risks
- The template currently mixes old and new repo names such as `.Codex/` and `.agents/skills/`.
- `quality_reports/` contains both tracked reference material and gitignored session logs, so the wording needs to stay precise.

## Verification
- Re-read the edited markdown files and check that `quality_reports/referee_workspace/` is described consistently.
- Confirm `git status` shows only the intended documentation and workspace additions before commit.
