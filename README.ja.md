# 🌍 メール認証付きフルスタックTodoアプリケーション

Spring BootバックエンドとReactフロントエンドで構築された包括的なTodoアプリケーションで、メール認証システムによる安全な認証機能を提供します。

## 🌐 利用可能な言語 / Available Languages / 言語選択

- [🇰🇷 한국어](README.md) (デフォルト)
- [🇺🇸 English](README.en.md)
- [🇯🇵 日本語](README.ja.md)
- [🇨🇳 中文](README.zh.md)
- [🇪🇸 Español](README.es.md)

---

## 🚀 主要機能

### コア機能
- **ユーザー認証**: 安全な登録とログインシステム
- **メール認証**: SMTPによる6桁認証コード送信
- **Todo管理**: Todoの作成、読み取り、更新、削除、完了状態の切り替え
- **ユーザープロフィール**: 個人情報と設定の管理
- **JWT認証**: リフレッシュトークンを使用したステートレス認証

### メール認証システム
- **6桁コード**: 安全な数値認証コード
- **10分有効期限**: セキュリティのための自動コード有効期限
- **レート制限**: メール爆撃防止（1分間のクールダウン）
- **再送信機能**: ユーザーが新しいコードを要求可能
- **プロフェッショナルテンプレート**: 美しいHTMLメールテンプレート
- **アカウント有効化**: ログイン前にメール認証が必要

### セキュリティ機能
- **パスワードハッシュ化**: BCrypt暗号化
- **入力検証**: 包括的なサーバーサイド検証
- **CORS設定**: 安全なクロスオリジンリクエスト
- **ロールベースアクセス**: ユーザーと管理者ロールの管理
- **保護されたルート**: フロントエンドルートの保護

## 🛠️ 技術スタック

### バックエンド
- **フレームワーク**: Spring Boot 3.x
- **言語**: Java 17+
- **データベース**: H2（インメモリ）
- **セキュリティ**: JWTを使用したSpring Security
- **メール**: Thymeleafテンプレートを使用したSpring Boot Mail
- **ビルドツール**: Gradle

### フロントエンド
- **フレームワーク**: React 18+
- **言語**: JavaScript/JSX
- **HTTPクライアント**: インターセプター付きAxios
- **ルーティング**: React Router v6
- **状態管理**: Context API
- **スタイリング**: レスポンシブデザイン付きCSSモジュール

## 📋 前提条件

このアプリケーションを実行する前に以下が必要です：

- **Java 17+** のインストールと設定
- **Node.js 16+** とnpmのインストール
- **Gradle 7+** （または含まれるラッパーを使用）
- **メールアカウント** SMTP設定用（Gmail推奨）

## 🚀 インストールとセットアップ

### 1. リポジトリのクローン
```bash
git clone <repository-url>
cd fullstack-practice-cursor
```

### 2. バックエンド設定

#### バックエンドディレクトリに移動
```bash
cd backend
```

#### メール設定の構成
バックエンドディレクトリに`.env`ファイルを作成するか、環境変数を設定してください：

```bash
# Gmail SMTP設定
export EMAIL_USERNAME=your-email@gmail.com
export EMAIL_PASSWORD=your-app-password
export EMAIL_FROM=noreply@todoapp.com

# または.envファイルを作成：
EMAIL_USERNAME=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
EMAIL_FROM=noreply@todoapp.com
```

#### Gmailアプリパスワードの設定
1. Gmailアカウントで2段階認証を有効化
2. アプリパスワードを生成：
   - Googleアカウント設定に移動
   - セキュリティ → 2段階認証プロセス → アプリパスワード
   - 「メール」用のパスワードを生成
   - このパスワードを`EMAIL_PASSWORD`として使用

#### バックエンドのビルドと実行
```bash
# Gradleラッパーを使用
./gradlew build
./gradlew bootRun

# またはシステムGradleを使用
gradle build
gradle bootRun
```

バックエンドは`http://localhost:8080`で開始されます

### 3. フロントエンド設定

#### フロントエンドディレクトリに移動
```bash
cd app
```

#### 依存関係のインストール
```bash
npm install
```

#### 開発サーバーの開始
```bash
npm start
```

フロントエンドは`http://localhost:3000`で開始されます

## 📧 メール設定

### SMTP設定
アプリケーションはGmail SMTP用に事前設定されています：

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${EMAIL_USERNAME}
spring.mail.password=${EMAIL_PASSWORD}
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

### 代替メールプロバイダー
他のプロバイダー用に`application.properties`を修正できます：

#### Outlook/Hotmail
```properties
spring.mail.host=smtp-mail.outlook.com
spring.mail.port=587
```

#### Yahoo
```properties
spring.mail.host=smtp.mail.yahoo.com
spring.mail.port=587
```

## 🔐 デフォルト管理者アカウント

アプリケーションは起動時にデフォルト管理者ユーザーを作成します：

- **ユーザー名**: `admin`
- **パスワード**: `Admin123!`
- **メール**: `admin@example.com`
- **ステータス**: メール認証完了と有効化済み

## 📱 APIエンドポイント

