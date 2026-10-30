---
name: field-synthesis
description: Synthesize a body of research papers into a field map. Use when mapping a subfield, comparing research lines, tracing method evolution, or identifying agreements and disagreements across papers.
---

# Field Synthesis

Build a structured model of a research field from a defined paper corpus. A field map is an evidence-backed account of how ideas relate, not a pile of summaries.

## Process

1. **Set the corpus boundary.** Record the research question, inclusion/exclusion criteria, databases or sources searched, time range, and known access or language limits.
2. **Check corpus coverage.** Identify foundational papers, influential recent work, relevant surveys, competing approaches, and known negative or contradictory results. Record missing regions.
3. **Analyze representative papers.** Use `paper-analysis` for pivotal or disputed papers. Do not assume every paper needs equal depth.
4. **Choose conceptual axes.** Organize the field by research question, mechanism, assumptions, method family, evaluation setting, or theoretical position. Chronology can supplement this structure but should not replace it.
5. **Build the claim map.** Identify which papers support, contradict, qualify, extend, or do not address each major claim.
6. **Trace evolution.** Explain how methods and explanations changed, what problem each line attempted to solve, and which assumptions persisted.
7. **Map boundaries and tensions.** Identify settings where conclusions differ, methods fail, metrics disagree, or evidence is underdetermined.
8. **Separate field gaps from corpus gaps.** A missing topic in the collected papers may reflect incomplete retrieval. Call it a research gap only when the search boundary and evidence justify that interpretation.

## Output

Produce:
- a short field overview;
- major research clusters and their central claims;
- a method/mechanism taxonomy;
- a timeline of important shifts;
- a claim relationship map;
- unresolved disagreements and boundary conditions;
- a list of candidate opportunities, clearly marked as hypotheses for further investigation;
- corpus coverage and limitations.

Use stable paper IDs and cite exact source locators. Read `docs/references/SCIENTIFIC-CLAIMS.md` and `docs/references/EVIDENCE-STANDARDS.md` when needed.

## Completion criterion

A domain expert can see the major research lines, why they differ, what evidence supports their central claims, and where the synthesis remains uncertain. Every claimed disagreement is linked to the papers that create it.
