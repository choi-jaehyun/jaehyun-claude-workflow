# R Review Protocol

## Map

- Preparation
- Review categories
- Report template
- Review rules

## Preparation

1. Read the target script end-to-end.
2. Read the local repo standard in `../r-code-conventions/references/r-standards.md`.
3. Review systematically rather than free-form.
4. Report only. Do not edit source files while using this skill.

## Review categories

### 1. Structure and header

- Check for a header block with project, script, purpose, inputs, and outputs.
- Check whether the script fits the numbered pipeline structure when it belongs in `code/`.
- Check for a logical order: setup, load, transform, compute, write outputs.
- Check for clear section separators.

### 2. Packages and paths

- Packages should load near the top, preferably with `pacman::p_load()` or explicit `library()` calls.
- All paths should use `here()`.
- Output directories should be created explicitly with `dir.create(..., recursive = TRUE, showWarnings = FALSE)`.
- Core data manipulation should default to `data.table`.

### 3. Explicitness versus abstraction

- Prefer explicit code for visible core operations such as regressions and figure creation.
- Recommend a function when repeated blocks create copy-paste risk or hide a multi-step pattern that should be named.
- If functions exist, check naming, comments, defaults, and return values.

### 4. `data.table` conventions

- Check for idiomatic `:=`, `.()`, `by = .(...)`, `merge()`, `fread()`, and `fwrite()`.
- Flag mixed tidyverse plus `data.table` pipelines unless there is a strong reason.

### 5. Console output hygiene

- `message()` should be sparse and milestone-oriented.
- `cat()` and `print()` should not be used for routine progress logging.
- End-of-script completion messages should be concise and informative.

### 6. Reproducibility

- If randomness exists, look for one visible `set.seed()`.
- Check for hidden dependencies, hardcoded machine-specific values, or unexplained magic numbers.
- Check that intermediate outputs land in the expected project directories.

### 7. Figure quality

- Plot construction and saving should be separate.
- `ggsave()` should specify width and height explicitly.
- Check for a deliberate theme and palette instead of raw defaults.
- Prefer direct labels over legends when feasible.
- Flag cluttered grids, unreadable axis breaks, and inconsistent styling across figures.

### 8. Domain correctness

- Check whether the implemented estimator matches the documented formula or research design.
- Check whether standard errors and clustering match the design.
- Check whether estimands are labeled correctly.
- Revisit the repo standards for known pitfalls before calling something correct.

### 9. Comment quality

- Comments should explain why, not restate what obvious code already says.
- Flag stale commented-out code and missing explanations around non-obvious logic.

### 10. Professional polish

- Check indentation, line length, spacing, logical naming, and `TRUE`/`FALSE` usage.
- Prefer snake_case for variables and functions.

## Report template

```markdown
# R Code Review: [script_name].r
**Date:** [YYYY-MM-DD]
**Reviewer:** r-reviewer skill

## Summary
- **Total issues:** N
- **Critical:** N
- **High:** N
- **Medium:** N
- **Low:** N

## Issues

### Issue 1: [Brief title]
- **File:** `[path/to/file.r]:[line_number]`
- **Category:** [Structure / Packages / Style / data.table / Console / Reproducibility / Figures / Domain / Comments / Polish]
- **Severity:** [Critical / High / Medium / Low]
- **Current:**
  ```r
  [problematic code]
  ```
- **Proposed fix:**
  ```r
  [corrected code]
  ```
- **Rationale:** [Why this matters]

## Checklist summary
| Category | Pass | Issues |
| --- | --- | --- |
| Structure and header | Yes/No | N |
| Packages and paths | Yes/No | N |
| Explicitness versus abstraction | Yes/No | N |
| data.table conventions | Yes/No | N |
| Console output | Yes/No | N |
| Reproducibility | Yes/No | N |
| Figures | Yes/No | N |
| Domain correctness | Yes/No | N |
| Comments | Yes/No | N |
| Polish | Yes/No | N |
```

## Review rules

- Be specific: line numbers and exact snippets matter.
- Be actionable: every issue needs a plausible fix.
- Prioritize correctness before style.
- When the repo standard and generic best practice conflict, explain the tradeoff rather than hiding it.
