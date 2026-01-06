repo/
├─ material/
│  └─ <topic>/
│     ├─ draft.md              # 原始草稿（像 issue 一樣，允許很亂）
│     ├─ snippets.md           # 指令/config/code（Optional）
│     ├─ context.md            # 背景/環境/做過什麼（Optional）
│     ├─ links.md              # 參考/關鍵字（Optional）
│     └─ assets/               # 圖/截圖（Optional）
│
├─ result/
│  └─ <topic>/
│     ├─ organized-draft.md    # AI 整理分類後的草稿
│     ├─ analysis.md           # AI 產生的分析報告（分類、結構建議、重點）
│     └─ enhancement.md        # AI 產生的深度分析和寫作增強建議（Optional）
│
├─ specs/
│  └─ <topic>/
│     └─ spec.md               # 這一篇的額外偏好/限制（Optional）
│
├─ .specify/
│  └─ memory/
│     ├─ constitution.md       # 硬規則（不可違背）
│     └─ spec.md               # 軟規則 + 輸出格式契約（盡量做到）
│
├─ .github/
│  └─ prompts/
│     ├─ gen-article.prompt.md    # 整理材料和產生分析報告的 prompt
│     └─ gen-short.prompt.md      # 深度分析和寫作增強建議的 prompt
|
├─ RUNBOOK.md                  # 操作流程（SOP）
└─ README.md
