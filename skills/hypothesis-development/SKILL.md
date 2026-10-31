---
name: hypothesis-development
description: Develop a research opportunity into a concrete method, explaining how its design addresses the problem and differs from known approaches.
---

# Hypothesis Development

Develop an idea far enough that the researcher can understand and judge the proposed solution. Read `docs/references/SCIENTIFIC-CLAIMS.md` for the evidence standard appropriate to its contribution type.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update `research/directions/<direction-name>/proposal.md` using the hypothesis-card template. Link the direction from `research/overview.md`.

## Process

1. **Define the problem and core tension.** Describe the task, setting, specific difficulty or questioned assumption, and why the closest known approaches leave it unresolved.
2. **Design from first principles first.** Before adding constraints to avoid prior work, ask what the cleanest, most direct mechanism for resolving the difficulty would be. Prefer a sharp core idea or simplification over a defensive patchwork of existing components.
3. **Specify the method.** Explain inputs, outputs, and the key operations that change the current approach. Define the central algorithm, objective, or construction concretely enough to see how it works; a label or an unspecified scoring function is not a method. When the core idea admits materially different realizations, give the minimal clean instantiation first and note the main design alternative rather than locking in arbitrary boilerplate early.
4. **Connect design to difficulty.** Explain which part of the problem each key design choice addresses and why it should help. Keep every moving part earning its keep; drop components that exist only to look different from prior papers.
5. **Work through an example.** Trace a small concrete instance through the current approach and the proposal, showing step by step where their behavior diverges and what design question the trace exposes.
6. **Position against known neighbors.** Compare the formed design against neighboring literature to identify shared building blocks and actual differences. If a neighbor already solves the problem cleanly, either reframe the problem, find a genuinely simpler or stronger mechanism, or set the candidate aside—do not bolt on incidental complexity just to claim novelty. Request focused `novelty-audit` work once the candidate is concrete.
7. **State the expected contribution and feasibility.** Explain the capability, efficiency, simplification, measurement, or understanding success would add. Identify essential data, model access, or resource requirements and the main open design question.

For a theoretical contribution, specify the proposition, assumptions, and proof approach. For a mechanistic or causal contribution, articulate the explanation and relevant alternatives. Detailed validation belongs to `decisive-test-design` when the task advances to experiment planning.

## Output

Use `templates/hypothesis-card.md`. Center the output on the problem, method, design rationale, worked example, and difference from known approaches. Write the method and worked example directly without repetitive sentence-level disclaimers that the proposal is untested; the artifact status already marks it as a proposal.

## Completion criterion

A reader can trace the method's key steps through the example, connect its design choices to the stated difficulty, and explain the potential contribution relative to known work. An unresolved core algorithm should be identified as the next design task rather than hidden behind boilerplate formulas or an experiment plan.
