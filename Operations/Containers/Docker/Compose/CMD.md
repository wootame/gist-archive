# Docker Compose コマンドリファレンス

## サービス管理

**サービス起動（バックグラウンド）**
```bash
docker-compose up -d
```

**サービス起動（フォアグラウンド）**
```bash
docker-compose up
```

**サービス起動（ビルドあり）**
```bash
docker-compose up -d --build
```

**サービス停止**
```bash
docker-compose stop
```

**サービス停止と削除**
```bash
docker-compose down
```

**サービス停止と削除（ボリューム含む）**
```bash
docker-compose down -v
```

**サービス停止と削除（イメージ含む）**
```bash
docker-compose down --rmi all
```

**サービス再起動**
```bash
docker-compose restart
```

**特定サービスのみ起動**
```bash
docker-compose up -d <サービス名>
```

**特定サービスのみ再起動**
```bash
docker-compose restart <サービス名>
```

## サービス操作

**実行中のサービス一覧**
```bash
docker-compose ps
```

**サービスのログ確認**
```bash
docker-compose logs
```

**サービスのログをリアルタイムで確認**
```bash
docker-compose logs -f
```

**特定サービスのログ確認**
```bash
docker-compose logs <サービス名>
```

**サービスでコマンド実行**
```bash
docker-compose exec <サービス名> <コマンド>
```

**サービスに接続**
```bash
docker-compose exec <サービス名> bash
```

**サービスの設定確認**
```bash
docker-compose config
```

**サービスのビルド**
```bash
docker-compose build
```

**サービスのビルド（キャッシュなし）**
```bash
docker-compose build --no-cache
```

**特定サービスのビルド**
```bash
docker-compose build <サービス名>
```

**イメージの取得**
```bash
docker-compose pull
```

**サービスのスケール**
```bash
docker-compose up -d --scale <サービス名>=<数>
```

## その他

**docker-compose のバージョン確認**
```bash
docker-compose --version
```

**一時的にコマンド実行（コンテナは削除される）**
```bash
docker-compose run --rm <サービス名> <コマンド>
```

**サービスの一時停止**
```bash
docker-compose pause <サービス名>
```

**サービスの再開**
```bash
docker-compose unpause <サービス名>
```

**プロセス確認**
```bash
docker-compose top
```