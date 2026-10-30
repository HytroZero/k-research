---
name: decisive-test-design
description: Design the smallest informative experiment or analysis for a research decision, including comparisons, ablations, or tests of competing explanations. Produces a plan for an execution agent.
---

# Decisive Test Design

Design a test that helps decide whether to continue, revise, or stop investing in an idea.

## Process

1. **Name the decision.** State what the test should resolve: whether a method helps, whether an effect is useful, or which explanation fits.
2. **State expected outcomes.** For an empirical proposal, identify the expected improvement or observation relative to a relevant baseline. For a mechanistic or causal question, state the competing explanations and their differing predictions. For a theoretical claim, identify the proof obligation and useful analytical checks; simulations can guide the work but do not establish the theorem.
3. **Choose the smallest informative comparison.** Specify the method, dataset or setting, intervention, and baseline. Add ablations when they resolve a concrete attribution question.
4. **Make the comparison interpretable.** Address relevant confounds such as unequal compute, leakage, tuning budgets, or measurement noise. Choose controls according to the claim and scale of the test.
5. **Define measurements and decision rules.** Specify the main metric, aggregation, and what positive, null, or ambiguous results would imply. Include repeats or uncertainty estimates when needed to distinguish a useful effect from noise.
6. **Stage the work.** Separate the first cheap test from follow-up validation. State resource requirements; use measured resource data for numerical estimates.

## Output

Provide the decision question, expected outcome, test setup, baseline and necessary controls, measurements, and a result-to-decision table. Include a prediction matrix only when comparing explanations. Record unresolved issues only if they affect interpretation or the next action.

The execution handoff should contain enough detail to implement the first test, including data, configurations, and outputs to record. Report this as a planned experiment.

## Completion criterion

Plausible outcomes lead to clear next actions, and the setup can measure the proposed benefit or finding. When the goal is to distinguish mechanisms, the test must separate their predictions; when it is to evaluate a method, a fair comparison is sufficient.
