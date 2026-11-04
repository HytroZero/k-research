> Placement: Update `papers/notes/<paper-id>.md` and link it from `papers/index.md`. Keep one note per analyzed paper. See [Project Layout](../docs/PROJECT-LAYOUT.md). This placement note is a template instruction, not output content.

# Paper Note

## Identity

- Paper ID:
- Title:
- Authors:
- Year / venue:
- DOI / preprint ID:
- Canonical URL:
- Version inspected:
- Access level: full_text / abstract_only / metadata_only / inaccessible / unverified
- Retrieval date:

## Research question and setting

State the problem, target setting, and why the authors consider it important.

## Contribution claims

Separate the paper's claims from your interpretation. Classify each claim using `docs/references/SCIENTIFIC-CLAIMS.md`.

| Claim ID | Claim | Type | Source locator | What the paper actually establishes |
|---|---|---|---|---|

## Mechanism or method

Explain the central procedure, objective, or causal chain step by step so another researcher can see how it operates.

## Assumptions and dependencies

List the formal, empirical, data, or compute assumptions the method or conclusion relies on.

## Evidence

Record the primary evidence bearing on each core claim. Use relations (`supports`, `contradicts`, `qualifies`, `contextualizes`, `does_not_address`), status (`direct`, `indirect`, `secondary`, `unverified`, `unknown`), and strength (`strong`, `moderate`, `weak`). For `unverified` or `unknown`, record status without strength.

| Evidence ID | Claim and relation | Experiment, proof, or observation | Result and conditions (baselines, metrics, setting) | Locator | Status and strength |
|---|---|---|---|---|---|

## Results and scope

Synthesize the demonstrated operating boundary—where the method or finding holds, degrades, or remains untested—without repeating individual rows from the evidence table.

## Limitations

### Author-stated

Record limitations explicitly acknowledged in the paper, with locators.

### Analyst-inferred

State additional limitations only when supported by the paper's setup, assumptions, or missing controls.

## Relation to prior work

Identify the closest prior work and state what this paper actually changes, rather than repeating the introduction's framing.

## Unresolved questions

List open questions that follow directly from the paper's assumptions, evidence, or boundary conditions.

## Confidence and missing information

State overall confidence in this reading and note any uninspected sections, appendices, code, or theorems that could affect the conclusions.
