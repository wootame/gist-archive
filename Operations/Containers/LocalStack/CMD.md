# LocalStack コマンドリファレンス

## 起動・停止

**Docker Compose で起動**
```bash
docker compose up -d
```

**ログ確認**
```bash
docker compose logs -f localstack
```

**停止**
```bash
docker compose stop localstack
```

**削除（コンテナ・ネットワーク）**
```bash
docker compose down
```

## ヘルスチェック

**ヘルスエンドポイント確認**
```bash
curl http://localhost:4566/_localstack/health
```

**サービス状態を整形して確認（jq 使用）**
```bash
curl -s http://localhost:4566/_localstack/health | jq
```

## AWS CLI 連携

**AWS CLI で LocalStack を使う（エンドポイント指定）**
```bash
aws --endpoint-url=http://localhost:4566 s3 ls
```

**環境変数でダミークレデンシャル設定**
```bash
export AWS_ACCESS_KEY_ID=test
export AWS_SECRET_ACCESS_KEY=test
export AWS_DEFAULT_REGION=ap-northeast-1
```

**S3 バケット作成（LocalStack）**
```bash
aws --endpoint-url=http://localhost:4566 s3 mb s3://local-bucket
```

**SQS キュー作成（LocalStack）**
```bash
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name sample-queue
```

## awslocal 利用

**awslocal インストール**
```bash
pip install awscli-local
```

**awslocal で S3 一覧**
```bash
awslocal s3 ls
```

**awslocal で DynamoDB テーブル一覧**
```bash
awslocal dynamodb list-tables
```

## トラブルシュート

**使用中ポート確認（4566）**
```bash
lsof -i :4566
```

**LocalStack コンテナ再作成**
```bash
docker compose down -v && docker compose up -d
```

**初期化データを含めてリセット**
```bash
rm -rf ./localstack-data
```
