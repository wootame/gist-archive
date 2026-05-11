# ファイル・ディレクトリ操作

## このファイルの対象範囲

- ファイル/ディレクトリの作成・移動・削除
- テキスト検索・加工（grep / rg / sed / awk）
- 圧縮、通信、ハッシュは `other.md` を参照

## 注意書き（共通）

- 破壊的操作（`rm -rf`、上書き、権限変更）は実行前に対象パスを再確認する
- 本番環境では、可能なら `-i` やバックアップ付きオプションを優先する

## ファイル書き込み（echo / cat / tee）

**1行を書き込み（新規作成 or 上書き）**
```bash
echo "hello" > sample.txt
```

**1行を追記**
```bash
echo "next line" >> sample.txt
```

**変数展開せずに文字列をそのまま書き込む**
```bash
echo '$HOME/${USER}' > literal.txt
```

**複数行を書き込み（ヒアドキュメント）**
```bash
cat <<'EOF' > config.env
APP_NAME=myapp
LOG_LEVEL=info
EOF
```

**sudo権限で書き込み（リダイレクト失敗を回避）**
```bash
echo "127.0.0.1 example.local" | sudo tee -a /etc/hosts > /dev/null
```

**ディレクトリ配下をすべて削除**
```bash
rm -rf /path/to/dir/*
```

**危険：非推奨（`.` `..` を巻き込む可能性）**
```bash
rm -rf /path/to/dir/.*
```

**ディレクトリ配下を安全にすべて削除（隠しファイル含む）**
```bash
rm -rf /path/to/dir/{*,.[!.]*,..?*}
```

**ディレクトリごと削除**
```bash
rm -rf /path/to/dir
```

**削除前に対象を確認（ドライラン）**
```bash
find /path/to/dir -maxdepth 1 -mindepth 1 -print
```

**ファイル名で検索**
```bash
find /path/to/dir -name "filename"
```

**拡張子で検索**
```bash
find /path/to/dir -name "*.txt"
```

**ディレクトリのみ検索**
```bash
find /path/to/dir -type d
```

## ファイル操作（mv / cp / mkdir など）

**ファイル名を変更**
```bash
mv old.txt new.txt
```

**ファイルを別ディレクトリへ移動**
```bash
mv app.log /var/log/myapp/
```

**上書き確認しながら移動**
```bash
mv -i source.txt destination.txt
```

**上書きを強制して移動**
```bash
mv -f source.txt destination.txt
```

**ディレクトリごと移動**
```bash
mv ./old_dir ./archive/old_dir
```

**ファイルをコピー**
```bash
cp source.txt backup.txt
```

**ディレクトリを再帰コピー**
```bash
cp -r ./src ./src_backup
```

**属性を保持してコピー**
```bash
cp -a ./project ./project.bak
```

**空ファイルを作成（存在すれば更新時刻のみ更新）**
```bash
touch notes.txt
```

**ディレクトリを作成（親ディレクトリも同時作成）**
```bash
mkdir -p /path/to/new/dir
```

**シンボリックリンク作成**
```bash
ln -s /var/www/current ./current_link
```

**実行権限を付与**
```bash
chmod +x script.sh
```

**所有者を変更**
```bash
sudo chown -R user:user /path/to/dir
```

## テキスト確認（cat -n）

**行番号付きで表示**
```bash
cat -n file.txt
```

**空行を除いて行番号付け**
```bash
cat -b file.txt
```

## grep

**文字列検索（再帰）**
```bash
grep -R "TODO" .
```

**行番号付きで検索**
```bash
grep -n "ERROR" app.log
```

**大文字小文字を無視**
```bash
grep -i "warning" app.log
```

**拡張正規表現（OR検索）**
```bash
grep -E "error|fatal|panic" app.log
```

**一致しない行を表示**
```bash
grep -v "^#" .env
```

**一致件数のみ表示**
```bash
grep -c "timeout" server.log
```

## ripgrep（rg）

**高速に再帰検索（ripgrep）**
```bash
rg "TODO"
```

**行番号付きで検索（デフォルトで表示）**
```bash
rg "createUser"
```

**拡張子を絞って検索**
```bash
rg "SELECT" -g '*.sql'
```

**特定ディレクトリを除外して検索**
```bash
rg "password" -g '!node_modules/**' -g '!dist/**'
```

**ファイル名のみ表示**
```bash
rg -l "FIXME"
```

**補足**
- `repgrep` は一般的なコマンド名ではなく、通常は `ripgrep`（`rg`）を指します。

## sed

**最初に一致した文字列だけ置換**
```bash
sed 's/foo/bar/' file.txt
```

**すべて置換（global）**
```bash
sed 's/foo/bar/g' file.txt
```

**n行目だけ置換**
```bash
sed '3s/foo/bar/' file.txt
```

**範囲行だけ置換（2〜5行目）**
```bash
sed '2,5s/foo/bar/g' file.txt
```

**一致行を削除**
```bash
sed '/^#/d' file.txt
```

**インプレース編集（バックアップあり）**
```bash
sed -i.bak 's/old/new/g' file.txt
```

## awk

**1列目と3列目を表示**
```bash
awk '{print $1, $3}' file.txt
```

**カンマ区切りの2列目を表示**
```bash
awk -F',' '{print $2}' data.csv
```

**ヘッダー以外の件数を数える**
```bash
awk 'NR>1 {count++} END {print count}' data.csv
```

**2列目の合計を計算**
```bash
awk '{sum += $2} END {print sum}' numbers.txt
```

**条件付き抽出（3列目が100以上）**
```bash
awk '$3 >= 100 {print $0}' report.txt
```