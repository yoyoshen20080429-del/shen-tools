# AGENTS.md — LLM 研究與個人知識庫維運規範（LLM Wiki）

本知識庫參考 Andrej Karpathy 的 **LLM Wiki** 模式建置，透過持久化、雙向連結的 Markdown 知識圖譜，將零散文獻編譯為可隨時間累積（Compounding）的研究資產。

---

## 一、三層系統架構（Architecture）

1. **`raw/`（原始資料層 — Immutable 不可變）**
   - 存放所有原始輸入文獻、貼上的文章、論文與截圖附件。
   - **鐵律**：LLM 只能讀取 `raw/`，**絕對不可修改或刪除**其中的原始內容。
   - 子目錄：`raw/papers/`、`raw/articles/`、`raw/assets/`。
2. **`wiki/`（知識庫層 — LLM 全權維護）**
   - 由 LLM 編譯、摘要、拆解概念並建立雙向連結（`[[wikilinks]]`）的結構化知識頁面。
   - 子目錄：
     - `wiki/overview.md`：研究總覽與演進地圖
     - `wiki/index.md`：內容導向總目錄（Catalog）
     - `wiki/log.md`：時間序列操作日誌（Append-only）
     - `wiki/papers/`：論文深度筆記
     - `wiki/articles/`：文章與史料摘要頁
     - `wiki/concepts/`：核心概念、方法論與技術拆解
     - `wiki/models/`：模型架構與演進分析
     - `wiki/entities/`：研究機構、學者或關鍵人物／組織實體
     - `wiki/benchmarks/`：基準測試與資料集
     - `wiki/syntheses/`：跨文獻深度比較與綜合分析
     - `wiki/_templates/`：標準頁面模板
3. **研究應用與簡報產出層（Strict Wiki-Grounded Outputs）**
   - `notes/`：基於 `wiki/` 現有知識產出的專題研究筆記（支援 LaTeX）。
   - `slides_outline/`：對應研究筆記的簡報逐頁腳本大綱。
   - `slides_html/`：互動式日系文青粉彩 HTML 簡報（內建 KaTeX 渲染）。

---

## 二、頁面格式規範（Conventions）

### 1. YAML Frontmatter（所有 `wiki/` 內容頁必備）
```yaml
---
title: 頁面標題
type: paper | article | concept | model | entity | benchmark | synthesis
tags: [LLM, Research]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: ["raw/articles/檔名.md"]
---
```

### 2. 雙向連結（Wikilinks）
- 引用知識庫內其他頁面時，一律使用 Obsidian 標準連結格式：`[[concepts/心理博弈與資訊不對稱]]` 或 `[[entities/諸葛亮|諸葛亮]]`。
- 每個頁面底部應設有 `## 相關連結` 區塊，維護知識圖譜連通性。

---

## 三、核心作業流程（Operations）

### 1. Ingest（文獻攝取流程）
每當使用者提供新文章、論文或截圖時，依序執行：
1. **保存原始檔**：將原文一字不漏存入 `raw/articles/YYYY-MM-DD-標題.md`（或 `raw/papers/`），若有圖片附件則存入 `raw/assets/`。
2. **撰寫摘要頁**：於 `wiki/articles/` 或 `wiki/papers/` 建立結構化摘要頁，提煉背景、核心機制、數據與關鍵引述。
3. **拆解與更新關聯頁**：建立或更新相關的概念頁（`wiki/concepts/`）、模型頁（`wiki/models/`）、實體頁（`wiki/entities/`）；若新資料與舊頁矛盾，必須明確標註 `[觀點衝突/更新]`。
4. **更新總覽、索引與日誌**：更新 `wiki/overview.md`、`wiki/index.md`，並在 `wiki/log.md` 最底部追加：
   `## [YYYY-MM-DD] ingest | 標題`

### 2. Research & Slides（專題研究筆記與日系粉彩 HTML 簡報流程）
當使用者提出研究問題或要求針對特定主題生成研究產出時：
1. **嚴格知識邊界（Strict Wiki Boundary）**：
   - `notes/YYYY-MM-DD-主題.md` 的正文 **100% 僅能引用 `wiki/` 內已收錄的知識**，每個論點皆須附上 `[[wiki頁面]]` 出處連結。
   - 若某面向在 `wiki/` 內缺乏資料，必須誠實標註 `> [知識缺口] 目前 Wiki 尚未收錄此部分細節`，**嚴禁將外部搜尋結果混入正文**。
   - 支援完整 **LaTeX 數學公式**（`$inline$` 與 `$$display$$`）。
2. **建議參考文獻（待 Ingest）**：
   - 於 `notes/` 最末端的 `## 建議參考文獻（待 Ingest）` 區塊，列出上網搜尋到的相關外部文獻。
   - 每筆文獻須提供**可直接點擊開啟或下載的真實來源連結（URL）**、**建議收錄理由**與**預期可補齊的知識缺口**，方便使用者一鍵下載並貼回進行 Ingest 流程。
3. **簡報逐頁大綱（`slides_outline/`）**：
   - 根據 `notes/` 內容，產出 `slides_outline/YYYY-MM-DD-主題-outline.md`，規劃逐頁標題、視覺佈局、精煉重點、LaTeX 公式與講者備忘錄（Speaker Notes）。
4. **日系文青粉彩 HTML 簡報（`slides_html/`）**：
   - 產出單一獨立可離線播放的 `slides_html/YYYY-MM-DD-主題.html`。
   - **預設視覺風格：「晴空蘇打與檸檬汽水（Soda & Lemon）」可愛日系文青低飽和粉彩風**
     - 背景底色：海鹽香草白（`#F5F9FA`）
     - 主強調色：霧霾晴空藍（`#8FB8CA`）
     - 次強調色：奶油檸檬黃（`#EFE0A8`）、蜜桃珊瑚粉（`#ECA89A`）
     - 文字色：深海藍灰（`#3B4954`）
     - 視覺細節：圓角卡片、微立體偏移陰影（Soft Offset Shadow）、日系小書籤 Wiki 出處標籤、可愛圓形編號徽章。
   - **內建技術功能**：載入 **KaTeX** 自動渲染所有 LaTeX 公式；支援鍵盤 `←` / `→` / `空白鍵` 翻頁、進度條、頁碼顯示、講者備忘錄一鍵展開/收合。
5. **登記日誌與索引**：同步更新 `wiki/index.md` 與 `wiki/log.md`（`## [YYYY-MM-DD] research | 主題`）。

### 3. Lint（知識庫健康檢查）
定期檢查：
- 找出沒有連入連結的孤島頁面（Orphan pages）。
- 檢查不同頁面間的數據或論點衝突。
- 盤點在多個頁面被提及但尚未建立專屬頁面的核心概念，並主動建議下一步可搜尋補充的文獻。
