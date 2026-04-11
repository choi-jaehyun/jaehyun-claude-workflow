# Domain Review Reference

## Map

- Identification and assumptions
- Derivation and estimation
- Citation fidelity
- Code-theory alignment
- Backward logic
- Cross-document consistency
- Report template
- Severity rules

## Identification and assumptions

### General

- Define the estimand clearly: ATE, ATT, LATE, CATE, or something else.
- Name the identification strategy explicitly and explain why it is appropriate.
- State assumptions before drawing the causal conclusion that depends on them.
- Check whether the institutional setting makes the assumptions plausible.
- Note serious threats to identification, not just favorable interpretations.

### Difference-in-differences

- Check whether parallel trends is stated, motivated, and supported with pre-trend evidence where possible.
- Check for no-anticipation concerns.
- If timing is staggered, ask whether TWFE negative-weight problems or contamination issues are addressed.
- Ask whether treatment-effect heterogeneity is compatible with the estimator.
- Check whether changing panel composition biases comparisons.
- Ask whether spillovers or SUTVA violations are plausible.

### Instrumental variables

- Check instrument relevance and whether the first stage is reported clearly.
- Ask whether the exclusion restriction is argued from institutional knowledge rather than asserted.
- For LATE claims, assess whether monotonicity is plausible.
- If there are multiple instruments, look for an overidentification discussion.
- Ask who the compliers are and whether that population supports the policy claim being made.

### Regression discontinuity

- Check for manipulation tests on the running variable.
- Ask whether continuity of potential outcomes at the cutoff is argued, not merely assumed.
- Note the bandwidth selection rule and whether alternative bandwidths are reported.
- Flag high-order polynomial specifications unless strongly justified.
- Look for covariate balance near the cutoff.
- If compliance is imperfect, confirm the design is treated as fuzzy RD rather than sharp RD.

### Synthetic control and matching

- Check pre-treatment fit on outcomes and covariates.
- Ask whether the donor pool is free of treated or contaminated units.
- Look for placebo or permutation inference for synthetic control.
- For matching, verify balance and overlap.
- For selection-on-observables arguments, ask whether unconfoundedness is defended with context.

### Event studies

- Check the reference period and whether it is clearly stated.
- Examine pre-treatment coefficients jointly, not just one by one.
- Note endpoint binning and whether the interpretation is still valid.
- In staggered designs, consider Sun-Abraham-style contamination issues.

## Derivation and estimation

### Algebra and decompositions

- Verify each equals sign in multi-step derivations.
- Check whether decomposition pieces actually sum to the whole.
- Verify conditioning events, indicators, expectations, sums, and integrals.
- For matrix formulas, confirm dimensions match.
- For IV, verify the Wald ratio interpretation carefully.

### TWFE and DiD decompositions

- If Goodman-Bacon is cited, confirm the decomposition is described correctly.
- Ask whether negative weights are possible and, if so, whether the document acknowledges them.
- When alternative estimators are used, make sure the estimand is stated precisely.

### Standard errors and inference

- Check whether clustering matches the level of treatment assignment.
- If the number of clusters is small, look for small-sample corrections or bootstrap methods.
- Ask whether spatial correlation could invalidate simple clustered standard errors.
- If there are many outcomes or subgroup analyses, consider multiple-testing concerns.
- Note when specification search may have created pre-test bias.

### Common estimation pitfalls

- Logging zero outcomes changes the estimand; note whether the text acknowledges that.
- Flag bad controls, especially post-treatment controls.
- Flag potential collider adjustments.
- Ask what estimand weighting choices imply.
- Check whether fixed effects versus first differences is justified.
- Note incidental-parameters concerns in short panels with many fixed effects.

## Citation fidelity

- Verify that a cited paper actually supports the claim made in the text.
- Check that the result is attributed to the correct paper.
- Check theorem, proposition, or equation numbers if the document cites them.
- When a `literature/` directory exists, read the actual paper rather than relying only on memory.

### Commonly misattributed results

