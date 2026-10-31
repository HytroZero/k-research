# AGENTS.md

## Project scope

K Research is a collection of composable research skills. It helps researchers find worthwhile problems, develop ideas, compare prior work, and update research decisions. Experiment execution, infrastructure, and manuscript drafting belong to other tools or agents.

## Design priorities

- Preserve room for idea creation. Skills should support research judgment without prescribing one universal thinking process. Treat brainstorming lenses as options, not a checklist every idea must satisfy.
- Let ideas develop before filtering them by literature overlap. Use prior work to inform and position ideas; avoid adding components solely to manufacture novelty.
- Judge simple methods, combinations, and complex methods by their useful contribution. Simplicity is valuable when it serves the problem, not a mandatory aesthetic.
- Keep factual grounding separate from creative exploration. Claims about existing work and observed results need evidence; proposed ideas can begin with intuitions, analogies, or questioned assumptions.
- Default direction discovery ends with a problem-and-method recommendation. Methods selected for recommendation receive the review-and-revision cycle owned by `hypothesis-development`. Detailed experiment planning is follow-on work. Preserve explicit requests for a complete research plan.
- Add a constraint only when it addresses a concrete failure and belongs at that research stage. Prefer removing unnecessary instructions to accumulating gates, disclaimers, and output fields.

## Editing skills and documentation

- Write agent instructions in English. Use direct, natural prose. In academic writing, omit statements that only shield an argument from criticism without advancing it.
- Read the target skill and the references or templates it uses before changing its behavior. Keep detailed procedures in the owning skill and shared principles in the relevant reference document.
- Replace obsolete instructions rather than retaining parallel versions or compatibility scaffolding without a current need.
- Keep templates consistent with the skill's intended output; avoid turning optional analysis into mandatory sections.
- For workflow or invocation changes, consult `docs/ARCHITECTURE.md`; for terminology, consult `GLOSSARY.md`.
- For evidence or novelty changes, consult the relevant files in `docs/references/`. For persisted artifact changes, consult `docs/RESEARCH-STATE.md` and the affected schemas; for capability interfaces, consult `docs/MCP-CONTRACT.md`.
- When changing public skill names, descriptions, or deliverables, update affected metadata and both README versions. Keep `MANIFEST.txt` current when adding or removing authored files.

## Validation

- Review changed instructions together with their callers and templates for conflicting requirements. Use relevant cases in `docs/EVALUATION.md` when evaluating behavior; distinguish textual review from observed model performance.
- Match validation to the change. Check affected links and structured-file syntax where relevant; avoid introducing a test framework for prose-only edits.
