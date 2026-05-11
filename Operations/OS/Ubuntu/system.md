# システム情報

## このファイルの対象範囲

- システム情報、プロセス、サービス、ネットワーク、ストレージ確認
- ユーザー/権限変更は `user-permission.md` を参照

## 注意書き（共通）

- `kill -9` は最終手段として使い、通常は `kill` や `systemctl stop` を優先する
- `sudo` を伴うネットワーク/サービス操作は対象ホストを確認してから実行する

**OSバージョン確認**
```bash
lsb_release -a
```

```bash
cat /etc/os-release
```

**カーネルバージョン確認**
```bash
uname -r
```

**ディスク使用状況**
```bash
df -h
```

**ディレクトリサイズ確認**
```bash
du -sh /path/to/dir
```

**サブディレクトリも表示**
```bash
du -h --max-depth=1 /path/to/dir
```

**メモリ使用状況**
```bash
free -h
```

**CPU情報**
```bash
lscpu
```

**稼働時間とロードアベレージ**
```bash
uptime
```

**ホスト名関連情報**
```bash
hostnamectl
```

**時刻・タイムゾーン確認**
```bash
timedatectl
```

**リアルタイムリソース監視**
```bash
top
```

## プロセス管理

**プロセス一覧**
```bash
ps aux
```

**特定プロセス検索**
```bash
ps aux | grep <process_name>
```

**PIDで終了**
```bash
kill <PID>
```

**強制終了**
```bash
kill -9 <PID>
```

**補足**
- データ破損リスクを下げるため、まずは `kill <PID>` を試す

**プロセス名で終了**
```bash
pkill <process_name>
```

**プロセスツリー表示**
```bash
ps -ef --forest
```

**起動コマンドを含めて検索**
```bash
pgrep -af <keyword>
```

## サービス管理（systemd）

**サービス状態確認**
```bash
systemctl status <service_name>
```

**サービス起動 / 停止 / 再起動**
```bash
sudo systemctl start <service_name>
sudo systemctl stop <service_name>
sudo systemctl restart <service_name>
```

**起動時に自動起動を有効化**
```bash
sudo systemctl enable <service_name>
```

**自動起動を無効化**
```bash
sudo systemctl disable <service_name>
```

**サービスログを追跡表示**
```bash
journalctl -u <service_name> -f
```

## ネットワーク

**IPアドレス確認**
```bash
ip addr show
```

```bash
ifconfig
```

**ポート使用状況**
```bash
sudo netstat -tuln
```

```bash
sudo ss -tuln
```

**特定ポートを使用しているプロセス確認**
```bash
sudo lsof -i :<port>
```

**待受ポートとプロセスを表示**
```bash
sudo ss -ltnp
```

**宛先への疎通確認**
```bash
ping -c 4 8.8.8.8
```

**名前解決確認**
```bash
dig example.com +short
```

## ストレージ・デバイス

**ブロックデバイス一覧**
```bash
lsblk
```

**マウント一覧**
```bash
mount | column -t
```

**UUID を含めて確認**
```bash
sudo blkid
```