# Multi-Agent Task Orchestrator

> **v0.3.0：统一命名迁移。** 本 Skill 用于让 Hermes 判断是否应当委派、拆解任务、选择执行通道、协调多成员、验收结果并持续复盘。A2A、Claude Code、Codex 都是可选通道，而不是强制依赖。

一个供 Hermes Agent 使用的个人 Skill：将复杂任务拆解为可验收的工作包，按收益选择 Hermes 直接执行、内部 `delegate_task` 或 A2A peer，并对最终交付负责。

## 核心能力

- **先判断是否下派**：小型、单一且可验证的任务由 Hermes 直接完成；只有分工带来明确收益时才委派。
- **选择合适通道**：可使用 Hermes 直接执行、`delegate_task` 或能力匹配的 A2A peer；Claude Code 与 Codex 仅是可选成员。
- **安全协作**：避免同一工作树的并行重叠写入；需要并行写代码时使用隔离 worktree。
- **证据化验收**：不把成员口头“已完成”视为完成；必须检查 diff 并取得真实验收结果。
- **自动复盘**：任何实际委派或团队协作任务完成、阻塞或取消后，都保存基于真实证据的复盘记录，推动后续规则改进。
- **授权边界**：未获明确授权时，不提交、推送、创建 PR、部署或发布。

## 使用方式

在新 Hermes 会话中直接描述复杂工作，例如：

```text
使用 multi-agent-task-orchestrator 管理当前任务：
先判断是否值得委派；只在有明确收益时拆分并下派；
小任务由 Hermes 自己完成；最终进行验收和复盘。
不要提交、推送或部署。
```

如果希望特定成员参与，可附加约束：

```text
如有必要，可让 Claude Code 实现，让 Codex 独立审查；但不要为了使用它们而强行派工。
```

## 执行通道

| 通道 | 适用情形 |
|---|---|
| Hermes 直接执行 | 小任务、单一可验证工作包、难以安全拆分的改动 |
| `delegate_task` | 短时、边界明确、适合并行的内部子任务 |
| A2A peer | 已配置且能力匹配的外部或本地执行成员；可支持多轮上下文 |

## 自动复盘

对每个实际发生**委派或团队协作**的任务，Hermes 在完成、阻塞或取消时都会自动创建复盘。独自完成的小任务不强制生成，除非有高风险失败或用户要求记录。

默认保存到当前项目：

```text
docs/retrospectives/YYYY-MM-DD-<简短-kebab-case-任务名>.md
```

同名记录自动追加 `-2`、`-3` 等序号，绝不覆盖历史。复盘包含：任务契约、执行通道、负责人、A2A `context_id`（如有）、变更范围、实际命令与退出码、未运行项、风险和候选规则。

若项目不可写或不存在该目录，Hermes 应改存到本 Skill 仓库；仍无法保存时，必须在最终报告中说明原因。

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
