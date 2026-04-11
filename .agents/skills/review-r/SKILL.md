---
name: review-r
description: Run the R code review protocol on R scripts using the local `$r-reviewer` and `$r-code-conventions` skills. Produces a report without editing files.
disable-model-invocation: true
argument-hint: "[filename or 'all']"
---

# Review R Scripts

Run the comprehensive R code review protocol.

## Steps

1. **Identify scripts to review:**
   - If `$ARGUMENTS` is a specific `.r` filename: review that file only
   - If `$ARGUMENTS` is `all`: review all R scripts in `code/` and exclude `code/temp/` and `code/archive/`

2. **For each script, apply the local review stack:**
   - Read `.agents/skills/r-code-conventions/SKILL.md`
   - Follow `.agents/skills/r-reviewer/SKILL.md`
   - Save the report to `quality_reports/[script_name]_r_review.md`

3. **After all reviews complete, present a summary:**
   - Total issues found per script
   - Breakdown by severity (Critical / High / Medium / Low)
   - Top 3 most critical issues

4. **IMPORTANT: Do NOT edit any R source files.**
   Only produce reports. Fixes are applied after user review.
