repo/
├─ material/
│  └─ <topic>/
│     ├─ draft.md              # 原始草稿（像 issue 一樣，允許很亂）
│     ├─ snippets.md           # 指令/config/code（可選）
│     ├─ context.md            # 背景/環境/做過什麼（可選）
│     ├─ links.md              # 參考/關鍵字（可選）
│     └─ assets/               # 圖/截圖（可選）
│
├─ result/
│  └─ <topic>/
│     ├─ article.md            # AI 生成的可發佈長文（<= 6 分鐘）
│     └─ threads.md            # AI 生成的 Threads 摘要
│
├─ specs/
│  └─ <topic>/
│     └─ spec.md               # 這一篇的額外偏好/限制（可選）
│
├─ .specify/
│  └─ memory/
│     ├─ constitution.md       # 硬規則（不可違背）
│     └─ spec.md               # 軟規則 + 輸出格式契約（盡量做到）
│
|─ prompts/
|  ├─ gen-article.prompt.md    # 生成本文的 prompt（根目錄）
|  └─ gen-short.prompt.md      # 生成 Threads 摘要的 prompt（根目錄）
|
├─ RUNBOOK.md                  # 操作流程（SOP）
└─ README.md