### 認証
```
POST   /api/auth/register           - ユーザー登録
POST   /api/auth/verify-email       - コードによるメール認証
POST   /api/auth/resend-verification - 認証コードの再送信
POST   /api/auth/login              - ユーザーログイン
POST   /api/auth/logout             - ユーザーログアウト
GET    /api/auth/me                 - 現在のユーザー情報の取得
```

### Todos（保護されたルート）
```
GET    /api/todos          - ユーザーのtodosを取得
GET    /api/todos/{id}     - 特定のtodoを取得
POST   /api/todos          - 新しいtodoを作成
PUT    /api/todos/{id}     - todoを更新
DELETE /api/todos/{id}     - todoを削除
PATCH  /api/todos/{id}/toggle - 完了状態の切り替え
```

## 🔄 メール認証フロー

### 1. ユーザー登録
1. ユーザーが登録フォームを記入
2. システムがアカウントを作成（無効化状態）
3. 認証コードが生成され送信される
4. ユーザーが認証ページにリダイレクトされる

### 2. メール認証
1. ユーザーがメールで6桁コードを受信
2. ユーザーが認証フォームにコードを入力
3. システムがコードと有効期限を検証
4. アカウントが有効化され有効になる
5. 歓迎メールが送信される
6. ユーザーがログインページにリダイレクトされる

### 3. ログインアクセス
1. ユーザーが認証情報でログイン
2. システムがメール認証状態を確認
3. 認証済みの場合、JWTトークンが生成される
4. 保護されたルートへのユーザーアクセスが許可される

## 🎨 メールテンプレート

アプリケーションには3つのプロフェッショナルなメールテンプレートが含まれています：

1. **認証メール**: 認証コードが含まれた歓迎メッセージ
2. **歓迎メール**: 成功した認証後に送信
3. **パスワードリセット**: 将来のパスワードリセット機能用

すべてのテンプレートはレスポンシブで以下を含みます：
- プロフェッショナルなブランディング
- 明確な行動喚起ボタン
- セキュリティ通知と有効期限警告
- モバイルフレンドリーなデザイン

## 🧪 テスト

### バックエンドテスト
```bash
cd backend
./gradlew test
```

### フロントエンドテスト
```bash
cd app
npm test
```

### メールテスト
1. テスト用の実際のメールアカウントを使用
2. メールが届かない場合はスパムフォルダを確認
3. SMTP認証情報が正しいことを確認
4. 複数のリクエストを送信してレート制限をテスト

## 🐛 トラブルシューティング

### 一般的な問題

#### メールが送信されない
- SMTP認証情報を確認
- Gmailアプリパスワードが正しいことを確認
- Gmailで2FAが有効になっていることを確認
- ファイアウォール/ネットワーク制限を確認

#### 認証コードの問題
- コードは10分後に期限切れ
- 最大5回の認証試行
- 再送信リクエスト間の1分間クールダウン
- メールのスパムフォルダを確認

#### ビルドエラー
- Java 17+がインストールされていることを確認
- Gradleバージョンの互換性を確認
- すべての依存関係が解決されていることを確認

#### フロントエンドの問題
- ブラウザキャッシュとlocalStorageをクリア
- JavaScriptエラーのためにコンソールを確認
- バックエンドがポート8080で実行されていることを確認

### デバッグモード
`application.properties`でデバッグログを有効化：
```properties
logging.level.com.example.todoapp=DEBUG
logging.level.org.springframework.mail=DEBUG
```

## 🔒 セキュリティ考慮事項

- **認証コードは10分後に期限切れ**
- **レート制限**でメール爆撃を防止
- **最大試行回数**でブルートフォース攻撃を制限
- **本番環境ではHTTPS必須**
- **機密データ用の環境変数**
- **すべてのエンドポイントでの入力検証**

## 🚀 本番環境デプロイ

### 環境変数
本番環境の値を設定：
- `jwt.secret`: 強力でユニークな秘密鍵
- `spring.mail.username`: 本番環境のメールアカウント
- `spring.mail.password`: 本番環境のアプリパスワード
- データベース接続の詳細

### セキュリティヘッダー
本番環境でセキュリティヘッダーを有効化：
- HTTPS強制
- CORS制限
- レート制限
- 入力サニタイゼーション

## 📝 貢献

1. リポジトリをフォーク
2. 機能ブランチを作成
3. 変更を加える
4. 新機能のテストを追加
5. プルリクエストを提出

## 📄 ライセンス

このプロジェクトはMITライセンスの下でライセンスされています - 詳細はLICENSEファイルを参照してください。

## 🤝 サポート

サポートと質問：
- リポジトリにイシューを作成
- トラブルシューティングセクションを確認
- APIドキュメントを確認

## 🎯 ロードマップ

- [ ] パスワードリセット機能
- [ ] 2段階認証
- [ ] ソーシャルログイン統合
- [ ] モバイルアプリ開発
- [ ] 高度なtodo機能（カテゴリ、優先度）
- [ ] チームコラボレーション機能
- [ ] APIレート制限
- [ ] 包括的なテストカバレッジ

---

**楽しいコーディングを！🎉**
