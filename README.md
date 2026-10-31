# K Research

**Define a research problem. Find a way to solve it.**

[中文](README.zh-CN.md)

11 composable agent skills for collecting papers, understanding a field, developing research ideas, checking novelty, and planning informative experiments.

## Setup

### Add the marketplace in the Codex GUI

1. Open **Plugins** in the Codex desktop app.
2. Choose **Add marketplace** and enter `HytroZero/k-research`.
3. Confirm to add the marketplace.

### Use with another agent

Download the full repository and keep its directory structure intact. Skills use shared files in `docs/`, `templates/`, and `schemas/`.

Ask your agent to read and follow `skills/<skill-name>/SKILL.md`, using this repository as the root for shared file paths. No separate installation is needed for this workflow.

## Use

Replace `<repo>` with the local repository path:

```text
Read <repo>/skills/ask-k/SKILL.md and help me choose where to start
with research on efficient long-context inference.
```

```text
Read <repo>/skills/discover-research-direction/SKILL.md and follow it
to explore research directions in efficient long-context inference.
```

You can also use any [individual skill](skills/) directly. Direction discovery centers on the problem, proposed method, and difference from prior work. Detailed experiment design follows when experiments or a full research plan are requested, or a developed method is ready for validation. Outputs include paper notes, literature maps, research proposals, and separate experiment plans.

## Research project files

Research outputs use one [standard layout](docs/PROJECT-LAYOUT.md): `README.md` is the human entry point, `research/` holds the overview and direction proposals, and `papers/` holds the complete index, bibliography, notes, and PDFs. Agent-only state, cache, and temporary work stay in `.research/`.

Skills update current documents rather than saving a report per run. Files are created only when needed; experiment plans remain a follow-on deliverable. Existing K Research outputs are consolidated into this layout. Meaningful decision changes stay in `research/decisions.md`; no file snapshots or backup history are generated, including without Git.

## Skills

| Skill | Description |
|---|---|
| [ask-k](skills/ask-k/SKILL.md) | Choose the right skill or short workflow for your current research stage, with a ready-to-use invocation. |
| [discover-research-direction](skills/discover-research-direction/SKILL.md) | Develop worthwhile problems and concrete methods, verify their differences from closest work, and recommend a research direction. |
| [collect-paper](skills/collect-paper/SKILL.md) | Build a screened paper collection for a topic, verify sources, download key PDFs, and save an index and BibTeX bibliography. |
| [paper-analysis](skills/paper-analysis/SKILL.md) | Read an individual paper to explain its question, method, claims, evidence, and limitations, with source locators. |
| [field-synthesis](skills/field-synthesis/SKILL.md) | Connect a body of papers into a field map covering research lines, method evolution, agreements, disagreements, and open questions. |
| [opportunity-discovery](skills/opportunity-discovery/SKILL.md) | Find worthwhile research problems and possible approaches from practical bottlenecks, desired capabilities, observations, and unresolved questions. |
| [hypothesis-development](skills/hypothesis-development/SKILL.md) | Develop a concrete method with a problem-grounded rationale, worked example, closest-work comparison, and expected contribution. |
| [novelty-audit](skills/novelty-audit/SKILL.md) | Search and inspect the closest prior work to assess overlap, identify substantive differences, and support a novelty judgment. |
| [decisive-test-design](skills/decisive-test-design/SKILL.md) | Plan the smallest informative experiment or analysis, specifying comparisons, measurements, and how results guide the next decision; hand the plan to an execution agent. |
| [belief-update](skills/belief-update/SKILL.md) | Incorporate new papers or results into hypotheses and research decisions, recording the evidence and preserving decision history. |
| [red-team](skills/red-team/SKILL.md) | Conduct an optional adversarial review of a developed idea, prioritize consequential objections, and propose concrete probes to resolve them. |

## Documentation

[Architecture](docs/ARCHITECTURE.md) · [Research state](docs/RESEARCH-STATE.md) · [Examples](examples/)

## License

[MIT](LICENSE) © 2026 HytroZero.
