# Docker コマンドリファレンス

## コンテナ管理

**コンテナ一覧（実行中）**
```bash
docker ps
```

**コンテナ一覧（すべて）**
```bash
docker ps -a
```

**コンテナ起動**
```bash
docker start <コンテナ名またはID>
```

**コンテナ停止**
```bash
docker stop <コンテナ名またはID>
```

**コンテナ再起動**
```bash
docker restart <コンテナ名またはID>
```

**コンテナ削除**
```bash
docker rm <コンテナ名またはID>
```

**起動中のコンテナを強制削除**
```bash
docker rm -f <コンテナ名またはID>
```

**停止中のコンテナをすべて削除**
```bash
docker container prune
```

**コンテナ実行（対話モード）**
```bash
docker run -it <イメージ名> bash
```

**コンテナ実行（バックグラウンド）**
```bash
docker run -d <イメージ名>
```

**コンテナ実行（ポートマッピング）**
```bash
docker run -p <ホストポート>:<コンテナポート> <イメージ名>
```

**コンテナ実行（名前指定）**
```bash
docker run --name <コンテナ名> <イメージ名>
```

**コンテナ実行（ボリュームマウント）**
```bash
docker run -v <ホストパス>:<コンテナパス> <イメージ名>
```

**コンテナ実行（環境変数指定）**
```bash
docker run -e <変数名>=<値> <イメージ名>
```

## コンテナ操作

**実行中のコンテナに接続**
```bash
docker exec -it <コンテナ名またはID> bash
```

**実行中のコンテナでコマンド実行**
```bash
docker exec <コンテナ名またはID> <コマンド>
```

**コンテナのログ確認**
```bash
docker logs <コンテナ名またはID>
```

**コンテナのログをリアルタイムで確認**
```bash
docker logs -f <コンテナ名またはID>
```

**コンテナのログ（最新N行）**
```bash
docker logs --tail <行数> <コンテナ名またはID>
```

**コンテナの詳細情報確認**
```bash
docker inspect <コンテナ名またはID>
```

**コンテナのリソース使用状況**
```bash
docker stats
```

**特定コンテナのリソース使用状況**
```bash
docker stats <コンテナ名またはID>
```

**コンテナからホストへファイルコピー**
```bash
docker cp <コンテナ名>:<コンテナ内パス> <ホストパス>
```

**ホストからコンテナへファイルコピー**
```bash
docker cp <ホストパス> <コンテナ名>:<コンテナ内パス>
```

## イメージ管理

**イメージ一覧**
```bash
docker images
```

**イメージ検索**
```bash
docker search <イメージ名>
```

**イメージ取得**
```bash
docker pull <イメージ名>:<タグ>
```

**イメージ削除**
```bash
docker rmi <イメージ名またはID>
```

**使用されていないイメージをすべて削除**
```bash
docker image prune
```

**すべての未使用イメージを削除**
```bash
docker image prune -a
```

**イメージのビルド**
```bash
docker build -t <イメージ名>:<タグ> .
```

**イメージのビルド（Dockerfileを指定）**
```bash
docker build -t <イメージ名>:<タグ> -f <Dockerfileパス> .
```

**イメージのビルド（キャッシュなし）**
```bash
docker build --no-cache -t <イメージ名>:<タグ> .
```

**イメージの履歴確認**
```bash
docker history <イメージ名またはID>
```

**イメージのタグ付け**
```bash
docker tag <元イメージ名> <新イメージ名>:<タグ>
```

**イメージのプッシュ**
```bash
docker push <イメージ名>:<タグ>
```

## ネットワーク管理

**ネットワーク一覧**
```bash
docker network ls
```

**ネットワーク作成**
```bash
docker network create <ネットワーク名>
```

**ネットワーク削除**
```bash
docker network rm <ネットワーク名>
```

**ネットワークの詳細情報**
```bash
docker network inspect <ネットワーク名>
```

**コンテナをネットワークに接続**
```bash
docker network connect <ネットワーク名> <コンテナ名>
```

**コンテナをネットワークから切断**
```bash
docker network disconnect <ネットワーク名> <コンテナ名>
```

**未使用ネットワーク削除**
```bash
docker network prune
```

## ボリューム管理

**ボリューム一覧**
```bash
docker volume ls
```

**ボリューム作成**
```bash
docker volume create <ボリューム名>
```

**ボリューム削除**
```bash
docker volume rm <ボリューム名>
```

**ボリュームの詳細情報**
```bash
docker volume inspect <ボリューム名>
```

**未使用ボリューム削除**
```bash
docker volume prune
```

## システム管理

**Docker のバージョン確認**
```bash
docker --version
```

**Docker の詳細情報**
```bash
docker info
```

**ディスク使用状況**
```bash
docker system df
```

**未使用リソースをすべて削除**
```bash
docker system prune
```

**すべての未使用リソースを削除（ボリューム含む）**
```bash
docker system prune -a --volumes
```

## トラブルシューティング（Windows / Docker Desktop）

**デーモンの稼働状況確認**
```bash
docker info
```
応答が返らずハングする場合、デーモンがフリーズしている可能性が高い。

**Docker Desktop 関連プロセスの確認**
```powershell
Get-Process -Name "*docker*" | Select-Object Name, Id, Path
```

**応答がない場合の強制再起動**
```powershell
Stop-Process -Name "Docker Desktop","com.docker.backend","com.docker.build","com.docker.dev-envs","docker" -Force
Start-Process "C:\Program Files\Docker\Docker\Docker Desktop.exe"
```
Docker Desktop の起動・デーモン初期化には数十秒〜数分かかる。

**再起動後の疎通確認（ポーリング）**
```bash
until docker info >/dev/null 2>&1; do sleep 3; done; echo "Docker daemon is ready"
```