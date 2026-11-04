# Evidence Standards

## Source hierarchy

Prefer the source that owns the claim:
1. original paper, preprint, proceedings version, or official artifact;
2. official dataset, benchmark, code repository, technical report, or specification;
3. a review or survey that points to the primary source;
4. a credible secondary explanation;
5. informal discussion, blog, or social post.

A lower-tier source can be useful for discovery. It should not silently become the final support for a technical claim when the primary source is available.

## Claim-to-source discipline

For each material statement:
- identify the exact claim;
- attach the source that supports it;
- record the locator;
- classify the relationship (`supports`, `contradicts`, `qualifies`, `contextualizes`, `does_not_address`);
- distinguish what the source says from what the agent infers.

A paper's abstract is not evidence for details that appear only in its methods or results. If only an abstract was read, state that limitation.

## Evidence strength and status

Record verification and directness using the `status` labels in `docs/RESEARCH-STATE.md` (`direct`, `indirect`, `secondary`, `unverified`, `unknown`). For verified sources, assess qualitative `strength` with reasons:
- **`strong`:** primary source directly tests or proves the claim, with a relevant design and transparent reporting.
- **`moderate`:** relevant but indirect, limited in scope, or dependent on assumptions.
- **`weak`:** suggestive, underpowered, indirect, or based on a proxy that may not measure the claim.

When a source or locator has not been checked (`unverified`) or available material does not answer the question (`unknown`), state that status directly rather than assigning a strength label. Do not convert these labels into unsupported numeric probabilities.

## Negative evidence

A failed replication, null result, or counterexample matters only within its tested conditions. Record the setting, metric, sample, and method. Do not generalize a local failure into universal impossibility.

## Search absence

"No paper found" is a statement about a search process, not a statement about the world. Record:
- databases or search tools used;
- search strings and synonyms;
- date range;
- citation chaining performed;
- language and access limits;
- stopping rule.

Phrase the conclusion as "not found within this search boundary" unless the search is unusually comprehensive and independently checked.

## Quotations and locators

Prefer concise paraphrase plus exact locator. Use quotations only when wording itself matters. Never fabricate quotations, page numbers, figure numbers, or citations. If a PDF version and proceedings version differ, record which version was inspected.
