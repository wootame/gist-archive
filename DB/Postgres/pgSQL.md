# PostgreSQL PL/pgSQL（pgSQL）リファレンス

## DO ブロック

**最小構成**
```sql
do $$
begin
  raise notice 'Hello PL/pgSQL';
end
$$;
```

**変数宣言と代入**
```sql
do $$
declare
  v_name text := 'Taro';
begin
  raise notice 'name=%', v_name;
end
$$;
```

## 条件分岐・ループ

**IF / ELSIF / ELSE**
```sql
do $$
declare
  v_score int := 85;
begin
  if v_score >= 90 then
    raise notice 'A';
  elsif v_score >= 80 then
    raise notice 'B';
  else
    raise notice 'C';
  end if;
end
$$;
```

**FOR ループ**
```sql
do $$
declare
  i int;
begin
  for i in 1..5 loop
    raise notice 'i=%', i;
  end loop;
end
$$;
```

**配列 FOREACH**
```sql
do $$
declare
  v_item text;
  v_list text[] := array['a', 'b', 'c'];
begin
  foreach v_item in array v_list loop
    raise notice 'item=%', v_item;
  end loop;
end
$$;
```

## 例外処理

**EXCEPTION ブロック**
```sql
do $$
begin
  perform 1 / 0;
exception
  when division_by_zero then
    raise notice '0除算を検知しました';
  when others then
    raise notice '想定外エラー: %', sqlerrm;
end
$$;
```

## 関数

**関数作成（戻り値あり）**
```sql
create or replace function app.fn_user_count()
returns bigint
language plpgsql
as $$
declare
  v_count bigint;
begin
  select count(*) into v_count from app.users;
  return v_count;
end;
$$;
```

**呼び出し**
```sql
select app.fn_user_count();
```

## プロシージャ（PostgreSQL 11+）

**プロシージャ作成**
```sql
create or replace procedure app.pr_set_user_status(
  p_user_id bigint,
  p_status text
)
language plpgsql
as $$
begin
  update app.users
     set status = p_status,
         updated_at = now()
   where id = p_user_id;
end;
$$;
```

**呼び出し**
```sql
call app.pr_set_user_status(1, 'inactive');
```

## トリガー

**トリガー関数作成（updated_at 自動更新）**
```sql
create or replace function app.trg_set_updated_at()
returns trigger
language plpgsql
as $$
begin
  new.updated_at := now();
  return new;
end;
$$;
```

**トリガー作成**
```sql
create trigger trg_users_bu
before update on app.users
for each row
execute function app.trg_set_updated_at();
```

## 動的SQL

**EXECUTE で動的SQL実行**
```sql
do $$
declare
  v_table text := 'users';
  v_count bigint;
begin
  execute format('select count(*) from app.%I', v_table)
    into v_count;

  raise notice 'count=%', v_count;
end
$$;
```

## 戻り値テーブル関数

**複数行を返す関数**
```sql
create or replace function app.fn_active_users()
returns table(id bigint, name text, email text)
language plpgsql
as $$
begin
  return query
  select u.id, u.name, u.email
    from app.users u
   where u.status = 'active'
   order by u.id;
end;
$$;
```

**呼び出し**
```sql
select * from app.fn_active_users();
```

## パフォーマンス補助

**実行計画確認**
```sql
explain analyze
select *
  from app.users
 where status = 'active';
```

**関数定義確認（psql）**
```sql
\sf app.fn_user_count
```
