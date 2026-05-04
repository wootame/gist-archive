# Cloudflare Wrangler コマンドリファレンス

## セットアップ

**バージョン確認**
```bash
wrangler --version
```

**グローバルインストール（npm）**
```bash
npm install -g wrangler
```

**ログイン**
```bash
wrangler login
```

**ログイン状態確認**
```bash
wrangler whoami
```

## プロジェクト作成

**Workers プロジェクト作成（推奨）**
```bash
npm create cloudflare@latest <project_name>
```

**既存ディレクトリで Wrangler 初期化**
```bash
wrangler init
```

## 開発・デプロイ

**ローカル開発サーバー起動**
```bash
wrangler dev
```

**環境を指定してローカル起動**
```bash
wrangler dev --env <environment_name>
```

**本番デプロイ**
```bash
wrangler deploy
```

**環境を指定してデプロイ**
```bash
wrangler deploy --env <environment_name>
```

## 設定・運用

**シークレット登録**
```bash
wrangler secret put <KEY>
```

**シークレット一覧**
```bash
wrangler secret list
```

**実行ログを追跡**
```bash
wrangler tail
```

**デプロイ履歴一覧**
```bash
wrangler deployments list
```

**Workers 設定ファイルを検証**
```bash
wrangler deploy --dry-run
```

## よく使うオプション

**設定ファイルを指定**
```bash
wrangler deploy --config wrangler.toml
```

**環境指定（staging / production など）**
```bash
wrangler <command> --env <environment_name>
```

**互換日付を上書き**
```bash
wrangler dev --compatibility-date <YYYY-MM-DD>
```
