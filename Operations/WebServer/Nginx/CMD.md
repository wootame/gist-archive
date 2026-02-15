# Nginx コマンドリファレンス

## サービス管理

**ステータス確認**
```bash
sudo systemctl status nginx
```

**起動**
```bash
sudo systemctl start nginx
```

**停止**
```bash
sudo systemctl stop nginx
```

**再起動**
```bash
sudo systemctl restart nginx
```

**設定再読み込み（ダウンタイムなし）**
```bash
sudo systemctl reload nginx
```

**有効化**
```bash
sudo systemctl enable nginx
```

**無効化**
```bash
sudo systemctl disable nginx
```

## 設定ファイル

**構文チェック**
```bash
sudo nginx -t
```

**設定ファイルの場所**
- メイン設定: `/etc/nginx/nginx.conf`
- サイト設定: `/etc/nginx/sites-available/`
- 有効サイト: `/etc/nginx/sites-enabled/`

## ログ確認

**アクセスログ（リアルタイム）**
```bash
sudo tail -f /var/log/nginx/access.log
```

**エラーログ（リアルタイム）**
```bash
sudo tail -f /var/log/nginx/error.log
```

**アクセスログの最終行表示**
```bash
sudo tail -n 100 /var/log/nginx/access.log
```

**エラーログの最終行表示**
```bash
sudo tail -n 100 /var/log/nginx/error.log
```