| Claim | Correct source or clarification |
| --- | --- |
| LATE or local average treatment effect | Imbens and Angrist (1994) |
| Parallel trends is testable from pre-trends | Parallel trends itself is untestable; pre-trends are only suggestive |
| TWFE negative weights in staggered DiD | de Chaisemartin and D'Haultfoeuille (2020); Goodman-Bacon (2021) for decomposition |
| Robust staggered DiD estimators | Callaway and Sant'Anna (2021); Sun and Abraham (2021); Borusyak, Jaravel, and Spiess (2024) |
| Wild cluster bootstrap | Cameron, Gelbach, and Miller (2008) |
| RDD bandwidth selection | Imbens and Kalyanaraman (2012); Calonico, Cattaneo, and Titiunik (2014) |
| Synthetic control | Abadie and Gardeazabal (2003) for the method; Abadie, Diamond, and Hainmueller (2010) for inference |
| Propensity score | Rosenbaum and Rubin (1983) |
| FWL or regression anatomy | Frisch-Waugh-Lovell theorem; Angrist and Pischke for the teaching interpretation |
| Clustering guidance | Abadie, Athey, Imbens, and Wooldridge (2023); Cameron and Miller (2015) |
| Log-of-zero concerns | Chen and Roth (2024); Mullahy and Norton (2024) |
| Bartik or shift-share decomposition | Goldsmith-Pinkham, Sorkin, and Swift (2020) for shares; Borusyak, Hull, and Jaravel (2022) for shocks |
| Weak-IV thresholds | Stock and Yogo (2005) and newer weak-IV guidance such as Lee, McCrary, Moreira, and Porter (2022) |

## Code-theory alignment

### General

- Check that the code implements the exact specification described in the document.
- Verify that sample restrictions in the text match the code.
- Verify that variable definitions in code match the theory and tables.
- Check whether the standard error method in code matches the written description.
- Make sure the reported sample sizes can be traced back to the code.

### Known package pitfalls

#### `fixest`

- `feols()` can drop singleton fixed-effect groups silently.
- Default clustering behavior may not match the text.
- Check `i()` reference categories carefully.
- Distinguish absorbed effects from estimated effects.

#### `rdrobust`

- The bandwidth is often data-driven; report what was used.
- Bias-corrected confidence intervals differ from conventional ones.
- Clustering must be set explicitly.

#### `estimatr`

- Confirm the clustering variable matches the paper.
- Confirm which HC correction is actually used.

#### `data.table`

- Check joins for unintended row-count changes.
- Check grouped `:=` calls for the intended level of aggregation.
- Watch for type coercion on keyed merges.

#### Base R and modeling defaults

- `lm()` and `glm()` can silently drop observations with missing values.
- Weights should be applied through model arguments rather than ad hoc pre-processing unless justified.
- Random procedures need a visible `set.seed()`.

## Backward logic

- Start from the conclusion or policy recommendation and trace it backward to the causal estimate.
- Then trace the estimate back to the identification strategy.
- Then trace the identification strategy back to the assumptions.
- Ask whether external-validity claims exceed the estimand.
- Look for circular reasoning where the result is used to justify the assumption.

### Common logic gaps

- Claiming ATE when the design only identifies ATT or LATE.
- Making broad policy claims that require external validity not established by the design.
- Treating robustness to observed controls as if it solved omitted-variable bias entirely.
- Treating individually insignificant pre-trends as proof of parallel trends.
- Interpreting a null estimate as no effect without discussing power or detectable effect sizes.

## Cross-document consistency

- Use consistent notation across the project.
- Check that references to tables, figures, and appendices match the actual artifacts.
- Check that the same term keeps the same meaning across documents.
- Check that text variable names match code variable names where the mapping is meant to be direct.
- Check sample sizes and descriptive statements against outputs when available.

## Report template

Use this structure for the saved report:

```markdown
# Substance Review: [Filename]
**Date:** [YYYY-MM-DD]
**Reviewer:** domain-reviewer skill
**Document type:** [manuscript / slides / lecture notes / assignment / other]

## Summary
- **Overall assessment:** [SOUND / MINOR ISSUES / MAJOR ISSUES / CRITICAL ERRORS]
- **Total issues:** N
- **Blocking issues:** M
- **Non-blocking issues:** K

## Lens 1: Identification and assumptions
### Issues found: N
#### Issue 1.1: [Brief title]
- **Location:** [section / page / slide / equation]
- **Severity:** [CRITICAL / MAJOR / MINOR]
- **Claim in document:** [exact text or equation]
- **Problem:** [what is missing or wrong]
- **Suggested fix:** [specific correction]

## Lens 2: Derivation and estimation
[Repeat]

## Lens 3: Citation fidelity
[Repeat]

## Lens 4: Code-theory alignment
[Repeat]

## Lens 5: Backward logic
[Repeat]

## Cross-document consistency
[Findings]

## Critical recommendations
1. [Most important fix]
2. [Second priority]

## Positive findings
- [What the document gets right]
- [What the document gets right]
```

## Severity rules

- `CRITICAL`: the identification argument, derivation, or estimand is wrong in a way that could invalidate the core claim.
- `MAJOR`: an assumption, citation, inference, or alignment issue materially weakens the result.
- `MINOR`: the statement should be sharpened, qualified, or documented better but is not fatally wrong.

Always report, never edit, while using this skill.
