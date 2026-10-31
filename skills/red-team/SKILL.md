---
name: red-team
description: Adversarially review a research idea or hypothesis. Use when the user requests adversarial review or a concrete unresolved concern warrants deeper scrutiny.
---

# Research Red Team

Make the strongest evidence-based case against the candidate. Use this focused review after the candidate has been developed. Match objections to its contribution type using `docs/references/SCIENTIFIC-CLAIMS.md`.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Integrate objections and their resolution into the direction's `proposal.md`, `related-work.md`, or existing `evaluation-plan.md`, according to the subject. Record changed decisions in `research/decisions.md`; do not create a separate review report or an unrequested experiment plan.

## Process

1. **Read the full case.** Inspect the research question, hypothesis, mechanism, novelty audit, evidence, proposed tests, and project constraints. Read `GLOSSARY.md` and prior decisions.
2. **Steelman before attacking.** State the strongest version of the proposed contribution in a way its author would recognize. This prevents attacking a strawman.
3. **Attack the novelty claim.** Does prior work already supply the intended contribution? Assess what a component swap, prompt change, training recipe, or implementation change adds in capability, efficiency, or understanding; simplicity alone is not an objection.
4. **Examine the rationale.** Identify assumptions that could make the proposal ineffective. Examine causal links and competing mechanisms when a causal or mechanistic explanation is part of the contribution. Require a proof when the contribution asserts a theorem.
5. **Attack the evidence plan.** Check whether the proposed test measures the intended benefit or finding. Require discrimination between explanations when that is the research question. Look for confounds, leakage, weak baselines, unfair comparisons, proxy metrics, cherry-picking, underpowered tests, and missing controls.
6. **Attack scope and generalization.** Check whether the planned evaluation supports the intended scope. Prioritize mismatches that change the research decision.
7. **Attack practical and reproducibility assumptions.** Identify dependencies on inaccessible data, compute, proprietary systems, fragile infrastructure, or undocumented choices. Do not invent costs; state what needs estimation.
8. **Rank objections.** Use:
   - `fatal`: if true, invalidates the core contribution;
   - `major`: materially weakens the claim or likely changes the decision;
   - `repairable`: can be addressed by narrowing, adding evidence, or redesigning a test;
   - `minor`: affects clarity or completeness but not the core case.
9. **Turn each major objection into a probe.** State what evidence would confirm or dismiss it.

## Output

For each objection, provide:
- severity;
- the claim or assumption under attack;
- the strongest argument;
- supporting source or reasoning;
- what would happen if it is true;
- a concrete discriminating probe;
- whether it is currently resolved.

End with:
- strongest case for the idea;
- consequential objections found, if any;
- unresolved fatal/major objections;
- recommended action: `proceed`, `revise`, `defer`, or `reject`.

## Discipline

Be adversarial about the idea and fair to the evidence. Do not invent reviewer opinions or attribute claims to papers without checking them. Separate source-backed objections from speculative risks.

## Completion criterion

Every fatal and major objection is either supported, refuted, or explicitly unresolved with a proposed probe. Cosmetic comments do not crowd out threats to the central contribution.
