#### texture的透明渐变边框问题:
当某一张低分辨率的图,放大倍数很高时会出现.
主要有2个原因:
* 开启了线性插值(GL_LINEAR),并且超出边界的处理为 重复(GL_REPEAT)(重复是默认值),会导致放大倍数很高时,被肉眼看见.这种情况会在图片的四周出现透明渐变边框.
* 开启了线性插值,并且将一张不是2**n的尺寸的图片转换成了2**n的尺寸的图片,但是没有图片的部分的颜色是(0,0,0,0),导致线性插值的边界部分出现了透明渐变.这种情况会在图片的右边和下边出现透明渐变边框.

#### 解决方案
* 解决方案1,使用像素风进行插值(可以解决原因1,2):
```
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.NEAREST)
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.NEAREST)
```

* 解决方案2,使用线性插值,但是在非2**n的尺寸的图片转换的时候,把图片最外层的像素再多重复一遍.但是发送uv时,仍然只发送原始的数据.
```
	//超出边界处理为截断.
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR)
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR)
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE)
	p.glctx.TexParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE)

	// 把图片最外层的像素再多重复一遍.
	for i:=0;i<h;i++{
		thisGlImage.RGBA.SetRGBA(w,i,thisGlImage.RGBA.RGBAAt(w-1,i))
	}
	for i:=0;i<w;i++{
		thisGlImage.RGBA.SetRGBA(i,h,thisGlImage.RGBA.RGBAAt(i,h-1))
	}
	thisGlImage.RGBA.SetRGBA(w,h,thisGlImage.RGBA.RGBAAt(w-1,h-1))
```