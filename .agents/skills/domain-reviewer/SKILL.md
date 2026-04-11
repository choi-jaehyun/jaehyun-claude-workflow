---
name: domain-reviewer
description: Substantive referee-style review for empirical economics manuscripts, slides, lecture notes, assignments, and similar academic documents. Use when Codex should stress-test identification, derivations, citations, code-theory alignment, or overall logic without editing the source file.
---

# Domain Reviewer

Use this skill when the job is substantive correctness rather than prose polish. Think like a careful top-field referee: fair, precise, and skeptical about identification and inference.

## Workflow

1. Resolve the target document and infer the document type.
2. If the project includes supporting code, tables, figures, bibliography files, or PDFs in `literature/`, use them to verify claims rather than relying on the prose alone.
3. Read [references/review-lenses.md](references/review-lenses.md) and apply the five review lenses in order.
4. Save a structured report to `quality_reports/[filename_without_ext]_substance_review.md`.
5. Do not edit the source document while using this skill.

## Working style

- Focus on identification, estimands, derivations, citation fidelity, and code-theory alignment.
- For long PDFs in `literature/`, read the abstract or introduction first and then only the targeted pages needed to verify a claim.
- Be stricter with manuscripts than with teaching materials. Flag simplifications only when they become misleading.
- Quote exact sections, equations, page numbers, or code locations when raising an issue.

## Use the full checklist

The detailed review protocol, common misattributions, package-specific pitfalls, and report template live in [references/review-lenses.md](references/review-lenses.md).
