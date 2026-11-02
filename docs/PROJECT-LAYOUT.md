# Research Project Layout

This contract governs files produced by K Research in the user's research project, not the skill distribution itself. Read it before creating, moving, or updating project artifacts. Paths below are relative to the research project; skill references to docs, templates, and schemas are relative to the suite root.

Standalone teaching documents produced by `textbook-style-explanation` are outside this research-artifact contract and use the user's requested destination. Editing an existing research document retains that document's established location.

## Standard tree

```text
README.md
research/
  overview.md
  decisions.md
  directions/
    <direction-name>/
      proposal.md
      related-work.md
      evaluation-plan.md
papers/
  index.md
  references.bib
  notes/
    <paper-id>.md
  pdf/
    <paper-id>.pdf
.research/
  state/
  cache/
  scratch/
```

Create directories and files only when there is content to store. A conversation-only answer does not require filesystem artifacts. For persisted work, use these paths in new and existing projects; do not introduce alternative layouts or path-mapping files. Existing application code, datasets, and other tools' outputs remain outside this contract.

## Human reading surface

- `README.md` is the entry point: research question, current recommendation, and links to existing reading material. Integrate this navigation with an existing project README without replacing unrelated content.
- `research/overview.md` owns the field synthesis, worthwhile problems, candidate comparison, and current recommendation. Keep detailed methods in direction proposals and link them here.
- `research/decisions.md` contains dated entries with stable decision IDs, alternatives, evidence, reasons, and reconsideration triggers. Append meaningful decisions or changes, not a report for every invocation. Link superseding entries to earlier entries in this file.
- `research/directions/<direction-name>/proposal.md` owns a distinct candidate's problem, method, rationale, worked example, expected contribution, feasibility, and current status. Multiple hypotheses supporting the same direction belong in this file. Review findings and new evidence update the relevant sections.
- `related-work.md` owns the direction's detailed closest-work comparison, novelty judgment, counterevidence, and search boundary. The proposal summarizes the difference and links here.
- `evaluation-plan.md` owns detailed validation and execution handoff when experiments or a full plan are requested, or a developed method enters validation. Link it from the proposal; do not create it during ordinary idea discovery.
- `papers/index.md` is the complete current corpus index, including scope, coverage gaps, source provenance, and links to available notes and PDFs. `papers/references.bib` is its single bibliography. Merge additions into both files rather than creating supplements.
- `papers/notes/<paper-id>.md` is the sole reading note for a paper actually analyzed. `papers/pdf/<paper-id>.pdf` is its saved original. Record the inspected or downloaded source version without retaining local version copies.

All substantive conclusions, evidence, objections, and decision-relevant limitations must be understandable from this surface. Link every new human document into the reading navigation, directly from the README or through its linked overview or paper index. Templates supply content structure, not additional output filenames. Use relevant sections without duplicating full analyses across documents.

## Agent workspace

- `.research/state/` holds only durable continuation information, stable IDs, and structured records needed by a consumer. Reference human documents by path, heading, and ID; do not maintain a second narrative of the research. Schema-required summaries may be stored when structured persistence is used, and must agree with the human documents. Structured storage is optional.
- `.research/cache/` holds reproducible retrieval responses and extracted text.
- `.research/scratch/` holds temporary scripts, intermediate results, search execution logs, and debugging output. Remove this run's obsolete scratch files at completion; retain only material needed for active continuation.

Use stable purpose-based names inside these directories and update existing files. Do not create per-run or per-agent directory trees. Keep search scope and consequential exclusions in the human index or related-work document even when execution logs are internal. A reusable tool needs an explicit development task before becoming a maintained project tool.

## Naming and new files

Use short English kebab-case path names; write prose in the user's requested language. Assign readable stable paper IDs such as `smith-2025-paper-keyword`, resolving collisions once. Preserve existing stable IDs, including their spelling. Direction names describe the idea and remain stable across ordinary revisions. Do not name current files by date, run number, agent, or final-version suffix.

Update an existing file for the same object. Create a direction directory only for a distinct candidate that needs a developed account or an explicitly requested diagnostic study, and a paper note only for an analyzed paper. Link a diagnostic study directly from the overview when it has no method proposal. New permanent output types outside the tree require an explicit revision to this contract, not an agent's local exception.

## Updates and history

Maintain current complete documents. Record meaningful changes of judgment and their reasons in `research/decisions.md`; retain supporting and contradicting evidence in the relevant human documents. Git supplies file history where available. Do not create snapshots, backup copies, history directories, or parallel local event logs, including in non-Git projects. Version fields used for concurrency do not require old file copies. Do not initialize or commit to Git merely to satisfy this contract.

When migrating existing K Research outputs, consolidate unique content and provenance into the standard destinations, repair references, then remove superseded K Research files. Keep one corpus index and bibliography. Do not retain a compatibility tree. Preserve unrelated user content; resolve ambiguous ownership before removing a file.

## Completion

Before finishing a filesystem task, merge additions into the current documents, make the reading navigation complete, verify affected local links, and remove this run's obsolete scratch material. Check the index and bibliography against the entire retained corpus, not only the latest batch. Report the result in the conversation; do not save extra completion, verification, or process-summary reports.
