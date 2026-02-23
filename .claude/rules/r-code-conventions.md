---
paths:
  - "**/*.r"
  - "**/*.R"
  - "code/**"
---

# R Code Conventions

These standards apply to all R scripts in this repository.

---

## 1. Package Philosophy

Take a **minimalist but sensible** approach:

- **data.table** — Primary tool for data wrangling. Strongly preferred over tidyverse.
- **fixest** — Regression analysis (`feols`, etc.).
- **ggplot2** — Visualization.
- **here** — All file paths. Never `setwd()`, never absolute paths.
- **pacman** — Package management via `p_load()`.
- **collapse** — Fast grouped operations when needed.

Avoid elaborate tidyverse pipelines. data.table syntax is preferred for most data manipulation.

## 2. Script Structure

Every script should have a header and fit into the numbered pipeline:

```r
# ============================================================
# Project: [Project Name]
# Script: 1-01.0_clean_data.r - [description]
#
# Input: [files]
# Output: [files]
# ============================================================
```

Every script should have rm(list = ls()) right before the pacman::p_load() call.

### Naming convention

Scripts use a stage-substep prefix: `STAGE-GROUP.STEP_description.r`

- **`1-XX.X_`** — Data cleaning and merging (decrypt, translate, concatenate, merge)
- **`2-XX.X_`** — Descriptive output (graphs, tables)
- **`3-XX.X_`** — Analysis (regression, DiD, IV, RDD, etc.)

Within each stage: `1-01.0_` → `1-01.1_` → `1-02.0_` (group number, then decimal sub-step).

Experimental scripts go in `code/temp/` with a **`temp_`** filename prefix. Archived scripts go in `code/archive/`.

Section separators: `# Section name -------`

A `main.r` orchestrator calls all active scripts via `source(here("code", "1-01.0_...r"))`.

## 3. Path Management

- **Always use `here()`** to build file paths
- **Never use `setwd()`**
- **Never hardcode absolute paths**

```r
# Good
dt <- fread(here("data", "raw", "source.csv"))
fwrite(results, here("data", "temp", "processed.csv"))

# Bad
dt <- fread("/Users/cwing/projects/my_project/data/raw/source.csv")
setwd("~/projects/my_project")
```

## 4. Code Style: Explicitness vs Abstraction

- **Prefer explicitness** for core operations. It should be easy to see exactly where a regression gets run or a figure gets made.
- **Use functions and loops only when warranted** — when you'd otherwise write 20+ nearly-identical lines.
- **Avoid premature abstraction.** Three similar lines of code is often better than a function that obscures what's happening.

## 5. data.table Conventions

```r
# Column creation
dt[, new_col := old_col * 100]

# Aggregation
dt[, .(total = sum(value, na.rm = TRUE)), by = .(state, year)]

# Merging
panel <- merge(dt1, dt2, by = c("state", "year"))

# I/O
dt <- fread(here("data", "raw", "file.csv"))
fwrite(dt, here("data", "temp", "processed.csv"))
```

Do not mix tidyverse and data.table in the same pipeline.

## 6. Console Output Policy

- **Allowed:** `message()` for progress milestones only
- **Forbidden:** `cat()`, `print()`, ASCII banners, per-iteration output
- End each script with: `message("script_name.r complete: N rows written")`

## 7. ggplot2 & Figure Style

### Construction
- **Separate plot creation from saving:**
  ```r
  p <- ggplot(data, aes(x, y)) + geom_point()
  ggsave(here("outputs", "figures", "2-01.0_birth_share_trends.png"), p, width = 10, height = 8)
  ```
- **Output file names mirror the script:** `[stage]-[group].[step]_[description].png`
  - e.g., script `2-01.0_descriptives.r` → figure `2-01.0_birth_share_trends.png`
- Explicit dimensions in `ggsave()`: `width`, `height` always specified
- **Titles:** Include by default. For LaTeX figures, omit (let `\caption{}` handle it) but keep the title as a comment for easy toggling.

### Colour Palette
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
- **Primary pair:** navy + pink (two-series plots)
- **Extended:** teal, orange, purple, slate (3+ series)
- **Bar charts:** navy fill
- **Regression / fit lines:** pink

### Theme
```r
theme_clean <- theme_bw() +
  theme(
    panel.background = element_rect(fill = "white", colour = NA),
    plot.background  = element_rect(fill = "white", colour = NA),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.line        = element_line(colour = "black", linewidth = 0.4),
    panel.border     = element_blank(),
    text = element_text(size = 12)
  )
```
- **Show axes.** Always visible x and y axis lines.
- **No grid.** Remove major and minor grid lines unless specifically needed.
- **White background.** No grey panel fill.

### Labels Over Legends
- **Prefer direct text labels** on or near lines/points rather than a separate legend.
- Use `annotate("text", ...)` or `geom_text()` at endpoints or peaks.
- Use `coord_cartesian(clip = "off")` with extra `plot.margin` when labels extend beyond the plot area.
- Colour-matched labels (same colour as the series they identify).

### Line Plots
- **All lines solid.** Do not use dashed lines to distinguish series — colour and labels handle that.
- `linewidth = 1` for primary series, `0.8` for secondary.

## 8. Variable Naming

- **Snake_case** for everything
- Descriptive names: `tot_spend_per_100`, `adoption_year_quarter`, `n_rx_obesity`
- Consistent temporal variables: `year`, `quarter`, `year_quarter`

## 9. Reproducibility

- `set.seed()` called ONCE at top if randomness is used (YYYYMMDD format)
- All packages loaded at top via `pacman::p_load()` or `library()`
- All paths relative via `here()`
- `dir.create(..., recursive = TRUE, showWarnings = FALSE)` for output directories

## 10. Common Pitfalls

<!-- Add project-specific pitfalls here -->

| Pitfall | Impact | Prevention |
|---------|--------|------------|
| `setwd()` in scripts | Breaks on other machines | Use `here()` with data/raw, data/temp, data/clean |
| `cat()` for status | Noisy stdout | Use `message()` sparingly |
| Tidyverse where data.table is clearer | Inconsistent style | Default to data.table |
| Nested `ggsave()` | Hard to debug | Separate creation from saving |
| Hardcoded absolute paths | Breaks on other machines | Use `here()` |
