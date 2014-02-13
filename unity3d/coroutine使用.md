http://unitygems.com/coroutines/
### bug 清理
* Time.Scale被设置为0时,yield return new WaitForSecound(1f)不会返回
* 开线程的对象被干掉后(disable或dsctory),和系统相关的coroutine的api无效(如WaitForSecound)

### 特性
* 原生的yield break 退出当前coroutines,Fvz版退出当前函数
* yield return null等到下一帧
* 原生yield return StartCoroutine(xxx()) Fvz版 yield return xxx() 调用另一个函数
