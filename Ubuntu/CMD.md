# Ubuntu コマンドリファレンス

## ファイル・ディレクトリ操作

### ディレクトリ配下をすべて削除
```bash
# 基本形
rm -rf /path/to/dir/*
```

**注意**: `.*` を含めると `.` と `..` まで一致する可能性があるため非推奨
```bash
# 推奨しない
rm -rf /path/to/dir/.*
```

### ディレクトリ配下を安全にすべて削除（隠しファイル含む）
```bash
rm -rf /path/to/dir/{*,.[!.]*,..?*}
```

### ディレクトリごと削除
```bash
rm -rf /path/to/dir
```

### ファイル検索
```bash
# ファイル名で検索
find /path/to/dir -name "filename"

# 拡張子で検索
find /path/to/dir -name "*.txt"

# ディレクトリのみ検索
find /path/to/dir -type d
```

## パッケージ管理（APT）

### パッケージ一覧更新
```bash
sudo apt update
```

### パッケージアップグレード
```bash
sudo apt upgrade

# 確認なしで実行
sudo apt upgrade -y
```

### パッケージインストール
```bash
sudo apt install <package_name>
```

### パッケージ削除
```bash
# パッケージのみ削除
sudo apt remove <package_name>

# 設定ファイルも削除
sudo apt purge <package_name>
```

### 不要なパッケージ削除
```bash
sudo apt autoremove
```

### パッケージ検索
```bash
apt search <keyword>
```

### インストール済みパッケージ確認
```bash
dpkg -l

# 特定パッケージ確認
dpkg -l | grep <package_name>
```

## システム情報

### OSバージョン確認
```bash
lsb_release -a

# または
cat /etc/os-release
```

### カーネルバージョン確認
```bash
uname -r
```

### ディスク使用状況
```bash
df -h
```

### ディレクトリサイズ確認
```bash
du -sh /path/to/dir

# サブディレクトリも表示
du -h --max-depth=1 /path/to/dir
```

### メモリ使用状況
```bash
free -h
```

### CPU情報
```bash
lscpu
```

## プロセス管理

### プロセス一覧
```bash
ps aux

# 特定プロセス検索
ps aux | grep <process_name>
```

### プロセス終了
```bash
# PIDで終了
kill <PID>

# 強制終了
kill -9 <PID>

# プロセス名で終了
pkill <process_name>
```

## ネットワーク

### IPアドレス確認
```bash
ip addr show

# または
ifconfig
```

### ポート使用状況
```bash
sudo netstat -tuln

# または
sudo ss -tuln
```

### 特定ポートを使用しているプロセス確認
```bash
sudo lsof -i :<port>
```

## ユーザー・権限管理

### ファイル所有者変更
```bash
sudo chown <user>:<group> /path/to/file

# 再帰的に変更
sudo chown -R <user>:<group> /path/to/dir
```

### ファイル権限変更
```bash
chmod 755 /path/to/file

# 再帰的に変更
chmod -R 755 /path/to/dir
```

## 圧縮・解凍

### tar.gz 作成
```bash
tar -czf archive.tar.gz /path/to/dir
```

### tar.gz 解凍
```bash
tar -xzf archive.tar.gz
```

### zip 作成
```bash
zip -r archive.zip /path/to/dir
```

### zip 解凍
```bash
unzip archive.zip
```
