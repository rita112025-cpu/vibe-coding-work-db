# 修正追蹤清單（2026-09-14）

依〈完整整理〉審查網站清單（Claude／Codex 雙模式）的問題清單。
狀態：`待修` → `已修` → `已驗證`；`需決定` 表示要先確認範圍。
目前：#01–#16、#18 與審查發現 R1–R12 已完成並 commit；#17、#19 需決定。

## 現狀（已完成，已驗證）

- [x] id 6 verification-before-completion 改為 obra/superpowers，移除 official（commit aae1b98）
- [x] 全站改用 `npx openskills install <repo>`，移除 `#skill` 後綴
- [x] vercel-react-best-practices 正名為 react-best-practices（SKILL.md 內部名稱仍是 vercel-react-best-practices）
- [x] figma、playwright-skill、andrej-karpathy-guidelines、security-guidance 停用安裝指令（GitHub 已核對：路徑不存在）
- [x] 3 個 MCP Server 改為「另外設定」並連到官方文件
- [x] docx／xlsx／pptx／pdf 的 Codex 指令改列四個路徑（installer `--path` 支援多值，已核對原始碼）
- [x] 卡片標示「優先四項／按需選用／來源不符／MCP Server」
- [x] 雙模式切換正常，console 無錯誤

## P0：會讓人裝錯或裝壞

- [x] **#01 共用資料夾沒被裝上** · 已驗證 · `index.html` 卡片 2、3、5、`README.md`
  - 卡片、Hub、README 寫明 `_shared` 與 fe-guardrails；Claude 建議 `--global` 並複製到 `~/.claude/skills/_shared`。
- [x] **#02 fe-code-review 在 Codex 跑不起來** · 已驗證 · 卡片 3、側欄
  - 保留在優先四項；卡片與 Codex 模式側欄標明「只當審查清單」。
- [x] **#03 Hub 區塊的設定範例是虛構格式** · 已驗證 · 「如何建立自己的 Hub」
  - 改成雙模式目錄結構與優先四項安裝指令，切換模式內容跟著換。
- [x] **#04 AGENTS.md 強制觸發不存在的 skill** · 已驗證 · `AGENTS.md`
  - 暫停項不觸發；未安裝先提示；React 用 skill 名稱 `vercel-react-best-practices`；docx 類已有就不重裝。
- [x] **#05 README 安裝指令全錯** · 已驗證 · `README.md`
  - 改成 openskills install／Python installer，補優先四項、MCP、Windows `py` 說明。

## P1：說法矛盾或誤導

- [x] **#06 側欄推薦與清單矛盾** · 已驗證 · 推薦改優先四項；figma 標暫停；Playwright 標工具；postgres 註明已封存。
- [x] **#07 暫停卡片同一句話顯示兩次** · 已驗證 · 描述改「原列用途：…」。
- [x] **#08 retro 描述與 SKILL.md 不符** · 已驗證 · 照 SKILL.md 改；提示改 CLAUDE.md／AGENTS.md。
- [x] **#09 標語仍暗示全部可直接裝** · 已驗證 · REVIEW FIRST；計數「16 項：9 可裝 · 4 暫停 · 3 MCP」。
- [x] **#10 Codex 安裝位置沒講清楚** · 已驗證 · 寫明 `$CODEX_HOME/skills` 與官方 `.agents/skills`、`--dest`。

## P2：體驗與收尾

- [x] **#11「安裝前必讀」太長又擋在標題前** · 已驗證 · 移到標題下方、只顯示目前模式；間距 class 已確認存在。
- [x] **#12 verification 卡片圖示遺失** · 已驗證 · 補回原圖示。
- [x] **#13 `.codex/config.toml.example` 過時** · 已驗證 · 移除引用碼；GitHub 改官方遠端；context7 附 API key 寫法。
- [x] **#14 `.vscode/mcp.json` 格式錯** · 已驗證 · 改用 `servers` 鍵，Postgres 連線字串改用輸入提示。
- [x] **#15 舊版 HTML 副本仍公開** · 已刪除
  - `Index-Dual.html`、`vibe-coding.html` 已從 repo 移除（仍可從 git 歷史還原）。
- [x] **#16 Codex 一次性腳本留在根目錄** · 已刪除
  - `update-catalog.cjs` 未被 git 追蹤，已移到 Windows 資源回收筒。
- [ ] **#17 figma 替代來源** · 需決定
  - `jackyu/claude-skills` 有同名 figma skill，尚未審查。
- [x] **#18 最終審查與驗證** · 已完成
  - `/fe-code-review` 四軸＋內建 code-review；修正後重跑語法、CSS class、資料不變量、雙模式、深淺色、375px、TOML/JSON 檢查。

## 審查發現（/fe-code-review）

- [x] **R1** `mt-2` 不在編譯後 CSS，必讀區段落黏在一起 → 改 `mt-2.5` · 已驗證
- [x] **R2** `_shared` 複製位置與預設專案安裝不符；Codex Hub 沒說明；沒提 fe-guardrails → 已補 · 已驗證
- [x] **R3** Windows `python` 是商店轉址會失敗、cmd.exe 不展開 `$HOME`、`CODEX_HOME` 未處理 → 網站、Hub、README 補說明 · 已驗證
- [x] **R4** 專案層 `.codex/config.toml` 可能把資料庫密碼 commit 進公開 repo → 註解改寫＋新增 `.gitignore` · 已驗證
- [x] **R5** AGENTS.md 用資料夾名叫 React skill、docx 類會被要求重裝 → 已修 · 已驗證
- [x] **R6** 一次裝多路徑遇到既有 skill 會中途停止 → 卡片 14 與 Codex 提示說明 · 已驗證
- [x] **R7** official 徽章被上一輪全數移除，docx 卡仍寫「官方」→ 恢復 id 7、14 · 已驗證
- [x] **R8** 狀態判斷散在 status 前綴、category、install 真假值 → 新增 `state` 欄位，計數與顏色都讀它 · 已驗證
- [x] **R9** 暫停卡與 MCP 卡的 stars 文字前仍畫星形；「來源不符／待確認」混用；日期格式不一 → 已修 · 已驗證
- [x] **R10** 搜尋「暫停」0 筆 → 搜尋納入狀態與注意事項 · 已驗證
- [x] **R11** 無障礙：同名連結、標題大綱、清單符號被念出 → 加 aria-label、aria-labelledby、aria-hidden · 已驗證
- [x] **R12** `npx openskills sync` 會在 AGENTS.md 末尾追加規則；`.vscode/mcp.json` 開 repo 即生效 → 網站與 README 註明 · 已驗證

## 未修（已記錄）

- MCP 卡原本顯示 TOML 的程式分支已不會執行（無害，改壓縮碼風險大於收益）
- README「9／4／3」是寫死的數字（靜態文件）
- AGENTS.md「必須自動觸發」標題底下有暫停項（每行已寫明，保留觸發版結構）
- 重新整理時 Codex 使用者會先閃一下 Claude 版內容（改動前就有）
- 卡片資料缺欄位會整頁白屏（資料寫死且已驗證齊全）

## 需決定（新增）

- [ ] **#19 Postgres MCP 替代方案** · 需決定
  - 範本仍用已封存的 `@modelcontextprotocol/server-postgres`，沒有官方維護版；換成第三方要先審查。
