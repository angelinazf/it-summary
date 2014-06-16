参考: https://dev.mysql.com/doc/refman/5.6/en/update.html
### 例子
```
UPDATE AdminUser SET username='xxx',password='xxx' where id = 1;
```
### Single-table syntax:
```
UPDATE [LOW_PRIORITY] [IGNORE] table_reference
    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
    [WHERE where_condition]
    [ORDER BY ...]
    [LIMIT row_count]
```

### Multiple-table syntax:
```
UPDATE [LOW_PRIORITY] [IGNORE] table_references
    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
    [WHERE where_condition]
```