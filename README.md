# A2A Code Team Orchestrator

一个供 Hermes Agent 使用的个人 Skill：让 Hermes 作为项目总管，通过 A2A 协议协调本地的 Claude Code 与 Codex peer，完成计划、实现、独立审查、测试与验收。

## 目标

- Hermes 负责任务契约、拆解、调度、集成和基于证据的验收。
- Claude Code 与 Codex 是 A2A 对等执行成员，不是 Hermes 内部 `delegate_task` 子代理。
- 禁止同一工作树内对可能重叠的文件并行写入；并行写代码必须使用隔离 worktree。
- 不将“Agent 声称完成”视为完成：必须检查 diff 并运行验收命令。
- 任何提交、推送、创建 PR、部署或发布，都要求用户明确授权。

## 安装

### 作为 Hermes 本地 Skill

将本仓库的 `SKILL.md` 复制或安装到 Hermes 的 Skills 目录；也可通过 Hermes 的 Skills 安装功能使用该仓库的 `SKILL.md` 直链。

启动新会话后，以类似下列方式发出指令：

```text
团结团队：让 Claude Code 实现该仓库的认证重构；让 Codex 独立审查 diff 并补充测试；Hermes 负责协调与最终验收。不要提交、推送或部署。
```

## A2A 前提

需要 Hermes 的 A2A toolset 已启用，并配置可达 peers。当前 Skill 的默认 peer 名称：

- `claude_code`
- `codex`

可先让 Hermes 用 `a2a_list` 和 `a2a_discover` 检查连接与能力。不要在 A2A 消息中发送密码、API key、token 或 `.env` 内容。

## 文档

- [主 Skill](./SKILL.md)
- [持续优化机制](./docs/continuous-improvement.md)
- [复盘记录模板](./docs/retrospective-template.md)
- [变更记录](./CHANGELOG.md)

## 许可证

[MIT](./LICENSE)
