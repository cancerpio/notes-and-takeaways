啟用2FA 與 下載Recovery Code
啟用2FA:
可以在手機裝Google Authenticator等等驗證App, 然後在 github 的 Setting(右上角) -> Authentication and Password 頁面中啟用2FA
啟用時，會出現一個QR Code，手機的驗證App掃了這個QR Code就可以新增這個帳號的2FA 即時驗證碼，之後登入時只要在驗證App中找到這個帳號的驗證碼並輸入即可。
Recover Code
當2FA相關裝置或驗證App無法啟用，或者拿不到驗證碼時，可以切換成驗證Recover Code的方式來登入　
Recover Code的取得
啟用2FA設定後，Github會給予多組Recover Code，並且可以一鍵下載，這個檔案要自己保存，之後有需要用Recover Code時就可以拿來用。
下載時，預設的檔名是: github-recovery-codes.txt
Ref
https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/recovering-your-account-if-you-lose-your-2fa-credentials