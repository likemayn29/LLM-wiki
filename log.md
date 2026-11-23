# LLM Research Wiki — 變更歷程 (Changelog)

> 本文件為 append-only 變更紀錄，遵循 `## [YYYY-MM-DD] action | subject` 格式。

---

## [2026-11-19] init | 建立 LLM Wiki 基礎架構
- 制定並建立 `[[AGENTS.md]]` 作為知識庫運作憲法。
- 建立核心資料夾架構：`raw/`, `sources/`, `concepts/`, `methods/`, `benchmarks/`, `syntheses/`。
- 初始化 `[[index.md]]` 與 `[[log.md]]`。
- 明確界定 `asssets/` 為教學 HTML 簡報保留區，跳過一般 Wiki 流程。

## [2026-11-19] synthesize | LLM 在教學上的運用問題與核心挑戰
- 建立專題綜述：`[[syntheses/llm-in-education-challenges]]`
- 梳理六大教學運用痛點（幻覺、認知卸載、評量失效、數位落差、教學法脫節、隱私合規）與對應解決矩陣。
- 規劃教學簡報轉換架構，準備產出 HTML 互動投影片。

## [2026-11-19] present | 產出 HTML 教學簡報：LLM 在教學上的運用問題
- 依據 `[[syntheses/llm-in-education-challenges]]` 內容轉化為 11 頁現代化互動式 HTML 簡報。
- 儲存至 `[[slides/llm-in-education-challenges.html]]`。
- 支援鍵盤導航（方向鍵/空白鍵）、投影片縮圖總覽 (O)、講者備忘錄 (S)、全螢幕 (F) 與自適應 16:9 比例。
