##### 每一次覆盖已有的项目之后需要做的事情:
* 删除原项目中已经编译好的jar包,使用正在修改的java文件取代
* 打开AndroidManifest.xml文件.按command+shift+f 整理文件格式,用command+s保存文件
	* 删除 android:debuggable="true" 这一行 (没做build失败)
	* 把后面的一行 
		android:name="com.unity3d.player.UnityPlayerProxyActivity"
	替换成
		android:name="com.unity3d.player.UnityPlayerNativeActivity"
		(没做爆异常ActivityNotFoundException)

* 尽量少打包eclipse项目太浪费时间了.