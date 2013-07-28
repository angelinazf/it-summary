* 这两张表应该使用某个id互相关联
* 查询在表A中存在,但是不在表B中存在的数据

### 使用in和子查询
```
select * 
  from table_a
  where table_a.uid not in(
    select DISTINCT uid
        from table_b
    )
```

### 使用left join和is null
```
select *
  from table_a
  left join table_b on table_a.uid=table_b.uid
  where table_b.uid is null
```