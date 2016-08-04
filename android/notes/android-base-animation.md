Android基本动画
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
- [Android中的adapter](https://github.com/addcn/ideas/blob/master/android/notes/android-base-adapter.md)
- [Android中的sqlite](https://github.com/addcn/ideas/blob/master/android/notes/android-base-sqlite.md)

----------

Android中动画分为三种：

- 补间动画
	- 补间动画也称View动画，它的作用对象只能是View，它有四种典型的变换效果，分别是：平移动画、缩放动画、旋转动画、透明度动画。这四种动画效果可以通过java代码的方式动态的创建，也可以通过xml文件来创建。


- 属性动画
	- 属性动画，除了最基本的对View进行平移、缩放、旋转、透明度操作外，还可以将动画作用于指定的对象上，例如将一个Point对象从(0, 0)位置移动到(100, 100)位置。但是，有一点要注意，属性动画只能只能在Android3.0即以上版本使用，如果要兼容Android3.0以下版本，可以考虑使用JakeWharton的动画库：[http://nineoldandroids.com/](http://nineoldandroids.com/)，这个库在Android3.0以下的属性动画其实还是传统的补间动画！


- 帧动画
	- 帧动画是顺序的播放一系列图片，从而产生动画的效果，其实也就是图片的切换。但是如果图片过多、过大的话是很容易产生OOM的，所以使用时需要注意。


















参考文章

> [Android 你应该知道的动画](http://www.jianshu.com/p/bb206e3b0e02#)

> [属性动画ValueAnimator在自定义View中的使用](http://mafei.site/2016/07/17/android-valueanimator/)


