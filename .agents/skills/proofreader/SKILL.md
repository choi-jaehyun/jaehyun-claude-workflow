---
name: proofreader
description: Proofread academic writing in `.tex`, `.qmd`, `.md`, `.pdf`, and extractable `.docx` files. Use after drafting or revising papers, slides, lecture notes, assignments, or documentation when Codex should report grammar, typo, overflow, citation, and consistency issues without editing the source.
---

# Proofreader

Use this skill for writing quality and presentation issues. It complements, but does not replace, substantive review.

## Workflow

1. Resolve the target document and infer the format.
2. Read [references/checklist.md](references/checklist.md) for format-specific handling and the proofreading checklist.
3. Read the whole document, or chunk long PDFs into manageable page ranges.
4. Save the review to `quality_reports/[filename_without_ext]_proofread_report.md`.
5. Do not edit the source file while using this skill.

## Notes

- For `.docx`, use any DOCX extraction workflow available in the current session. If none is available, review an exported PDF or the extractable text you can access.
- Every issue should include the exact location, current text, proposed fix, category, and severity.
- If the writing also needs econometric or identification review, pair this skill with `$domain-reviewer`.
