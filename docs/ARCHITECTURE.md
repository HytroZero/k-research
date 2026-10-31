# Architecture

## Product boundary

Easy AI Research is a **scientific reasoning layer**. Its job is to help a researcher understand a field, identify worthwhile questions, develop concrete methods grounded in those questions, assess novelty, expose weaknesses, and update decisions when evidence changes.

It does not own:
- code implementation or experiment execution;
- SSH, GPU provisioning, scheduling, or cost enforcement;
- dataset processing pipelines;
- full manuscript drafting, LaTeX, or submission workflows.

Those capabilities can be provided by other agents. This suite hands them a structured Research Brief and receives their results as new evidence.

## Three layers

### 1. Skills: research discipline

Skills encode procedures, judgment criteria, quality gates, and output contracts. The user-invoked skills orchestrate; model-invoked skills provide reusable disciplines.

### 2. MCP: capability interface

MCP exposes a small set of operations for literature retrieval, citation context, research graph queries, and persistent artifact storage. See `MCP-CONTRACT.md`.

### 3. Research state: shared memory

The state layer stores papers, claims, evidence, opportunities, hypotheses, contributions, and decisions. It gives every skill and the GUI a common source of truth.

## Invocation topology

```text
Human
  |
  +--> ask-k (user-invoked router)
  |
  +--> discover-research-direction (user-invoked orchestrator)
          |
          +--> collect-paper
          +--> paper-analysis
          +--> field-synthesis
          +--> opportunity-discovery
          +--> hypothesis-development
          +--> novelty-audit
          +--> red-team (optional, for requested review or a concrete concern)
          +--> decisive-test-design (follow-on, for experiment planning)
          +--> belief-update

Any agent may independently invoke a model-invoked skill when its trigger fits.
```

A user-invoked skill must not invoke another user-invoked skill. The router can recommend the full workflow; the user chooses to start it.

## Main research loop

1. Collect and index an initial corpus with BibTeX and key PDFs, then build a field model.
2. Define useful problems: the setting, specific difficulty or questioned assumption, consequence, and why existing approaches leave it open.
3. Develop concrete methods from first principles with design choices tied to those difficulties; trace their operation through a worked example and then position them against known neighbors without adding defensive complexity.
4. Verify mature candidates against the closest prior work through a focused novelty audit.
5. Recommend pursuing, refining, deferring, or rejecting the direction based on problem value, method fit, substantive difference, and basic feasibility. Deliver the Research Brief here by default.
6. When experiments or a full plan are requested, or a method enters validation, design the smallest informative experiment in a separate plan. Use full red-team review on demand.
7. When new evidence arrives, update the state and revisit affected decisions.

The loop can stop at any stage. The process should preserve useful negative findings and rejected hypotheses.

## Human control

The agent performs factual legwork: search, retrieval, comparison, and synthesis. The researcher retains decisions involving values and trade-offs: which problem matters, acceptable risk, target community, available resources, and whether to pursue a direction.

Ask the user only for information that cannot be recovered from the corpus or tools, and ask at the point where the decision becomes consequential.
