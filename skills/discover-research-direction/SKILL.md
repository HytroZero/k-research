---
name: discover-research-direction
description: Develop promising research ideas, compare closest prior work, and select a direction with a practical first test.
disable-model-invocation: true
---

# Discover Research Direction

Turn a research area into promising candidates and an actionable recommendation. Develop ideas before subjecting the strongest candidates to focused checks.

## Operating stance

- Read `GLOSSARY.md` and existing project artifacts; reuse relevant literature and decisions.
- Perform factual investigation with available sources and tools. Ask the researcher for priorities and trade-offs that cannot be inferred.
- Invoke the relevant model-invoked skills through the host's Skill mechanism, or read their `SKILL.md` when that mechanism is unavailable.
- Use `docs/references/SCIENTIFIC-CLAIMS.md` to match evidence requirements to contribution type and research stage.
- Preserve source provenance and decision history. Report unknowns when they affect the recommendation or next action.

## 1. Frame and orient

Establish the target problem, community, intended contribution, available resources, and existing corpus. If the scope is too broad for useful investigation, propose a focused scope to the researcher.

Use `paper-analysis` and `field-synthesis` to understand representative approaches and relevant bottlenecks. Build enough context to generate concrete ideas; expand the literature pass as candidates reveal specific questions.

**Ready to proceed:** the scope, relevant approaches, and practical constraints are clear enough to identify useful problems.

## 2. Develop candidates

Use `opportunity-discovery`, then `hypothesis-development`. Explore improvements in capability, efficiency, reliability, evaluation, or understanding, including simple modifications and combinations of existing methods.

For each candidate, state:
- the problem and why it matters;
- the proposed method or intervention;
- the intuition for why it could help;
- the expected observable outcome;
- a feasible first comparison;
- the potential contribution.

**Ready to proceed:** candidates have a worthwhile problem, reasonable rationale, and a practical test. Mechanism explanations and formal theory are developed when they are part of the intended contribution.

## 3. Compare closest work

Use `novelty-audit` on the developed candidates worth advancing. Inspect the closest methods and results, including work that may already solve the problem. State the actual difference and why it matters.

**Ready to proceed:** the closest-work comparison supports a decision to test, revise, or set aside each shortlisted candidate. If retrieval leaves a material question open, record the specific missing comparison and decide whether to retrieve it first or proceed with a cheap exploratory test.

## 4. Resolve key risks and design the first test

For the most promising candidates, identify concrete issues that could remove the contribution's value or make the experiment uninterpretable. Examples include prior work implementing the same idea, extra compute explaining the gain, leakage, or unavailable data.

Use `decisive-test-design` to specify the smallest informative experiment or analysis, relevant baseline, measurements, and result-to-decision rules. A fair empirical comparison can justify the next step without resolving the full mechanism.

Use `red-team` for a full adversarial review when the user requests it or a specific unresolved concern warrants deeper investigation. It is an optional branch, not a required gate for every idea.

**Ready to proceed:** the first test can guide further investment, and any issue that blocks its usefulness has a concrete resolution or next action.

## 5. Recommend and record

Compare candidates using `docs/references/DECISION-RUBRIC.md`. Present the recommended direction, why it is worth trying, its difference from closest work, and the first test. Include risks only where they affect the choice or test design. Record why alternatives were revised, deferred, or rejected.

Ask the researcher to choose when priorities or resource trade-offs require their judgment. Produce `templates/research-brief.md` and `templates/decision-record.md`; omit optional sections that add no decision value. Persist artifacts and append a history event if the research-state interface is available.

## Completion criterion

The researcher can see what to try, why it matters, how it differs from closest work, and which initial result would justify continuing or revising it. Test execution is handed off to an execution agent.
