# その他のコマンド

## このファイルの対象範囲

- 圧縮/解凍、ダウンロード、ハッシュ、監視などの補助コマンド
- ファイル操作とテキスト加工は `file.md` を参照

## 注意書き（共通）

- 一括処理（`xargs`、`nohup`）は対象確認とログ確認を先に行う
- 外部URLから取得したファイルはハッシュ検証後に利用する

## 圧縮・解凍

**tar.gz 作成**
```bash
tar -czf archive.tar.gz /path/to/dir
```

**tar.gz 解凍**
```bash
tar -xzf archive.tar.gz
```

**zip 作成**
```bash
zip -r archive.zip /path/to/dir
```

**zip 解凍**
```bash
unzip archive.zip
```

**tar.bz2 作成**
```bash
tar -cjf archive.tar.bz2 /path/to/dir
```

**tar.bz2 解凍**
```bash
tar -xjf archive.tar.bz2
```

**展開先ディレクトリを指定して解凍**
```bash
tar -xzf archive.tar.gz -C /path/to/extract
```

**アーカイブ内容を確認（解凍しない）**
```bash
tar -tzf archive.tar.gz
```

## ダウンロード・疎通確認

**ファイルをダウンロード（保存名そのまま）**
```bash
wget https://example.com/file.tar.gz
```

**出力ファイル名を指定してダウンロード**
```bash
wget -O app.tar.gz https://example.com/latest.tar.gz
```

**レスポンスヘッダーのみ確認**
```bash
curl -I https://example.com
```

**APIへJSONをPOST**
```bash
curl -X POST https://api.example.com/items \
	-H 'Content-Type: application/json' \
	-d '{"name":"sample"}'
```

## 文字列・ハッシュ

**Base64 エンコード**
```bash
echo -n "hello" | base64
```

**Base64 デコード**
```bash
echo "aGVsbG8=" | base64 -d
```

**SHA-256 ハッシュ計算**
```bash
sha256sum file.txt
```

**MD5 ハッシュ計算**
```bash
md5sum file.txt
```

## バッチ実行・監視

**find結果を xargs で一括削除**
```bash
find ./logs -name '*.log' | xargs rm -f
```

**先に削除対象を確認**
```bash
find ./logs -name '*.log' -print
```

**0.5秒ごとにコマンド監視**
```bash
watch -n 0.5 "df -h"
```

**コマンドをバックグラウンド実行してログ保存**
```bash
nohup ./start.sh > app.log 2>&1 &
```

