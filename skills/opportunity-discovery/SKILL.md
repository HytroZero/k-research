---
name: opportunity-discovery
description: Find worthwhile research problems from practical bottlenecks, desired capabilities, empirical observations, and unresolved questions.
---

# Opportunity Discovery

Identify problems worth solving and promising starting points for solutions.

## Project files

Before writing project files, read [Project Layout](../../docs/PROJECT-LAYOUT.md) and follow its destinations, update rules, and completion checks. Update the problems and candidate comparison in `research/overview.md`. Create a direction proposal only when an opportunity is developed into a distinct candidate.

## Process

1. **Read the context.** Inspect the field map, relevant papers, project constraints, and prior decisions.
2. **Look for high-leverage openings.** Examine the task and literature through multiple lenses:
   - **Concrete bottlenecks:** where current approaches fail, degrade, or incur prohibitive cost, and what consequence follows.
   - **Shared assumptions:** premises that competing methods all take for granted, especially complexity that might be removed or inverted.
   - **Problem reframing and analogies:** whether the difficulty becomes simpler under a different representation, objective, or a mechanism from an adjacent domain.
   - **Unexplained observations or measurement blind spots:** anomalies, conflicting findings (after checking experimental conditions), or properties existing benchmarks miss.
3. **Ground the problem.** Explain how relevant methods approach the difficulty and why it remains open. Connect factual claims about prior work or empirical behavior to sources, measurements, or explicit task requirements; distinguish corpus gaps from field gaps.
4. **Make the core tension concrete.** Use a small concrete scenario or task instance to show where current behavior falls short and what a good solution must do.
5. **Sketch initial angles.** Propose what could change—a new mechanism, a simplification, a reframed objective, or a combination—and why it might work. Note obvious neighboring work, but let the problem drive the direction before filtering by literature overlap.
6. **Prioritize problems.** Assess problem value, room for a substantive contribution, and basic feasibility under project constraints. Name missing information that affects the choice.

## Output

For each opportunity, include the problem and setting, practical or scientific consequence, why existing approaches leave it open (or what shared assumption they rely on), a concrete scenario, and one or more candidate solution angles. Cite the sources or task requirements that motivate it. Detailed methods belong to `hypothesis-development`; experiments belong to a later stage.

Simple changes, simplifications, and combinations can support valuable research. Judge them by the problem they address and the value of a successful solution.

## Completion criterion

The researcher can explain why each shortlisted problem matters, what current approaches leave unresolved or assume away, and which solution angle is worth developing next. An experiment plan is not required to establish a research opportunity.
