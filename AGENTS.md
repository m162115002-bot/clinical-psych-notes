# AGENTS.md - 臨床心理學課程講義速版 開發與擴充規範

## 1. 專案目的 (Project Purpose)
本專案為「臨床心理學課程講義速版」，是一個專注於考前快速複習、完整題庫演練與完整版講義簡報下載的靜態網頁知識庫。
AI 協作者的任務是嚴格遵守本文件的「日系文青 × 低飽和度粉彩」設計系統、檔案命名與版型結構，協助維護首頁索引並快速生成風格高度一致的新講義頁面。

## 2. 技術架構與檔案規範 (Architecture & File Conventions)
- **純靜態單檔原則**：使用純 HTML5、CSS3 與原生 JavaScript，不依賴任何前端框架或編譯工具，確保可直接部署於 GitHub Pages。每個 HTML 頁面必須將 `<style>` 與 `<script>` 完整封裝於自身檔案中。
- **目錄結構**：
  ```text
  clinical-psych-notes/
  ├── AGENTS.md                  # 本專案規範文件
  ├── index.html                 # 首頁（講義總覽目錄與分類篩選器）
  ├── notes/                     # 存放所有獨立講義內頁
  │   └── YYYY-MM-slug.html      # 講義內頁檔案
  └── slides/                    # 存放與講義同風格的完整簡報下載檔
      └── YYYY-MM-slug.pptx      # 講義對應簡報 (.pptx)
  ```
- **檔名規範**：講義內頁一律存放於 `notes/` 資料夾，對應簡報存放於 `slides/` 資料夾，皆採用 `YYYY-MM-英文短名`（全小寫、連字號分隔，例如 `2026-11-hospital-psych.html` 與 `2026-11-hospital-psych.pptx`）。

## 3. 視覺設計系統 (Design System - 日系文青低飽和粉彩風)
整體採用「日系手帳 / 文青筆記本風格」，溫潤米白底色搭配低飽和度莫蘭迪粉彩（Morandi Pastel）、圓潤邊角（`18px`～`24px`）與柔和細邊框：
- **基礎色票**：
  - 網頁背景（溫潤和紙米白）：`--bg-main: #faf8f5;`
  - 卡片底色（純淨奶白）：`--bg-card: #fffefc;`
  - 主要文字（柔焦炭棕灰）：`--text-primary: #4a4542;`
  - 次要文字（暖灰褐）：`--text-secondary: #7c746e;`
  - 邊框線條（奶茶淺灰）：`--border: #ebe5dd;`
  - 主強調色（乾燥玫瑰粉）：`--primary: #c98a8a;`
  - 主強調色淺底：`--primary-light: #f6eaea;`
- **字體與圓角細節**：
  - 字體：`font-family: "Zen Maru Gothic", "Noto Sans TC", -apple-system, BlinkMacSystemFont, sans-serif;`（引入 Google Fonts `Zen Maru Gothic` 與 `Noto Sans TC`）。
  - 卡片圓角 `20px`～`24px`，按鈕與標籤採用藥丸圓角 `999px`，陰影使用極柔和的暖調陰影 `0 6px 20px rgba(138, 121, 108, 0.06)`。
- **五大分類專屬低飽和粉彩標籤色（Pastel Badge Colors）**：
  - `心理衡鑑`（霧霾粉藍）：背景 `#e4edf2`，文字 `#567285`（class: `badge-assessment`）
  - `心理治療`（鼠尾草綠）：背景 `#e5efe8`，文字 `#547360`（class: `badge-therapy`）
  - `精神病理學`（蜜桃杏粉）：背景 `#f7e8e0`，文字 `#9c6654`（class: `badge-psychopathology`）
  - `神經心理學`（薰衣草灰紫）：背景 `#ede7f3`，文字 `#716187`（class: `badge-neuro`）
  - `健康心理學`（奶油薄荷）：背景 `#e2f1ee`，文字 `#4d7870`（class: `badge-health`）

## 4. 新增講義的標準作業程序 (Workflow for Adding Lectures)
當使用者要求「新增一篇關於 [主題] 的講義」或提供文獻資料時，AI 必須依序執行以下兩項任務：

### 任務 A：建立講義內頁 (`notes/YYYY-MM-slug.html`) 與完整簡報 (`slides/YYYY-MM-slug.pptx`)
1. **完整簡報生成原則**：製作 `.pptx` 簡報時，必須完整保留文獻中的核心理論、實證研究細節、數據與表格對照（不可過度刪減成空泛大綱），並套用與網頁相同的低飽和度粉彩配色。
2. 內頁必須依序包含以下 6 個固定區塊：
   - **導覽列與標題區**：返回首頁連結（`../index.html`）、分類標籤、講義主標題（`<h1>`）與更新日期。
   - **一句話秒懂定義 (`.definition-box`)**：使用虛線框的粉彩便利貼框，用精準的 1～2 句話點出該主題最核心的臨床定義。
   - **關鍵考點條列 (`.key-points`)**：使用無序清單條列 3～5 個最常考的核心概念，關鍵詞需加粗（`<strong>`）。
   - **易混淆概念對照表 (`.comparison-table`)**：使用圓角外框包覆的 HTML `<table>` 比較兩個以上容易混淆的診斷、理論、因應風格或評估工具。
   - **自我檢測互動選擇題庫 (`.quiz-section`)**：必須包含 **至少 20 題四選一互動式選擇題**，配備懸浮即時計分板與即時解析。
   - **頁面最下方：簡報下載區 (`.download-box`)**：標題簡潔標示為「簡報下載」，放置於講義頁面最底部提供 `.pptx` 下載。

### 任務 B：同步更新首頁索引 (`index.html`)
在 `index.html` 的 `<div class="lecture-grid">` 最上方插入新講義卡片，確保 `data-category` 與分類名稱完全一致。

## 5. 禁止事項 (Constraints)
- **嚴禁修改既有資料**：更新 `index.html` 時，不可刪除或更動已存在的講義卡片。
- **嚴禁使用高飽和刺眼色票**：所有新增元件必須遵守低飽和莫蘭迪粉彩與暖灰文字規範，禁止使用純黑 `#000` 或高飽和亮藍/亮紅。
- **嚴禁過度精簡簡報內容**：簡報需完整呈現文獻各節重點與研究案例。
