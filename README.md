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
│  ├─ Containers/
│  │  └─ Docker/
│  │     ├─ Compose/
│  │     └─ Docker/
│  ├─ WebServer/
│  │  └─ Nginx/
│  │     └─ CMD.md
│  ├─ ProcessManager/
│  │  └─ PM2/
│  │     └─ CMD.md
│  ├─ SystemService/
│  │  └─ Systemd/
│  │     └─ CMD.md
│  ├─ OS/
│  │  └─ Ubuntu/
│  │     └─ CMD.md
│  └─ Security/
│     └─ UFW/
│        └─ CMD.md
├─ Tools/
│  └─ Browser/
│     └─ SHORTCUTS.md
└─ Docs/
	└─ Markdown/
		└─ SYNTAX.md
```

## 分類ルール

- 概念整理は `Concepts/`（クラウド分類など）
- データベース実務は `Data/Databases/`（CMD / SQL / 手続き言語）
- サーバー運用コマンドは `Operations/`
- ツール固有の操作メモは `Tools/`
- 記法や文書作成系は `Docs/`