### 报错及解决方案:
#### Error checking for billing v3 support. (response: 3:Billing Unavailable)
* GooglePlay版本太旧
* 所在地区不支持GooglePlay支付

#### The publisher cannot purchase this item.
* 管理APK上传的google账号不能用于测试支付,必须再注册一个账号用于测试支付

#### 要求绑定信用卡
* 去淘宝上买GooglePlay礼品卡,应该是10刀的那种,充到你的测试账号上,然后就可以测试了,(10刀不会被消耗,但是也取不出来了)
* 当然你也可以绑定一张visa礼品卡或visa信用卡


#### This version of the application is not configured for billing through Google Play
* android:versionCode 要和某个上传上去的版本的的versionCode一模一样才可以进行支付测试.
* Google takes a while to process applications and update them to their servers, for me it takes about half a day. So after saving the apk as a draft on Google Play, you must wait a few hours before the in-app products will respond normally and allow for regular purchases.
* Export and sign APK. Unsigned APK trying to make purchases will get error.