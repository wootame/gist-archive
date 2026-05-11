# パッケージ管理（APT）

## このファイルの対象範囲

- APT/dpkg による導入・削除・復旧・固定
- サービス状態やログ確認は `system.md` を参照

## 注意書き（共通）

- 本番環境では、更新前に変更対象と影響範囲を確認する
- `purge` や `autoremove` 実行前は削除候補を確認する

**パッケージ一覧更新**
```bash
sudo apt update
```

**パッケージアップグレード**
```bash
sudo apt upgrade
```

**確認なしで実行**
```bash
sudo apt upgrade -y
```

**パッケージインストール**
```bash
sudo apt install <package_name>
```

**パッケージのみ削除**
```bash
sudo apt remove <package_name>
```

**設定ファイルも削除**
```bash
sudo apt purge <package_name>
```

**削除予定パッケージを確認（シミュレーション）**
```bash
sudo apt -s autoremove
```

**不要なパッケージ削除**
```bash
sudo apt autoremove
```

**パッケージ検索**
```bash
apt search <keyword>
```

**インストール済みパッケージ一覧**
```bash
dpkg -l
```

**特定パッケージ確認**
```bash
dpkg -l | grep <package_name>
```

## 詳細確認

**パッケージ情報を表示**
```bash
apt show <package_name>
```

**インストール候補バージョンを確認**
```bash
apt policy <package_name>
```

**依存関係を確認**
```bash
apt depends <package_name>
```

**どのパッケージがファイルを提供しているか確認**
```bash
dpkg -S /usr/bin/<binary_name>
```

## メンテナンス

**ローカルキャッシュ削除（安全）**
```bash
sudo apt clean
```

**古いキャッシュのみ削除**
```bash
sudo apt autoclean
```

**壊れた依存関係の修復**
```bash
sudo apt --fix-broken install
```

**途中で止まった設定処理を再実行**
```bash
sudo dpkg --configure -a
```

## バージョン固定・解除

**アップグレード対象から除外（hold）**
```bash
sudo apt-mark hold <package_name>
```

**除外解除（unhold）**
```bash
sudo apt-mark unhold <package_name>
```

**hold されているパッケージ一覧**
```bash
apt-mark showhold
```

## ファイルからインストール

**.deb をインストール**
```bash
sudo dpkg -i ./package.deb
```

**.deb インストール後の依存解決**
```bash
sudo apt -f install
```