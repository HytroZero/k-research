> Placement: Update `research/directions/<direction-name>/evaluation-plan.md` and link it from `proposal.md` (or from `research/overview.md` for a standalone diagnostic study). Create this file only when experiments or a full research plan are requested, or when a developed method enters validation. See [Project Layout](../docs/PROJECT-LAYOUT.md). This placement note is a template instruction, not output content.

# Evaluation Plan

- Direction / Hypothesis ID:
- Status: planned / in_progress / completed / revised

## Decision question and expected outcome

State what this test resolves—whether the proposed method helps, whether an effect is useful, or which explanation holds—and the expected observation or proof obligation.

## Minimal test setup

Specify the smallest informative experiment or analysis first: dataset or setting, intervention or method configuration, and baseline. Add ablations or follow-up stages only when they resolve a specific attribution or scaling question.

## Controls and interpretability

State how the comparison controls for confounds that could change the conclusion, such as compute, parameter count, tuning budget, data leakage, or measurement noise.

## Measurements and decision rules

Define the primary metric, aggregation, and uncertainty or repeat requirements. Map plausible outcomes to the next research decision:

| Observed outcome | Interpretation | Next decision (`continue` / `revise` / `defer` / `stop`) |
|---|---|---|

## Competing explanations (optional)

Include a prediction matrix only when the test is designed to separate competing mechanisms or explanations.

| Explanation | Predicted pattern | Discriminating condition |
|---|---|---|

## Execution handoff

Provide the concrete details an execution agent needs to run the first test: data or environment source, configurations to compare, resource requirements, and exact outputs and locators to return for `belief-update`. Note any unresolved setup issue that affects interpretation.
