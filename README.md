# jaehyun-claude-workflow

A template repository for AI-assisted empirical research and teaching workflows.
It started as a Claude Code workflow, and it now also includes a Codex-native skill tree in `.agents/skills` while preserving the original `.claude` material.

*Credits* -- I started with Coady Wing's workflow. Coady started from Pedro H. C. Sant'Anna's workflow and then added and changed things from there. You can find that setup here: [pedrohcgs/claude-code-my-workflow](https://github.com/pedrohcgs/claude-code-my-workflow).

---

## What this repo includes

| Component | Purpose |
| --- | --- |
| `AGENTS.md` | Codex-facing project guide and short session memory |
| `CLAUDE.md` | Claude-facing project guide kept for compatibility |
| `.agents/skills/` | Codex-native skills for review, verification, workflow, and project conventions |
| `.claude/agents/` | Original Claude agent specs preserved as source material |
| `.claude/rules/` | Original Claude rules preserved as source material |
| `quality_reports/` | Plans, referee-writing references, review outputs, and session logs |
| `code/`, `manuscript/`, `outputs/`, `slides/` | Research and teaching project skeleton |

---

## Current skill layout

### Codex-native skills in `.agents/skills`

- `compile-paper`
- `devils-advocate`
- `domain-reviewer`
- `proofread`
- `proofreader`
- `r-code-conventions`
- `r-reviewer`
- `review-paper`
- `review-r`
- `run-pipeline`
- `split-pdf`
- `validate-bib`
- `verifier`
- `workflow`

### Preserved Claude source material in `.claude`

- `agents/domain-reviewer.md`
- `agents/proofreader.md`
- `agents/r-reviewer.md`
- `agents/verifier.md`
- `rules/r-code-conventions.md`
- `rules/workflow.md`

The intended setup is:

- Keep `.claude/` intact as the original source library
- Use `.agents/skills/` as the active Codex skill layer
- Customize `AGENTS.md` for project-specific context

---

## What the main skills do

| Skill | Purpose |
| --- | --- |
| `/compile-paper` | Compile the LaTeX manuscript and report errors and warnings |
| `/run-pipeline` | Run `main.r` or a target R script and verify outputs |
| `/proofread [file]` | Writing quality review for papers, slides, notes, and docs |
| `/review-r [file]` | Report-only review of R code quality and reproducibility |
| `/review-paper [file]` | Substantive manuscript review with referee-style concerns |
| `/validate-bib` | Cross-check citations against bibliography entries |
| `/devils-advocate [file]` | Challenge pedagogy, ordering, notation, and cognitive load |
| `/split-pdf [path or query]` | Deep-read academic PDFs in smaller chunks |

---

## Workflow model

The current repo workflow is:

1. Store project context in `AGENTS.md`
2. Use Codex skills from `.agents/skills`
3. Keep `.claude/` as preserved upstream logic and source material
4. Save plans and review outputs under `quality_reports/`
5. Append detailed session history to `quality_reports/session_logs/lab_journal.md`

For substantial work, the intended loop is:

```text
PLAN -> IMPLEMENT -> VERIFY -> REVIEW -> FIX -> RE-VERIFY
```

The main supporting skills for that loop are:

- `workflow`
- `verifier`
- `proofreader`
- `r-reviewer`
- `domain-reviewer`

## Quality reports layout

- `quality_reports/plans/` stores short saved plans for substantial work.
- `quality_reports/referee_workspace/` stores tracked reference material for referee reports, editor cover letters, and reviewing guidelines.
- `quality_reports/session_logs/lab_journal.md` is the full gitignored session archive and should stay local.

---

## Prerequisites

- Git
- R
- LaTeX distribution
- Quarto
- An AI coding environment that can use this repo structure

Helpful but optional:

- GitHub CLI (`gh`)
- RStudio for `.Rproj`-anchored `here()` paths

---

## Getting started

### 1. Create a new project from the template

Use the GitHub template UI, or:

```bash
gh repo create my-new-project --template choi-jaehyun/jaehyun-claude-workflow --private --clone
cd my-new-project
```

### 2. Open the project correctly

To keep `here()` anchored to the project root:

- In RStudio, open the `.Rproj` file
- In VS Code, open the project folder itself

### 3. Customize the project guides

At minimum, update:

- `AGENTS.md`
- `CLAUDE.md` if you still plan to use Claude-facing project guidance

Fill in:

- project name
- project overview
- immediate plans
- any project-specific structure notes

### 4. Put your data and documents in place

Typical locations:

- `data/raw/` for raw data
- `manuscript/` for LaTeX papers
- `slides/` for teaching decks
- `literature/` for reference PDFs

### 5. Start working with the repo

Use your AI coding tool of choice and point it at:

- `AGENTS.md` for current project instructions
- `.agents/skills/` for Codex-native skill behavior
- `.claude/` only when you want to inspect the original Claude-side source material

---

## Project structure

```text
project/
|-- AGENTS.md
|-- CLAUDE.md
|-- .agents/
|   `-- skills/
|-- .claude/
|   |-- agents/
|   `-- rules/
|-- code/
|-- data/
|   |-- raw/
|   |-- clean/
|   `-- temp/
|-- data_dict/
|-- literature/
|-- manuscript/
|-- outputs/
|   |-- figures/
|   `-- tables/
|-- quality_reports/
|   |-- plans/
|   |-- referee_workspace/
|   `-- session_logs/
|-- slides/
|-- README.md
`-- *.Rproj
```

---

## Coding conventions summary

- Use `data.table` for core data manipulation
- Use `here()` for paths
- Avoid `setwd()` and absolute machine-specific paths
- Prefer explicit code over premature abstraction
- Use `message()` rather than noisy console printing
- Use snake_case naming
- Save figures explicitly with `ggsave()` dimensions

The active Codex-facing reference for R standards is:

- `.agents/skills/r-code-conventions/references/r-standards.md`

The original Claude rule is preserved at:

- `.claude/rules/r-code-conventions.md`

---

## Notes

- `.claude/` should be treated as preserved source material unless you intentionally want to revise the upstream Claude setup.
- `.agents/skills/` is now the main place for Codex skill behavior.
- `AGENTS.md` is the preferred short session-memory file for Codex in this repo.
- `quality_reports/referee_workspace/` is for reusable referee-writing examples and guidance, while `lab_journal.md` remains a local-only working log.
