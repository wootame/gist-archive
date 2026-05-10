# VSCode コマンド・ショートカットリファレンス

## 起動（CLI: code）

**カレントディレクトリを VSCode で開く**
```bash
code .
```

**特定フォルダを開く**
```bash
code <dir>
```

**特定ファイルを開く**
```bash
code <file>
```

**指定行・列を開く**
```bash
code -g <file>:120:8
```

**新しいウィンドウで開く**
```bash
code -n <dir>
```

**現在のウィンドウで開く**
```bash
code -r <dir>
```

**差分比較モードで開く**
```bash
code --diff <file1> <file2>
```

**拡張機能一覧を表示**
```bash
code --list-extensions
```

## ファイル・検索

**クイックオープン**
```
Ctrl + P
```

**グローバル検索**
```
Ctrl + Shift + F
```

**開いているファイル内検索**
```
Ctrl + F
```

**開いているファイル内置換**
```
Ctrl + H
```

**ワークスペース全体置換**
```
Ctrl + Shift + H
```

**シンボル検索（ワークスペース）**
```
Ctrl + T
```

**行へ移動**
```
Ctrl + G
```

## 編集

**複数カーソル追加**
```
Alt + クリック
```

**次の一致を選択**
```
Ctrl + D
```

**一致をすべて選択**
```
Ctrl + Shift + L
```

**行コピー（下に複製）**
```
Shift + Alt + ↓
```

**行移動（下へ）**
```
Alt + ↓
```

**行削除**
```
Ctrl + Shift + K
```

**コメント切替（行）**
```
Ctrl + /
```

**コメント切替（ブロック）**
```
Shift + Alt + A
```

**整形**
```
Shift + Alt + F
```

## ナビゲーション

**定義へ移動**
```
F12
```

**定義を横で表示（Peek）**
```
Alt + F12
```

**参照を表示**
```
Shift + F12
```

**前の場所へ戻る**
```
Alt + ←
```

**次の場所へ進む**
```
Alt + →
```

## ターミナル・実行

**統合ターミナル表示/非表示**
```
Ctrl + `
```

**新しいターミナル作成**
```
Ctrl + Shift + `
```

**タスク実行**
```
Ctrl + Shift + B
```

**デバッグ開始/続行**
```
F5
```

**デバッグ停止**
```
Shift + F5
```

**ブレークポイント切替**
```
F9
```

## エディタ・UI 操作

**コマンドパレット**
```
Ctrl + Shift + P
```

**設定を開く（UI）**
```
Ctrl + ,
```

**サイドバー表示/非表示**
```
Ctrl + B
```

**エクスプローラーにフォーカス**
```
Ctrl + Shift + E
```

**ソース管理にフォーカス**
```
Ctrl + Shift + G
```

**拡張機能ビューにフォーカス**
```
Ctrl + Shift + X
```

**Zen Mode 切替**
```
Ctrl + K, Z
```

## ワークスペース運用

**フォルダをワークスペースへ追加**
```
File > Add Folder to Workspace...
```

**ワークスペース保存**
```
File > Save Workspace As...
```

**最近使ったワークスペースを開く**
```
File > Open Recent
```

## よく使う連携例

**Git 変更ファイルを VSCode で開く（PowerShell）**
```powershell
git diff --name-only | ForEach-Object { code $_ }
```

**README を指定行から開く（PowerShell）**
```powershell
code -g "README.md:1:1"
```

**2 ファイル比較を VSCode で開く（PowerShell）**
```powershell
code --diff "before.txt" "after.txt"
```
