# R Code Standards

## Map

- Package philosophy
- Script structure
- Path management
- Explicitness versus abstraction
- `data.table` conventions
- Console output
- Figure style
- Variable naming
- Reproducibility
- Common pitfalls

## Package philosophy

Use a minimalist but sensible stack:

- `data.table` for primary data wrangling
- `fixest` for estimation
- `ggplot2` for figures
- `here` for paths
- `pacman` for package loading when appropriate
- `collapse` when grouped performance matters

Avoid elaborate tidyverse pipelines when `data.table` would be clearer and more consistent with the project.

## Script structure

Every pipeline script should have a header like this:

```r
# ============================================================
# Project: [Project Name]
# Script: 1-01.0_clean_data.r - [description]
#
# Input: [files]
# Output: [files]
# ============================================================
```

Place `rm(list = ls())` immediately before `pacman::p_load()` when the project follows that convention.

Use a stage-substep naming scheme:

- `1-XX.X_` for data cleaning and merging
- `2-XX.X_` for descriptive output
- `3-XX.X_` for analysis

Within a stage, use sequential group and sub-step numbering such as `1-01.0_`, `1-01.1_`, `1-02.0_`.

Use `code/temp/temp_*.r` for exploratory scripts and `code/archive/` for retired scripts.

Use section separators such as:

```r
# Section name -------
```

## Path management

- Always use `here()`.
- Never use `setwd()`.
- Never hardcode absolute paths.

Examples:

```r
dt <- fread(here("data", "raw", "source.csv"))
fwrite(results, here("data", "temp", "processed.csv"))
```

## Explicitness versus abstraction

- Prefer explicit code for core operations.
- Use functions or loops when they genuinely reduce error risk or remove large repeated blocks.
- Avoid premature abstraction for one-off tasks.

## `data.table` conventions

```r
dt[, new_col := old_col * 100]
dt[, .(total = sum(value, na.rm = TRUE)), by = .(state, year)]
panel <- merge(dt1, dt2, by = c("state", "year"))
dt <- fread(here("data", "raw", "file.csv"))
fwrite(dt, here("data", "temp", "processed.csv"))
```

Do not mix tidyverse verbs into the same data pipeline unless there is a clear reason.

## Console output

- Allowed: `message()` for major milestones
- Avoid: `cat()`, `print()`, decorative banners, noisy per-iteration output
- End scripts with a concise completion message when helpful

## Figure style

### Construction

- Create the plot object separately from saving it.
- Always specify `width` and `height` in `ggsave()`.
- Keep output file names aligned with the script name, such as `2-01.0_birth_share_trends.png`.

### Palette

Use a small deliberate palette such as:

```r
pal <- c(
  navy   = "#000080",
  pink   = "#FF1493",
  teal   = "#2A9D8F",
  orange = "#D4780A",
  purple = "#6A3D9A",
  slate  = "#708090"
)
```

Preferred defaults:

- navy plus pink for two-series plots
- navy for bars
- pink for fitted lines

### Theme

Use a clean white background with visible axes and no default grid clutter:

```r
theme_clean <- theme_bw() +
  theme(
    panel.background = element_rect(fill = "white", colour = NA),
    plot.background  = element_rect(fill = "white", colour = NA),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line        = element_line(colour = "black", linewidth = 0.4),
    panel.border     = element_blank(),
    text             = element_text(size = 12)
  )
```

### Labels over legends

- Prefer direct labels on lines and points where practical.
- Use legends only when direct labels would create clutter.
- Keep axis labels readable, sentence case, and unit-aware.

### Line plots

- Prefer solid lines.
- Use color and direct labels to distinguish series rather than line type when possible.

## Variable naming

- Use snake_case everywhere.
- Prefer descriptive names such as `adoption_year_quarter` or `tot_spend_per_100`.
- Keep time variables consistent across scripts.

## Reproducibility

- Use `set.seed()` once if randomness is involved.
- Load packages near the top.
- Create required output directories explicitly.
- Keep all paths relative to the project root.

## Common pitfalls

| Pitfall | Impact | Prevention |
| --- | --- | --- |
| `setwd()` in scripts | Breaks on other machines | Use `here()` |
| `cat()` for status | Noisy stdout | Use `message()` sparingly |
| Tidyverse where `data.table` is clearer | Inconsistent style | Default to `data.table` |
| Nested `ggsave()` calls | Harder to debug | Separate plot creation from saving |
| Hardcoded absolute paths | Breaks on other machines | Build paths with `here()` |
