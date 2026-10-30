# Architecture

## Product boundary

Easy AI Research is a **scientific reasoning layer**. Its job is to help a researcher understand a field, identify worthwhile questions, develop testable hypotheses, assess novelty, expose weaknesses, and update decisions when evidence changes.

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
  +--> research (user-invoked router)
  |
  +--> discover-research-direction (user-invoked orchestrator)
          |
          +--> paper-analysis
          +--> field-synthesis
          +--> opportunity-discovery
          +--> hypothesis-development
          +--> novelty-audit
          +--> red-team (optional, for requested review or a concrete concern)
          +--> decisive-test-design
          +--> belief-update

Any agent may independently invoke a model-invoked skill when its trigger fits.
```

A user-invoked skill must not invoke another user-invoked skill. The router can recommend the full workflow; the user chooses to start it.

## Main research loop

1. Build a field model from a defined corpus.
2. Find useful problems and opportunities from literature, observations, or task needs.
3. Develop concrete ideas with a rationale and expected observable outcomes.
4. Compare developed candidates against the closest prior work.
5. Identify decision-relevant risks in the most promising candidates; use full red-team review on demand.
6. Design the smallest informative experiment or analysis.
7. Select, revise, defer, or reject the direction.
8. When new evidence arrives, update the state and revisit affected decisions.

The loop can stop at any stage. The process should preserve useful negative findings and rejected hypotheses.

## Human control

The agent performs factual legwork: search, retrieval, comparison, and synthesis. The researcher retains decisions involving values and trade-offs: which problem matters, acceptable risk, target community, available resources, and whether to pursue a direction.

Ask the user only for information that cannot be recovered from the corpus or tools, and ask at the point where the decision becomes consequential.
