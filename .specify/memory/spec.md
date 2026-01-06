# .specify/memory/spec.md
# Editorial Spec (Soft Rules + Output Contract)

## 系列定位
- Series name: Notes & Takeaways
- 可選一句話：Short fixes and lessons from real-world debugging.

## 目標
- 協助作者整理和組織寫作材料
- 透過分類和分析，幫助作者發現文章結構和重點
- 提供具體建議，但保留作者的判斷和創作空間
- 最終以協助作者產出累積社群可見度 / 話語權，並留下可回顧的，有價值的文章或短文為目標

## 產出物（必須遵守）
- 整理後的草稿：`result/<topic>/organized-draft.md`
- 分析報告：`result/<topic>/analysis.md`

## 整理後的草稿格式（必須遵守）
`result/<topic>/organized-draft.md` 應包含：

1) 原始材料摘要
- 列出所有讀取的原始檔案和其主要內容概述

2) 分類後的內容
- 依照性質和目的將材料分類（例如：問題描述、解決方案、背景資訊、參考資料等）
- 每個分類下包含：
  - 分類說明（為什麼這樣分類）
  - 該分類下的所有內容片段
  - 每個片段標註來源（檔案名、段落位置）

3) 重複或矛盾資訊標記
- 若發現重複內容，標記並說明
- 若發現矛盾資訊，標記並說明可能的解釋

4) 待補充資訊
- 指出材料中可能缺少的重要資訊
- 建議需要進一步收集的資料

## 分析報告格式（必須遵守）
`result/<topic>/analysis.md` 應包含：

1) 資料分類報告
- 分類架構說明（分類標準、各分類的定義）
- 各分類的內容統計（數量、重要性評估）
- 分類之間的關聯性分析

2) 建議的文章結構
- 基於材料內容，建議的文章大綱
- 每個章節應包含：
  - 章節標題建議
  - 該章節應涵蓋的內容（對應到分類後的資料）
  - 章節之間的邏輯順序說明
  - 預估篇幅或重點程度

3) 最有價值必講的點
- 列出 3-7 個最重要的觀點或資訊
- 每個點應包含：
  - 為什麼重要（對讀者的價值）
  - 對應的材料來源
  - 建議的呈現方式（段落、條列、範例等）
  - 在文章結構中的建議位置

4) 寫作建議
- 目標讀者分析（基於材料內容推斷）
- 適合的文風建議
- 可能的標題方向（2-3 個選項）
- 需要特別注意的事項（技術細節、風險、驗證方式等）

## 生成管線契約（必須遵守）
- 生成器只能讀：
  - `material/<topic>/` 內所有 md（含可選的 draft/snippets/context/links）
  - （可選）`specs/<topic>/spec.md`
  - `.specify/memory/constitution.md`
  - `.specify/memory/spec.md`
- 生成器只能寫：
  - `result/<topic>/organized-draft.md`
  - `result/<topic>/analysis.md`
- 不得修改 `material/`，不得動到其他 `<topic>`。
