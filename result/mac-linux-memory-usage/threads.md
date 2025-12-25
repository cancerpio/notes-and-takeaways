macOS/Linux 上看到「記憶體快滿（31GB/32GB）但壓力低、系統還很順」？多半不是 RAM 不夠，是 OS 在用 RAM 當檔案快取。

解法：不要看 top 的 `unused`，改看「可立即釋放/可用」指標 + swap 活動。

```bash
# macOS：看可釋放比例 + swap
memory_pressure

# Linux：看 available / MemAvailable
free -h
cat /proc/meminfo | grep MemAvailable
```

Verify
- macOS：`System-wide memory free percentage >= 60%` 且 `Swapins/Swapouts = 0` → 多半正常
- Linux：`free -h` 的 `available` 還有餘裕，且 swap 使用量為 0（或不持續上升）→ 多半正常
- 危險訊號：free% < 40% 或 swap 開始增加，且你明顯變慢

注意事項 / rollback
- 不要為了「看起來空」去常態清快取/重開機；真的有壓力再查高記憶體進程。

#memory_pressure #MemAvailable #pagecache #swap