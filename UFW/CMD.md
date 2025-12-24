# UFW (Uncomplicated Firewall) コマンドリファレンス

## 基本操作

**ステータス確認**
```bash
sudo ufw status
```

**詳細表示**
```bash
sudo ufw status verbose
```

**番号付きで表示**
```bash
sudo ufw status numbered
```

**有効化**
```bash
sudo ufw enable
```

**無効化**
```bash
sudo ufw disable
```

**リセット（全ルール削除）**
```bash
sudo ufw reset
```

## デフォルトポリシー設定

**受信を拒否**
```bash
sudo ufw default deny incoming
```

**送信を許可**
```bash
sudo ufw default allow outgoing
```

**受信を許可**
```bash
sudo ufw default allow incoming
```

**送信を拒否**
```bash
sudo ufw default deny outgoing
```

## ルール追加

**TCPを許可**
```bash
sudo ufw allow <Port>/tcp
```

**UDPを許可**
```bash
sudo ufw allow <Port>/udp
```

**TCP/UDP両方を許可**
```bash
sudo ufw allow <Port>
```

**SSH (22/tcp)を許可**
```bash
sudo ufw allow ssh
```

**HTTP (80/tcp)を許可**
```bash
sudo ufw allow http
```

**HTTPS (443/tcp)を許可**
```bash
sudo ufw allow https
```

**FTP (21/tcp)を許可**
```bash
sudo ufw allow ftp
```

**特定IPから全ポート許可**
```bash
sudo ufw allow from <IP Address>
```

**特定IPから特定ポート許可**
```bash
sudo ufw allow from <IP Address> to any port <Port>
```

**特定IPから特定ポート・プロトコル許可**
```bash
sudo ufw allow from <IP Address> to any port <Port> proto tcp
```

**サブネットから全ポート許可**
```bash
sudo ufw allow from 192.168.1.0/24
```

**サブネットから特定ポート許可**
```bash
sudo ufw allow from 192.168.1.0/24 to any port <Port>
```

**TCPポート範囲を許可**
```bash
sudo ufw allow 6000:6007/tcp
```

**UDPポート範囲を許可**
```bash
sudo ufw allow 6000:6007/udp
```

## ルール削除

**ルール番号確認**
```bash
sudo ufw status numbered
```

**番号指定で削除**
```bash
sudo ufw delete <番号>
```

**ポートルールを削除**
```bash
sudo ufw delete allow <Port>/tcp
```

**IPルールを削除**
```bash
sudo ufw delete allow from <IP Address>
```

## ルール拒否

**ポートを拒否**
```bash
sudo ufw deny <Port>/tcp
```

**サービスを拒否**
```bash
sudo ufw deny ssh
```

**特定IPを拒否**
```bash
sudo ufw deny from <IP Address>
```

**特定IPから特定ポートを拒否**
```bash
sudo ufw deny from <IP Address> to any port <Port>
```

## 接続制限（レート制限）

**SSH接続を制限（ブルートフォース対策）**
```bash
sudo ufw limit ssh
```

## ログ設定

**ログ有効化**
```bash
sudo ufw logging on
```

**ログレベル：low**
```bash
sudo ufw logging low
```

**ログレベル：medium**
```bash
sudo ufw logging medium
```

**ログレベル：high**
```bash
sudo ufw logging high
```

**ログレベル：full**
```bash
sudo ufw logging full
```

**ログ無効化**
```bash
sudo ufw logging off
```

**ログ確認**
```bash
sudo tail -f /var/log/ufw.log
```

## よく使う設定例

**Webサーバー設定：デフォルト受信拒否**
```bash
sudo ufw default deny incoming
```

**Webサーバー設定：デフォルト送信許可**
```bash
sudo ufw default allow outgoing
```

**Webサーバー設定：SSH許可**
```bash
sudo ufw allow ssh
```

**Webサーバー設定：HTTP許可**
```bash
sudo ufw allow http
```

**Webサーバー設定：HTTPS許可**
```bash
sudo ufw allow https
```

**Webサーバー設定：有効化**
```bash
sudo ufw enable
```

**特定IPからのSSH接続のみ許可：デフォルト受信拒否**
```bash
sudo ufw default deny incoming
```

**特定IPからのSSH接続のみ許可：特定IPからポート22を許可**
```bash
sudo ufw allow from <信頼できるIP> to any port 22
```

**特定IPからのSSH接続のみ許可：有効化**
```bash
sudo ufw enable
```

