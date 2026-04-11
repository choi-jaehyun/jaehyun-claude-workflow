---
name: proofread
description: Run the proofreading protocol on project files using the local `$proofreader` skill. Checks grammar, typos, overflow, consistency, and academic writing quality without editing files.
disable-model-invocation: true
argument-hint: "[filename or 'all']"
---

# Proofread Academic Writing

Run the proofreading protocol on papers, slides, notes, or other written content. Produce a report of all issues found without editing any source files.

## Steps

1. **Identify files to review:**
   - If `$ARGUMENTS` is a specific filename: review that file only
   - If `$ARGUMENTS` is `all`: review all `.tex`, `.qmd`, and `.md` files in the project

2. **For each file, follow the local proofreader skill** in `.agents/skills/proofreader/SKILL.md`, which checks for:
   - Grammar
   - Typos
   - Overflow and layout risks
   - Citation, notation, and terminology consistency
   - Academic writing quality

3. **Produce a detailed report** for each file listing every finding with:
   - Location
   - Current text
   - Proposed fix
   - Category
   - Severity

4. **Save each report** to `quality_reports/[filename_without_ext]_proofread_report.md`

5. **IMPORTANT: Do NOT edit any source files.**
   Only produce the report. Fixes are applied separately after user review.

6. **Present a summary** to the user:
   - Total issues found per file
   - Breakdown by category
   - Most critical issues highlighted
