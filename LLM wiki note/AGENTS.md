# AGENTS.md — LLM Research Wiki 維護規範與操作手冊

本文件是此 LLM 研究論文知識庫的「最高維護憲法」。所有操作本專案的 LLM Agent 必須嚴格遵守本規範，以確保知識庫能隨時間持續累積、交織演進並發揮「知識複利（Knowledge Compounding）」的效益。

---

## 1. 專案願景與 Agent 角色定位

### 1.1 核心理念（Karpathy LLM Wiki 模式）
傳統 RAG 系統每次面對問題都是「從零檢索」碎片資料，沒有知識沉澱。本專案借鑑 Andrej Karpathy 的 LLM Wiki 精神：
- **編譯一次，長期演進**：論文閱讀後的萃取成果永久沉澱在結構化的 Markdown 筆記中。
- **持續交織複利**：每收錄一篇新文獻，Agent 不僅撰寫單篇摘要，更主動更新關聯概念、補充演算法比較、更新評測數據排行榜。
- **人機協同分工**：
  - **人類研究員（User）**：負責挑選文獻源、提出深層問題、引導研究方向、瀏覽 Obsidian 圖譜。
  - **LLM Agent**：負責粗重瑣碎的維護工作——摘要、交叉鏈結、概念萃取、版本比對、建檔與簿記。

### 1.2 雙重目標
1. **學術知識庫**：建立全面、嚴謹、具備高度交叉參照的 LLM 研究知識網絡。
2. **教學簡報基底**：筆記特別注重**「研究痛點（Pain Points）」**、**「核心直觀（Intuition / Analogy）」**與**「關鍵架構圖說明」**，為後續產出高品質教學型 HTML 簡報儲備素材。

---

## 2. 目錄邊界與檔案職責

專案根目錄結構與職責劃分如下：

```text
.
├── AGENTS.md            # [本手冊] Agent 行為規範與 SOP
├── index.md             # [內容索引] 全站卡片目錄與導覽
├── log.md               # [變更歷程] 時間序 append-only 日誌
├── raw/                 # [真實之源] 原始資料（唯讀，Agent 不得修改）
├── sources/             # [論文卡片] 單篇論文結構化筆記
├── concepts/            # [核心概念] 理論、問題定義、研究典範
├── methods/             # [方法技術] 具體模型、架構、演算法
├── benchmarks/          # [評測基準] 數據集與各家 SOTA 追蹤
├── syntheses/           # [橫向綜述] 多篇對比、演進史、專題研究
└── asssets/ (或 assets/) # [隔離保留區] 供後續 HTML 簡報使用，一般 Wiki 流程跳過
```

### 邊界隔離守則（重要）
1. **`raw/` 唯讀守則**：存放使用者提供的原始 PDF、arXiv 摘要、文字剪貼或手寫筆記。Agent 只能讀取，**絕對嚴禁修改或刪除 `raw/` 內的任何原始檔案**。
2. **`asssets/`（或 `assets/`）隔離守則**：此資料夾存放未來產出教學型 HTML 簡報所需的投影片圖檔與展示資源。**在一般 `/ingest`、`/query`、`/lint` 流程中，Agent 必須完全忽略此目錄，不得隨意掃描、變更或納入普通筆記索引**。

---

## 3. 雙向鏈結與 Frontmatter 規格

### 3.1 Obsidian 雙向鏈結規範
- 實體與概念鏈結一律使用雙向鏈結語法：`[[檔名|顯示名稱]]` 或 `[[檔名]]`。
- **概念歸一化（Canonical Linking）**：相同的概念與模型必須連結至同一個主卡片，不可建立重複頁面（例如：一律鏈結至 `[[concepts/test-time-compute|測試期計算擴展]]`，而非在多處各自寫死定義）。
- 路徑標準：引用同目錄或其他目錄皆建議使用相對或分類路徑，如 `[[sources/2024-deepseek-r1|DeepSeek-R1]]`、`[[methods/grpo|GRPO]]`。

