# UFW (Uncomplicated Firewall) コマンドリファレンス

## 基本操作

### ステータス確認
```bash
sudo ufw status

# 詳細表示
sudo ufw status verbose

# 番号付きで表示
sudo ufw status numbered
```

### 有効化
```bash
sudo ufw enable
```

### 無効化
```bash
sudo ufw disable
```

### リセット（全ルール削除）
```bash
sudo ufw reset
```

## デフォルトポリシー設定

### デフォルトを拒否（推奨）
```bash
# 受信を拒否
sudo ufw default deny incoming

# 送信を許可
sudo ufw default allow outgoing
```

### デフォルトを許可
```bash
sudo ufw default allow incoming
sudo ufw default deny outgoing
```

## ルール追加

### ポート単位で許可
```bash
# TCP
sudo ufw allow <Port>/tcp

# UDP
sudo ufw allow <Port>/udp

# TCP/UDP両方
sudo ufw allow <Port>
```

### 一般的なサービスで許可
```bash
# SSH (22/tcp)
sudo ufw allow ssh

# HTTP (80/tcp)
sudo ufw allow http

# HTTPS (443/tcp)
sudo ufw allow https

# FTP (21/tcp)
sudo ufw allow ftp
```

### IP アドレス単位で許可
```bash
# 特定IPから全ポート許可
sudo ufw allow from <IP Address>

# 特定IPから特定ポート許可
sudo ufw allow from <IP Address> to any port <Port>

# 特定IPから特定ポート・プロトコル許可
sudo ufw allow from <IP Address> to any port <Port> proto tcp
```

### サブネット単位で許可
```bash
sudo ufw allow from 192.168.1.0/24
sudo ufw allow from 192.168.1.0/24 to any port <Port>
```

### ポート範囲で許可
```bash
sudo ufw allow 6000:6007/tcp
sudo ufw allow 6000:6007/udp
```

## ルール削除

### 番号指定で削除
```bash
# ルール番号確認
sudo ufw status numbered

# 番号指定で削除
sudo ufw delete <番号>
```

### ルール指定で削除
```bash
sudo ufw delete allow <Port>/tcp
sudo ufw delete allow from <IP Address>
```

## ルール拒否

### ポート単位で拒否
```bash
sudo ufw deny <Port>/tcp
sudo ufw deny ssh
```

### IP アドレス単位で拒否
```bash
sudo ufw deny from <IP Address>
sudo ufw deny from <IP Address> to any port <Port>
```

## 接続制限（レート制限）

### SSH接続を制限（ブルートフォース対策）
```bash
sudo ufw limit ssh
# 30秒間に6回以上の接続試行をブロック
```

## ログ設定

### ログ有効化
```bash
sudo ufw logging on

# ログレベル設定
sudo ufw logging low
sudo ufw logging medium
sudo ufw logging high
sudo ufw logging full
```

### ログ無効化
```bash
sudo ufw logging off
```

### ログ確認
```bash
sudo tail -f /var/log/ufw.log
```

## よく使う設定例

### Webサーバー設定
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```

### 特定IPからのSSH接続のみ許可
```bash
sudo ufw default deny incoming
sudo ufw allow from <信頼できるIP> to any port 22
sudo ufw enable
```

