### 现象
mysql> show tables;
+-------------------+
| Tables_in_fastcat |
+-------------------+
| Kvdb              |
+-------------------+
mysql> select * from Kvdb;
ERROR 1146 (42S02): Table 'fastcat.kvdb' doesn't exist

也不能删除数据库

### 不需要数据时
* 去mysql的放数据的实际位置(在哪?基本靠猜.),把 叫那个数据库名的 目录删除.