### 3.2 YAML Frontmatter 統一格式
所有 Markdown 筆記（除了 `index.md` 與 `log.md`）頂端皆必須包含標準 YAML Frontmatter，以便 Obsidian Dataview 查詢與圖譜篩選：

```yaml
---
title: "卡片標題"
type: source | concept | method | benchmark | synthesis
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - llm
  - 子標籤1
aliases:
  - 別名1
  - 別名2
---
```

---

## 4. 筆記範本 (Templates)

Agent 建立新頁面時，須依據下列標準模板填充結構：

### 4.1 論文卡片模板 (`sources/YYYY-slug.md`)
```markdown
---
title: "論文標題"
type: source
year: YYYY
authors: ["第一作者", "第二作者", "et al."]
venue: "ArXiv / NeurIPS / ICML 等"
arxiv_id: "2401.xxxxx"
code_url: "https://github.com/..."
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - paper
  - llm
---

# 論文標題

- **論文連結**：[arXiv:2401.xxxxx](https://arxiv.org/abs/2401.xxxxx)
- **程式碼庫**：[GitHub](https://github.com/...)
- **發表時間**：YYYY 年 M 月

## 1. 一句話總結 (TL;DR)
> 用精準的一句話概括此論文的核心突破與價值。

## 2. 研究痛點與動機 (Motivation & Problem Statement)
- 過去的方法有何局限？
- 本篇論文試圖解決的核心挑戰是什麼？

## 3. 核心貢獻與方法架構 (Contributions & Methodology)
- **核心技術**：[[methods/method-slug|具體方法名稱]]
- **架構特點**：
  - 特點 A
  - 特點 B

## 4. 教學直觀與核心比喻 (Teaching Intuition & Analogy)
> **教學視角（供後續 HTML 簡報使用）**：
> 用最白話、直觀的比喻或圖解邏輯解釋本篇技術的精髓。為何這個設計巧妙？

## 5. 關鍵實驗與成果 (Key Results & Benchmarks)
- 在 [[benchmarks/benchmark-slug|評測基準]] 上表現：
  - Metric 1: X% (超越 Baseline Y%)
  - Metric 2: Z

## 6. 局限性與未來方向 (Limitations & Open Questions)
- 訓練成本、擴展瓶頸或邊界案例。

## 7. 關聯頁面 (Related Wiki Links)
- 涉及概念：[[concepts/...]]
- 涉及方法：[[methods/...]]
- 評測指標：[[benchmarks/...]]
```

### 4.2 概念卡片模板 (`concepts/slug.md`)
```markdown
---
title: "概念名稱"
type: concept
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - concept
  - llm
aliases:
  - 英文全稱
  - 簡稱
---

# 概念名稱

## 1. 概念定義 (Definition)
定義與理論背景。

## 2. 教學直觀 (Intuition)
用簡單的比喻說明其物理/數學意涵。

## 3. 關鍵機制或派生方向
- 分支 A
- 分支 B

## 4. 相關文獻與演進 (Evolution & Papers)
- [[sources/2024-paper-a|論文 A]]：首次提出...
- [[sources/2024-paper-b|論文 B]]：擴展了此概念...
```

### 4.3 方法/模型卡片模板 (`methods/slug.md`)
```markdown
---
title: "方法/模型名稱"
type: method
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - method
  - algorithm
---

# 方法/模型名稱

## 1. 方法概述
演算法或模型架構的核心機制。

## 2. 演算法核心步驟 / 虛擬碼邏輯
數學公式或核心演算法流程。

## 3. 優缺點對比
| 優勢 | 劣勢/代價 |
| :--- | :--- |
| ...  | ...       |

## 4. 代表論文與實作
- 提出論文：[[sources/...]]
```

### 4.4 評測基準卡片模板 (`benchmarks/slug.md`)
```markdown
---
title: "基準名稱"
type: benchmark
task_type: "Reasoning / Coding / General"
metric: "Pass@1 / Accuracy"
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
---

# 評測基準名稱

## 1. 任務說明
評測的具體能力（例如高中數學競賽題、Python 函數生成）。

## 2. 歷史與 SOTA 演進排行
| 模型 / 論文 | 得分 | 備註/設定 (Few-shot, CoT 等) | 記錄日期 |
| :--- | :--- | :--- | :--- |
| [[sources/...\|模型 A]] | 85.2% | pass@1 | YYYY-MM |
```

