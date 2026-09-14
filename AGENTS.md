# AGENTS.md - 強制自動觸發規則
# 放在專案根目錄，Codex 會讀；Claude Code 讀 CLAUDE.md，可在 CLAUDE.md 寫一行 @AGENTS.md 引用

## ⚠️ 強制執行規則（必須遵守）

你收到任何任務時，**必須先判斷是否符合以下觸發條件，符合就必須先載入對應 Skill 再執行**，不准跳過。

- **Skill 尚未安裝**：先告訴使用者並附上本站卡片的安裝指令，不要假裝已載入，也不要自行改用其他來源。
- **標示「暫停」的項目**：來源不存在，不要觸發，也不要安裝。

### 工程開發 - 必須自動觸發
- 使用者說「新增頁面、新增模組、新增功能、開新功能」或 `/fe-arch` → **必須先執行 fe-arch** 釐清架構與邊界
- 使用者說「準備 push、要上 MR、幫我檢查程式碼」或 `/fe-code-review` → **必須先執行 fe-code-review**（依賴 Claude Code 工具與 plugin；Codex 只能照它的檢查項目人工審查）
- 使用者跑完 `git diff` 或說「幫我產生 MR」→ **必須先執行 fe-mr-generator**（偏 GitLab MR）
- 使用者收到 MR 或被指派 Reviewer → **必須先執行 fe-mr-review**（偏 GitLab MR，需要 glab）

### 工作流程 - 必須自動觸發
- 使用者貼需求文件、口語需求、PRD → **必須先執行 fe-issue** 轉成 Issue + AC
- 使用者說「做完了、完成了、可以上了」→ **必須先執行 verification-before-completion** 跑測試/build/lint，驗證不過不算完成
- 使用者說「下班前、結束任務、回顧一下」→ **必須先執行 retro**（偏 Claude Code 工作流程）
- 使用者說「處理文件、客戶給的 docx、xlsx、pdf」→ **必須先執行 docx / xlsx / pptx / pdf skill**（環境已有同類文件處理功能就直接用，不必重裝）
- 使用者開始過度設計、寫得很複雜 → **暫停**：andrej-karpathy-guidelines 來源不存在，不要觸發

### 設計整合 - 必須自動觸發
- 使用者貼 Figma 連結 → **必須先用 Figma 官方 MCP**（Claude：`figma@claude-plugins-official` plugin；Codex：`codex mcp add figma --url https://mcp.figma.com/mcp`）。未設定或未登入 Figma 時先提示使用者，不要改用其他來源
- 使用者寫 React / Next.js / 要優化效能 → **必須先執行 vercel-react-best-practices**（安裝後的資料夾名稱是 `react-best-practices`）

### 測試與驗證 - 必須自動觸發
- 功能做完需要補測試 → **暫停**：playwright-skill 來源不存在，不要觸發
- 處理 auth / API / 金流 / 登入 → **暫停**：security-guidance 來源不存在，不要觸發

### MCP Servers - 設定完成才使用
範本在 `.vscode/mcp.json` 和 `.codex/config.toml.example`，需另外設定憑證並測試連線。**未設定時不要假設可用**：
- `context7`：問任何函式庫用法時 → 必須先用 context7 查最新官方文件，不要用記憶回答
- `github`：需要查 PR / 建 issue / 操作 repo 時 → 必須用 github-mcp（需要 GitHub 認證）
- `postgres`：需要查資料、驗證欄位、看慢查詢時 → 必須用 postgres-mcp（需要資料庫連線；參考伺服器已封存）

## Skills 清單

安裝狀態以本機為準。建議先裝優先四項：fe-arch、fe-issue、fe-code-review、verification-before-completion。

### 工程開發
- `fe-arch` - 新功能前架構釐清（優先）
- `fe-code-review` - push 前預審（優先）
- `fe-mr-generator` - git diff 產生 MR
- `fe-mr-review` - MR 審查

### 設計整合
- `vercel-react-best-practices` - React/Next.js 最佳實踐（資料夾 `react-best-practices`）
- `figma` - Figma 官方 MCP 與 skills（Beta，需登入 Figma）

### 測試與驗證
- `verification-before-completion` - 完成前驗證（優先，來源 obra/superpowers）
- `playwright-skill` - 暫停（來源不存在）
- `security-guidance` - 暫停（來源不存在）

### 工作流程
- `fe-issue` - 需求轉 Issue（優先）
- `andrej-karpathy-guidelines` - 暫停（來源不存在）
- `docx / xlsx / pptx / pdf` - 文件處理
- `retro` - 回顧沉澱

### MCP Servers（需另外設定）
- `context7-mcp` - 最新文件
- `github-mcp` - GitHub 操作
- `postgres-mcp` - 資料庫

## 使用方式

### 手動觸發（最穩）
```
/fe-arch 新增登入頁
/fe-issue 把這份需求轉 Issue
/verification-before-completion
```

### 自動觸發
只要符合上面的「何時用」條件，你就必須自動載入，不需要使用者手動打斜線。

## 來源
本站：https://rita112025-cpu.github.io/vibe-coding-work-db/
切到 Claude 或 Codex 模式照卡片指令安裝；安裝前先審查
