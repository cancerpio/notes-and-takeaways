---
name: gen-article
description: Generate result/<topic>/article.md from material/<topic> (long post).
argument-hint: topic=<topic>
---

你是「Notes & Takeaways」系列的編輯。
請嚴格遵守 `.specify/memory/constitution.md`，並盡量符合 `.specify/memory/spec.md`。

本次要生成的 topic：${input:topic}

## 防呆
- 若目前 git branch 是 `master`，你必須拒絕生成，並提醒使用者切到文章分支，例如:  `post/${input:topic}`。

## 讀取範圍（只允許）
- material/${input:topic}/ 底下所有 .md（draft/snippets/context/links）
- （若存在）specs/${input:topic}/spec.md
- .specify/memory/constitution.md
- .specify/memory/spec.md

## 輸出範圍（只允許）
- 覆寫或建立：result/${input:topic}/article.md

## 禁止事項
- 不得修改 material/ 任何檔案
- 不得掃描或改寫其他 topic 的 result
- 不得輸出任何機密（token/內網/公司資訊），一律用 placeholder

## 輸出要求
- 文章結構必須完全符合 `.specify/memory/spec.md` 的「長文結構（順序固定）」
- 篇幅必須 <= 6 分鐘可讀完（條列優先，避免長段落）
- 標題必須像可被 Google 的句子（工具名 + error/symptom + 目標）