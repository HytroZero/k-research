---
name: paper-analysis
description: Analyze an academic paper. Use when extracting a paper's research question, contribution, mechanism, assumptions, claims, evidence, results, limitations, or relation to prior work.
---

# Paper Analysis

Extract what a paper actually establishes, with source locators. The output should let another researcher use the paper without relying on a vague summary.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update `papers/notes/<paper-id>.md` and link it from `papers/index.md`. Store extracted text in `.research/cache/`.

## Process

1. **Identify the source.** Resolve title, authors, year, venue/version, DOI or preprint ID, canonical URL, and retrieval date. Note whether you inspected full text, abstract only, or metadata only.
2. **Recover the question.** State the problem, target setting, intended audience, and why the authors consider it important.
3. **Extract contribution claims.** Separate the paper's own claims from your interpretation. Classify each claim using `docs/references/SCIENTIFIC-CLAIMS.md`.
4. **Reconstruct the mechanism or method.** Explain the central idea as a sequence of steps or causal links. List assumptions and dependencies.
5. **Inspect the evidence.** For every core claim, identify the supporting experiment, theorem, analysis, dataset, figure, table, or argument. Record baselines, controls, metrics, sample/setting, and uncertainty where available.
6. **Find the boundaries.** Extract stated limitations and infer additional limitations only when the evidence supports the inference. Separate author-stated limitations from your own.
7. **Position the paper.** Identify relevant prior work and what this paper changes. Do not infer priority or novelty from the introduction's wording alone.
8. **Record open questions.** List unresolved questions that follow from the paper's assumptions, evidence, or scope.

## Evidence discipline

- Prefer full text and primary sources over abstracts and secondary summaries.
- Every material extracted claim needs a locator. Use section, page, figure, table, theorem, or appendix.
- If a locator cannot be verified, mark it `unverified`.
- Keep author claims, observed results, and your interpretation in separate fields.
- Do not invent metrics, sample sizes, statistical significance, quotations, or bibliographic facts.
- Read `docs/references/EVIDENCE-STANDARDS.md` when deciding how strongly a source supports a claim.

## Output

Use `templates/paper-note.md`. Include:
- bibliographic identity and source-access level;
- research question and setting;
- contribution claims;
- mechanism/method;
- assumptions;
- evidence table with locators and relation to claims;
- results and scope;
- limitations;
- unresolved questions;
- confidence and missing information.

## Completion criterion

Every core claim is either linked to a verified source locator or explicitly marked unverified/unknown. The note distinguishes what the paper demonstrates from what it merely suggests.
