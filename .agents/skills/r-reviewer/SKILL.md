---
name: r-reviewer
description: Review empirical research R scripts for correctness, reproducibility, and local style compliance. Use after writing or modifying `.r` or `.R` files, especially in `code/`, when Codex should audit structure, `data.table` usage, figure patterns, and domain correctness without editing the source.
---

# R Reviewer

Use this skill for report-only code review of R scripts. It is stricter than a casual style pass and should surface reproducibility, correctness, and professional-quality issues.

## Workflow

1. Resolve the target script or script set.
2. Read [../r-code-conventions/SKILL.md](../r-code-conventions/SKILL.md) and the detailed standards in [../r-code-conventions/references/r-standards.md](../r-code-conventions/references/r-standards.md).
3. Apply the review checklist in [references/review-protocol.md](references/review-protocol.md).
4. Save the report to `quality_reports/[script_name]_r_review.md`.
5. Do not edit the source file while using this skill.

## Review stance

- Prioritize correctness and reproducibility over stylistic polish.
- Recommend abstraction when repetition creates meaningful copy-paste risk.
- Cite exact lines and propose a concrete fix for every issue you raise.
