# ユーザー・権限管理

## このファイルの対象範囲

- ユーザー/グループ、sudo、ACL、umask の管理
- サービス起動やプロセス操作は `system.md` を参照

## 注意書き（共通）

- `chown -R` / `chmod -R` は対象ディレクトリを誤ると広範囲に影響する
- sudo 権限変更後は再ログインして反映状態を確認する

**ファイル所有者変更**
```bash
sudo chown <user>:<group> /path/to/file
```

**再帰的に変更**
```bash
sudo chown -R <user>:<group> /path/to/dir
```

**ファイル権限変更**
```bash
chmod 755 /path/to/file
```

**再帰的に変更**
```bash
chmod -R 755 /path/to/dir
```

## ユーザー管理

**ユーザー作成（ホームディレクトリ作成）**
```bash
sudo useradd -m <user>
```

**ユーザー削除（ホームディレクトリも削除）**
```bash
sudo userdel -r <user>
```

**パスワード変更**
```bash
sudo passwd <user>
```

**ユーザー情報確認**
```bash
id <user>
```

## グループ管理

**グループ作成**
```bash
sudo groupadd <group>
```

**ユーザーをグループへ追加**
```bash
sudo usermod -aG <group> <user>
```

**現在シェルに反映（再ログインまでの暫定）**
```bash
newgrp <group>
```

**所属グループ確認**
```bash
groups <user>
```

## sudo 権限

**sudo グループに追加**
```bash
sudo usermod -aG sudo <user>
```

**sudoers を安全に編集**
```bash
sudo visudo
```

**現在の sudo 権限確認**
```bash
sudo -l
```

## ACL / umask

**現在の umask 確認**
```bash
umask
```

**一時的に umask を設定**
```bash
umask 027
```

**ACL を付与（特定ユーザーに rwx）**
```bash
setfacl -m u:<user>:rwx /path/to/file
```

**ACL を確認**
```bash
getfacl /path/to/file
```