## 方法1
```
show create table `tbl_name`
```
然后正则找到AUTO_INCREMENT 


## 方法2
```
show table status where Name="tbl_name"
```
然后取出那一行里面Auto_increment的值

## 不可行的方法
下面这些信息不足..

```
explain `tbl_name`
show columns from `tbl_name`
```
