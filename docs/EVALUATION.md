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
| `hypothesis-development` | problem specificity, method clarity, design-to-difficulty correspondence, worked-example consistency, substantive difference from known work |
| `novelty-audit` | closest-work recall, overlap classification accuracy, counterevidence recall |
| `red-team` | severity-weighted issue recall, actionable objection rate, false-positive burden |
| `decisive-test-design` | ability to inform the next decision, control adequacy, cost of the first test; discrimination when testing mechanisms |
| `belief-update` | correct update direction, calibration, preservation of contradictory evidence |

## Behavioral cases

Check these cases alongside literature accuracy:
- A useful training-recipe change with no theory: explain the concrete change and why it addresses the problem; leave detailed validation to the experiment stage.
- A combination or simplification of known components: compare its actual difference and potential benefit, rather than rejecting it for being simple or a combination.
- A close neighbor that already solves the problem: reframe the problem, find a genuinely simpler or stronger mechanism, or set the idea aside rather than bolting on defensive complexity just to look different.
- A claimed improvement obtained with extra compute: propose a matched-budget control.
- A causal explanation: request an intervention or comparison that distinguishes explanations.
- A theorem claim: identify proof obligations; empirical success alone does not establish it.
- An early empirical idea: develop the problem and method with a worked example; identify the next design or literature question.
- A direction-discovery request: deliver a problem-and-method recommendation without requiring an experiment plan.
- An explicit full research-plan request: complete problem and method development, then produce a separate, linked experiment plan without an extra approval gate.
- A familiar method presented under a new name: use neighboring work during development to expose overlap before a formal audit.
- An undefined central score or operation: identify the missing method design rather than compensate with detailed baselines.
- A cheap experiment attached to a weak problem: prioritize problem value and method fit over experimental convenience.

## Human review

Use at least two domain experts for high-stakes benchmark cases where feasible. Ask them to annotate independently before adjudication. Record disagreement; expert disagreement is itself a property of the task.

Reviewers should answer:
1. Is the research question important to the field?
2. Are the cited sources the right sources?
3. Does each citation support the attached claim?
4. Did the system find the closest prior work?
5. Is the claimed novelty substantive?
6. Does the method address the stated difficulty, and can its steps be followed through the example?
7. Did the review identify concrete issues that affect the decision, with full red-team review reserved for cases that need it?
8. Would the output change a researcher's decision?
9. When an experiment plan was requested, would it usefully inform whether to continue or revise?

## Reporting

Report per-skill results and failure cases. Avoid a single aggregate "research intelligence score" that hides trade-offs.

Do not use conference acceptance as the primary metric. Acceptance depends on venue fit, timing, execution quality, reviewer variance, and many factors outside the skills' control.

## Release gate

Before calling a version useful:
- factual claims about prior work and observed results have traceable sources; proposed outcomes are identified as proposals;
- closest-work search is documented, including search boundaries;
- unknowns that change a decision have a concrete next action;
- candidates explain the problem, method, design rationale, worked example, and expected contribution relative to known work;
- direction discovery can complete before detailed experiment planning, while explicit experimental requests receive an actionable plan;
- the final recommendation can be reconstructed from its evidence and decision history.
