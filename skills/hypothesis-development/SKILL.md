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
6. **Position against known neighbors.** Compare the formed design against neighboring literature to identify shared building blocks and actual differences. If a neighbor already solves the problem cleanly, either reframe the problem, find a genuinely simpler or stronger mechanism, or set the candidate aside—do not bolt on incidental complexity just to claim novelty. Use this initial comparison to inform the review below.
7. **State the expected contribution and feasibility.** Explain the capability, efficiency, simplification, measurement, or understanding success would add. Identify essential data, model access, or resource requirements and the main open design question.

For a theoretical contribution, specify the proposition, assumptions, and proof approach. For a mechanistic or causal contribution, articulate the explanation and relevant alternatives. Detailed validation belongs to `decisive-test-design` when the task advances to experiment planning.

## Review and revise before recommendation

Apply this step to concrete methods selected for recommendation, including standalone method-development requests. Let early sketches develop before selecting candidates. Skip review only when the user explicitly asks to skip it. This skill owns the review cycle; callers reuse its results rather than launching another cycle for the same method.

1. **Prepare one shared proposal.** Include the problem, method, rationale, worked example, contribution, constraints, known neighbors, and available evidence. Keep this version unchanged while reviewers work. Supply relevant source and project paths and the suite root so each reviewer can read its skill and references.
2. **Run two independent reviewers in parallel.** Use the host's subagent mechanism: one reviewer follows `skills/red-team/SKILL.md`, focusing on mechanism, assumptions, failure cases, and feasibility; the other follows `skills/novelty-audit/SKILL.md`, searching and checking closest work and substantive differences. Both receive the same proposal and return findings with reasoning or source locators. They do not wait for each other's findings, revise the candidate, write shared project files, or invoke method development or further review agents. Missing inputs are findings for the parent to resolve.
3. **Integrate and revise.** Wait for both reviews, assess their evidence, and resolve conflicting judgments. Update the method, rationale, example, and contribution together where objections warrant changes. Explain consequential changes and why important objections were not adopted. Reviewers advise; their severity labels or novelty outcomes do not automatically veto a valuable method. Reframe, defer, or reject a method when the case warrants it rather than adding components merely to satisfy reviewers.
4. **Bound follow-up.** Default to one review-and-revision round. If revision materially changes the core mechanism or contribution claim, allow one targeted second round with the affected reviewer or both. Share the revised proposal and relevant findings for that follow-up. Stop after two rounds for this development task; report remaining consequential issues and the next action instead of looping until reviewers agree. Mark findings tied to superseded designs accordingly; do not present an unchecked revised claim as audited.
5. **Publish the integrated result.** The parent updates the existing proposal and related-work document, and records meaningful decision changes according to Project Layout. Include the review mode, key revisions, and remaining consequential objections in the proposal's relevant sections; keep detailed literature comparisons in related work.

If the host cannot run subagents, perform the two skill reviews sequentially and then integrate them, explicitly stating that these were not independent subagent reviews. If a reviewer fails, retry within the current round or complete its discipline in the parent and disclose the fallback. Unavailable sources remain an explicit search limitation, not evidence of novelty. A missing experiment plan or experimental result is not itself an objection at the method stage; detailed validation remains follow-on work.

## Output

Use `templates/hypothesis-card.md`. Center the output on the problem, method, design rationale, worked example, and difference from known approaches. Write the method and worked example directly without repetitive sentence-level disclaimers that the proposal is untested; the artifact status already marks it as a proposal.

## Completion criterion

A reader can trace the method's key steps through the example, connect its design choices to the stated difficulty, and explain the potential contribution relative to known work. Selected methods have completed the review-and-revision cycle, or explicitly identify a user-requested skip or an incomplete review. An unresolved core algorithm should be identified as the next design task rather than hidden behind boilerplate formulas or an experiment plan.
