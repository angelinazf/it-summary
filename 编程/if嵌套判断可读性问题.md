现在有下列代码
```
func Login(token string)(err error){
	_,err = orm.read(xxx)
	if err!=nil{
		if err==orm.ErrNoRows{
			return fmt.Errorf("账号不存在,请先绑定账号再登录")
		}
		return err
	}
	loginUserSomeWay(token)
	return
}
```
* 可读性好,符合读者的思路
* 嵌套层数太多

### 改写方案1
```
func Login(token string)(err error){
	_,err = orm.read(xxx)
	if err!=nil && err!=orm.ErrNoRows{
		return err
	}else if err==orm.ErrNoRows{
		return fmt.Errorf("账号不存在,请先绑定账号再登录")
	}
	loginUserSomeWay(token)
	return
}
```
* 嵌套层数少
* 可读性差,什么情况下不会报错?这个问题需要逻辑推理才可解答.

### 改写方案2
```
func Login(token string)(err error){
	_,err = orm.read(xxx)
	if err==orm.ErrNoRows{
		return fmt.Errorf("账号不存在,请先绑定账号再登录")
	}else if err!=nil{
		return err
	}
	loginUserSomeWay(token)
	return
}
```
* 嵌套层数少
* 可读性适中,但是如果 账号不存在,请先绑定账号再登录这个分支 里面写了很多东西就又悲剧了.
* 一开始很难想到这个方案.
* 和try...catch的经典写法一致.
