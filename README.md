# interactive-lesson-deck

把教材做成「老師上課投影、學生可以操作」的互動教學網站，並提供一份可攜式 Agent Skill，供支援 `SKILL.md` 的 AI Agent 使用。

- **一頁一重點**：概念與練習依教學節奏安排。
- **圖解與操作相互連動**：學生拖曳、點選或調整時，圖像、例句或答案同步更新。
- **單一 HTML 優先**：可直接用瀏覽器開啟；依課程需求提供目錄、講解面板、教師控制工具。
- **不綁定特定 Agent**：Skill 使用開放的 Agent Skills `SKILL.md` 格式，流程不要求特定廠商工具。

## 專案內容

| 路徑 | 說明 |
|---|---|
| `index.html` | 成品範例：高職英文「時態系列」11 個主題、22 頁 |
| `skills/interactive-lesson-deck/` | 通用 Skill 套件，包含主文件、樣板、完整案例和科目參考 |
| `.claude/skills/interactive-lesson-deck/` | Claude Code 相容副本，內容與通用 Skill 同步 |

## 使用成品範例

線上版：https://princejonathan.github.io/interactive-lesson-deck/

下載後也可直接用瀏覽器開啟 `index.html`。

| 按鍵 | 功能 |
|---|---|
| ← → | 上一頁／下一頁 |
| 1–9、0 | 跳到主題 1–9、10 |
| M | 目錄 |
| H | 講解 |
| Q | 換一題 |
| Enter | 對答案 |
| P / R / F | 播放暫停／重設／放大圖解 |
| L / D / E / C | 雷射筆／畫筆／橡皮擦／清除本頁筆跡 |

## 使用 Skill 製作其他教材

將 `skills/interactive-lesson-deck/` 這個完整資料夾安裝到你使用的 Agent 所支援的 Skills 位置，或在對話中提供 `SKILL.md` 與同資料夾的 `assets/`、`references/`。各 Agent 的自動探索路徑可能不同，請依該 Agent 的說明安裝；支援 Agent Skills 開放格式的工具可直接讀取此套件。

接著提供教材，並描述學習對象、範圍和課堂用途，例如：「請把這份教材做成互動教學簡報網站，先整理內容並提出逐頁規劃。」若已提供充分資訊，也可要求直接製作。Skill 會先整理教材與規劃，再依需求製作可操作頁面並檢查。

格式說明：[Agent Skills Specification](https://agentskills.io/specification)

## 授權與教材

- 本專案的程式碼與 Skill 可自由使用。
- 範例中的英文例句與練習題取自出版社教材，僅作為教學展示範例；**原書 PDF 不包含在此儲存庫**。若要用於自己的課程，請改用你有權使用的教材內容。

