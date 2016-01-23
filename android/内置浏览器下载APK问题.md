### 如果希望android内置浏览器可以正常下载APK,需要:
* 如果是https连接,请把需要被下载的这个域名的证书,设置为默认证书.android的apk下载是不支持https的sni的. (未证实)

* 设置下载url的header的Content-Type为 application/vnd.android.package-archive (未证实)
* 正确设置下载url的Content-Length为 正确的值. (已证实)