# PostgreSQL コマンドリファレンス

## サービス管理

**ステータス確認（systemd）**
```bash
sudo systemctl status postgresql
```

**起動**
```bash
sudo systemctl start postgresql
```

**停止**
```bash
sudo systemctl stop postgresql
```

**再起動**
```bash
sudo systemctl restart postgresql
```

**有効化（OS起動時）**
```bash
sudo systemctl enable postgresql
```

**無効化（OS起動時）**
```bash
sudo systemctl disable postgresql
```

**ログ確認（journalctl）**
```bash
sudo journalctl -u postgresql -f
```

## 接続・ログイン

**postgres ユーザーで psql 起動**
```bash
sudo -u postgres psql
```

**ユーザー・DB を指定して接続**
```bash
psql -h <ホスト> -p <ポート> -U <ユーザー名> -d <DB名>
```

**SSL 必須で接続**
```bash
psql "host=<ホスト> port=<ポート> dbname=<DB名> user=<ユーザー名> sslmode=require"
```

**接続情報確認**
```bash
\conninfo
```

**DB一覧表示**
```bash
\l
```

**データベース切り替え**
```bash
\c <DB名>
```

**環境変数で接続先を指定**
```bash
export PGHOST=<ホスト> PGPORT=<ポート> PGUSER=<ユーザー名> PGDATABASE=<DB名>
```

**終了**
```bash
\q
```

## DB・ロール管理（CLI）

**データベース作成**
```bash
createdb -U <ユーザー名> <DB名>
```

**データベース削除**
```bash
dropdb -U <ユーザー名> <DB名>
```

**ユーザー作成（ロール作成）**
```bash
createuser -U postgres -P <ユーザー名>
```

**ロールに作成権限付与**
```bash
psql -U postgres -d postgres -c "alter role <ユーザー名> createdb;"
```

**ロールにスーパーユーザー権限付与（必要時のみ）**
```bash
psql -U postgres -d postgres -c "alter role <ユーザー名> superuser;"
```

## psql メタコマンド

**テーブル一覧**
```bash
\dt
```

**スキーマ一覧**
```bash
\dn
```

**テーブル定義表示**
```bash
\d <テーブル名>
```

**関数一覧**
```bash
\df
```

**権限一覧表示**
```bash
\du
```

**実行時間表示 ON**
```bash
	iming
```

## バックアップ・リストア

**DBを SQL 形式でバックアップ**
```bash
pg_dump -h <ホスト> -p <ポート> -U <ユーザー名> <DB名> > backup.sql
```

**DBをカスタム形式でバックアップ**
```bash
pg_dump -h <ホスト> -p <ポート> -U <ユーザー名> -F c -f backup.dump <DB名>
```

**SQLバックアップを復元**
```bash
psql -h <ホスト> -p <ポート> -U <ユーザー名> -d <DB名> -f backup.sql
```

**カスタムバックアップを復元**
```bash
pg_restore -h <ホスト> -p <ポート> -U <ユーザー名> -d <DB名> backup.dump
```

**全DBの論理バックアップ**
```bash
pg_dumpall -h <ホスト> -p <ポート> -U <ユーザー名> > all_databases.sql
```

**並列リストア（ディレクトリ形式）**
```bash
pg_restore -h <ホスト> -p <ポート> -U <ユーザー名> -d <DB名> -j 4 backup_dir
```

## 設定・ログ

**設定ファイルパス確認（psql内）**
```bash
show config_file;
```

**接続許可設定ファイル確認（psql内）**
```bash
show hba_file;
```

**ログディレクトリ確認（psql内）**
```bash
show log_directory;
```

**postgresql.conf 構文チェック（再起動前）**
```bash
postgres -D <データディレクトリ> -t
```
