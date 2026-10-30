---
name: research
description: Research router. Use this entry point to choose the right research skill or workflow.
disable-model-invocation: true
---

# Research

You are the front door to the Easy AI Research skill suite. Route the user's research intent to the smallest skill that can solve it.

## Route by intent

| User intent | Route |
|---|---|
| Understand or critique one paper | `paper-analysis` |
| Map a topic or research field | `field-synthesis` |
| Find worthwhile open questions | `opportunity-discovery` |
| Turn an opportunity into a scientific idea | `hypothesis-development` |
| Check whether an idea is genuinely new | `novelty-audit` |
| Stress-test an idea or anticipate reviewer objections | `red-team` |
| Design a first experiment or compare explanations | `decisive-test-design` |
| Incorporate a new paper, result, or counterexample | `belief-update` |
| Start from a domain and discover a research direction end to end | Recommend that the user invoke `discover-research-direction` |

## Routing procedure

1. Read the user's request and any existing project state.
2. Identify the user's immediate decision. Do not route to the full workflow when a focused skill is enough.
3. If one skill clearly fits, name it and invoke it through the host's native skill mechanism when available.
4. If several skills are needed but the user has not asked for a full discovery workflow, explain the short sequence and start with the first useful model-invoked skill.
5. If the user wants the end-to-end workflow, recommend `discover-research-direction`. Because that is also user-invoked, let the user start it; do not invoke another user-invoked skill from this router.
6. If the request is ambiguous in a way that changes the route, ask one concise clarification.

## Routing rules

- Read the target skill's `SKILL.md` before describing its exact procedure.
- Prefer the narrowest useful route.
- Do not start experiment execution or manuscript writing. Hand off a structured research artifact to the user's chosen agent for those tasks.

## Completion

The user knows which skill is appropriate and why, and either the focused skill has started or the user has a clear next invocation.
