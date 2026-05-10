# GitHub 操作（CLI: gh）

## 初期設定・認証

**バージョン確認**
```bash
gh --version
```

**GitHubにログイン**
```bash
gh auth login
```

**ログイン状態確認**
```bash
gh auth status
```

**ログアウト**
```bash
gh auth logout
```

## リポジトリ操作

**現在ディレクトリをGitHubリポジトリとして作成**
```bash
gh repo create <リポジトリ名> --private --source=. --remote=origin --push
```

**リポジトリをクローン**
```bash
gh repo clone <owner>/<repo>
```

**リポジトリをブラウザで開く**
```bash
gh repo view --web
```

**リポジトリ情報を表示**
```bash
gh repo view <owner>/<repo>
```

**Fork を作成して clone**
```bash
gh repo fork <owner>/<repo> --clone
```

## Pull Request

**Pull Request作成**
```bash
gh pr create --base <ベースブランチ> --head <ブランチ名>
```

**Pull Request作成（タイトル・本文指定）**
```bash
gh pr create --base <ベースブランチ> --head <ブランチ名> --title "<タイトル>" --body "<本文>"
```

**Pull Request一覧**
```bash
gh pr list
```

**現在ブランチの Pull Request を表示**
```bash
gh pr view
```

**Pull Request詳細をブラウザで開く**
```bash
gh pr view <番号> --web
```

**Pull Requestにレビューコメント**
```bash
gh pr review <番号> --comment --body "<コメント>"
```

**Pull Requestを承認**
```bash
gh pr review <番号> --approve
```

**Pull Requestをマージ（squash）**
```bash
gh pr merge <番号> --squash --delete-branch
```

**Pull Requestの差分をチェックアウト**
```bash
gh pr checkout <番号>
```

## Issue

**Issue一覧**
```bash
gh issue list
```

**Issue作成**
```bash
gh issue create --title "<タイトル>" --body "<本文>"
```

**Issue詳細表示**
```bash
gh issue view <番号>
```

**Issueをブラウザで開く**
```bash
gh issue view <番号> --web
```

**Issueにコメント追加**
```bash
gh issue comment <番号> --body "<コメント>"
```

**Issueをクローズ**
```bash
gh issue close <番号>
```

## Actions（Workflow）

**Workflow一覧**
```bash
gh workflow list
```

**Workflow実行履歴一覧**
```bash
gh run list
```

**最新実行のログ表示**
```bash
gh run view --log
```

**失敗ジョブを再実行**
```bash
gh run rerun <run-id> --failed
```

**Workflowを手動実行**
```bash
gh workflow run <workflow.yml> --ref <branch>
```

## Release

**リリース一覧**
```bash
gh release list
```

**リリース作成（タグ作成込み）**
```bash
gh release create <tag> --title "<タイトル>" --notes "<リリースノート>"
```

**アセット付きリリース作成**
```bash
gh release create <tag> <file1> <file2> --title "<タイトル>" --notes "<リリースノート>"
```

**リリースをダウンロード**
```bash
gh release download <tag>
```

## 検索・確認

**リポジトリ検索**
```bash
gh search repos "<keyword>"
```

**Issue検索**
```bash
gh search issues "<keyword>"
```

**PR検索**
```bash
gh search prs "<keyword>"
```

## よく使う連携例

**自分がレビュー担当の PR を一覧**
```bash
gh pr list --search "review-requested:@me state:open"
```

**現在ブランチから PR を作ってすぐブラウザで開く**
```bash
gh pr create --fill ; gh pr view --web
```

**CI の最新実行ログを確認**
```bash
gh run list --limit 1 ; gh run view --log
```