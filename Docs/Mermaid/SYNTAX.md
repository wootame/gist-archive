# Mermaid 構文リファレンス

## フローチャート

**基本構文（上から下）**
```mermaid
flowchart TD
  A[開始] --> B{条件}
  B -->|Yes| C[処理1]
  B -->|No| D[処理2]
  C --> E[終了]
  D --> E
```

**左から右**
```mermaid
flowchart LR
  A --> B --> C
```

## シーケンス図

**基本構文**
```mermaid
sequenceDiagram
  participant U as User
  participant A as API
  participant D as DB

  U->>A: リクエスト
  A->>D: クエリ
  D-->>A: 結果
  A-->>U: レスポンス
```

**活性化表示**
```mermaid
sequenceDiagram
  participant App
  participant Service

  App->>+Service: 実行
  Service-->>-App: 完了
```

## クラス図

**基本構文**
```mermaid
classDiagram
  class User {
    +String id
    +String name
    +login()
  }

  class Order {
    +String orderId
    +create()
  }

  User "1" --> "*" Order : places
```

## ER 図

**基本構文**
```mermaid
erDiagram
  USER ||--o{ ORDER : places
  USER {
    string id PK
    string email
  }
  ORDER {
    string id PK
    string user_id FK
  }
```

## 状態遷移図

**基本構文**
```mermaid
stateDiagram-v2
  [*] --> Idle
  Idle --> Running : start
  Running --> Idle : stop
  Running --> Error : fail
  Error --> Idle : reset
```

## ガントチャート

**基本構文**
```mermaid
gantt
  title リリース計画
  dateFormat YYYY-MM-DD

  section 開発
  実装           :a1, 2026-05-01, 7d
  テスト         :after a1, 5d

  section 運用
  本番リリース   :2026-05-15, 1d
```

## 円グラフ

**基本構文**
```mermaid
pie title 言語比率
  "TypeScript" : 45
  "Python" : 35
  "Go" : 20
```

## サブグラフ

**グルーピング**
```mermaid
flowchart TD
  subgraph Frontend
    A[Web]
  end

  subgraph Backend
    B[API]
    C[DB]
  end

  A --> B --> C
```

## スタイル指定

**ノード色・枠線変更**
```mermaid
flowchart LR
  A[Client] --> B[Server]
  style A fill:#e8f3ff,stroke:#1e88e5,stroke-width:2px
  style B fill:#e8ffe8,stroke:#2e7d32,stroke-width:2px
```

**classDef で再利用**
```mermaid
flowchart LR
  classDef app fill:#fff4e5,stroke:#ef6c00,stroke-width:2px;
  A[Gateway]:::app --> B[Lambda]:::app
```

## コメント

**行コメント**
```mermaid
%% これはコメント
flowchart LR
  A --> B
```

## 使い分けの目安

- 処理手順: フローチャート
- API の時系列: シーケンス図
- モデル設計: クラス図 / ER 図
- ライフサイクル: 状態遷移図
- スケジュール: ガントチャート
