---
name: textbook-style-explanation
description: Explain a theory, hypothesis, method, concept, or principle in clear textbook-style prose, or rewrite technical material for understanding. Use when the user asks to explain, teach, or understand how an idea works, with or without a research project.
---

# Textbook Style Explanation

Teach the reader how an idea works, why we need it, and how each step of the reasoning holds together—in the spirit of Gilbert Strang's *Introduction to Linear Algebra* and Adrian Banner's *The Calculus Lifesaver*. Write like a great teacher at the blackboard: direct, warm, and concrete, thinking out loud with the reader rather than reciting a reference manual.

This is a standalone teaching skill. The subject can come from any discipline, a supplied passage, or a direct question; no research project, literature workflow, or fixed chapter template is required.

## Calibrate to the reader and source

Match the reader's language, background, and target depth from the prompt, asking only when an ambiguity would lead to the wrong explanation. Fold missing prerequisites in right where they are needed instead of opening with a long remedial detour.

When working from supplied or cited material, inspect it before attributing claims and keep its assumptions intact while reorganizing the exposition for clarity. If the subject is a proposed hypothesis or untested method, make its internal logic clear while keeping its premises, proposed mechanism, and unestablished predictions distinct.

## How to build understanding

Use the teaching moves that fit the subject rather than marching through a rigid checklist:

- **Start with the problem that forces the idea into existence.** Open with a concrete question, a physical or geometric picture, or the exact point where a naive approach breaks down. For instantaneous velocity, show why dividing distance by a finite time interval only ever gives an average, so the reader feels the need for a limit before seeing the derivative formula.
- **Concrete numbers and small cases before general notation.** Like Strang, put a small, tangible example on the board early—a $2 \times 2$ case, a three-token sequence, a toy physical system—and work it far enough that the reader can see the mechanism operating in plain sight before or alongside the general formula.
- **Look at the central object from two angles.** Pair algebra with geometry, a formula with the computation it performs, or an objective function with the force it exerts on the variables. Understanding clicks when two views of the same thing line up.
- **Think out loud before the tricky step.** Like Banner, never pull a transformation, substitution, or auxiliary construction out of a hat. Pause before the move to say *why* we are doing it, what obstacle it clears, and why a tempting shortcut fails. Spend your words on the real conceptual bottlenecks, not on routine algebra or repetitive summaries.
- **Layer rigor honestly.** Keep intuition, heuristic derivation, formal proof, and empirical observation distinct. State the assumptions that actually do work in a step, and point out where an analogy stops holding. If a full proof would derail the explanation, give the core mechanism and name what remains to be proved; if the proof *is* the subject, walk through it completely.

## Voice and notation

Write in clear, conversational paragraphs that carry a continuous train of thought. Direct questions (*"What happens if $\lambda = 0$?"*) and brief, natural asides keep the reader engaged without turning the prose into a scripted dialogue. Never write "it is obvious," "clearly," or "trivially"—if a step is worth mentioning, show how it works.

Demystify every piece of notation on the spot:
- Translate what an equation is actually saying into plain words, and connect it grammatically to the surrounding prose.
- Explain every symbol the reader needs to parse the expression—variables, functions, sets, constants, indices, subscripts, superscripts, and operators—before or right beside its first appearance, and again if its role changes. A brief inline phrase is often enough; use a compact symbol list or table when an expression introduces many moving parts at once.

Let the subject dictate the layout. Use headings, diagrams, tables, or worked examples when they clarify the structure; skip textbook boilerplate such as exercises, historical preambles, or end-of-chapter recaps unless requested.

## Deliver and verify

Deliver the explanation directly in the conversation unless the user asks to write or edit a file. Use the user's requested path for standalone files; do not create research state, proposals, or experiment plans as a side effect.

Before finishing, read the explanation from the reader's seat: every term and symbol is introduced when needed, no consequential step leaps across a gap, the worked numbers match the general formula, and the ending resolves the opening question. Fix any gap in the prose itself rather than appending a checklist or process report.
