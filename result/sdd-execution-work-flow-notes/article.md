# Copilot/Cursor 產出越修越怪：用 SDD→Execution→Review→Spec Sync 把協作流程拉回正軌

## Environment
- macOS / 同一個 repo 內用 VS Code + Copilot、Cursor 來寫作或開發

## Symptoms
- 一直在改 output（文章/程式輸出），但結果「越修越怪」、方向開始飄
- spec 跟現況分裂：你以為的規格 ≠ repo 真的長相，下一輪 AI 會照錯的 spec 施工
- 需求講成「想法」，沒有變成「可驗收條件」，導致 AI 只能自由發揮

## Quick Fix
```text
把每一輪都固定成：
SDD（收斂） → Execution（落地） → Review（驗收） → Spec Sync（對齊）

---

[SDD / 收斂]
- 把需求寫成可驗收條件（能用 yes/no 檢查）
- 一次只改 1 個主題 / 1 組驗收標準
- 產出 tasks / checklist（讓 AI 照圖施工）
- Gate：spec 清楚、可驗收、無矛盾，才進 Execution

[Execution / 落地]
- 先要「Execution Plan」：會改哪些檔案、怎麼改、風險與 rollback
- 允許大範圍改動（重構/搬檔/補內容），以「把事情做完」為優先
- 你只做兩件事：看 diff + 抽查關鍵行為/段落（不要在這階段重新發散 spec）

[Review / 驗收]
- 用 spec 的驗收條件逐條對照成果（spec 是裁判，不是參考）
- 小偏離：回到 Execution 修
- 大偏離：回到 SDD 先修 spec（避免越修越亂）

[Spec Sync / 對齊]
- 把真正落地後的結構/行為/限制/已知 trade-off 回寫到 spec
- 原則：spec 不能落後到會誤導下一輪施工
```
- 重點是「先收斂再放大」：SDD 把邊界畫清楚，Execution 才能放心讓 agent 大量施工。
- 一旦你感覺「越改越怪」，就立刻回到 SDD，把 spec 收斂到可驗收再繼續。

## Why It Happens
- 沒有單一真相（single source of truth）：spec 不完整或過期，導致產出方向漂移
- 沒有 Gate：不夠清楚就進 Execution，後面只能用輸出反推需求，越修越亂
- 變更粒度太大：一次改太多主題，review 無法有效判斷哪裡偏了

## Verify
- 10 秒自檢：往下滑前，你能不能直接複製「本輪 checklist」開始做（且不需要腦補）
- SDD Gate：spec 是否滿足「清楚、可驗收、無矛盾」？（不滿足就不要進 Execution）
- Review Gate：拿 spec 的驗收條件逐條勾選，是否全部能打勾？
- Spec Sync：這輪落地後，有沒有把「真正發生的變更」同步回 spec，避免下一輪照舊 spec 施工？

## Notes
- 風險：Execution 階段若你同時改 spec + 改實作/內容，容易失控；建議把 spec 變更集中在 SDD。
- Rollback：如果 output 開始發散，先停手 → 回到 SDD 只修 spec（把驗收條件寫清楚）→ 再重跑 Execution。
- Keywords：spec-driven development、execution-first、acceptance criteria、single source of truth、review gate
