# gist-archive

コマンド・SQL・概念メモを用途別に分類したアーカイブです。

## ディレクトリ構成

```text
gist-archive/
├─ Concepts/
│  └─ Cloud/
│     ├─ BaaS.md
│     ├─ CaaS.md
│     ├─ CDN.md
│     ├─ DBaaS.md
│     ├─ FaaS.md
│     ├─ IaaS.md
│     ├─ IDaaS.md
│     ├─ PaaS.md
│     └─ SaaS.md
├─ Data/
│  └─ Databases/
│     ├─ Oracle/
│     │  ├─ CMD.md
│     │  ├─ SQL.md
│     │  └─ PL／SQL.md
│     └─ Postgres/
│        ├─ CMD.md
│        ├─ SQL.md
│        └─ pgSQL.md
├─ Operations/
│  ├─ Cloud/
│  │  └─ AWS/
│  │     ├─ CLI/
│  │     │  └─ CMD.md
│  │     └─ SAM/
│  │        └─ CMD.md
│  ├─ Containers/
│  │  ├─ Docker/
│  │  │  ├─ Compose/
│  │  │  └─ Docker/
│  │  └─ LocalStack/
│  │     └─ CMD.md
│  ├─ OS/
│  │  └─ Ubuntu/
│  │     └─ CMD.md
│  ├─ ProcessManager/
│  │  └─ PM2/
│  │     └─ CMD.md
│  ├─ Security/
│  │  └─ UFW/
│  │     └─ CMD.md
│  ├─ SystemService/
│  │  └─ Systemd/
│  │     └─ CMD.md
│  ├─ VersionControl/
│  │  └─ Git/
│  │     └─ CMD.md
│  └─ WebServer/
│     └─ Nginx/
│        └─ CMD.md
├─ Tools/
│  └─ Browser/
│     └─ SHORTCUTS.md
└─ Docs/
│  ├─ Markdown/
│  │  └─ SYNTAX.md
│  ├─ Mermaid/
│  │  └─ SYNTAX.md
│  └─ PUML/
│     └─ SYNTAX.md
```

## 分類ルール

- 概念整理は `Concepts/`（クラウド分類など）
- データベース実務は `Data/Databases/`（CMD / SQL / 手続き言語）
- サーバー運用コマンドは `Operations/`
- Git / GitHub 操作は `Operations/VersionControl/Git/`
- ツール固有の操作メモは `Tools/`
- 記法や文書作成系は `Docs/`