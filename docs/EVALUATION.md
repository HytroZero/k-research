# Evaluation Protocol

Evaluate whether the skills improve research judgment, not whether their prose sounds academic.

## Evaluation set

Build a benchmark from completed research projects and historical papers. For each case, preserve:
- a dated literature corpus boundary;
- the research question as it was known at that time;
- known closest prior work;
- the actual unresolved issue or eventual discovery, if known;
- expert annotations for claims, evidence, and novelty;
- examples where the apparently promising direction was already anticipated or later falsified.

Use time-sliced evaluation where possible: only provide the model papers available before the outcome date. This reduces hindsight leakage.

## Skill-level measures

| Skill | Useful measures |
|---|---|
| `collect-paper` | topic relevance, verified source eligibility, version deduplication, BibTeX accuracy, working PDF links |
| `paper-analysis` | claim extraction precision, evidence-locator accuracy, limitation recall |
| `field-synthesis` | coverage of major research clusters, correct conflict mapping, unsupported synthesis rate |
| `opportunity-discovery` | expert-rated importance, evidence traceability, false-gap rate |
| `hypothesis-development` | problem value, proposal clarity, rationale, measurable outcomes, feasible first test |
| `novelty-audit` | closest-work recall, overlap classification accuracy, counterevidence recall |
| `red-team` | severity-weighted issue recall, actionable objection rate, false-positive burden |
| `decisive-test-design` | ability to inform the next decision, control adequacy, cost of the first test; discrimination when testing mechanisms |
| `belief-update` | correct update direction, calibration, preservation of contradictory evidence |

## Behavioral cases

Check these cases alongside literature accuracy:
- A useful training-recipe change with no theory: develop a rationale and fair comparison, then allow exploration.
- A combination of known components: compare its actual difference and potential benefit, rather than rejecting it for being a combination.
- A claimed improvement obtained with extra compute: propose a matched-budget control.
- A causal explanation: request an intervention or comparison that distinguishes explanations.
- A theorem claim: identify proof obligations; empirical success alone does not establish it.
- An early empirical idea: omit generic disclaimers and a mandatory full red-team pass; identify the next useful test.

## Human review

Use at least two domain experts for high-stakes benchmark cases where feasible. Ask them to annotate independently before adjudication. Record disagreement; expert disagreement is itself a property of the task.

Reviewers should answer:
1. Is the research question important to the field?
2. Are the cited sources the right sources?
3. Does each citation support the attached claim?
4. Did the system find the closest prior work?
5. Is the claimed novelty substantive?
6. Would the first test usefully inform whether to continue or revise?
7. Did the review identify concrete issues that affect the decision, with full red-team review reserved for cases that need it?
8. Would the output change a researcher's decision?

## Reporting

Report per-skill results and failure cases. Avoid a single aggregate "research intelligence score" that hides trade-offs.

Do not use conference acceptance as the primary metric. Acceptance depends on venue fit, timing, execution quality, reviewer variance, and many factors outside the skills' control.

## Release gate

Before calling a version useful:
- factual claims about prior work and observed results have traceable sources; proposed outcomes are identified as proposals;
- closest-work search is documented, including search boundaries;
- unknowns that change a decision have a concrete next action;
- candidates contain a reasonable rationale and observable expected outcomes;
- empirical ideas can advance to a first test without a complete mechanism or proof;
- the final recommendation can be reconstructed from its evidence and decision history.
