### mac 应用签名过程:
* 首先你需要找苹果搞一个开发者账号 99刀的那个.(已知公司版苹果开发者账号可以进行签名.)
* 然后去搞一张 Mac Certificates (Production)
* 同一个账号可以持有多张 Mac Certificates (Production),是否可以同时用于签名仍然有待验证.
* 这个东西有一个私钥,还有一个证书,其中只有生成的那个人的电脑上有私钥.证书可以使用开发者账号的账号密码,随意在网站进行下载.
* 然后就可以使用私钥和证书对应用进行签名. (如何分享私钥和证书仍然在研究中.)
	* 命令类似于 codesign --force --sign 'Developer ID Application: xxxCompany (2xxx)' tmp/xxx.app 
	* 这个命令运行正常不代表签名完成.(必须使用spctl进行检查.)
* 签名之后的app里面任何文件变化都会导致应用签名错误,实际运行时会各种弹窗.
* 如果你没有私钥,就无法使用那张证书进行签名.
* 使用 spctl --assess --type execute /Applications/xxx.app 检查签名是否在当前系统上正常.(不正常会导致各种弹窗.)
* 本地生成的代码,不会弹窗询问是否要打开,可以把生成的东西放到网站上,再下载下来,此时系统就会询问是否允许运行.

### reference
* https://developer.apple.com/library/mac/technotes/tn2206/_index.html#//apple_ref/doc/uid/DTS40007919-CH1-TNTAG207