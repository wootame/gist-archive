# PlantUML (PUML) 構文リファレンス

## 基本

**最小構成**
```puml
@startuml
Alice -> Bob: Hello
@enduml
```

**タイトルと注釈**
```puml
@startuml
title ログイン処理
note top: この図は認証フロー
User -> API: POST /login
@enduml
```

## シーケンス図

**基本構文**
```puml
@startuml
actor User
participant API
database DB

User -> API: ログイン要求
API -> DB: ユーザー照合
DB --> API: 結果
API --> User: トークン返却
@enduml
```

**条件分岐**
```puml
@startuml
actor User
participant API

User -> API: 認証
alt 認証成功
  API --> User: 200 OK
else 認証失敗
  API --> User: 401 Unauthorized
end
@enduml
```

## ユースケース図

**基本構文**
```puml
@startuml
left to right direction
actor ユーザー
rectangle システム {
  usecase "ログイン" as UC1
  usecase "注文作成" as UC2
}
ユーザー --> UC1
ユーザー --> UC2
@enduml
```

## クラス図

**基本構文**
```puml
@startuml
class User {
  +id: String
  +name: String
  +login()
}

class Order {
  +orderId: String
  +create()
}

User "1" -- "*" Order : places
@enduml
```

## アクティビティ図

**基本構文**
```puml
@startuml
start
:入力値を検証;
if (有効?) then (yes)
  :保存;
else (no)
  :エラー返却;
endif
stop
@enduml
```

## ステート図

**基本構文**
```puml
@startuml
[*] --> Idle
Idle --> Running : start
Running --> Idle : stop
Running --> Error : fail
Error --> Idle : reset
@enduml
```

## コンポーネント図

**基本構文**
```puml
@startuml
component Web
component API
database Postgres

Web --> API
API --> Postgres
@enduml
```

## ER 風表現（IE記法）

**エンティティ関係**
```puml
@startuml
entity User {
  * id : uuid
  --
  email : varchar
}

entity Order {
  * id : uuid
  --
  user_id : uuid
}

User ||--o{ Order
@enduml
```

## スキン・見た目

**テーマ適用**
```puml
@startuml
!theme plain
Alice -> Bob: theme example
@enduml
```

**色指定**
```puml
@startuml
skinparam backgroundColor #FAFAFA
skinparam ArrowColor #1565C0
Alice -> Bob: styled
@enduml
```

## コメント

**1行コメント**
```puml
' これはコメント
@startuml
Alice -> Bob: test
@enduml
```

**複数行コメント**
```puml
/'
複数行コメント
'/
@startuml
Alice -> Bob: test
@enduml
```

## 使い分けの目安

- UML 全般を厳密に記述: PlantUML
- Markdown 上で手軽に可視化: Mermaid
- 複雑な相互作用の詳細化: PlantUML シーケンス図
