# .specify/memory/spec.md
# Editorial Spec (Soft Rules + Output Contract)

## 系列定位
- Series name: Notes & Takeaways
- 可選一句話：Short fixes and lessons from real-world debugging.

## 目標
- 把踩雷經驗轉成「可被搜尋、可快速套用」的短文
- 不給自己太大負擔，但能持續輸出價值
- 累積社群可見度/話語權，同時留下可回顧紀錄

## 文風（盡量做到）
- 口語、直接、少形容詞多動詞
- 原理只講到「避免再踩一次」的程度，不寫教科書
- 優先用小標 + 條列，避免大段敘述

## 產出物（必須遵守）
- 長文輸出：`result/<topic>/article.md`
- 短文輸出：`result/<topic>/threads.md`

## 長文結構（必須遵守，順序固定）
1) Title
- 必須是可被 Google 的句子（工具名 + 錯誤/症狀 + 目標）

2) Environment（1 行）
- OS / tool version / 場景（local / CI / container 等）

3) Symptoms（1~3 點）
- error message / 症狀 / 你原本要做什麼

4) Quick Fix（可複製 block）
- 一段 command/config/code block
- block 下方補 1~2 句重點（做了什麼、限制是什麼）

5) Why It Happens（1~3 點）
- 只講到能避免再踩一次即可

6) Verify（具體步驟）
- 指令 / 期待輸出 / 檢查方式

7) Notes（可選）
- 風險 / rollback / 延伸關鍵字（2~5 個）

## Threads 短文結構（必須遵守）
- 以短段落呈現，避免長段落
必須包含：
1) 問題一句話（工具 + 症狀）
2) 解法（可複製 block）
3) Verify（1~3 點）
4) 注意事項/rollback（必要才寫）
5) #keywords（可選）

## 生成管線契約（必須遵守）
- 生成器只能讀：
  - `material/<topic>/` 內所有 md（含可選的 snippets/context/links）
  - （可選）`specs/<topic>/spec.md`
  - `.specify/memory/constitution.md`
  - `.specify/memory/spec.md`
- 生成器只能寫：
  - `result/<topic>/article.md`
  - `result/<topic>/threads.md`
- 不得修改 `material/`，不得動到其他 `<topic>`。
