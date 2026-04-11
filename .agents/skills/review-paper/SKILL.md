---
name: review-paper
description: Comprehensive manuscript review covering identification strategy, econometric specification, citation fidelity, and potential referee objections. Uses the local `$domain-reviewer` skill plus a short synthesis pass.
disable-model-invocation: true
argument-hint: "[paper filename or path to .tex/.pdf]"
allowed-tools: ["Read", "Grep", "Glob", "Write", "Task"]
---

# Manuscript Review

Produce a thorough, constructive review of an academic manuscript - the kind of report a top-journal referee would write.

**Input:** `$ARGUMENTS` - path to a paper (`.tex`, `.pdf`, or `.qmd`).

## Steps

1. **Locate and read the manuscript.** Check:
   - Direct path from `$ARGUMENTS`
   - The `manuscript/` directory
   - Partial matches if needed

2. **Run the local substantive review skill:**
   - Read `.agents/skills/domain-reviewer/SKILL.md`
   - Follow its five-lens protocol for identification, derivation, citation fidelity, code-theory alignment, and backward logic
   - Save the substantive report to `quality_reports/[filename_without_ext]_substance_review.md`

3. **Supplement that review** with these additional checks:
   - Writing quality: clarity, concision, tone, abstract quality, and whether tables or figures are self-contained
   - Literature positioning: whether the key papers are cited, characterized accurately, and clearly distinguished from the current contribution

4. **Generate 3-5 referee objections** - the tough questions a top referee would ask.

5. **Produce the combined review report** and save it to `quality_reports/paper_review_[sanitized_name].md`

## Output format

```markdown
# Manuscript Review: [Paper Title]

**Date:** [YYYY-MM-DD]
**File:** [path to manuscript]

## Summary assessment

**Overall recommendation:** [Strong Accept / Accept / Revise and Resubmit / Reject]

[2-3 paragraph summary: main contribution, strengths, and key concerns]

## Strengths

1. [Strength 1]
2. [Strength 2]

## Major concerns

### MC1: [Title]
- **Dimension:** [Identification / Econometrics / Argument / Literature / Writing]
- **Issue:** [Specific description]
- **Suggestion:** [How to address it]

## Minor concerns

### mc1: [Title]
- **Issue:** [Description]
- **Suggestion:** [Fix]

## Referee objections

### RO1: [Question]
**Why it matters:** [Why this could be fatal]
**How to address it:** [Suggested response or additional analysis]
```

## Principles

- **Be constructive.** Every criticism should come with a suggestion.
- **Be specific.** Reference exact sections, equations, and tables.
- **Think like a referee at a top-5 journal.**
- **Distinguish fatal flaws from minor issues.**
- **Acknowledge what is done well.**
