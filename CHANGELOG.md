# Changelog

所有值得复用的行为变化都记录在此文件中。

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

## [0.1.1] - 2026-08-29

### Added

- 每个实际使用 A2A peer 的团队任务结束、阻塞或取消时，Hermes 必须自动生成独立复盘记录。
- 标准化复盘路径：`docs/retrospectives/YYYY-MM-DD-<任务名>.md`；同名文件按序号保留，不覆盖历史。
- 复盘必须记录实际证据、命令与退出状态；未运行项目必须明确标记并说明原因。
- 复盘候选规则的写回门槛与版本化要求。

## [0.1.0] - 2026-08-29

### Added

- 初始版本：Hermes 通过 A2A 协调 Claude Code 与 Codex peer。
- 任务契约、角色分工、工作树写入隔离、A2A `context_id` 连续性和最终验收规则。
- 面向真实任务复盘的持续优化设计与模板。
