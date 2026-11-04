---
name: belief-update
description: Update a research project's hypotheses and decisions from new evidence. Use when new papers, experiment results, replications, counterexamples, or external reviews arrive and may change the current research direction.
---

# Research Belief Update

Integrate new evidence into the research state without rewriting history or overreacting to one result.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update the affected human documents and append meaningful judgment changes to `research/decisions.md`. Update optional structured state in place; do not save a separate update report.

## Process

1. **Identify the incoming evidence.** Record source, origin, timestamp, author/agent, artifact ID, and exact locator. For experiment results, require the execution agent's configuration, data version, code version, and measurement definition when available.
2. **Check provenance and integrity.** Distinguish raw observation, derived analysis, interpretation, and unverified report. If provenance is insufficient, mark the evidence provisional.
3. **Map affected claims and hypotheses.** Identify which predictions, assumptions, novelty claims, and decisions the evidence bears on. Include evidence that qualifies or does not address a claim.
4. **Compare against prior predictions.** State what the hypothesis predicted, what was observed, and whether the result was expected, surprising, ambiguous, or outside the tested scope.
5. **Check interpretation.** Investigate concrete confounds, measurement problems, or implementation differences that could change the decision. Compare mechanisms when the result bears on an explanatory claim.
6. **Update status.** Use `supported`, `weakened`, `rejected`, `revised`, or `unresolved` as appropriate. Status is qualitative and must be justified. Do not manufacture precise probabilities.
7. **Revisit downstream artifacts.** Mark affected opportunities, contribution claims, novelty judgments, test plans, and decisions as current, superseded, or requiring review.
8. **Choose the next decision.** Recommend continue, revise, run a discriminating follow-up, defer, or stop. Explain what evidence would change that recommendation.
9. **Record the change.** Update current artifacts and append meaningful changes of judgment, their evidence, and reasons to `research/decisions.md` using `templates/decision-record.md`. Follow the shared state contract; prior file copies are not required.

## Output

Include:
- incoming evidence and provenance;
- affected hypotheses and claims;
- prediction-versus-observation comparison;
- interpretation issues that affect the decision, if any;
- updated status and rationale;
- changed and unchanged conclusions;
- next recommended research decision;
- unresolved questions that determine the next action.

## Discipline

Tie the update to the observed result and tested conditions. If measurement noise, leakage, or an unfair comparison affects interpretation, identify the issue and the follow-up needed to resolve it.

## Completion criterion

The new evidence is traceably connected to the claims it affects, the reason for every status change is recorded, and previous decisions remain readable in `research/decisions.md`.
