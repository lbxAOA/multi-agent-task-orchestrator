# Changelog

所有值得复用的行为变化都记录在此文件中。

## [0.4.0] - 2026-09-02

### Added

- 新增结构化多智能体讨论流程：任务契约、独立定性分析、Hermes 中继交叉质询、定性归纳、定量方案比较、失败预演和执行计划。
- 新增默认 0–5 分决策矩阵、风险暴露、三点时间估算、敏感性分析和置信度规则。
- 新增讨论停止条件，避免无限对话、多数票决策和按模型品牌决策。
- 新增 `docs/structured-deliberation.md` 和 `docs/execution-plan-template.md`。

### Changed

- 明确 `a2a_orchestrate` 只是扇出收集；真正的 Agent 相互讨论必须由 Hermes 显式转发前一轮结果。
- 讨论阶段默认只读；写入必须在执行计划形成后进行。
- 保持复盘按需启用，不因加入讨论流程而恢复自动复盘。

## [0.3.1] - 2026-09-02

### Changed

- 将强制自动复盘改为按需复盘。
- 只有用户或任务契约明确启用，或维护者明确要求分析团队表现时，才创建复盘记录。
- 明确未创建复盘时不得虚构复盘文件，也不影响任务完成判定。
- 保留复盘模板和持续优化文档，供需要时使用。

## [0.3.0] - 2026-08-31

### Renamed

- Skill slug 从 `a2a-code-team-orchestrator` 更名为 `multi-agent-task-orchestrator`。
- GitHub 仓库同步更名为 `lbxAOA/multi-agent-task-orchestrator`。

### Changed

- 名称与实际能力对齐：通用任务拆解、按收益委派、多智能体协作、独立审查、验收与复盘。
- 统一 README、复盘模板与持续优化文档中的通用多智能体表述。

## [0.2.0] - 2026-08-31

### Changed

- 从强制 A2A / Claude Code / Codex 的代码团队规则升级为通用多智能体任务总管。
- Hermes 先判断委派是否带来明确收益，再按任务边界、能力匹配、风险、并行收益和验收成本选择直接执行、`delegate_task` 或 A2A peer。
- A2A 中的 Claude Code 与 Codex 改为可选执行成员，不再是每个任务的硬性前提。
- 自动复盘触发条件扩展为任何实际委派或多成员协作任务；复盘模板新增执行通道字段。

## [0.1.0] - 2026-08-29

### Added

- 初始版本：Hermes 通过 A2A 协调 Claude Code 与 Codex peer。
- 任务契约、角色分工、工作树写入隔离、A2A `context_id` 连续性和最终验收规则。
