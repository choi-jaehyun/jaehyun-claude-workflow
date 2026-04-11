---
name: workflow
description: Coordinate substantial repository work with this project's plan-build-verify loop. Use when Codex is handling multi-file changes, needs a saved plan, wants a structured verification pass, or needs to update AGENTS.md session memory at the end of work.
---

# Workflow

Use this skill for non-trivial repository work. It adapts the old Claude workflow rule to this repo's Codex setup, with `AGENTS.md` as the session-memory file.

## When to formalize a plan

- Use a saved plan for multi-file changes, new features, unclear approaches, or anything likely to need verification and review.
- Skip the formal plan for small one-file edits, running an existing skill, or answering informational questions.

## Core loop

1. Save a short plan file in `quality_reports/plans/YYYY-MM-DD_short-description.md`.
2. Implement the change.
3. Verify with the relevant local skill:
   - `$verifier` for compile, render, or execution checks
   - `$proofreader` for writing quality
   - `$r-reviewer` for R scripts
   - `$domain-reviewer` for substantive academic review
4. Fix issues in priority order and re-run verification.
5. Stop after three review/fix rounds unless the user explicitly wants more iteration.

## Recovery and handoff

- At the start of a session, read `AGENTS.md`, then check `git log --oneline -10`, then inspect `git diff`.
- Do not read `quality_reports/session_logs/lab_journal.md` unless the user asks or `AGENTS.md` leaves a critical context gap.
- Use [references/workflow-loop.md](references/workflow-loop.md) for the plan template, end-of-session logging format, and quality heuristics.
