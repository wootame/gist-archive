# Git / GitHub コマンドリファレンス

## 初期設定

**ユーザー名設定（グローバル）**
```bash
git config --global user.name "<ユーザー名>"
```

**メールアドレス設定（グローバル）**
```bash
git config --global user.email "<メールアドレス>"
```

**設定確認**
```bash
git config --list
```

## リポジトリ作成・接続

**新規リポジトリ初期化**
```bash
git init
```

**リモートリポジトリをクローン**
```bash
git clone <リポジトリURL>
```

**リモートURL確認**
```bash
git remote -v
```

**originを追加**
```bash
git remote add origin <リポジトリURL>
```

## 変更の確認・コミット

**状態確認**
```bash
git status
```

**差分確認（未ステージ）**
```bash
git diff
```

**差分確認（ステージ済み）**
```bash
git diff --cached
```

**ファイルをステージ**
```bash
git add <ファイル名>
```

**すべての変更をステージ**
```bash
git add .
```

**コミット**
```bash
git commit -m "<メッセージ>"
```

**直前コミットを修正**
```bash
git commit --amend
```

## ブランチ運用

**ブランチ一覧**
```bash
git branch
```

**ブランチ作成**
```bash
git branch <ブランチ名>
```

**ブランチ作成＋切り替え**
```bash
git switch -c <ブランチ名>
```

**ブランチ切り替え**
```bash
git switch <ブランチ名>
```

**ブランチ削除（ローカル）**
```bash
git branch -d <ブランチ名>
```

## 取得・同期

**最新情報を取得（マージしない）**
```bash
git fetch origin
```

**取得してマージ**
```bash
git pull origin <ブランチ名>
```

**取得してrebase**
```bash
git pull --rebase origin <ブランチ名>
```

**リモートへプッシュ（初回）**
```bash
git push -u origin <ブランチ名>
```

**リモートへプッシュ**
```bash
git push origin <ブランチ名>
```

## 変更の取り消し・退避

**作業ツリーの変更を破棄**
```bash
git restore <ファイル名>
```

**ステージを取り消し**
```bash
git restore --staged <ファイル名>
```

**コミットを打ち消す（履歴を残す）**
```bash
git revert <コミットID>
```

**直前コミットまで戻す（履歴を書き換え）**
```bash
git reset --hard HEAD~1
```

**変更を退避**
```bash
git stash
```

**退避一覧**
```bash
git stash list
```

**退避を戻す**
```bash
git stash pop
```

## 履歴・タグ

**履歴確認（1行表示）**
```bash
git log --oneline --graph --decorate
```

**タグ作成**
```bash
git tag <タグ名>
```

**タグをプッシュ**
```bash
git push origin <タグ名>
```

## GitHub 操作（CLI: gh）

**GitHubにログイン**
```bash
gh auth login
```

**現在ディレクトリをGitHubリポジトリとして作成**
```bash
gh repo create <リポジトリ名> --private --source=. --remote=origin --push
```

**Pull Request作成**
```bash
gh pr create --base <ベースブランチ> --head <ブランチ名>
```

**Pull Request一覧**
```bash
gh pr list
```

**Issue一覧**
```bash
gh issue list
```
