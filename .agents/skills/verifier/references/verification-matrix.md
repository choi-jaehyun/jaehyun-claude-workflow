# Verification Matrix

## Map

- R scripts
- LaTeX manuscripts
- Quarto documents
- Bibliography checks
- Full pipeline checks
- Report template

## R scripts

Run the target script directly:

```powershell
Rscript path\to\script.r
```

Check:

- exit code
- warnings or errors in stdout and stderr
- whether expected output files were created
- whether output files have non-zero size

If the project uses `code/main.r`, consider a full-pipeline run when the change affects multiple stages.

## LaTeX manuscripts

Preferred command from the project root:

```powershell
latexmk -pdf -interaction=nonstopmode manuscript/main.tex
```

Fallback if `latexmk` is unavailable:

```powershell
Push-Location manuscript
pdflatex -interaction=nonstopmode main.tex
biber main
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
Pop-Location
```

Check:

- exit code
- overfull hbox warnings
- undefined citations or references
- missing files or packages
- whether `manuscript/main.pdf` exists and has non-zero size

## Quarto documents

```powershell
quarto render path\to\file.qmd
```

Check:

- exit code
- render warnings
- expected HTML, PDF, or revealjs output exists
- output file size is non-zero

## Bibliography checks

For changed `.bib` files or manuscript sources:

- collect citation keys used in the changed `.tex`, `.qmd`, or `.md` files
- confirm those keys exist in the bibliography file
- flag unused bibliography entries only if the task calls for a cleanup pass

## Full pipeline checks

Use this when the user requests end-to-end verification or when the change affects multiple pipeline stages:

```powershell
Rscript code/main.r
```

Check:

- exit code
- warnings and errors
- expected outputs under `outputs/tables/`, `outputs/figures/`, and any required intermediate directories
- non-zero file size for key artifacts

## Report template

```markdown
## Verification Report

### [filename]
- **Command:** [what was run]
- **Exit code:** [0 = pass, nonzero = fail]
- **Warnings:** [count and summary]
- **Output exists:** Yes / No
- **Output size:** [size]

### Summary
- Total files checked: N
- Passed: N
- Failed: N
- Warnings: N
```

## Rules

- Run commands from the directory they expect.
- Report all warnings, even if the build technically succeeds.
- Do not claim a pass without evidence that the expected artifact exists.
