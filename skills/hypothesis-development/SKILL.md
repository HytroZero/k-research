---
name: hypothesis-development
description: Develop a research opportunity into a concrete method, explaining how its design addresses the problem and differs from known approaches.
---

# Hypothesis Development

Develop an idea far enough that the researcher can understand and judge the proposed solution. Read `docs/references/SCIENTIFIC-CLAIMS.md` for the evidence standard appropriate to its contribution type.

## Process

1. **Define the problem.** Describe the task, setting, specific difficulty, and consequence. Explain why the closest known approaches leave this difficulty unresolved, with sources or observations supporting that account.
2. **Specify the method.** Explain inputs, outputs, and the key operations that change the current approach. Define the central algorithm, objective, or construction sufficiently to understand how it works; a name or an unspecified scoring function is not a concrete method.
3. **Connect design to difficulty.** Explain which part of the problem each key design choice addresses and why it could help. Develop theory or a causal mechanism when that is the intended contribution; practical design reasoning can support an empirical proposal.
4. **Work through an example.** Carry a small task instance through the current approach and the proposal, showing where their behavior differs. Mark constructed examples as illustrative rather than observed evidence.
5. **Compare known neighbors.** Use existing literature throughout development to identify shared components, actual differences, and remaining gaps in the proposal. Request focused `novelty-audit` work when the candidate is concrete enough to compare.
6. **State the expected contribution and feasibility.** Explain the capability, efficiency, measurement, or understanding success would add. Identify essential data, model access, or resource requirements and unresolved design choices. Keep expected outcomes distinct from results.

For a theoretical contribution, specify the proposition, assumptions, and proof approach. For a mechanistic or causal contribution, articulate the explanation and relevant alternatives. Detailed validation belongs to `decisive-test-design` when the task advances to experiment planning.

## Output

Use `templates/hypothesis-card.md`. Center the output on the problem, method, design rationale, worked example, and difference from known approaches. Describe the expected outcome in terms of the task; measurement protocols and a first experiment are optional follow-on artifacts.

## Completion criterion

A reader can trace the method's key steps through the example, connect its design choices to the stated difficulty, and explain the potential contribution relative to known work. An unresolved core algorithm should be identified as the next design task rather than hidden behind an experiment plan.
