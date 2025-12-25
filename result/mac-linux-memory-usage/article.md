# macOS memory_pressure / Linux free -h：記憶體顯示快滿但壓力低，如何判斷是否真的缺 RAM

## Environment
- macOS / Linux / local（或 server）

## Symptoms
- top / 活動監視器顯示記憶體快滿（例如 31GB/32GB），但系統仍順暢、記憶體壓力「低」
- top 的 `unused` 很少，讓你以為「RAM 不夠」
- 你想確認：到底是正常快取？還是真的要擔心 swap / 記憶體壓縮？

## Quick Fix
```bash
# macOS：看「系統可立即釋放」的比例 + swap 活動
memory_pressure

# Linux：看 Available（可用，含可釋放快取）
free -h
# 或
cat /proc/meminfo | grep MemAvailable
```
- 重點：不要只看「總使用量」或 `unused`；改看 macOS 的 `System-wide memory free percentage` / Linux 的 `available`。
- 同時確認是否有 swap 活動（macOS 的 Swapins/Swapouts、Linux 的 Swap 使用量/活躍度）。

## Why It Happens
- 現代 OS 會把閒置 RAM 當檔案快取（macOS 的 Inactive / Linux 的 page cache），提升 I/O 效能
- 這類快取「需要時可釋放」，所以「看起來用很多」不等於「真的有壓力」
- top 的 `unused` 更像「完全閒置」，不是「可用」；Linux 的 `available` 才接近「真的還能用多少」

## Verify
1) macOS
- 執行：`memory_pressure`
- 期待：
   - `System-wide memory free percentage >= 60%`：多半正常
   - `Swapins: 0` 且 `Swapouts: 0`：沒有在用交換空間（通常代表 RAM 還夠）
- 需要注意：
   - `System-wide memory free percentage < 40%` 或 Swapins/Swapouts 開始上升，且體感變慢

2) Linux
- 執行：`free -h`
- 期待：
   - `available` 還有餘裕（相對於 total 不是貼地）
   - `Swap` 行顯示使用量為 0（或很低且不持續上升）
- 備用：`cat /proc/meminfo | grep MemAvailable` 看 `MemAvailable`

## Notes
- 風險：為了「看起來空」去常態清快取/重開機，通常只會讓效能變差，且治標不治本。
- Rollback：如果你真的做了調整（例如改 swap 相關設定或應用記憶體限制），用同一組指標回驗（`memory_pressure` / `free -h`）來確認有沒有改善。
- Keywords：memory_pressure、MemAvailable、page cache、swap