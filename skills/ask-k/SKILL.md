---
name: ask-k
description: Ask which K Research skill or workflow fits your current situation.
disable-model-invocation: true
---

# Ask K

Help the researcher choose where to start and what to do next. Read the relevant skill's `SKILL.md` before describing its behavior or recommending that a step be skipped. The map below is for orientation; each skill owns its detailed procedure.

## Main flow: direction to first experiment

1. **`collect-paper`** takes a broad topic and builds a screened paper collection, an index, BibTeX, and key local PDFs. Start here when the researcher needs reading material.
2. **`paper-analysis`** reads individual papers; **`field-synthesis`** connects their methods and findings into a field map. Use the former for a particular paper and the latter for a body of work.
3. **`opportunity-discovery`** identifies worthwhile problems and possible approaches from the literature, observations, or task needs.
4. **`hypothesis-development`** turns an opportunity into a concrete proposal with a rationale, expected outcome, and practical first comparison. Empirical ideas can advance without a complete mechanism explanation or formal proof.
5. **`novelty-audit`** compares developed candidates with their closest prior work and clarifies the actual difference.
6. **`decisive-test-design`** plans the smallest informative experiment or analysis for the strongest candidates, addressing concrete issues that affect interpretation. Hand the plan to an execution agent to implement and run it.
7. **`belief-update`** incorporates returned results or new papers and revisits the research decision. Continue with a revised idea, a targeted literature check, or a follow-up test according to what changed.

For an end-to-end investigation, recommend **`discover-research-direction`**. It coordinates collection, understanding, candidate development, comparison, focused risk checks, and a Research Brief. It is a separate user-invoked workflow: give the researcher the invocation rather than starting it from this router.

## Enter where the work is

| Current situation | Starting point |
|---|---|
| A broad topic, but no paper collection | `collect-paper` |
| One paper to understand | `paper-analysis` |
| Papers collected, relationships unclear | `field-synthesis` |
| Familiar with the field, looking for useful problems | `opportunity-discovery` |
| An idea that needs a concrete method and testable outcome | `hypothesis-development` |
| A developed idea that may overlap existing work | `novelty-audit` |
| A candidate ready for an initial experiment | `decisive-test-design` |
| New experimental results, papers, or counterexamples | `belief-update` |
| A requested adversarial review or a specific concern needing deeper scrutiny | `red-team` |
| A full investigation from a research area to a selected direction | `discover-research-direction` |

Reuse existing artifacts and enter at the relevant stage. Full `red-team` review is optional; ordinary candidate development does not require it. Experiment execution and manuscript writing are handed to the researcher's chosen execution or writing agent.

## Choose and respond

1. Read the request and inspect relevant existing project artifacts to establish the current stage. Ask one focused question only when the answer changes the route.
2. Read the candidate skills and choose the smallest useful route. If several are needed, explain the short sequence and the immediate starting point.
3. By default, respond with the recommended skill, why it fits, and a ready-to-use invocation containing the user's topic or task. Wait for the researcher to choose before starting work.
4. If the researcher explicitly asks to choose and start, invoke the selected model-invoked skill through the host's Skill mechanism, or read and follow its instructions when that mechanism is unavailable. The end-to-end user-invoked workflow remains a recommendation for the researcher to start.

## Completion

The researcher knows which skill fits, why, and what to invoke next. When choosing and starting was explicitly requested, the selected model-invoked skill has begun.
