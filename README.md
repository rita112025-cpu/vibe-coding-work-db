# 工作用 Vibe Coding 資料庫

> 從 mcpservers.org 篩出工作中真的會用到的。拒絕玩具範例，只留能直接放進日常開發、文件處理、測試驗證的 Skills 與 MCP，複製即用。

**線上版：** https://rita112025-cpu.github.io/vibe-coding-work-db/

## 特色

- **16 個精選**：已按工作情境分類（工程開發 / 設計整合 / 測試與驗證 / 工作流程 / MCP Servers）
- **雙模式支援**：右上角一鍵切換
  - `Claude`：`.claude/commands/` / `mcp.json` 用法
  - `Codex`：`.codex/` / `config.toml` 用法，VS Code 原生支援
- **可直接複製安裝**：每個卡片都有 `何時用` + 複製按鈕
- **PRACTICAL / WORK-READY / CURATED**

## 雙模式怎麼用

線上版右上角有兩個切換：

- `AGENT: Claude | Codex`：切換指令格式
  - Claude 版複製的是 `npx add-skill ...` 或 `.claude/settings.json` 片段
  - Codex 版複製的是 `codex skill install ...` 或 `config.toml` 片段
- `THEME: ☀️ / 🌙`：淺色深色

## VS Code + Codex 設定

本 repo 已內建範本：

```
.vscode/mcp.json              # VS Code MCP 設定
.codex/config.toml.example    # Codex CLI 設定範本
AGENTS.md                     # 告訴 Codex 這個 repo 有哪些 skills
```

### 安裝步驟

1. Clone 本專案
2. VS Code 安裝擴充 `Codex`
3. `Ctrl+Shift+P` → `Codex: Open Chat` → 輸入「列出這個專案的可用 skills」
4. 需要 MCP Server 的，照卡片上的「可直接複製安裝」貼上即可

```bash
# 範例：安裝 fe-arch
# Claude
npx claude-code-templates add fe-arch

# Codex
codex skill install fe-arch
```

## 本機開發

這是純靜態站，一個 `index.html` 就是全部。

```bash
# 直接開
open index.html
# 或用 serve
npx serve .
```

## 目錄結構

```
.
├── index.html                  # 主站（雙模式版）
├── AGENTS.md                   # Codex 說明檔
├── .vscode/mcp.json            # VS Code MCP
└── .codex/config.toml.example  # Codex 設定範本
```

## 授權

MIT

---
Made with ❤️ for 工作用 Vibe Coding
