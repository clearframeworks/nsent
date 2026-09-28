# NSENT Methodology

## Purpose
NSENT is a hypothesis-comparison aid. It is not a detector of truth, motive, conspiracy, wrongdoing, or causation.

## Conceptual model
The original heuristic is represented as:

`Likely Explanation = f(Observed Behavior, Incentives, Constraints, Capability, Timing, Distribution of Benefits/Costs, Evidence)`

The comparison layer borrows the logic of Bayesian hypothesis testing: explanations should gain support when the observed evidence would be more expected under that explanation than under its competitors.

The static implementation cannot infer semantic likelihoods reliably without a language model. It therefore uses a transparent deterministic proxy:

`Support(H) = .28 Evidence + .16 Context + .13 Incentive + .13 Capability + .10 Constraints + .10 Timing + .10 Distribution`

Each component is lexical similarity between a supplied hypothesis and the relevant user input. Scores are normalized across the supplied hypotheses.

## Critical interpretation rule
A displayed 60% means roughly "60% of the support allocated among the explanations supplied to this tool under this scoring model." It does NOT mean there is a 60% real-world probability that the explanation is true.

## Recommended production evolution
1. Preserve the current input schema and interface.
2. Replace lexical extraction with a structured-output language-model adapter.
3. Require the model to return evidence-for, evidence-against, assumptions, missing information, and likelihood ratios for every hypothesis.
4. Keep the deterministic normalization/calculation outside the model.
5. Show provenance for every scored claim.
6. Add sensitivity analysis: show how results change when assumptions or weights change.
7. Add a required null/baseline explanation to reduce motivated reasoning.
