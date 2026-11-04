# Research State and Artifact Contract

This document defines the shared language and lifecycle for research artifacts. JSON Schemas in `schemas/` are the machine-readable contracts; Markdown templates in `templates/` guide human-readable content. Read [Project Layout](PROJECT-LAYOUT.md) before persisting artifacts; it owns paths, human/agent separation, migration, and file lifecycle.

## Core entities

- **ResearchProject:** scope, domain, central question, constraints, and current status.
- **Paper:** bibliographic identity, source provenance, and extracted content. Collection records also carry a citation key, inclusion reason, verified source eligibility, and optional PDF location/version. `source_access` records inspection depth, independently of download status.
- **Claim:** a proposition made by a source or proposed by the current research.
- **Evidence:** a source-grounded observation tied to a locator and a relation to one or more claims.
- **Opportunity:** an evidence-grounded reason to investigate a problem.
- **Hypothesis:** a testable proposal with a rationale and expected observable outcomes. Mechanisms, competing explanations, and explicit falsification conditions are included when relevant to the contribution or test.
- **Contribution:** the precise new knowledge or capability that successful work would establish.
- **ResearchDecision:** a choice to pursue, refine, continue, revise, defer, reject, or stop, with evidence and alternatives.

## Identity and versioning

Every artifact has a stable ID. Do not use titles as IDs. A title can change; identity should not.

When an artifact materially changes, update its current document and any consumed structured record in place. Record meaningful changes of judgment and their reasons in `research/decisions.md`, linking superseding decisions by stable ID. Git may retain file history; neither Git nor non-Git projects create backup copies, snapshots, or local history/event files. Version counters serve identity and concurrency, not a requirement to retain old files.

A new paper, result, or counterexample should create new evidence records. Do not silently edit the historical record to make the current narrative look consistent.

## Evidence relations

Use one of these relations when connecting evidence to a claim:

- `supports`
- `contradicts`
- `qualifies`
- `contextualizes`
- `does_not_address`

`does_not_address` is useful when a paper is relevant to the topic but does not test the claim being discussed.

## Evidence status

Use explicit status labels:
- `direct`: the source directly reports or proves the point;
- `indirect`: the point is inferred from source material;
- `secondary`: the source summarizes another source;
- `unverified`: the source or locator has not been checked;
- `unknown`: the available material cannot establish the point.

A skill must not upgrade `indirect`, `secondary`, or `unverified` evidence to `direct` without checking the primary source. When a qualitative evidence strength is recorded alongside status, use `strong`, `moderate`, or `weak` as defined in `docs/references/EVIDENCE-STANDARDS.md`.

Hypothesis records require `rationale` and at least one observable prediction. The observable describes the expected task behavior; it need not specify a measurement protocol. `first_test` is optional and is populated when experiment planning begins. When updating an older record, add a rationale from the documented idea and record any changed judgment in the decision log.

## Hypothesis lifecycle

Suggested statuses:
- `candidate`
- `under_review`
- `testable`
- `supported`
- `weakened`
- `rejected`
- `revised`
- `deferred`

Status is a summary, not a probability. Keep the supporting and contradicting evidence visible.

## Decision lifecycle

A decision record should state:
- what was decided;
- which alternatives were considered;
- why the selected path was preferred;
- what evidence was decisive;
- what uncertainty remains;
- what observation would trigger reconsideration.

Decisions may be superseded, not erased.

## Minimum provenance

For every literature-derived statement, preserve as many of the following as available:
- title and author list;
- year and venue;
- DOI, arXiv ID, ACL Anthology ID, OpenReview ID, or another stable identifier;
- canonical URL;
- exact section, page, figure, table, theorem, or appendix locator;
- retrieval date;
- whether full text or only abstract/metadata was inspected.

If an exact locator is unavailable, say so. Never invent page numbers, quotations, or bibliographic details.
