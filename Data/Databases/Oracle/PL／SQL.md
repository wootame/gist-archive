# Oracle PL/SQL リファレンス

## 匿名ブロック

**最小構成**
```sql
begin
  dbms_output.put_line('Hello PL/SQL');
end;
/
```

**変数宣言と代入**
```sql
declare
  v_name varchar2(100);
begin
  v_name := 'Taro';
  dbms_output.put_line(v_name);
end;
/
```

## 条件分岐・ループ

**IF / ELSIF / ELSE**
```sql
declare
  v_score number := 85;
begin
  if v_score >= 90 then
    dbms_output.put_line('A');
  elsif v_score >= 80 then
    dbms_output.put_line('B');
  else
    dbms_output.put_line('C');
  end if;
end;
/
```

**FOR ループ**
```sql
begin
  for i in 1 .. 5 loop
    dbms_output.put_line('i=' || i);
  end loop;
end;
/
```

**WHILE ループ**
```sql
declare
  i number := 1;
begin
  while i <= 3 loop
    dbms_output.put_line('loop=' || i);
    i := i + 1;
  end loop;
end;
/
```

## 例外処理

**NO_DATA_FOUND / OTHERS**
```sql
declare
  v_name users.name%type;
begin
  select name into v_name
    from users
   where id = 999999;

  dbms_output.put_line(v_name);
exception
  when no_data_found then
    dbms_output.put_line('データが見つかりません');
  when others then
    dbms_output.put_line('想定外エラー: ' || sqlerrm);
end;
/
```

## ストアドプロシージャ

**作成**
```sql
create or replace procedure pr_set_user_status (
  p_user_id in users.id%type,
  p_status  in users.status%type
)
as
begin
  update users
     set status = p_status
   where id = p_user_id;
end;
/
```

**実行**
```sql
exec pr_set_user_status(1, 'inactive');
```

## ストアドファンクション

**作成**
```sql
create or replace function fn_user_count
  return number
as
  v_count number;
begin
  select count(*) into v_count from users;
  return v_count;
end;
/
```

**呼び出し**
```sql
select fn_user_count() from dual;
```

## パッケージ

**仕様部（spec）作成**
```sql
create or replace package pkg_user as
  procedure activate_user(p_user_id in users.id%type);
  procedure deactivate_user(p_user_id in users.id%type);
end pkg_user;
/
```

**本体（body）作成**
```sql
create or replace package body pkg_user as
  procedure activate_user(p_user_id in users.id%type) as
  begin
    update users set status = 'active' where id = p_user_id;
  end;

  procedure deactivate_user(p_user_id in users.id%type) as
  begin
    update users set status = 'inactive' where id = p_user_id;
  end;
end pkg_user;
/
```

## トリガー

**監査列を自動更新する BEFORE UPDATE トリガー**
```sql
create or replace trigger trg_users_bu
before update on users
for each row
begin
  :new.updated_at := systimestamp;
end;
/
```

## カーソル

**明示カーソル**
```sql
declare
  cursor c_users is
    select id, name from users where status = 'active';

  v_id users.id%type;
  v_name users.name%type;
begin
  open c_users;
  loop
    fetch c_users into v_id, v_name;
    exit when c_users%notfound;
    dbms_output.put_line(v_id || ':' || v_name);
  end loop;
  close c_users;
end;
/
```

## BULK 処理

**BULK COLLECT + FORALL**
```sql
declare
  type t_ids is table of users.id%type;
  v_ids t_ids;
begin
  select id bulk collect into v_ids
    from users
   where status = 'inactive';

  forall i in 1 .. v_ids.count
    update users
       set status = 'active'
     where id = v_ids(i);
end;
/
```

## デバッグ補助

**DBMS_OUTPUT を有効化**
```sql
set serveroutput on
```

**コンパイルエラー確認**
```sql
show errors
```
