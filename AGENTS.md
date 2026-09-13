# AGENTS.md - 強制自動觸發規則
# 放在專案根目錄，Claude Code 和 Codex 都會讀

## ⚠️ 強制執行規則（必須遵守）

你收到任何任務時，**必須先判斷是否符合以下觸發條件，符合就必須先載入對應 Skill 再執行**，不准跳過。

### 工程開發 - 必須自動觸發
- 使用者說「新增頁面、新增模組、新增功能、開新功能」或 `/fe-arch` → **必須先執行 fe-arch** 釐清架構與邊界
- 使用者說「準備 push、要上 MR、幫我檢查程式碼」或 `/fe-code-review` → **必須先執行 fe-code-review**
- 使用者跑完 `git diff` 或說「幫我產生 MR」→ **必須先執行 fe-mr-generator**
- 使用者收到 MR 或被指派 Reviewer → **必須先執行 fe-mr-review**

### 工作流程 - 必須自動觸發
- 使用者貼需求文件、口語需求、PRD → **必須先執行 fe-issue** 轉成 Issue + AC
- 使用者說「做完了、完成了、可以上了」→ **必須先執行 verification-before-completion** 跑測試/build/lint，驗證不過不算完成
- 使用者說「下班前、結束任務、回顧一下」→ **必須先執行 retro**
- 使用者說「處理文件、客戶給的 docx、xlsx、pdf」→ **必須先執行 docx / xlsx / pptx / pdf skill**
- 使用者開始過度設計、寫得很複雜 → **必須先執行 andrej-karpathy-guidelines**

### 設計整合 - 必須自動觸發
- 使用者貼 Figma 連結 → **必須先執行 figma skill**
- 使用者寫 React / Next.js / 要優化效能 → **必須先執行 vercel-react-best-practices**

### 測試與驗證 - 必須自動觸發
- 功能做完需要補測試 → **必須先執行 playwright-skill**
- 處理 auth / API / 金流 / 登入 → **必須先執行 security**

### MCP Servers - 自動使用工具
已安裝在 `.vscode/mcp.json` 和 `.codex/config.toml.example`：
- `context7`：問任何函式庫用法時 → 必須先用 context7 查最新官方文件，不要用記憶回答
- `github`：需要查 PR / 建 issue / 操作 repo 時 → 必須用 github-mcp
- `postgres`：需要查資料、驗證欄位、看慢查詢時 → 必須用 postgres-mcp

## 已安裝 Skills 清單

### 工程開發
- `fe-arch` - 新功能前架構釐清
- `fe-code-review` - push 前預審
- `fe-mr-generator` - git diff 產生 MR
- `fe-mr-review` - MR 審查

### 設計整合
- `vercel-react-best-practices` - React/Next.js 最佳實踐
- `figma` - Figma 直連

### 測試與驗證
- `verification-before-completion` - 完成前驗證
- `playwright-skill` - E2E 測試
- `security` - 安全掃描

### 工作流程
- `fe-issue` - 需求轉 Issue
- `andrej-karpathy-guidelines` - 防止過度設計
- `docx / xlsx / pptx / pdf` - 文件處理
- `retro` - 回顧沉澱

### MCP Servers
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
切到 Codex 模式複製指令安裝
