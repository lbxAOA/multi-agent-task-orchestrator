# Multi-Agent Task Orchestrator

> **v0.3.1：复盘改为可选。** 本 Skill 用于让 Hermes 判断是否应当委派、拆解任务、选择执行通道、协调多成员和验收结果。A2A、Claude Code、Codex 都是可选通道；复盘只在用户或任务契约明确启用时进行。

一个供 Hermes Agent 使用的个人 Skill：将复杂任务拆解为可验收的工作包，按收益选择 Hermes 直接执行、内部 `delegate_task` 或 A2A peer，并对最终交付负责。

## 核心能力

- **先判断是否下派**：小型、单一且可验证的任务由 Hermes 直接完成；只有分工带来明确收益时才委派。
- **选择合适通道**：可使用 Hermes 直接执行、`delegate_task` 或能力匹配的 A2A peer；Claude Code 与 Codex 仅是可选成员。
- **安全协作**：避免同一工作树的并行重叠写入；需要并行写代码时使用隔离 worktree。
- **证据化验收**：不把成员口头“已完成”视为完成；必须检查 diff 并取得真实验收结果。
- **可选复盘**：只有用户或任务契约明确启用时，才保存基于真实证据的复盘记录；未启用时不创建复盘文件。
- **授权边界**：未获明确授权时，不提交、推送、创建 PR、部署或发布。

## 使用方式

在新 Hermes 会话中直接描述复杂工作，例如：

```text
使用 multi-agent-task-orchestrator 管理当前任务：
先判断是否值得委派；只在有明确收益时拆分并下派；
小任务由 Hermes 自己完成；最终进行验收。
本次任务启用复盘，并将记录保存到 docs/retrospectives/。
不要提交、推送或部署。
```

如果希望特定成员参与，可附加约束：

```text
如有必要，可让 Claude Code 实现，让 Codex 独立审查；但不要为了使用它们而强行派工。

如果不需要复盘，可明确说：本次任务不要生成复盘文件。
```

## 执行通道

| 通道 | 适用情形 |
|---|---|
| Hermes 直接执行 | 小任务、单一可验证工作包、难以安全拆分的改动 |
| `delegate_task` | 短时、边界明确、适合并行的内部子任务 |
| A2A peer | 已配置且能力匹配的外部或本地执行成员；可支持多轮上下文 |

## 可选复盘（v0.3.1）

复盘不是默认动作，也不是任务完成条件。只有以下情况才创建复盘文件：

- 用户明确要求；
- 任务契约明确启用复盘；
- 用户提供历史复盘并明确要求据此改进 Skill。

发生重大故障时，Hermes 可以建议复盘，但未经明确启用不得自动创建。

启用后，复盘默认保存到当前项目：

```text
docs/retrospectives/YYYY-MM-DD-<简短-kebab-case-任务名>.md
```

同名记录追加 `-2`、`-3` 等序号，绝不覆盖历史。复盘包含任务契约、执行通道、负责人、A2A `context_id`（如有）、变更范围、实际命令与退出码、未运行项、风险和候选规则。

若未启用复盘，Hermes 不创建复盘文件，也不得声称已经生成。项目不可写或不存在该目录时，且复盘已经启用，Hermes 才改存到本 Skill 仓库；仍无法保存时，必须在最终报告中说明原因。

## 安装

本地安装后，Skill slug 为：

```text
multi-agent-task-orchestrator
```

GitHub：<https://github.com/lbxAOA/multi-agent-task-orchestrator>

主 Skill 原始文件：

```text
https://raw.githubusercontent.com/lbxAOA/multi-agent-task-orchestrator/main/SKILL.md
```

## 文档

- [主 Skill](./SKILL.md)
- [持续优化机制](./docs/continuous-improvement.md)
- [复盘记录模板](./docs/retrospective-template.md)
- [变更记录](./CHANGELOG.md)

## 许可证

[MIT](./LICENSE)
