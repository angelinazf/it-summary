### type="checkbox" 一个可以点中,点中后有小钩,不点中没有小钩的方框
html渲染方式
```
<!--初始没选中-->
<input type="checkbox" name="IsLeader">
<!--初始选中了-->
<input type="checkbox" name="IsLeader" checked>
```
在html渲染时填入value的值 是用来提交的时候发送的表单的值,不填默认是 'on'

原生提交行为:
	如果没有选中提交,提交的form表单中没有和这个input相关的项.
	如果选中了提交,提交的form表单中 IsLeader的值是 input的value的值,html上面没有value项时默认是'on'

在jQuery中
	使用`$($0).prop('checked')`来检查是否被选中
	使用`$($0).val()`不管是否选中 总是返回 input上面的value的值.


### type="password" 一个输入密码的输入框
html渲染方式
```
<input type="password" class="form-control" name="Password" value="xxx"/>
```

关于`autocomplete="off"`,目前各大浏览器(chrome41)都忽略了password框的这个属性,下面是目前绕开这个功能的办法:
```
<input type='text' name='xxx' value='xxx' />
<input type='password' style='display:none'/>
<input type="password" autocomplete="off" class="form-control" name="Password" value="xxx"/>
```
	