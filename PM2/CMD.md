# PM2 コマンドリファレンス

## プロセス管理

### 起動
```bash
# 単一ファイル起動
pm2 start app.js

# 名前を指定して起動
pm2 start app.js --name "my-app"

# ecosystem.config.js を使用
pm2 start ecosystem.config.js
```

### ステータス確認
```bash
pm2 status
# または
pm2 list
```

### 詳細情報確認
```bash
pm2 show <アプリ名またはID>
```

### 再起動
```bash
pm2 restart <アプリ名またはID>

# 全アプリ再起動
pm2 restart all
```

### 停止
```bash
pm2 stop <アプリ名またはID>

# 全アプリ停止
pm2 stop all
```

### 削除
```bash
pm2 delete <アプリ名またはID>

# 全アプリ削除
pm2 delete all
```

### リロード（ゼロダウンタイム）
```bash
pm2 reload <アプリ名またはID>
```

## ログ管理

### ログ表示
```bash
# 全アプリのログ
pm2 logs

# 特定アプリのログ
pm2 logs <アプリ名またはID>

# ログクリア
pm2 flush
```

## モニタリング

### リアルタイムモニタリング
```bash
pm2 monit
```

## 自動起動設定

### startup設定（システム起動時にPM2を自動起動）
```bash
pm2 startup
# 表示されたコマンドを実行
```

### 現在のプロセスリストを保存
```bash
pm2 save
```

### 保存済み設定から復元
```bash
pm2 resurrect
```

### startup設定解除
```bash
pm2 unstartup
```

## その他便利コマンド

### 環境変数を指定して起動
```bash
pm2 start app.js --env production
```

### CPU/メモリ使用量確認
```bash
pm2 status
```

### プロセスの更新
```bash
pm2 update
```
