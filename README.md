# K Research Skills

A composable skill suite for scientific research reasoning: understanding a field, finding research opportunities, developing testable ideas, comparing prior work, reviewing key risks, designing informative tests, and updating beliefs from new evidence.

**Product boundary:** this suite owns research intelligence and research decisions. It does not implement experiments, SSH/GPU orchestration, budget management, or manuscript writing. Those jobs belong to execution and writing agents that consume the research artifacts produced here.

## Design principles

- **Small and composable:** each model-invoked skill owns one research discipline.
- **Explicit process:** skills define steps, evidence requirements, decision gates, and completion criteria.
- **Progressive disclosure:** `SKILL.md` contains the procedure; deeper frameworks live in `docs/references/`.
- **Persistent research state:** papers, claims, evidence, hypotheses, and decisions are structured artifacts with stable IDs.
- **Evidence before confidence:** conclusions distinguish direct evidence, inference, absence of evidence, and unknowns.
- **Exploration first:** develop candidates from worthwhile problems, reasonable intuition, and feasible tests.
- **Evidence matched to contribution:** empirical ideas can advance without a formal proof or complete mechanism explanation.
- **Focused review:** compare closest work, then resolve risks that affect the next experiment. Full red-team review is available on demand.

The suite is inspired by the small, composable, user-invoked/model-invoked design in Matt Pocock's `mattpocock/skills`. It is an independent research-focused implementation, not a copy of that repository.

## Skill catalogue

### User-invoked skills

| Skill | Use |
|---|---|
| `research` | Router. Helps choose the right research skill or workflow. |
| `discover-research-direction` | Orchestrates the complete path from field understanding to a promising direction with a practical first test. |

User-invoked skills are marked with `disable-model-invocation: true` and `policy.allow_implicit_invocation: false` for Codex. A user-invoked skill may call model-invoked skills, but it must not invoke another user-invoked skill.

### Model-invoked skills

| Skill | Use |
|---|---|
| `paper-analysis` | Extracts a paper's question, contribution, mechanism, assumptions, claims, evidence, and limitations. |
| `field-synthesis` | Synthesizes a body of papers into a structured map of methods, claims, debates, and boundaries. |
| `opportunity-discovery` | Finds research opportunities grounded in tensions, failures, assumptions, and unresolved questions. |
| `hypothesis-development` | Develops a concrete proposal, rationale, expected outcome, and first test. |
| `novelty-audit` | Tests whether the proposed contribution is substantively distinct from the closest prior work. |
| `red-team` | Provides a full adversarial review when requested or needed for a concrete concern. |
| `decisive-test-design` | Designs the smallest informative comparison or test of explanations. |
| `belief-update` | Updates the research state when new papers, results, or counterevidence arrive. |

Model-invoked skills can be called directly by the user or discovered by an agent from their descriptions.

## Recommended workflow

```text
/research
   |
   +-- one paper ----------------------> paper-analysis
   |
   +-- map a field --------------------> field-synthesis
   |
   +-- find a research opportunity ----> opportunity-discovery
   |
   +-- deepen an idea -----------------> hypothesis-development
   |
   +-- check novelty ------------------> novelty-audit
   |
   +-- challenge an idea --------------> red-team
   |
   +-- design a discriminating test ---> decisive-test-design
   |
   +-- incorporate new evidence -------> belief-update

/discover-research-direction
   |
   +--> paper-analysis
   +--> field-synthesis
   +--> opportunity-discovery
   +--> hypothesis-development
   +--> novelty-audit
   +--> focused risk check (full red-team review on demand)
   +--> decisive-test-design
   +--> Research Brief + decision record
```

Develop candidates before judging them. Compare the closest work, then plan a first test for the strongest ideas. Simple modifications and combinations are assessed by their value and empirical differences.

## Repository layout

```text
easy-ai-research-skills/
├── README.md
├── GLOSSARY.md
├── skills/
│   ├── research/
│   ├── discover-research-direction/
│   ├── paper-analysis/
│   ├── field-synthesis/
│   ├── opportunity-discovery/
│   ├── hypothesis-development/
│   ├── novelty-audit/
│   ├── red-team/
│   ├── decisive-test-design/
│   └── belief-update/
├── docs/
│   ├── ARCHITECTURE.md
│   ├── RESEARCH-STATE.md
│   ├── MCP-CONTRACT.md
│   ├── EVALUATION.md
│   └── references/
├── schemas/
├── templates/
└── examples/
```

## Installation

Install the **whole suite** when possible. Several skills point to shared reference documents under `docs/references/`; installing isolated skill folders without those references reduces their effectiveness.

### Claude Code

Copy the `skills/` directories into the project's `.claude/skills/` directory, preserving each skill folder.

### Codex

Copy the `skills/` directories into the project's `.agents/skills/` directory, preserving each skill folder and its `agents/openai.yaml` metadata.

### Other agents

Use the agent's supported Agent Skills directory or the `skills` CLI. When publishing this repository to GitHub, it can be installed through the Skills ecosystem using the repository identifier. Check the target host's current skill-discovery and invocation rules.

The suite uses standard `SKILL.md` frontmatter plus Codex metadata. Some hosts may ignore `disable-model-invocation`; on those hosts, keep the two user-invoked skills out of automatic discovery or configure their equivalent manual-only policy.

## How to use

- Start with `/research` when you are unsure which research operation is appropriate.
- Start with `/discover-research-direction` when you want a complete, guided exploration.
- Invoke model skills directly when you already know the task, for example `novelty-audit` on an existing idea.
- Give skills a project directory containing the research artifacts, or ask them to produce a self-contained Markdown result when no persistent workspace exists.
- Ask the agent to preserve source URLs, DOI/arXiv identifiers, page/section/figure/table locators, and retrieval dates.

## Shared research state

The canonical artifact definitions are in `docs/RESEARCH-STATE.md` and `schemas/`. The templates under `templates/` are human-readable renderings of those artifacts.

Research history should be append-only: new evidence and decisions create new records or superseding versions. Do not silently rewrite a past decision. This makes the evolution of a research direction inspectable.

## MCP integration

The skills do not assume a particular MCP implementation. See [`docs/MCP-CONTRACT.md`](docs/MCP-CONTRACT.md) for a minimal tool/resource contract. The MCP layer should provide paper retrieval and persistent research-state operations. It should not grow into an experiment runner or manuscript-generation platform.

## Research quality

Use source-backed comparisons, relevant baselines, and tests that inform the next decision. Theory and mechanism analysis follow the contribution type; uncertainty belongs in the output when it changes an action or interpretation.

See [`docs/EVALUATION.md`](docs/EVALUATION.md) for the proposed evaluation protocol.
