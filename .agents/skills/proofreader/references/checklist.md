# Proofreading Reference

## Map

- Document handling
- Core issue categories
- Citation and notation consistency
- Report template

## Document handling

- `.tex`: read directly; watch for overfull hbox risk, citation command misuse, and LaTeX formatting issues.
- `.qmd`: read directly; for slides, watch for slide overflow, dense layouts, and render-sensitive syntax.
- `.md`: read directly; check headings, lists, links, and citation syntax if present.
- `.pdf`: read directly; if the file is long, review it in chunks rather than all at once.
- `.docx`: if a DOCX skill or extractor is available, use it. Otherwise review a PDF export or the extractable text only, and note the limitation.

## Core issue categories

### Grammar

- Subject-verb agreement
- Missing or incorrect articles
- Wrong prepositions
- Tense inconsistency
- Dangling modifiers
- Missing words that leave a sentence incomplete

### Typos

- Misspellings
- Search-and-replace artifacts
- Duplicated words
- Missing punctuation
- Extra punctuation

### Overflow and formatting

- In LaTeX, flag lines, equations, tables, or captions likely to trigger overfull boxes.
- In Quarto slides, flag material likely to overflow the slide or require impractically small fonts.
- In Word or PDF exports, flag obvious heading, spacing, or formatting inconsistencies visible in the rendered text.
- In general, flag tables or figures that look too wide for the page.

### Consistency

- Check notation: one symbol should not mean two different things.
- Check terminology: the same concept should not be renamed casually across sections.
- Check formatting: headings, boldface, italics, and list styles should be applied consistently.
- Check citation syntax consistency within the document's format.

### Academic quality

- Flag informal contractions and colloquial phrasing in formal academic writing.
- Flag unsupported claims that need citations.
- Flag awkward or ambiguous phrasing.
- Check whether citation keys appear to exist in the bibliography source when that file is available.

## Citation and notation consistency

### LaTeX with natbib

- `\citet{key}` for textual citations
- `\citep{key}` for parenthetical citations
- `\citeauthor{key}` and `\citeyear{key}` when needed

Red flags:

- Mixing natbib and biblatex commands in the same document
- Using textual versus parenthetical citations inconsistently in very similar sentence structures

### LaTeX with biblatex

- `\textcite{key}` for textual citations
- `\parencite{key}` for parenthetical citations
- `\autocite{key}` only if the style choice is intentional

### Quarto or Pandoc markdown

- `@key` for textual use
- `[@key]` for parenthetical use
- `[-@key]` to suppress the author name
- `[@key1; @key2]` for multiple citations

## Report template

```markdown
# Proofread Report: [Filename]
**Date:** [YYYY-MM-DD]
**Reviewer:** proofreader skill

### Issue N: [Brief description]
- **File:** [filename]
- **Location:** [section / slide / line]
- **Current:** "[exact text]"
- **Proposed:** "[corrected text]"
- **Category:** [Grammar / Typo / Overflow / Consistency / Academic Quality]
- **Severity:** [High / Medium / Low]
```

Save the report to `quality_reports/[filename_without_ext]_proofread_report.md`.
