### 使用类似下面的代码,对某个执行文件进行提权:
```
		kmgCmd.CmdSlice([]string{"osascript","-e",
			`do shell script "sudo chown root:admin '`+vpnPath+`';sudo chmod +s+x '`+vpnPath+`'" with administrator privileges`}).MustRun()
```
在第一次运行应用时会要求提供当前用户密码,然后就可以使用了.

### root提权与ui进程问题.
* 使用上述方法root提权的进程,不能开启ui窗口.(可以使用root进程和非root进程进行区分来进行工作,中间需要某种rpc流程进行通信.)
* 使用sudo在命令行手动提权,可以开启ui窗口.
* 调用root提权的进程,后面直接开启ui窗口,会导致打包在app里面的时候,第一次运行进行最小化,会无法还原的bug,解决方案为调用root提权代码后,不要再本进程里面开ui窗口,而是在本进程里面,再重新执行本进程的执行文件.