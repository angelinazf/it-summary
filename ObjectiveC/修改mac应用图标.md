按照下列格式把图标的不同格式码放在一个叫 AppIcon.iconset 的目录里面.
```
~/ > ll -alh tmp/AppIcon.iconset
icon_128x128.png
icon_128x128@2x.png
icon_16x16.png
icon_16x16@2x.png
icon_256x256.png
icon_256x256@2x.png
icon_32x32.png
icon_32x32@2x.png
icon_512x512.png
icon_512x512@2x.png
```

使用 下列命令来把这些图标打包成一个文件. 并且把最终结果放入 app里面的 Contents/Resources/AppIcon.icns 中.注意执行该命令前,要确保 Contents/Resources 目录存在.
```
iconutil -c icns -o tmp/xxx.app/Contents/Resources/AppIcon.icns tmp/AppIcon.iconset
```