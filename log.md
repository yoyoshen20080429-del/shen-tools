# Wiki 操作日誌（Chronological Log）

> 採 Append-only 時間序列紀錄，每筆條目以 `## [YYYY-MM-DD] <operation> | <Title>` 開頭，便於追蹤知識庫演進。

## [2026-11-16] init | 初始化 LLM Wiki 知識庫架構
- 建立 `AGENTS.md` 核心規範、三層資料夾架構（`raw/`、`wiki/` 及其子目錄）與標準模板。
- 建立 `wiki/index.md`、`wiki/log.md` 與 `wiki/overview.md`。

## [2026-11-16] ingest | 草船借箭
- 保存原始截圖至 `raw/assets/螢幕擷取畫面 2026-11-16 215416.png` 並轉錄原文至 `raw/articles/2026-11-16-草船借箭.md`。
- 建立摘要頁 `wiki/articles/草船借箭.md`。
- 建立概念頁 `wiki/concepts/心理博弈與資訊不對稱.md`。
- 建立人物實體頁：`wiki/entities/諸葛亮.md`、`wiki/entities/曹操.md`、`wiki/entities/魯肅.md`、`wiki/entities/周瑜.md`。
- 更新 `wiki/index.md` 與 `wiki/overview.md`。

## [2026-11-16] config | 擴充研究筆記與日系文青粉彩 HTML 簡報工作流
- 更新 `AGENTS.md`，新增 `notes/`、`slides_outline/`、`slides_html/` 規範。
- 確立「100% 僅引用 Wiki 現有知識 + 誠實標註知識缺口 + 可點擊下載建議文獻 + 支援 LaTeX」原則。
- 定案「晴空蘇打與檸檬汽水（Soda & Lemon）」為預設 HTML 簡報視覺風格。

## [2026-11-16] research | 諸葛亮草船借箭之戰場心理與決策分析
- 產出純 Wiki 研究筆記：`notes/2026-11-16-諸葛亮為何敢斷定曹操大霧只射箭不衝鋒且不用火箭.md`。
- 產出簡報逐頁大綱：`slides_outline/2026-11-16-諸葛亮為何敢斷定曹操大霧只射箭不衝鋒且不用火箭-outline.md`。
- 產出日系粉彩互動簡報：`slides_html/2026-11-16-諸葛亮為何敢斷定曹操大霧只射箭不衝鋒且不用火箭.html`。
