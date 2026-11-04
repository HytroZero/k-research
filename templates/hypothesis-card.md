> Placement: Update `research/directions/<direction-name>/proposal.md`. Integrate supporting hypotheses into that direction's proposal rather than creating separate cards. See [Project Layout](../docs/PROJECT-LAYOUT.md). This placement note is a template instruction, not output content.

# Direction Proposal

- Direction / Hypothesis ID:
- Status: candidate / under_review / testable / supported / weakened / rejected / revised / deferred
- Review status: unreviewed / subagent_parallel / sequential_fallback / skipped_by_user / incomplete

## Problem and setting

Describe the task, specific difficulty or questioned assumption, and consequence. Explain what known approaches leave unresolved, with supporting sources or observations.

## Proposed method

Describe inputs, outputs, and key steps. Define the central operation or objective concretely; when a core step has materially different realizations, state the minimal clean realization and any key design alternative.

## Design rationale

Connect each key design choice to the difficulty it addresses and explain why it should help. After review, explain consequential revisions and the reasons for retaining choices challenged by important objections.

## Worked example

Trace a small concrete instance through the current approach and the proposal, showing where their behavior diverges and what design question the trace exposes.

## Closest known work and difference

Explain shared components, the actual difference, and why it matters. Link sources and `related-work.md` when a novelty audit or detailed comparison exists.

## Expected outcome and contribution

State the useful change in task behavior, efficiency, simplification, or understanding that success would add.

## Feasibility, open objections, and next question

Identify essential data, model access, or compute requirements, any remaining fatal or major objections (with the probe or check that would resolve them), and the next issue to settle in the problem or method. Disclose any skipped or fallback review mode.

## Optional follow-on analysis

Include mechanism, assumptions, competing explanations, or theory when they carry the contribution. Link `evaluation-plan.md` when validation is requested or underway.
