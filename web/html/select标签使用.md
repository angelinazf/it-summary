### 样例
```
<select name="" >
    <option value="全部">全部</option>
    <option value="已通过" selected>已通过</option>
    <option value="已过期">已过期</option>
</select>
```

### 表单特性
* select和input一样会在表单里面添加一个key value项.
* select的value的初始值,在option上面使用selected进行选择,在select上面设置value没有效果

### jQuery特性
* 可以使用 $(this).val() 取出select上面的value值
* 可以是否 $(this).find('option') 取出里面所有的option