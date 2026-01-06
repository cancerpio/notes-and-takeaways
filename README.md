# Notes & Takeaways

This repo is a writing assistance pipeline:

- material/<topic>/ : raw notes, errors, commands, and context (raw truth)
- result/<topic>/   : organized materials and analysis reports
  - organized-draft.md  (分類整理後的草稿)
  - analysis.md        (分類報告、結構建議、重點建議)
  - enhancement.md     (深度分析和寫作增強建議，可選)

## Rules

- Hard rules (non-negotiable): .specify/memory/constitution.md
- Soft rules + output contract: .specify/memory/spec.md

Important:
- Never generate outputs on the `master` branch.
- Each generation must only touch a single topic:
  material/<topic>/ -> result/<topic>/

## Workflow: Organize materials and get writing suggestions

1) Create a branch:
- git checkout -b post/<topic>

2) Create folders:
- material/<topic>/
- result/<topic>/
- specs/<topic>/ (optional)

3) Write raw notes:
- material/<topic>/draft.md (required)
- snippets.md / context.md / links.md (optional)

4) Organize materials and get analysis (Copilot Chat / prompt files):
- /gen-article topic=<topic>
  - 產生：organized-draft.md（整理後的草稿）
  - 產生：analysis.md（分類報告、結構建議、重點建議）

5) Get enhancement suggestions (optional):
- /gen-short topic=<topic>
  - 產生：enhancement.md（深度分析和寫作增強建議）

If your environment doesn't support `topic=<topic>` arguments:
- run /gen-article then add: topic: <topic>
- run /gen-short then add: topic: <topic>

6) Review the organized materials and suggestions:
- result/<topic>/organized-draft.md（查看分類整理後的內容）
- result/<topic>/analysis.md（查看結構建議和重點）
- result/<topic>/enhancement.md（查看深度分析和優化建議，如果有執行）

7) Write your article based on the suggestions:
- 使用整理後的草稿作為基礎
- 參考建議的結構和重點
- 根據增強建議優化內容

8) Commit + PR merge back to master.