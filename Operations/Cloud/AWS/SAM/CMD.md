# AWS SAM コマンドリファレンス

## 初期設定

**バージョン確認**
```bash
sam --version
```

**新規プロジェクト作成**
```bash
sam init
```

**テンプレート検証**
```bash
sam validate
```

## ビルド・ローカル実行

**ビルド**
```bash
sam build
```

**キャッシュ利用でビルド高速化**
```bash
sam build --cached
```

**関数をローカル実行**
```bash
sam local invoke <logical_id>
```

**イベントファイルを指定して実行**
```bash
sam local invoke <logical_id> -e events/event.json
```

**API をローカル起動**
```bash
sam local start-api
```

**Lambda エミュレーターをローカル起動**
```bash
sam local start-lambda
```

## デプロイ

**ガイド付きデプロイ（初回推奨）**
```bash
sam deploy --guided
```

**設定ファイルを使ってデプロイ**
```bash
sam deploy
```

**ビルドからデプロイまで一括**
```bash
sam build && sam deploy
```

**パラメータ上書きしてデプロイ**
```bash
sam deploy --parameter-overrides Stage=dev LogLevel=info
```

## 開発補助

**関数ログ確認**
```bash
sam logs -n <function_name> --stack-name <stack_name> --tail
```

**差分同期（クラウド反映を高速化）**
```bash
sam sync --watch
```

**デプロイ済みスタックを削除**
```bash
sam delete --stack-name <stack_name>
```

## LocalStack 連携でよく使う例

**LocalStack エンドポイントへ API 呼び出し**
```bash
sam local start-api --docker-network localstack-network
```

**テンプレート内パラメータを使ってエンドポイント切替**
```bash
sam deploy --parameter-overrides AwsEndpoint=http://host.docker.internal:4566
```
