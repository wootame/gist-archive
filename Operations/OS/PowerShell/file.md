# ファイル・ディレクトリ操作

## 単体の基本操作

**現在位置を確認**
```powershell
Get-Location
```

**ディレクトリ一覧を表示**
```powershell
Get-ChildItem -Path "C:\path\to\dir"
```

**隠しファイルを含めて一覧表示**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Force
```

**ファイル新規作成**
```powershell
New-Item -Type File <ファイル>
```

**ディレクトリ新規作成**
```powershell
New-Item -Type Directory -Path "C:\path\to\new-dir"
```

**ファイルをコピー**
```powershell
Copy-Item -Path "C:\path\to\src.txt" -Destination "C:\path\to\dst.txt"
```

**ファイルを移動**
```powershell
Move-Item -Path "C:\path\to\src.txt" -Destination "C:\path\to\archive\src.txt"
```

**ファイル名を変更（Rename-Item）**
```powershell
Rename-Item -Path "C:\path\to\old-name.txt" -NewName "new-name.txt"
```

**パスの存在確認**
```powershell
Test-Path "C:\path\to\target.txt"
```

**ファイル全体を表示（cat は Get-Content のエイリアス）**
```powershell
cat "C:\path\to\file.txt"
```

**nvim でファイルを開く**
```powershell
nvim "C:\path\to\file.txt"
```

**nvim で指定行から開く（例: 120 行目）**
```powershell
nvim +120 "C:\path\to\file.txt"
```

**先頭 20 行を表示**
```powershell
Get-Content -Path "C:\path\to\file.txt" -TotalCount 20
```

**末尾 20 行を表示**
```powershell
Get-Content -Path "C:\path\to\file.txt" -Tail 20
```

**ファイルを上書き保存**
```powershell
Set-Content -Path "C:\path\to\file.txt" -Value "new content"
```

**ファイルに追記**
```powershell
Add-Content -Path "C:\path\to\file.txt" -Value "append line"
```

**ファイルを削除**
```powershell
Remove-Item -Path "C:\path\to\file.txt" -Force
```

**ディレクトリ配下をすべて削除**
```powershell
Remove-Item -Path "C:\path\to\dir\*" -Recurse -Force
```

**ディレクトリ配下を安全にすべて削除（隠し項目含む）**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Force | Remove-Item -Recurse -Force
```

**ディレクトリごと削除**
```powershell
Remove-Item -Path "C:\path\to\dir" -Recurse -Force
```

## 検索

**ファイル名で検索**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -Filter "filename"
```

**拡張子で検索**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -Filter "*.txt"
```

## パイプラインで組み合わせる基本操作

**配下の .log を削除**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -Filter "*.log" | Remove-Item -Force
```

**大きいファイル上位 10 件を確認**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -File |
	Sort-Object Length -Descending |
	Select-Object -First 10 FullName, Length
```

**ファイル一覧を CSV 出力**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -File |
	Select-Object FullName, Length, LastWriteTime |
	Export-Csv -Path "C:\path\to\files.csv" -NoTypeInformation -Encoding UTF8
```

## コマンドを組み合わせた複雑な処理

**特定文字列を含むファイルだけ別ディレクトリにコピー**
```powershell
Get-ChildItem -Path "C:\path\to\src" -Recurse -File |
	Where-Object { Select-String -Path $_.FullName -Pattern "ERROR" -Quiet } |
	Copy-Item -Destination "C:\path\to\error-files"
```

**一括リネーム（拡張子を保持して接頭辞を付ける）**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Filter "*.txt" -File |
	Rename-Item -NewName { "archived_" + $_.BaseName + $_.Extension }
```

**ファイル名の空白をアンダースコアに置換して一括リネーム**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -File |
	Where-Object Name -Match " " |
	Rename-Item -NewName { $_.Name -replace " ", "_" }
```

**cat で特定範囲の行を別ファイルへコピー（11〜30 行）**
```powershell
cat "C:\path\to\source.txt" |
	Select-Object -Skip 10 -First 20 |
	Set-Content "C:\path\to\part.txt"
```

**cat で抽出した行を既存ファイルへ追記**
```powershell
cat "C:\path\to\source.txt" |
	Select-String -Pattern "TODO|FIXME" |
	ForEach-Object { $_.Line } |
	Add-Content "C:\path\to\todo-summary.txt"
```

**JSON ログから必要項目を抽出して TSV を生成**
```powershell
cat "C:\path\to\app.log.json" |
	ConvertFrom-Json |
	Select-Object timestamp, level, message |
	Export-Csv -Path "C:\path\to\app.tsv" -Delimiter "`t" -NoTypeInformation -Encoding UTF8
```

**検索ヒットした最初のファイルを nvim で開く**
```powershell
$first = Get-ChildItem -Path "C:\path\to\src" -Recurse -File |
	Where-Object { Select-String -Path $_.FullName -Pattern "TODO" -Quiet } |
	Select-Object -First 1

if ($first) { nvim $first.FullName }
```

**Select-String の行番号を使って nvim で該当箇所を開く**
```powershell
$hit = Select-String -Path "C:\path\to\source.txt" -Pattern "ERROR" | Select-Object -First 1

if ($hit) { nvim +$($hit.LineNumber) $hit.Path }
```
