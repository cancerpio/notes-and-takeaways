遇到 Copilot/Cursor 產出「越修越怪」、需求越改越飄？多半不是你不會下 prompt，是流程沒 Gate。

解法：把每一輪固定成「先收斂、再放大」的節奏。

```text
SDD（收斂） → Execution（落地） → Review（驗收） → Spec Sync（對齊）

[SDD]
- 把需求寫成可驗收條件（能用 yes/no 檢查）
- 一次只改 1 個主題 / 1 組驗收標準
- 產出 tasks / checklist（讓 AI 照圖施工）

[Execution]
- 先要 Execution Plan：會改哪些檔案、怎麼改、風險與 rollback
- 允許大範圍施工；你只看 diff + 抽查關鍵行為

[Review]
- 用 spec 的驗收條件逐條勾選
- 小偏離回 Execution 修；大偏離回 SDD 先修 spec

[Spec Sync]
- 把實際落地後的結構/行為/限制回寫到 spec
```

Verify
- spec 讀起來是否「清楚、可驗收、無矛盾」？（不行就先別進 Execution）
- review 時能不能拿 spec 一條條打勾？
- 這輪結束有沒有做 Spec Sync，避免下一輪照過期 spec 施工？

注意事項 / rollback
- 如果你發現 output 開始發散：先停手 → 回到 SDD 只修 spec（把驗收條件寫清楚）→ 再重跑 Execution。

#specdriven #executionfirst #acceptancecriteria #reviewgate #singlesourceoftruth
