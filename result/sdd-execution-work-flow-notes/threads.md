問題一句話
在 SDD（Spec-driven）與 Execution（Execution-first）之間切換會造成節奏不一致、或 `specify init --here --force` 覆蓋自訂檔案，該怎麼檢查與回復？

解法（可複製）
```bash
# 先儲存現狀，避免被覆寫
git add -A && git commit -m "chore: save spec files before spec-kit init"

# 檢查專案健康狀態
specify check

# 若要升級模板或工具（已 commit），再執行
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
specify init --here --force
```

Verify
- `specify check` 預期回傳 pass，或列出可修正的項目 ✅
- `ls -la .specify .github/prompts` 可看到 `constitution.md`、`*.prompt.md` 等檔案 ✅
- 升級後用 `git diff` 檢查變更，必要時用 `git restore <file>` 還原 ✅

注意 / rollback
- 風險：`--force` 會覆蓋手動修改，升級前務必先 commit 或建立新 branch。⚠️
- 回復方法：`git restore <file>`、`git checkout -- <file>` 或 revert commit。

#SDD #SpecKit #SpecifyCLI