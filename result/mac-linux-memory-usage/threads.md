問題一句話
macOS / Linux 顯示記憶體高使用但系統仍流暢，該怎麼判斷是否需要處理？

解法（可複製）
```bash
# macOS
memory_pressure

# Linux
free -h
# 或
cat /proc/meminfo | grep MemAvailable
```

Verify
- macOS：`System-wide memory free percentage >= 60%`，且 `Swapins/Swapouts == 0` → ✅ 健康
- Linux：`Available` 欄位有餘地且無 swap 活動 → ✅ 健康

注意 / rollback
- 不要常態清除檔案快取或隨意重啟；先紀錄指標（`memory_pressure` / `free -h` / `vmstat`）再處理。
- 若需改系統參數或新增 swap，先備份/commit 設定並測試，變更後用相同指令驗證。

#macOS #Linux #memory #sysadmin