# Workflow: Plan → Build → Verify

## Plan First

For non-trivial tasks (multi-file, unclear approach, new features), **enter plan mode before writing code:**

1. Use `EnterPlanMode`
2. Draft the plan — what changes, which files, in what order
3. Save to `quality_reports/plans/YYYY-MM-DD_short-description.md`
4. Present to user and wait for approval
5. Exit plan mode, then implement

Skip planning for: single-file edits, running existing skills, informational questions.

## The Orchestrator Loop

After plan approval, execute autonomously:

```
IMPLEMENT → VERIFY → REVIEW (agents) → FIX → RE-VERIFY → SCORE
```

- **Verify:** compile/render/run code and confirm outputs exist
- **Review:** launch appropriate agents by file type (.tex → proofreader, .R → r-reviewer, etc.)
- **Fix:** critical → major → minor
- **Score:** apply quality thresholds (see below)
- **Max 3 review-fix rounds.** After that, present what remains.

"Just do it" mode (user says "handle it"): skip final approval pause, auto-commit if score >= 80.

## Quality Thresholds

- **80/100** — ready to commit
- **90/100** — ready for PR

## Session Management

**Start:** Read CLAUDE.md (contains recent sessions + project context) → check `git log --oneline -10` → check `quality_reports/plans/` for in-progress work. This is enough to get up to speed. Do NOT read the lab journal unless the user asks or something critical seems missing from CLAUDE.md.

**During:** Save important decisions to disk (plan files). Prefer auto-compression over `/clear`.

**End — two-track logging:**
1. **Lab journal** (`quality_reports/session_logs/lab_journal.md`): Append a full session entry — everything done, commands run, decisions made, errors hit. This is the permanent archive; be thorough.
2. **CLAUDE.md Recent Sessions block**: Prepend a new entry (newest on top). Keep only the 3 most recent — drop the oldest when adding a new one. Format:
   ```
   ### YYYY-MM-DD — [one-line description]
   - What was accomplished
   - Key decisions or findings
   - Blockers or open questions
   - Next steps
   ```

**Recovery** (after compression or new session): Read CLAUDE.md → `git log --oneline -10` → `git diff`. State what you understand the current task to be. Only read the lab journal if instructed.

## Continuous Learning

When a mistake is corrected, save a `[LEARN:tag]` entry to MEMORY.md:
```
[LEARN:r-code] fread silently drops rows when ... → use ...
```
