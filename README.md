# 工作用 Vibe Coding 資料庫

> 從 mcpservers.org 篩出工作中真的會用到的 Skills 與 MCP。拒絕玩具範例，每項都標出安裝狀態，審查後選用。

**線上版：** https://rita112025-cpu.github.io/vibe-coding-work-db/

## 特色

- **16 項，分三種狀態**：9 個 Skill 審查後可裝、4 個來源不符暫停安裝、3 個 MCP Server 需另外設定
- **按工作情境分類**：工程開發 / 設計整合 / 測試與驗證 / 工作流程 / MCP Servers
- **雙模式**：右上角切換 Claude / Codex，安裝指令與說明跟著換
- **每張卡片**：何時用、安裝狀態、注意事項、來源目錄連結；可安裝的才有複製按鈕
- **PRACTICAL / WORK-READY / CURATED / REVIEW FIRST**

## 建議先裝的四項

1. `fe-arch`
2. `fe-issue`
3. `fe-code-review`（依賴 Claude Code 工具與 plugin；Codex 只能當審查清單）
4. `verification-before-completion`（來源：obra/superpowers）

其他項目等真的需要再裝。第三方 Skill 可能含腳本或引用其他資料夾，安裝前讀完整 SKILL.md、引用檔案與權限。

## 雙模式怎麼用

線上版右上角有兩個切換：

- `AGENT: Claude | Codex`：切換安裝指令
  - Claude：`npx openskills install <repo>`，再互動勾選需要的 skill（不用 `#skill` 後綴，不要全選）。預設裝到專案 `.claude/skills`，加 `--global` 改裝到 `~/.claude/skills`。OpenSkills 是第三方工具，需要 Node.js 20.6+ 與 Git。Claude Code 會直接讀 skills 資料夾，不必跑 `npx openskills sync`（在本 repo 執行會在 AGENTS.md 末尾追加一段規則）。
  - Codex：用 Codex 內建的 skill-installer 腳本指定路徑安裝，需要 Python。Windows 的 `python` 若顯示 Python was not found，改用 `py`；`$HOME` 在 cmd.exe 不會展開，請用 PowerShell。預設裝到 `$CODEX_HOME/skills`（未設定時為 `~/.codex/skills`，有設 `CODEX_HOME` 時把指令裡的 `$HOME/.codex` 換掉）；官方文件列出的位置是專案 `.agents/skills` 與個人 `$HOME/.agents/skills`，需要時加 `--dest`。
- `THEME: ☀️ / 🌙`：淺色深色

MCP Server 與暫停安裝的項目不提供複製指令。

### 範例：安裝 fe-arch

```bash
# Claude：執行後在互動清單只勾 fe-arch
npx openskills install jackyu/claude-skills

# Codex
python "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" --repo jackyu/claude-skills --path skills/fe-arch --name fe-arch
```

fe-issue、fe-code-review、fe-mr-review 會引用 `skills/_shared`，fe-code-review 另外引用 `fe-guardrails`。`_shared` 沒有 SKILL.md，兩種安裝方式都不會帶上：

- Claude：加 `--global` 安裝（一起勾選 fe-guardrails），再把 repo 的 `skills/_shared` 複製到 `~/.claude/skills/_shared`
- Codex：fe-code-review 只當審查清單用，GitHub 專案也用不到 fe-issue 的 GitLab 步驟，可以略過

## VS Code + Codex 設定

本 repo 內建範本：

```
.vscode/mcp.json              # VS Code 內建 MCP 範本
.codex/config.toml.example    # Codex MCP 範本（CLI 與 IDE 擴充共用）
AGENTS.md                     # Codex 的 skill 觸發規則（Claude Code 讀 CLAUDE.md，可用 @AGENTS.md 引用）
```

### 安裝步驟

1. Clone 本專案
2. VS Code 安裝擴充 `Codex`
3. `Ctrl+Shift+P` → `Codex: Open Chat` → 輸入「列出這個專案的可用 skills」
4. MCP Server 依官方文件另外設定：GitHub 需要認證，Postgres 需要資料庫連線（參考伺服器已封存）。範本只是起點，連線測試通過才算可用，不要把憑證 commit 進 repo。
5. 用 VS Code 開啟本 repo 時 `.vscode/mcp.json` 會直接生效；不需要的 server 從檔案刪掉即可。

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
├── .vscode/mcp.json            # VS Code MCP 範本
└── .codex/config.toml.example  # Codex MCP 範本
```

## 授權

MIT

---
Made with ❤️ for 工作用 Vibe Coding
