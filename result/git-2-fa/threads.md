GitHub 登入想開 2FA，但最怕換手機/驗證器壞掉就「拿不到驗證碼、進不去帳號」。

做法：把 2FA 打開，並立刻把 recovery codes 下載離線保存（這是你的救命鑰匙）。

```
GitHub → Settings → Password and authentication（或 Authentication and password）
1) Two-factor authentication → Enable
2) 用 Google Authenticator / 其他驗證器 App 掃 QR code
3) 下載並保存 Recovery codes（預設檔名常見是 github-recovery-codes.txt）
```

Verify（確認自己真的準備好了）
- 登出再登入一次：會要求你輸入驗證器的一次性代碼
- 在 Settings 頁面確認 2FA 顯示為 Enabled
- 確認 recovery codes 已放到安全位置（密碼管理器/加密硬碟/離線保管），不是放在 Repo 或雲端公開資料夾

注意事項 / Rollback
- recovery codes 等同「備用密碼」，外流就有風險；請當成密碼等級保護
- 如果你懷疑 codes 外流，去 GitHub 重新產生（舊的會失效）
- 真的拿不到驗證器代碼時：改用 recovery code 登入

#GitHub #2FA #Authenticator #RecoveryCodes #AccountSecurity
