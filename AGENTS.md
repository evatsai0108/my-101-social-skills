# 專案規則與操作規範 (Project Guidelines & Rules)

## 版本控制規範 (Git Commit & Push Workflow)
- **核心守則（最高優先順序）**：每次任務、功能修改、檔案生成或資料更新執行完成後，**必須自動進行 Git 存檔並推送（`git add`、`git commit` 與 `git push`）**。
- **標準執行流程**：
  1. 每當任務完成或一個階段的修改告一段落，先執行 `git status` 檢視異動檔案。
  2. 使用 `git add` 將所有修改、新增的檔案加入暫存區。
  3. 執行 `git commit -m "..."` 撰寫繁體中文或 Conventional Commits 格式之清晰提交訊息（如 `feat: ...`、`fix: ...`、`style: ...` 等）。
  4. 執行 `git push` 將最新變更即時推送到遠端儲存庫，確保雲端託管網站（如 Netlify / GitHub Pages）能即時自動觸發構建與部署，隨時保持線上為最新版本。
  5. 確保工作區乾淨（Working tree clean），在回覆使用者時確認存檔與推送狀態。

## 網站與五大電子書 (PDF/HTML) 強制連動同步規範 (Web & PDF Content Synchronization)
- **核心守則（最高優先級強制規範）**：網站上若有任何教材、課綱、課堂主題、日期、故事、超能力招式、角色劇場（台詞/動作/提示）、學習單題目與選項、注音文本、IEP量化目標、普通班導師融合口訣便利貼、家庭共學打卡或字詞更動，**凡修改網站資料源，必須即刻連動重新編譯五大出版級電子書與手冊（PDF 及全冊 HTML）**，嚴禁只更新網頁資料而遺漏 PDF 手冊，確保線上互動網頁與線下出版級 PDF 教材永遠 100% 保持完全同步一致。
- **五大出版級 PDF 關聯清單與規格**：
  1. `備課平台/教師手冊.pdf`（106 頁 **B4 直式規格 250×353mm**，非 A4）
  2. `備課平台/101堂特教學習單_注音版_B4.pdf`（106 頁 **B4 直式規格 250×353mm**，字嗨注音標楷體，非 A4）
  3. `備課平台/101堂特教社交技巧彩色學習單全集.pdf`（106 頁 **A4 直式規格 210×297mm**）
  4. `備課平台/101堂特教社交技巧故事島與超能力招式全集.pdf`（104 頁 **A4 直式規格 210×297mm**）
  5. `備課平台/101堂特教社交技巧角色劇場與遊樂場實戰全集.pdf`（104 頁 **A4 直式規格 210×297mm**）
- **異動觸發與自動化編譯對應表**：
  - 若修改 `備課平台/app.js`（課綱、日期、故事、招式、IEP等）：
    - 必須編譯：`python3 scripts/compile_teacher_manual_pdf.py`
    - 必須編譯：`python3 scripts/compile_zhuyin_worksheets_b4_pdf.py`
    - 必須編譯：`python3 scripts/compile_master_pdf.py`
    - 必須編譯：`python3 scripts/compile_stories_and_skills_pdf.py`
  - 若修改 `備課平台/roleplay-data.js`（四角色情境、動作、台詞、撇步等）：
    - 必須編譯：`python3 scripts/compile_teacher_manual_pdf.py`
    - 必須編譯：`python3 scripts/compile_roleplay_and_game_pdf.py`
  - 若修改 `備課平台/worksheets-data.js`（學習單三選一選項、家庭共學打卡等）：
    - 必須編譯：`python3 scripts/compile_zhuyin_worksheets_b4_pdf.py`
    - 必須編譯：`python3 scripts/compile_master_pdf.py`
    - 必須編譯：`python3 scripts/compile_teacher_manual_pdf.py`
  - **一鍵全冊連動編譯**：直接執行 `python3 scripts/recompile_all_5_books.py`（依序重新編譯五大手冊並自動驗證）。
- **驗收與同步檢查標準**：
  1. 每次編譯後必須執行 `python3 scripts/verify_all_tocs.py`，確保五大 PDF 頁數、101 個目錄超連結跳轉與 HTML 關聯皆為 **100% PASS**。
  2. 編譯完成之 PDF 同步鏡像至 `備課平台/`。
  3. 同步完成後自動執行 Git 存檔並推送（`git add`、`git commit`、`git push`）。

## 網頁設計與 Favicon 規範 (Web Design & Favicon Requirement)
- **核心守則**：每當新建、開發或維護任何網頁（HTML/Web 專案）時，**必須為該網站設計專屬且切合主題的 favicon 並套用**。
- **標準執行流程**：
  1. **專屬視覺設計**：依據網站主題（如特教、教育、工具、儀表板等）設計清晰、高解析度的 Favicon（推薦使用現代 SVG 向量圖標或包含 PNG 備用，確保在瀏覽器分頁標籤、書籤列、亮色與深色模式下皆清晰美觀）。
  2. **標準代碼引入**：在每個 HTML 檔案的 `<head>` 區塊內，標準加入 `<link rel="icon" type="image/svg+xml" href="...">`（視需要加上 apple-touch-icon）。
  3. **檢查與驗收**：確保所有子頁面、獨立檢視頁（如列印頁、手冊預覽頁）皆正確關聯 favicon，不留預設空白。

## Gemini 與 Codex 規則同步 (GEMINI.md & AGENTS.md Synchronization)

- **全域對應**：本機 `~/.gemini/GEMINI.md` 與 `~/.codex/AGENTS.md` 是同一份全域規則的兩個版本，必須保持內容完全一致。
- **專案對應**：每個專案根目錄的 `GEMINI.md` 與 `AGENTS.md` 是同一份專案規則的兩個版本，必須保持內容完全一致。
- **雙向同步**：未來新增、修改或刪除任一規則時，必須在同一次任務同步更新同層級的另一份檔案；此要求同時適用於 Gemini 與 Codex。
- **差異處理**：開始工作先檢查對應規則是否一致；若有差異，依使用者最新明確要求整合，保留既有且未衝突的規則。無法判定的衝突先詢問，不可只依修改時間覆蓋。
- **範圍區分**：全域規則適用所有專案，專案規則僅適用該專案；同步時不可把專案專屬內容複製到全域檔案。
- **完成驗收**：規則更新後，必須逐字比對對應檔案，確認內容一致再回覆完成。
