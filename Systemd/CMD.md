# Systemd コマンドリファレンス

## サービス管理

**ステータス確認**
```bash
sudo systemctl status <service_name>
```

**起動**
```bash
sudo systemctl start <service_name>
```

**停止**
```bash
sudo systemctl stop <service_name>
```

**再起動**
```bash
sudo systemctl restart <service_name>
```

**設定再読み込み**
```bash
sudo systemctl reload <service_name>
```

**有効化**
```bash
sudo systemctl enable <service_name>
```

**無効化**
```bash
sudo systemctl disable <service_name>
```

**有効化状態確認**
```bash
sudo systemctl is-enabled <service_name>
```

## サービス一覧

**全サービス表示**
```bash
sudo systemctl list-units --type=service
```

**起動中のサービスのみ表示**
```bash
sudo systemctl list-units --type=service --state=running
```

**失敗したサービス表示**
```bash
sudo systemctl --failed
```

## ログ確認(journalctl)

**サービスログ表示**
```bash
sudo journalctl -u <service_name>
```

**リアルタイムでログ表示**
```bash
sudo journalctl -u <service_name> -f
```

**最新100行表示**
```bash
sudo journalctl -u <service_name> -n 100
```

**特定の日時からのログ表示**
```bash
sudo journalctl -u <service_name> --since "2025-12-18 00:00:00"
```

**今日のログ表示**
```bash
sudo journalctl -u <service_name> --since today
```

**昨日のログ表示**
```bash
sudo journalctl -u <service_name> --since yesterday
```

## デーモン再読み込み

**サービスファイル変更後の再読み込み**
```bash
sudo systemctl daemon-reload
```

**サービスファイルの場所**
- システム: `/etc/systemd/system/`
- ユーザー: `~/.config/systemd/user/`

**サービスファイル編集**
```bash
sudo systemctl edit <service_name>
```
