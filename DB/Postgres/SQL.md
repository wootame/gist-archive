# PostgreSQL SQL リファレンス

## セッション確認

**現在のDB・ユーザー確認**
```sql
select current_database(), current_user;
```

**現在時刻確認**
```sql
select now();
```

**検索パス確認**
```sql
show search_path;
```

## DDL（定義）

**スキーマ作成**
```sql
create schema if not exists app;
```

**テーブル作成**
```sql
create table if not exists app.users (
  id bigserial primary key,
  name text not null,
  email text unique,
  status text not null default 'active',
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);
```

**インデックス作成**
```sql
create index if not exists idx_users_status on app.users(status);
```

**列追加**
```sql
alter table app.users add column if not exists last_login_at timestamptz;
```

## DML（操作）

**INSERT**
```sql
insert into app.users (name, email)
values ('Taro', 'taro@example.com');
```

**複数行 INSERT**
```sql
insert into app.users (name, email)
values
  ('Hanako', 'hanako@example.com'),
  ('Jiro', 'jiro@example.com');
```

**UPDATE**
```sql
update app.users
   set status = 'inactive',
       updated_at = now()
 where email = 'taro@example.com';
```

**DELETE**
```sql
delete from app.users where status = 'inactive';
```

**UPSERT（ON CONFLICT）**
```sql
insert into app.users (email, name)
values ('taro@example.com', 'Taro')
on conflict (email)
do update set name = excluded.name,
              updated_at = now();
```

## SELECT 基本

**全件取得**
```sql
select * from app.users;
```

**条件検索**
```sql
select id, name, email
  from app.users
 where status = 'active';
```

**並び替え + 件数制限**
```sql
select id, name, created_at
  from app.users
 order by created_at desc
 limit 20;
```

**件数取得**
```sql
select count(*) as total from app.users;
```

## JOIN / 集計

**INNER JOIN**
```sql
select u.id, u.name, o.order_no, o.total_amount
  from app.users u
  join app.orders o on o.user_id = u.id;
```

**LEFT JOIN**
```sql
select u.id, u.name, o.order_no
  from app.users u
  left join app.orders o on o.user_id = u.id;
```

**GROUP BY + HAVING**
```sql
select user_id, count(*) order_count, sum(total_amount) total_amount
  from app.orders
 group by user_id
having count(*) >= 3;
```

## JSON / 配列

**JSONB フィールド抽出**
```sql
select payload->>'event_name' as event_name
  from app.events;
```

**JSONB 条件検索**
```sql
select *
  from app.events
 where payload @> '{"event_name":"signup"}'::jsonb;
```

**配列に値を追加**
```sql
update app.tags
   set labels = array_append(labels, 'new')
 where id = 1;
```

## 管理系SQL

**テーブル一覧**
```sql
select schemaname, tablename
  from pg_tables
 where schemaname not in ('pg_catalog', 'information_schema')
 order by schemaname, tablename;
```

**カラム情報確認**
```sql
select table_schema, table_name, column_name, data_type
  from information_schema.columns
 where table_schema = 'app'
 order by table_name, ordinal_position;
```

**実行中クエリ確認**
```sql
select pid, usename, state, wait_event_type, query
  from pg_stat_activity
 where state <> 'idle';
```

**ロック確認**
```sql
select l.pid, a.usename, a.query, l.mode, l.granted
  from pg_locks l
  join pg_stat_activity a on a.pid = l.pid;
```

## トランザクション

**開始**
```sql
begin;
```

**コミット**
```sql
commit;
```

**ロールバック**
```sql
rollback;
```

**セーブポイント**
```sql
savepoint sp_before_update;
```

**セーブポイントまで戻す**
```sql
rollback to savepoint sp_before_update;
```
