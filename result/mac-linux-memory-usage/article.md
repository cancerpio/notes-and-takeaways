# macOS / Linux：記憶體顯示高使用但壓力低，如何快速判斷與檢查

**Environment:** macOS (memory_pressure, vm_stat) / Linux (free -h, /proc/meminfo) — local / server

## Symptoms
- 總記憶體顯示接近滿載（例如 31GB/32GB），但系統仍順暢、少卡頓
- 活動監視器或指令顯示記憶體壓力為「低」，或 Swap I/O 為 0
- top 的 `unused` 很小，但沒有單一程式佔大量記憶體

## Quick Fix ✅（可複製）
```bash
# macOS：查看系統可立即釋放的記憶體比例
memory_pressure

# Linux：查看 Available 欄位
free -h
# 或
cat /proc/meminfo | grep MemAvailable
```
重點：看 macOS 的 `System-wide memory free percentage`（>=60% 通常正常）或 Linux 的 `Available` 欄位；同時確認 Swapins/Swapouts 為 0 即無 swap 活動。

## Why It Happens（1~3 點）
- 現代 OS 會把閒置記憶體當作檔案快取（macOS 的 Inactive / Linux 的 Page Cache），以提高 I/O 效能。
- 這些快取是「可立即釋放」的，並非不可回收的占用，所以總使用量高不等於有壓力。
- 系統也會使用記憶體壓縮（macOS 的 Compressed Memory、Linux 的 zswap/zram）來延緩使用 swap。

## Verify（具體步驟 & 預期）
1. macOS
   - 執行：`memory_pressure`
   - 預期：`System-wide memory free percentage >= 60%` → ✅ 健康；`Swapins: 0`、`Swapouts: 0` → ✅ 無 swap 活動
   - 危險訊號：`System-wide memory free percentage < 40%` 或有 Swapins/Swapouts → ⚠️ 需調查
2. Linux
   - 執行：`free -h`，看 `available` 欄位；或 `cat /proc/meminfo | grep MemAvailable`
   - 預期：`Available` 與總記憶體相比仍有餘地，且 swap 使用為 0 → ✅ 健康
   - 危險訊號：`Available` 很低或出現 swap I/O → ⚠️ 找出高記憶體進程（`ps aux --sort=-%mem`）並評估
3. 範例輸出（參考）
   - macOS:
     ```
     System-wide memory free percentage: 72.41
     Swapins: 0
     Swapouts: 0
     ```
   - Linux:
     ```
                   total        used        free      shared  buff/cache   available
     Mem:           62Gi       25Gi       2.0Gi       512Mi       35Gi       35Gi
     Swap:          16Gi         0B         16Gi
     ```

## Steps when 不健康（簡短）
- 先備份/紀錄指標（`memory_pressure` / `free -h` / `vmstat`），以便回溯。
- 找出高記憶體進程：`top` 或 `ps aux --sort=-%mem`，評估是否重啟或調整配置。
- 若系統頻繁進入 swap：考慮增加實體記憶體、建立/擴充 swap、或調整應用的記憶體限制。

## Notes / Risk & Rollback
- 不建議常態性清除檔案快取或把重啟當作常態解（會降低效能）。
- 若你要改系統參數或新增 swap，先 commit/備份設定並測試：變更後用相同指令驗證是否改善（`memory_pressure` / `free -h`）。
- 延伸關鍵字：memory_pressure、MemAvailable、Page Cache、Compressed Memory、zswap

---

**Short summary:** 高記憶體使用量多半由檔案快取造成，不代表系統有問題；先檢查「可用性」與 swap 活動，只有在 free% 很低或有 swap I/O 時才進一步處理。