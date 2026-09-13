# AGENTS.md - Codex 會階層讀取

這個專案使用 Agent Skills 標準，Claude Code 和 Codex 共用同一套 SKILL.md

## 已安裝 Skills 位置
- 全域: ~/.agents/skills/
- 專案: .agents/skills/ 或 .codex/skills/

從本站安裝: https://rita112025-cpu.github.io/vibe-coding-work-db/
切到 Codex 模式複製指令

## MCP Servers
- context7: 即時抓最新官方文件
- github: 直接操作 repo / PR / issue
- postgres: 查 schema / 跑 SQL

設定參考: .codex/config.toml.example 和 .vscode/mcp.json

## 工作流
- 新增功能前: /fe-arch
- 收到需求: /fe-issue
- 完成前驗證: /verification-before-completion
