Android中的shape
==================================================


Android界面开发

- [Android中的shape](https://github.com/addcn/ideas/blob/master/android/notes/android-base-shape.md)
- [Android中的selector](https://github.com/addcn/ideas/blob/master/android/notes/android-base-selector.md)
- [Android中align](https://github.com/addcn/ideas/blob/master/android/notes/android-base-align.md)
- [Android中的style](https://github.com/addcn/ideas/blob/master/android/notes/android-base-style.md)
- [Android中的inflate](https://github.com/addcn/ideas/blob/master/android/notes/android-base-inflate.md)
- [Android中的常用布局](https://github.com/addcn/ideas/blob/master/android/notes/android-base-layout.md)
- [Android中常用代码](https://github.com/addcn/ideas/blob/master/android/notes/android-base-code.md)
- [Android中view绘制流程](https://github.com/addcn/ideas/blob/master/android/notes/android-base-view.md)

----------


使用shape可以自定义以下四种类型的形状，通过android:shape指定：


1. `rectangle` 矩形，默认的形状，可以画出直角矩形、圆角矩形、弧形等
1. `oval` 椭圆形，用得比较多的是画正圆
1. `line` 线形，可以画实线和虚线
1. `ring` 环形，可以画环形进度条


用到以下特性：

- solid：实心

	设置形状填充的颜色，只有android:color一个属性

- padding：间隔

	设置内容与形状边界的内间距，可分别设置左右上下的距离

- gradient：渐变

	android:startColor和android:endColor分别为起始和结束颜色，ndroid:angle是渐变角度，必须为45的整数倍。

	另外渐变默认的模式为android:type="linear"，即线性渐变，可以指定渐变为径向渐变，android:type="radial"，径向渐变需要指定半径android:gradientRadius="50"。

- stroke：描边。

	设置描边，可描成实线或虚线。
	
	android:color 描边的颜色，android:width 描边的宽度，android:dashWidth 设置虚线时的横线长度，android:dashGap 设置虚线时的横线之间的距离。

	我们还可以把描边弄成虚线的形式，设置方式为：

		android:dashWidth="5dp" 
		android:dashGap="3dp"

	其中android:dashWidth表示'-'这样一个横线的宽度，android:dashGap表示之间隔开的距离。

- corners：圆角

	设置圆角，只适用于rectangle类型，可分别设置四个角不同半径的圆角，当设置的圆角半径很大时，比如200dp，就可变成弧形边。

	我们还可以把四个角设定成不同的角度，方法为：

		<corners 
		    android:topRightRadius="20.0dp"   //右上角
		    android:bottomLeftRadius="20.0dp" //右下角
		    android:topLeftRadius="10.0dp"     //左上角
		    android:bottomRightRadius="10.0dp" //左下角
		 />


	注意，bottomLeftRadius是右下角，而不是左下角。



典型用法： `corner_border_n.xml`

    <?xml version="1.0" encoding="utf-8"?>
    <shape xmlns:android="http://schemas.android.com/apk/res/android"
        android:shape="rectangle" >

        <!-- 圆角 -->
        <corners android:radius="3.0dp" />

        <padding
            android:bottom="2.0dp"
            android:left="2.0dp"
            android:right="2.0dp"
            android:top="2.0dp" />

        <!-- 实心 -->
        <solid android:color="#ffffff" />

        <size
            android:height="0.0dp"
            android:width="0.0dp" />

        <!-- 描边 -->
        <stroke
            android:width="1.0dp"
            android:color="#e1e1e1" />

    </shape>



参考文章

> [在线maker工具 http://angrytools.com/android/button/](http://angrytools.com/android/button/)


> [android样式的开发http://keeganlee.me/post/android/20150830](http://keeganlee.me/post/android/20150830)