# Oracle コマンドリファレンス

## 接続・ログイン

**SQL*Plus で接続（ローカル）**
```bash
sqlplus / as sysdba
```

**SQL*Plus で接続（ユーザー指定）**
```bash
sqlplus <ユーザー名>/<パスワード>@<ホスト>:<ポート>/<サービス名>
```

**接続識別子（tnsnames.ora）を使って接続**
```bash
sqlplus <ユーザー名>/<パスワード>@<接続識別子>
```

**OS認証で接続（管理者）**
```bash
sqlplus / as sysdba
```

**接続中ユーザー確認**
```bash
show user
```

**現在のコンテナ確認（CDB/PDB 環境）**
```bash
show con_name
```

**切断**
```bash
exit
```

## インスタンス・リスナー管理

**Oracle インスタンス起動**
```bash
startup
```

**MOUNT まで起動（リカバリ用途）**
```bash
startup mount
```

**OPEN まで起動**
```bash
alter database open;
```

**Oracle インスタンス停止**
```bash
shutdown immediate
```

**Oracle インスタンス停止（強制）**
```bash
shutdown abort
```

**インスタンス状態確認**
```bash
select instance_name, status from v$instance;
```

**リスナー状態確認**
```bash
lsnrctl status
```

**リスナー起動**
```bash
lsnrctl start
```

**リスナー停止**
```bash
lsnrctl stop
```

**リスナー設定再読み込み**
```bash
lsnrctl reload
```

## CDB / PDB 管理（マルチテナント）

**PDB 一覧表示**
```bash
show pdbs
```

**PDB 切り替え**
```bash
alter session set container=<PDB名>;
```

**PDB をオープン**
```bash
alter pluggable database <PDB名> open;
```

**PDB をクローズ**
```bash
alter pluggable database <PDB名> close immediate;
```

## Data Pump（バックアップ・移行）

**DIRECTORY オブジェクト作成**
```bash
create or replace directory <DIRECTORY名> as '<OS上のパス>';
```

**DIRECTORY 権限付与**
```bash
grant read, write on directory <DIRECTORY名> to <ユーザー名>;
```

**スキーマをエクスポート**
```bash
expdp <ユーザー名>/<パスワード>@<サービス名> schemas=<スキーマ名> directory=<DIRECTORY名> dumpfile=<ファイル名>.dmp logfile=<ログ名>.log
```

**スキーマをインポート**
```bash
impdp <ユーザー名>/<パスワード>@<サービス名> schemas=<スキーマ名> directory=<DIRECTORY名> dumpfile=<ファイル名>.dmp logfile=<ログ名>.log
```

**テーブル単位でエクスポート**
```bash
expdp <ユーザー名>/<パスワード>@<サービス名> tables=<スキーマ名>.<テーブル名> directory=<DIRECTORY名> dumpfile=<ファイル名>.dmp logfile=<ログ名>.log
```

**テーブル単位でインポート**
```bash
impdp <ユーザー名>/<パスワード>@<サービス名> tables=<スキーマ名>.<テーブル名> directory=<DIRECTORY名> dumpfile=<ファイル名>.dmp logfile=<ログ名>.log
```

## 診断・運用補助

**アラートログ格納先確認**
```bash
adrci exec="show homes"
```

**リスナーログ確認（末尾追跡）**
```bash
tail -f $ORACLE_BASE/diag/tnslsnr/<ホスト名>/listener/trace/listener.log
```

**Oracle ユーザー環境確認**
```bash
echo $ORACLE_HOME
```

**サービス名確認**
```bash
lsnrctl status | grep "Service"
```

## よく使う表示設定（SQL*Plus）

**行サイズ設定**
```bash
set linesize 200
```

**ページサイズ設定**
```bash
set pagesize 100
```

**SQL 実行時間表示**
```bash
set timing on
```

**SQL 実行結果を CSV で出力**
```bash
set markup csv on
```
