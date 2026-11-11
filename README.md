# Happy sugar 無料相談フォーム

## 構成
- index.html: スマホ対応フォーム、Cloudflare Turnstile、Supabase Edge Function送信
- Supabase Edge Function: submit-consultation (別途デプロイ済み)
- Supabase tables: hs_customers, hs_inquiries

## 公開前チェック（必須）
1. GitHub Pages: Settings > Pages > Deploy from a branch > main / (root)。
2. 独自ドメイン: consult.happysugar.online をPagesに設定し、WixのDNSで `consult` CNAMEを `happysugar-system.github.io` に向ける。既存のMX/SPF/DKIMは変更しない。
3. HTTPSが有効になってからアクセス。
4. Supabase Edge FunctionのJWT legacy verificationがOFFか確認。
5. Secrets: ALLOWED_ORIGINS=https://consult.happysugar.online, TURNSTILE_SECRET_KEY。Supabaseの既定のSUPABASE_URL / SUPABASE_SERVICE_ROLE_KEYが利用可能か確認。
6. Cloudflare Turnstileの許可ホスト名に consult.happysugar.online を設定。
7. 送信テストで hs_customers と hs_inquiries の両方に登録されることを確認。
8. 本番前にプライバシー説明・問い合わせ先・保管期間・委託先の扱いを事業者として確認。
9. Edge Functionの送信回数制限、Turnstileのhostname/action検証、監視・通知を追加してから本格集客を開始。
10. 添付ファイル機能は未実装。管理画面も未実装。

## 注意
- GitHubリポジトリはPublic。secret/service_roleキー、個人情報、実データは絶対にコミットしない。
- Site KeyとEdge Function URLは公開用の値。
- Originチェックは認証ではない。サーバー側のTurnstile検証とレート制限が必要。