### 4.5 綜合評述卡片模板 (`syntheses/slug.md`)
```markdown
---
title: "專題主題"
type: synthesis
date_created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - synthesis
  - survey
---

# 專題主題

## 1. 調研背景與核心問題
## 2. 主流方法橫向對比矩陣
## 3. 演進歷史時間線
## 4. 教學簡報切入建議 (Slide Structure Proposal)
```

---

## 5. 三大核心維護流程 (Core Workflows)

### 5.1 Ingest 流程（文獻收錄 SOP）
當使用者要求收錄一篇新論文時（提供 raw/ 檔案、arXiv 連結或文字）：
1. **閱讀與理解**：讀取原始來源，萃取主要研究問題、方法、貢獻、直觀比喻與評測數據。
2. **建立單篇卡片**：依照 `4.1` 範本在 `sources/` 建立 `sources/YYYY-slug.md`。
3. **擴散更新（關鍵步驟）**：
   - 檢查論文提到的關鍵技術：若 `concepts/` 或 `methods/` 尚未存在該技術卡片，則建立新卡；若已存在，**務必進入該卡片追加補充本論文的推進或新實踐**。
   - 若論文包含 Benchmark 分數，進入對應的 `benchmarks/` 卡片更新 SOTA 表格。
   - 若論文明確挑戰或改進了過去的某個 Baseline，至該 Baseline 筆記標記後續進展。
4. **追加日誌**：在 `log.md` 頂端或尾端追加一筆標準紀錄：
   ```markdown
   ## [YYYY-MM-DD] ingest | 論文標題
   - 建立來源筆記：[[sources/YYYY-slug]]
   - 更新/建立關聯：[[concepts/slug]], [[methods/slug]], [[benchmarks/slug]]
   ```
5. **更新索引**：在 `index.md` 的對應分類表格中加入新建立的筆記條目與一句話簡介。

### 5.2 Query 流程（提問與反哺 SOP）
當使用者針對知識庫進行提問（如：「比較 DeepSeek-R1 與 o1 在長鏈推理上的差異」）：
1. **索引檢索**：先查閱 `index.md`，挑選最相關的 3~5 篇 Wiki 卡片進行交叉比對。
2. **結構化回答**：結合各卡片內容，給出清晰、有條理且標註 `[[wikilinks]]` 的回答。
3. **知識反哺判定**：若本次問答產生了高價值的橫向對比、技術路線圖或演進梳理，Agent 應主動詢問使用者：
   > 「此對比分析具備長期參考價值，是否需要沉澱為 `syntheses/主題名稱.md` 存入知識庫？」
   若使用者同意，則寫入 `syntheses/` 並同步更新 `index.md` 與 `log.md`。

### 5.3 Lint 流程（定期健檢 SOP）
當使用者要求健檢（`/lint`）時，Agent 執行全庫掃描：
1. **孤立節點檢查**：找出沒有任何入鏈（inbound links）的卡片。
2. **遺漏概念挖掘**：掃描多篇論文中頻繁出現（如出現超過 3 次），但尚未在 `concepts/` 或 `methods/` 建立專門卡片的重要名詞。
3. **數據與結論衝突**：比對不同論文中針對相同評測或問題的結論是否有矛盾，提醒使用者補充評述。
4. **輸出健檢報告**：列出修復建議與可探索的研究空白。

---

## 6. 教學簡報轉換指南（未來延伸）

當後續準備製作教學型 HTML 簡報時：
- 簡報架構優先取材自 `syntheses/` 的橫向對比與 `sources/` 中的「教學直觀與核心比喻」。
- 投影片相關靜態圖片統一存取 `asssets/` 目錄。
- Agent 可根據特定主題，直接將 Wiki 內容轉換為 Markdown Slide 語法（如 Marp）或獨立 HTML 簡報檔。
