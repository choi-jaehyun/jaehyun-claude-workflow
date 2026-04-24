# CLAUDE.md — Project Workflow Template

**Project:** [PROJECT NAME]
**Type:** [research / teaching]
**Working Branch:** main

---

## Recent Sessions

<!-- INSTRUCTIONS FOR CLAUDE: At session end, prepend a new entry here (newest on top).
     Keep only the 3 most recent entries — drop older ones.
     Format: ### YYYY-MM-DD — [one-line description]
     Body: 3-5 bullet points: what was done, key decisions, what's next.
     Full history lives in quality_reports/session_logs/lab_journal.md — do NOT read it
     unless the user asks or something critical seems to be missing. -->

### 2026-04-24 - Added a referee workspace and documented it across the template
- Added `quality_reports/referee_workspace/` with referee-writing reference files, including a basic guideline plus example cover-letter and referee-report documents.
- Updated `README.md`, `AGENTS.md`, and `CLAUDE.md` so the template explains how `quality_reports/` now separates tracked reference material from the gitignored lab journal.
- Kept `AGENTS.md` as the primary Codex session-memory file while preserving `CLAUDE.md` for compatibility.
- Next step is to use the referee workspace in a real review workflow and decide how much of that process should become a dedicated skill.

---

## Immediate Plans

<!-- INSTRUCTIONS FOR CLAUDE: Keep 2-3 of the most important upcoming tasks here.
     Update this list at session end — mark completed items done, add new ones if discussed.
     Keep it short: one line per item, ordered by priority.
     Format: - [ ] Short description of task
              - [x] Completed task (remove these when list is updated) -->

- [ ] Forward-test the migrated skills on a real manuscript, R script, or pipeline run.
- [ ] Decide whether `CLAUDE.md` and `AGENTS.md` should both remain active session-memory files or be consolidated.
- [ ] Use `quality_reports/referee_workspace/` in a real referee-report workflow and decide whether it should become a dedicated review skill.

---

## Project Overview

<!-- Describe your project in 2-3 sentences. What question does it answer? -->

[DESCRIBE YOUR PROJECT HERE]

---

## Skills (Slash Commands)

| Command | What It Does |
|---------|-------------|
| `/compile-paper` | Compile LaTeX manuscript (latexmk + biber) |
| `/run-pipeline` | Run main.r and verify all outputs |
| `/proofread [file]` | Grammar, typo, and consistency review |
| `/review-r [file]` | R code quality and reproducibility review |
| `/review-paper [file]` | Full manuscript review (identification, econometrics, citations) |
| `/validate-bib` | Cross-reference citations vs bibliography |
| `/devils-advocate [file]` | Challenge design decisions |
| `/split-pdf [path or query]` | Download, split, and deeply read an academic PDF (4-page chunks, structured extraction) |

---

## Project Structure

<!-- Adapt to your project. Delete directories you don't need. -->

```
project/
├── CLAUDE.md
├── .claude/                     # Agents, rules, skills
├── code/
│   ├── main.r                   # Reproduces all results
│   ├── 1-01.0_clean_data.r      # Stage 1: data cleaning/merging
│   ├── 2-01.0_descriptives.r    # Stage 2: descriptive output
│   ├── 3-01.0_estimation.r      # Stage 3: analysis
│   ├── temp/                    # Experimental scripts (temp_ prefix)
│   └── archive/                 # Archived scripts
├── data/
│   ├── raw/                     # NOT in git
│   ├── clean/                   # NOT in git
│   └── temp/                    # NOT in git
├── data_dict/                   # Data dictionaries and documentation for raw data sources (NOT in git)
├── outputs/
│   ├── tables/
│   └── figures/
├── manuscript/
│   ├── main.tex                 # Compile from project root
│   └── references.bib
├── literature/                  # NOT in git
├── quality_reports/
│   ├── plans/
│   ├── referee_workspace/       # Referee-report guidance and examples
│   └── session_logs/
│       └── lab_journal.md           # NOT in git
```

**Compilation:** `latexmk -pdf manuscript/main.tex` from the project root.

---

## Code

### `code/` — Naming Convention

Scripts follow a numbered prefix that indicates their stage in the workflow:

- **`1-XX.X_`** — **Data cleaning and merging.** Build the analytical dataset: decrypt raw data, translate variable names, concatenate yearly files, merge sources.
- **`2-XX.X_`** — **Descriptive output.** Produce descriptive graphs and tables (e.g., birth share trends by gender).
- **`3-XX.X_`** — **Analysis.** Run main econometric analyses (regression, DiD, IV, RDD, etc.).

Within each stage, files are numbered to indicate sequential order:
- `1-01.0_` → `1-01.1_` → `1-02.0_`
- The number after the dash (`01`, `02`, ...) groups related tasks; the decimal (`0`, `1`, ...) denotes sub-steps within that group.

### `code/temp/`

Experimental or exploratory scripts not yet part of the main pipeline. Use a **`temp_`** prefix for these files.

### `code/archive/`

Archived scripts no longer active in the pipeline.

---

## Outputs

### `outputs/figures/`

Output figures generated by `2-` and `3-` stage scripts (descriptive plots, event study graphs, etc.).

Naming convention mirrors the script that produced the file: `[stage]-[group].[step]_[description].png`
- e.g., `2-01.0_birth_share_trends.png`, `3-01.0_event_study.png`

### `outputs/tables/`

Output tables generated by `2-` and `3-` stage scripts (summary statistics, regression tables, etc.).

Naming convention mirrors the script that produced the file: `[stage]-[group].[step]_[description].tex`
- e.g., `2-01.0_summary_stats.tex`, `3-01.0_main_regression.tex`

---

## Quality Reports

### `quality_reports/referee_workspace/`

Reference material for referee work such as reviewing guidelines, example referee reports, and sample cover letters to editors. Keep reusable examples and templates here.

---

## What Goes in Git

- **Commit:** code, outputs (tables/figures), manuscript, tracked `quality_reports/` materials such as `plans/` and `referee_workspace/`, .Rproj
- **Do NOT commit:** data/raw/, data/clean/, data/temp/, data_dict/, literature/, quality_reports/session_logs/lab_journal.md, .Rhistory, .RData

---

## Lab Journal

`quality_reports/session_logs/lab_journal.md` (gitignored) is the **full permanent archive** of all session work. Claude appends to it at every session end with complete detail. It is NOT read at session start — the Recent Sessions block in this file serves that purpose. Only read the lab journal when the user asks or when something appears to be missing from context.
