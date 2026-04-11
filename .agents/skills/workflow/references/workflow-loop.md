# Workflow Loop Reference

## Map

- When to plan
- Plan file template
- Execution loop
- Recovery
- Session-end logging
- Quality heuristics
- Continuous learning

## When to plan

Use a saved plan when the task is multi-file, high-risk, unclear, or likely to require verification and rework.

Skip the formal plan when the task is a quick one-file edit, an informational question, or a straightforward skill run.

## Plan file template

Save plans to `quality_reports/plans/YYYY-MM-DD_short-description.md`.

Suggested structure:

```markdown
# Plan: [short title]
**Date:** [YYYY-MM-DD]

## Goal
[What will change]

## Files
- [path]
- [path]

## Order
1. [step]
2. [step]

## Risks
- [risk]

## Verification
- [how the change will be checked]
```

## Execution loop

Use this order:

```text
IMPLEMENT -> VERIFY -> REVIEW -> FIX -> RE-VERIFY
```

Routing:

- Use `$verifier` for execution-based checks.
- Use `$proofreader` for writing quality.
- Use `$r-reviewer` for R code review.
- Use `$domain-reviewer` for substantive economics review.

Cap the loop at three review/fix rounds unless the user wants continued iteration.

## Recovery

At the start of a session or after context compression:

1. Read `AGENTS.md`.
2. Run `git log --oneline -10`.
3. Inspect `git diff`.

Do not read `quality_reports/session_logs/lab_journal.md` unless the user asks or the short session memory in `AGENTS.md` is not enough.

## Session-end logging

Update two places:

1. Append a full entry to `quality_reports/session_logs/lab_journal.md`.
2. Prepend a compact entry to the `Recent Sessions` section in `AGENTS.md`, keeping only the three newest entries.

`AGENTS.md` entry format:

```markdown
### YYYY-MM-DD - [one-line description]
- What was accomplished
- Key decisions or findings
- Blockers or open questions
- Next steps
```

Also refresh the `Immediate Plans` list so it keeps the top two or three next tasks only.

## Quality heuristics

- About `80/100`: usually good enough to commit
- About `90/100`: usually good enough for a PR

Treat these as heuristics, not hard gates.

## Continuous learning

If the repo uses a durable memory file such as `MEMORY.md`, add concise lessons when a non-obvious mistake is corrected.
