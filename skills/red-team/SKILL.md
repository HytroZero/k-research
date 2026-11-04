---
name: red-team
description: Adversarially review a research idea or hypothesis. Use during method-development review, when the user requests adversarial review, or when a concrete unresolved concern warrants deeper scrutiny.
---

# Research Red Team

Make the strongest evidence-based case against the candidate. Use this focused review after the candidate has been developed. Match objections to its contribution type using `docs/references/SCIENTIFIC-CLAIMS.md`.

## Project files

When delegated as a reviewer by `hypothesis-development`, return findings to the parent without writing project files or invoking method development or further review agents. Report missing inputs for the parent to resolve. The parent owns integration. For standalone use, follow the destinations below.

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Integrate objections and their resolution into the direction's `proposal.md`, `related-work.md`, or existing `evaluation-plan.md`, according to the subject. Record changed decisions in `research/decisions.md`; do not create a separate review report or an unrequested experiment plan.

## Process

1. **Read the full case.** Inspect the research question, hypothesis, mechanism, project constraints, and any available novelty audit, evidence, or proposed tests. During parallel method review, work from the shared proposal without waiting for the other reviewer’s audit. Read `GLOSSARY.md` and prior decisions.
2. **Steelman before attacking.** State the strongest version of the proposed contribution in a way its author would recognize. This prevents attacking a strawman.
3. **Check contribution assumptions.** In parallel method review, leave systematic closest-work search to the novelty reviewer; flag known overlap with sources when it affects the rationale. In standalone review, examine the novelty claim directly. Does prior work already supply the intended contribution? Assess what a component swap, prompt change, training recipe, or implementation change adds in capability, efficiency, or understanding; simplicity alone is not an objection.
4. **Examine the rationale.** Identify assumptions that could make the proposal ineffective. Examine causal links and competing mechanisms when a causal or mechanistic explanation is part of the contribution. Require a proof when the contribution asserts a theorem.
5. **Attack the evidence plan.** When a test plan exists, check whether the proposed test measures the intended benefit or finding. Require discrimination between explanations when that is the research question. Look for confounds, leakage, weak baselines, unfair comparisons, proxy metrics, cherry-picking, underpowered tests, and missing controls.
6. **Attack scope and generalization.** At the method stage, examine where the mechanism should break down without requiring experiments or a detailed plan. When evaluation is planned, check whether it supports the intended scope. Prioritize mismatches that change the research decision.
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
- recommended decision: `pursue` (or `continue`), `refine` (or `revise`), `defer`, or `reject`.

## Discipline

Be adversarial about the idea and fair to the evidence. Do not invent reviewer opinions or attribute claims to papers without checking them. Separate source-backed objections from speculative risks.

## Completion criterion

Every fatal and major objection is either supported, refuted, or explicitly unresolved with a proposed probe. Cosmetic comments do not crowd out threats to the central contribution.
