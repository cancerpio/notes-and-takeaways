# .specify/memory/constitution.md
# Hard Rules (Non-negotiables)

## 0) 防呆：禁止在 master 上生成
- 當目前 git branch 為 `master` 時，禁止執行任何會生成/覆寫 `result/` 的動作。
- 只能在文章分支（例如 `post/<topic>`）上生成，避免誤把所有文章重生覆蓋。

## 1) 資料流與權限
- `material/<topic>/` 是 raw truth：不得被生成器修改。
- 生成器只允許新增/覆寫：
  - `result/<topic>/article.md`
  - `result/<topic>/threads.md`
- 禁止掃描、改寫其他 `<topic>` 的任何檔案。

## 2) 篇幅（必須遵守）
- `result/<topic>/article.md` 閱讀時間必須 <= 6 分鐘。
- 長段落（> 5 行）必須拆段或改條列。

## 3) 開頭先給解法（必須遵守）
- 文章開頭 10 秒內必須出現可直接複製的解法（command/config/code block）+ 1~2 句重點。
- 讀者不往下滑也要能解掉 80% 問題。

## 4) 標題必須可被搜尋（必須遵守）
- 標題要像「遇到問題的人會拿去 Google 的句子」：
  - 工具/產品名（Docker/Postgres/Spring/Kafka...）
  - 症狀或 error message 關鍵片段
  - 讀者目標（想修什麼 / 想做到什麼）

## 5) 必須可驗證、可回退
- 必須提供 Verify：如何確認修好了（指令/輸出/檢查步驟）。
- 若修法有風險（清資料、改全域設定、影響環境），必須提供警告與 rollback（或替代做法）。

## 6) 不洩漏機密（必須遵守）
- 不得輸出公司/客戶/內網資訊、token、帳密、真實機器識別資訊。
- 一律使用 placeholder（<YOUR_TOKEN>、<INTERNAL_URL>、<PROJECT_ID>）。

## 7) 通俗，但禁止硬幽默（必須遵守）
- 允許：口語、像跟同事分享。
- 禁止：為了有趣硬套梗、迷因式標題（除非真的有助搜尋且不尷尬）。