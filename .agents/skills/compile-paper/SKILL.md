---
name: compile-paper
description: Compile the LaTeX manuscript. Runs latexmk, or a multi-pass pdflatex plus biber fallback, from the project root and reports errors, warnings, and undefined references.
disable-model-invocation: true
argument-hint: "[optional: path to main.tex]"
---

# Compile LaTeX Manuscript

Compile the LaTeX paper and report any issues.

## Steps

1. **Locate the manuscript:**
   - If `$ARGUMENTS` specifies a file: use that
   - Otherwise: use `manuscript/main.tex`

2. **Compile from the project root using latexmk** (preferred):
   ```bash
   latexmk -pdf -interaction=nonstopmode manuscript/main.tex
   ```
   If latexmk is not available, use multi-pass compilation:
   ```powershell
   Push-Location manuscript
   pdflatex -interaction=nonstopmode main.tex
   biber main
   pdflatex -interaction=nonstopmode main.tex
   pdflatex -interaction=nonstopmode main.tex
   Pop-Location
   ```

3. **Follow the local verifier protocol** in `.agents/skills/verifier/SKILL.md`:
   - Report compilation errors
   - Count overfull hbox warnings
   - Report undefined citations or references
   - Report missing files or packages

4. **Verify output:**
   - Confirm `manuscript/main.pdf` was generated
   - Report file size

5. **Report results** to the user:
   - PASS or FAIL with details
   - Count of warnings by type
   - Any undefined references listed
