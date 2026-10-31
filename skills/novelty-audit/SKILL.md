---
name: novelty-audit
description: Audit the substantive novelty of a research idea. Use when comparing a proposed contribution with closest prior work, checking overlap, testing a first-of-its-kind claim, or preparing a novelty assessment.
---

# Novelty Audit

Determine whether the candidate makes a material contribution beyond the closest prior work. The audit is a source-backed comparison, not a novelty score generated from intuition.

## Project files

When delegated as a reviewer by `hypothesis-development`, return findings to the parent without writing project files or invoking method development or further review agents. Report missing inputs for the parent to resolve. The parent owns integration. For standalone use, follow the destinations below.

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update `research/directions/<direction-name>/related-work.md` using the novelty-audit template, and update the proposal's summary of the difference.

## Process

1. **Decompose the candidate.** Extract its problem, proposed method or finding, setting, and intended contribution. Include a mechanism when it carries the contribution. If the idea is too vague to compare, develop it with `hypothesis-development` or ask for the missing decision.
2. **Generate search concepts.** Derive multiple query families from the mechanism, problem, components, terminology variants, predecessor methods, and expected effects. Search synonyms and adjacent terminology, not only the candidate's own wording.
3. **Find closest prior work.** Search databases and primary sources. Use backward and forward citation chaining where available. Include work from adjacent fields and less prominent venues if technically relevant.
4. **Inspect primary sources.** For the closest candidates, inspect the method, claims, and results. Abstract-only comparisons are provisional.
5. **Compare contribution dimensions.** Use `docs/references/NOVELTY-TAXONOMY.md`. For each closest paper, compare question, mechanism/method, assumptions, setting, evidence, and demonstrated boundary.
6. **Search for counterevidence.** Actively try to find a paper that already contains the central mechanism, prediction, or result. Record the strongest counterexample, not just supporting matches.
7. **Classify the audit.** Choose one outcome:
   - `substantiated`
   - `plausible_unverified`
   - `incremental`
   - `anticipated`
   - `contradicted`
   - `not_assessable`
8. **State confidence and search boundary.** Explain which databases, queries, dates, and citation paths were checked, what was inaccessible, and what remains unverified.

## Comparison table

For each closest prior work, include:
- stable paper ID and bibliographic identity;
- exact overlapping claim or mechanism;
- what the prior work already establishes;
- what the candidate adds;
- whether the difference is conceptual, mechanistic, methodological, theoretical, empirical, evaluative, or only contextual;
- source locators for both sides;
- residual uncertainty.

## Judgment rules

- Judge combinations and small changes by their concrete difference and useful outcome. Improvements in performance, efficiency, reliability, or evaluation can carry a contribution.
- Assess empirical improvements against relevant baselines and resource budgets. A complete mechanism explanation is required only when it is itself the claim.
- Ground novelty judgments in the closest-work comparison and record the search scope.
- Separate novelty from value: an incremental change can justify experimentation when its expected benefit matters.

Read `docs/references/EVIDENCE-STANDARDS.md` and `docs/references/NOVELTY-TAXONOMY.md`.

## Output

Use `templates/novelty-audit.md`. Include the audit outcome, closest-work table, strongest counterevidence, search boundary, and the next useful test, search, or revision.

## Completion criterion

A reader can reconstruct why the idea is judged novel, incremental, anticipated, contradicted, or not assessable from the cited primary sources. Uncertainty is explicit.
