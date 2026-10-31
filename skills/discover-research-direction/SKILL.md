---
name: discover-research-direction
description: Develop a worthwhile research problem and a concrete method, grounded in prior work, then recommend a direction.
disable-model-invocation: true
---

# Discover Research Direction

Turn a research area into a well-motivated problem and a concrete proposed solution. The default deliverable is a Research Brief centered on the problem, method, and substantive difference from prior work.

## Operating stance

- Read `GLOSSARY.md` and existing project artifacts; reuse relevant literature and decisions.
- Perform factual investigation with available sources and tools. Ask the researcher for priorities and trade-offs that cannot be inferred.
- Invoke the relevant model-invoked skills through the host's Skill mechanism, or read their `SKILL.md` when that mechanism is unavailable.
- Preserve source provenance and decision history. Use `docs/references/SCIENTIFIC-CLAIMS.md` to distinguish proposed contributions from established results.

## 1. Understand the setting and existing approaches

Establish the target task, community, resources, and existing corpus. If the scope is too broad, propose a focused scope.

Use `collect-paper` to build or refresh the corpus, then `paper-analysis` and `field-synthesis` to understand representative approaches. Follow how each approach addresses the task and which limitations remain. Expand retrieval as specific problems and design choices emerge.

**Ready to proceed:** the task, current approaches, and relevant constraints are concrete enough to identify useful problems.

## 2. Define worthwhile problems

Use `opportunity-discovery`. For each promising problem, describe the setting, the specific difficulty, its practical consequence, and why known approaches leave it unresolved. Ground the limitation in sources, observations, or explicit task requirements. An illustrative example can explain a difficulty; label it as illustrative when it is not an observed failure.

**Ready to proceed:** the reader can explain what needs solving and why it matters, independently of a proposed method or benchmark.

## 3. Develop methods against those difficulties

Use `hypothesis-development`. Explain the proposed method's inputs, key steps, and outputs, and connect its design choices to the difficulties identified above. Carry a small example through the current approach and the proposed solution. Compare known neighboring methods during development; revise designs when a neighbor already supplies the proposed solution.

**Ready to proceed:** each developed candidate has a specific problem, an understandable method, a rationale connecting the two, and a useful expected contribution. Basic resource feasibility is enough here; a detailed experiment plan is not a readiness gate.

## 4. Check the strongest candidates against closest work

Use `novelty-audit` for focused verification of mature candidates. Build on the comparisons made during problem and method development. State the actual difference and why it matters; use overlap findings to refine or set aside candidates.

Use `red-team` when requested or when a concrete unresolved concern warrants deeper investigation.

**Ready to proceed:** the closest-work comparison supports a recommendation, and any unresolved question that changes it has a specific next action.

## 5. Recommend and record

Compare candidates using `docs/references/DECISION-RUBRIC.md`. Produce `templates/research-brief.md` and `templates/decision-record.md`. Give the problem and method the explanatory detail needed to judge the direction; integrate prior work where it motivates the problem or a design choice. Record why alternatives were revised, deferred, or rejected.

Ask the researcher to choose when priorities or resource trade-offs require their judgment. Persist artifacts and append a history event if the research-state interface is available.

## Follow-on: experiment planning

Use `decisive-test-design` when the user requests experiments or a full research plan, or the task has advanced to validating a developed method. Put detailed baselines, controls, metrics, and execution instructions in a separate experiment plan and link it from the brief. An explicit experimental request should continue through this stage without an extra approval step.

## Completion criterion

The researcher can explain the problem, how the method addresses it, why the design could work, and what it adds to the closest work. The recommendation and next action follow from that account. Default direction discovery is complete without a detailed experiment plan.
