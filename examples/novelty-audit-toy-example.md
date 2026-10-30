# Toy Example: Novelty Audit

> This is a fictional teaching example. Paper labels P1-P3 and all findings are invented. It is not a statement about the real literature on agent memory.

## Candidate

"Use task-conditioned uncertainty to decide which agent memories to consolidate."

## Candidate decomposition

- Problem: long-running agents retain information that is not equally useful for future tasks.
- Rationale: retrieval uncertainty may help allocate a limited consolidation budget to useful memories.
- Method: a consolidation policy conditioned on task context and retrieval uncertainty.
- Intended contribution: show that the uncertainty signal identifies memories whose consolidation changes downstream task performance.

## Fictional prior work

| Paper | Fictional contribution | Overlap |
|---|---|---|
| P1 | Stores memories based on predicted future utility. | Overlaps with task-conditioned selection. |
| P2 | Consolidates memories using retrieval frequency and recency. | Overlaps with selective consolidation. |
| P3 | Uses uncertainty estimates to decide when to retrieve additional context. | Overlaps with uncertainty-aware retrieval, but not necessarily consolidation. |

## Initial audit

A weak audit would say: "No paper combines all three components, therefore the idea is novel."

A stronger audit asks:
1. Does P1 already condition memory selection on task context?
2. Is P3's uncertainty estimate effectively a consolidation signal under another name?
3. What useful improvement could this combination deliver under the same memory and compute budget?
4. What observable result would distinguish uncertainty-guided consolidation from utility-based selection?
5. Which small experiment would show whether the added uncertainty signal is worth using?

## Possible discriminating contribution

A useful empirical contribution could be improved downstream task performance under a defined distribution shift at the same memory and compute budget as utility-only or recency-only policies. A complete explanation of the mechanism can be investigated later.

The first test compares these policies at matched budgets and measures downstream task performance. Its results guide whether to continue with broader validation.

## Example audit outcome

`plausible_unverified`

Reason: the fictional corpus suggests meaningful overlap, but the central distinction is not yet established. The next step is to inspect full methods and derive a test that separates uncertainty-guided consolidation from existing utility-based selection.

## Lesson

The audit does not reward novelty by component count. It asks what useful method, empirical improvement, finding, or capability the proposal adds relative to existing approaches.
