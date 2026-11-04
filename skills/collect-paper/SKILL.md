---
name: collect-paper
description: Collect papers for a broad research direction, screen relevant work from leading venues or recognized research organizations, download key PDFs, and build a local index with BibTeX.
---

# Collect Paper

Turn a broad research direction into a usable initial paper collection. Produce a source-checked index and bibliography for subsequent reading. Field synthesis and research-direction recommendations belong to other skills.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update `papers/index.md` and `papers/references.bib`; save originals in `papers/pdf/`. Keep retrieval data in `.research/cache/` and temporary collection scripts and execution logs in `.research/scratch/`.

## 1. Scope the collection

Accept a topic phrase as sufficient input. Use optional seed papers, subtopics, dates, language preferences, and project constraints when supplied. Inspect an existing collection before starting a new one. Ask only when different interpretations would materially change the search.

Expand the topic into query families using technical synonyms, related tasks, predecessor methods, and adjacent terminology. State a bounded initial search scope. Seek representative foundational and recent papers and relevant surveys; follow citations where they reveal relevant work. Stop when the main query families have been checked and further results mostly duplicate the collection. Record useful gaps for a later pass instead of pursuing an exhaustive census.

## 2. Search and screen

Use available literature search and retrieval tools; verify records against proceedings, publisher pages, official paper repositories, author pages, or research-group publication pages. Search indexes and citation counts help discovery.

A retained paper must be relevant and satisfy at least one source criterion:
- publication at a leading conference or journal in the relevant field;
- authorship by a recognized research team, university, or company;
- a technically substantive preprint, workshop paper, or adjacent-field work that introduces a distinct mechanism, formulation, or counterexample not covered by mainstream venues.

Apply the criteria as alternatives. Verify venue, publication status, and author affiliations from the paper or an official source. Record the qualifying venue, organization, or substantive-inclusion rationale and a source URL. Do not equate a workshop or submitted manuscript with main-conference acceptance. If neither source eligibility nor a specific technical rationale can be established, keep the candidate in the search log for follow-up rather than the retained collection. Use a user-provided source list when available; otherwise make the chosen criteria explicit without interrupting routine collection for approval.

Read titles and abstracts, plus method passages when needed to determine relevance. Give each retained paper a short, topic-specific inclusion reason. Source eligibility selects the collection; assessment of the paper's findings belongs to later reading.

## 3. Deduplicate and identify

Match DOI, arXiv or other stable identifiers, then normalized titles and authors. Consolidate preprint and published versions into one paper record where they describe the same work. Prefer the published bibliographic record when verified; keep alternate version links and identify the PDF version actually saved.

Reuse existing paper IDs and citation keys. Assign stable unique IDs and BibTeX keys to new records; resolve key collisions. Preserve user notes and prior provenance on subsequent collection runs.

## 4. Save key PDFs and BibTeX

Select key papers for local PDFs based on direct relevance, foundational role, or usefulness as a representative method. Download accessible originals from proceedings, publishers, repositories, or author-hosted sources into `papers/pdf/`. Use stable paper IDs in filenames and preserve existing files unless intentionally updating a recorded version.

Verify that a download is a readable PDF and that its title/authors match the indexed paper. Record the source URL and saved version. If access or downloading fails, retain the paper's metadata and link with a concrete download status. A downloaded file does not imply that its full text was read.

Retrieve BibTeX from an authoritative bibliographic export where possible. Otherwise construct an entry from verified metadata, using an appropriate entry type and omitting unknown fields. Keep preprint and publication metadata distinct. Save one entry per retained paper to `papers/references.bib`, with keys matching the index. Check parsing, unique keys, and agreement of titles, authors, years, and identifiers with the records.

## 5. Build the index

Use the standard project layout. Maintain one complete index and bibliography across collection runs.

The index contains one row per retained paper with paper ID, citation key, title, authors, year, venue/publication status, qualifying source and verification link, canonical paper URL, relative PDF path or download status (with version), inspection depth, reading note link (when analyzed), and inclusion reason. Keep missing metadata explicit. Record inspection depth separately from download status.

Use `templates/paper-index.md` from the suite root. If persisting structured records, use `schemas/paper.schema.json`; the Markdown index is sufficient without a state backend.

In the index, maintain the search scope, query families, sources searched, retrieval dates, and material exclusions or access gaps. Temporary search execution details belong in `.research/scratch/`.

## Completion

Check that every retained paper has a qualifying source, an inclusion reason, and a matching BibTeX entry; every local PDF link resolves to the verified file. Report the collection location, paper count, PDF count, and any specific retrieval gaps. Finish at collection and indexing; hand the materials to `paper-analysis` or `field-synthesis` when the user requests further reading or the enclosing workflow continues.
