# Spec Kit / SDD：在 SDD 與 Execution 模式間該如何切換、檢查與回溯

**Environment:** Repository with Specify CLI & .specify, VS Code (Copilot Chat) — local / CI

## Symptoms
- 不確定該「改 spec」還是該「直接執行改動」（Spec 與實作越拉越遠）
- `specify init --here --force` 覆蓋自訂檔案或 Slash Command 沒出現
- AI 產出的結果與 Spec 不一致、導致 review 時反覆重工

## Quick Fix ✅（可複製）
```bash
# 先儲存現狀，避免被覆寫
git add -A && git commit -m "chore: save spec files before spec-kit init"

# 檢查專案狀態與缺失
specify check

# 若要拿新模板或升級工具（**升級前請先 commit**）
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
specify init --here --force
```
重點：在執行可能會覆蓋檔案的操作前務必 commit；用 `specify check` 判斷缺失，並用 `git diff`/`git restore` 回退不想接受的變更。

## Why It Happens（簡短）
- SDD（Spec-driven）與 Execution（Execution-first）是兩種不同心流：前者優先收斂 Spec，後者優先把工作做完，混用時會產生節奏不一致。 
- `--force` / 升級模板會直接覆寫 repo 裡的憲法 / prompt / template，若沒有先 commit 就會丟失手動調整。 
- AI Agent（不同 assistant）在理解 Prompt / Prompt File 的方式不同，未載入或未啟用時 Slash Command 不會顯示或生效。

## Verify（具體步驟 & 預期）
1. 儲存並檢查差異
   - `git status`、`git diff` → 確認已 commit 重要變更
2. 檔案存在性 / 健康檢查
   - `ls -la .specify .github/prompts` → 預期看到 `constitution.md`、`*.prompt.md` 等
   - `specify check` → 預期返回 pass 或列出明確可修正的項目
3. 在 IDE 測試 Slash Command
   - 在 Copilot Chat 輸入 `/speckit.constitution` → 預期看到對應提示選項
4. 升級後驗證
   - 執行 `specify init --here --force`（**已 commit**），再用 `git diff` 確認變更；必要時用 `git restore <file>` 還原

## Steps when workflow breaks（簡潔流程）
- 若發現被覆寫：用 `git restore` 或 `git checkout -- <file>` 還原，或從先前 commit revert。 
- 若 AI 產出與 Spec 不一致：暫停 Execution，回到 SDD 階段調整規格（把驗收條件寫清），再讓 Agent 重做。 
- 定期執行 Spec Sync：把實際落地的行為與決策回寫到 `.specify`（避免 spec 跑掉）。

## Notes / Risk & Rollback
- 風險：`specify init --here --force` 會覆蓋手動修改的檔案；升級前務必 commit 或建立新 branch。 
- Rollback：用 `git diff` 確認改動，`git restore <file>` 或 revert commit；若是模板衝突，先比較再合併變更。
- 小技巧：把常用 prompt 轉成 `.github/prompts/*.prompt.md`，並在 `.specify/memory/constitution.md` 建立基本規範（teams 的 “合約”），可減少誤用。 

---

**Short summary:** 在 SDD 與 Execution 間切換時，先 commit 再動 `specify init --force`；用 `specify check` 驗證專案健康，若 AI 產出偏離 Spec，回到 SDD 收斂 Spec 後再執行。