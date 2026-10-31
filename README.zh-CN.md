# K Research

**定义一个研究问题，找到解决它的方法**

[English](README.md)

11 个可组合的研究技能，帮助智能体收集论文、梳理领域、发展研究想法、检查新颖性和设计实验。

## 准备

### 在 Codex GUI 中添加 marketplace

1. 在 Codex 桌面应用中打开 **Plugins（插件）**。
2. 选择 **Add marketplace（添加市场）**，输入 `HytroZero/k-research`。
3. 确认添加 marketplace。

### 在其他智能体中使用

下载完整仓库并保留目录结构。技能会使用 `docs/`、`templates/` 和 `schemas/` 中的共享文件。

让智能体读取并遵循 `skills/<技能名>/SKILL.md`，以本仓库为根目录解析共享文件路径。此用法无需单独安装。

## 使用

将 `<repo>` 替换为本地仓库路径：

```text
读取 <repo>/skills/ask-k/SKILL.md，帮我判断
高效长上下文推理的研究应该从哪里开始。
```

```text
读取并遵循 <repo>/skills/discover-research-direction/SKILL.md，
探索高效长上下文推理的研究方向。
```

也可以直接使用任一[独立技能](skills/)。方向探索默认围绕问题、方法及其与已有工作的区别展开。用户要求实验或完整研究计划，或具体方法进入验证阶段时，再展开详细实验设计。产出包括论文笔记、领域梳理、研究方案和独立的实验计划。

## 研究项目文件

研究产物采用统一的[目录合同](docs/PROJECT-LAYOUT.md)：`README.md` 是人类阅读入口，`research/` 保存领域梳理与各方向方案，`papers/` 保存完整文献索引、统一书目、笔记和原文。agent 内部状态、缓存和临时工作统一放在 `.research/`。

技能更新当前文档，不按运行次数生成报告。文件按需创建，实验计划仍是后续工作。已有 K Research 产物统一归入标准目录。重要判断变化记录在 `research/decisions.md`；包括非 Git 项目在内，均不生成文件快照或备份历史。

## 技能一览

| 技能 | 描述 |
|---|---|
| [ask-k](skills/ask-k/SKILL.md) | 根据当前研究阶段选择合适的技能或简短工作流，并提供可直接使用的调用指令。 |
| [discover-research-direction](skills/discover-research-direction/SKILL.md) | 从研究领域出发，明确值得解决的问题、发展具体方法、核实与最接近工作的区别，并给出方向建议。 |
| [collect-paper](skills/collect-paper/SKILL.md) | 围绕主题检索和筛选论文，核实来源，下载关键 PDF，并建立论文索引和 BibTeX 文献库。 |
| [paper-analysis](skills/paper-analysis/SKILL.md) | 深入分析单篇论文的研究问题、方法、主张、证据和局限，并标注原文位置。 |
| [field-synthesis](skills/field-synthesis/SKILL.md) | 将多篇论文整合为领域图谱，梳理研究路线、方法演变、共识、分歧和未解决的问题。 |
| [opportunity-discovery](skills/opportunity-discovery/SKILL.md) | 从实际瓶颈、目标能力、实验观察和未解决的问题中，发现值得研究的问题及可能的解决思路。 |
| [hypothesis-development](skills/hypothesis-development/SKILL.md) | 将研究机会发展为具体方法，讲清问题与设计的对应关系、贯穿示例、已有工作差异和预期贡献。 |
| [novelty-audit](skills/novelty-audit/SKILL.md) | 检索并阅读最接近的已有工作，核查重叠之处和实质差异，形成有来源支持的新颖性判断。 |
| [decisive-test-design](skills/decisive-test-design/SKILL.md) | 设计能指导下一步决策的最小实验或分析，明确对比、测量指标及结果对应的行动，并将计划交给执行智能体。 |
| [belief-update](skills/belief-update/SKILL.md) | 根据新论文或实验结果更新研究假设和决策，记录证据与变更理由，保留历史判断。 |
| [red-team](skills/red-team/SKILL.md) | 对已发展的想法进行可选的对抗性审查，优先识别影响研究决策的反对意见，并提出具体的验证办法。 |

## 文档

[架构](docs/ARCHITECTURE.md) · [研究状态](docs/RESEARCH-STATE.md) · [示例](examples/)

## 许可证

[MIT](LICENSE) © 2026 HytroZero。
