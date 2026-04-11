---
name: r-code-conventions
description: Apply this repository's local R coding standards when writing, refactoring, or reviewing `.r` and `.R` files, especially under `code/`. Use it for pipeline structure, `here()` paths, `data.table`-first style, console and figure conventions, naming, and reproducibility.
---

# R Code Conventions

Use this skill as the repo-local source of truth for R work. Apply it before large R edits and before formal R code review.

## Quick rules

- Use `here()` for all paths. Never use `setwd()` or machine-specific absolute paths.
- Prefer `data.table` for core wrangling and avoid mixing `data.table` with tidyverse pipelines.
- Keep scripts in the numbered workflow; use `code/temp/temp_*.r` for experiments and `code/archive/` for retired scripts.
- Use `message()` sparingly for milestone logging. Do not use `cat()` or `print()` for routine status output.
- Build figures explicitly: create the plot object first, then call `ggsave()` with width and height.
- Use snake_case names, create output directories explicitly, and call `set.seed()` once when randomness exists.

## Full standard

Read [references/r-standards.md](references/r-standards.md) before making substantial R changes. It carries over the detailed script-structure, figure-style, and reproducibility rules from the original Claude rule set.

## Review alignment

When using `$r-reviewer`, apply this skill first so review findings reflect the repo's own standards rather than generic R preferences.
