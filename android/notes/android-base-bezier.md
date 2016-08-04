Android中的贝塞尔曲线
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



参考文章

基礎

> [Path之贝塞尔曲线](https://github.com/GcsSloop/AndroidNote/blob/master/CustomView/Advance/%5B06%5DPath_Bezier.md)
 
實例——繪製水波及曲線圖

> [自定义View——贝塞尔曲线](https://github.com/Idtk/Blog/blob/master/Blog/6%E3%80%81Bezier.md)

實例——天氣曲線如何繪製
二阶贝塞尔，三阶贝塞尔。天气预报曲线图


> [Android 自定义View高级特效，神奇的贝塞尔曲线](http://blog.csdn.net/qq_17250009/article/details/51027183)


安居客工程師博客

> [在Android中如何绘制光滑曲线（一）](http://tomkeyzhang.duapp.com/?p=88)

https://github.com/TomkeyZhang/BesselChart

http://hexo.trity.cc/2016/01/08/%E5%85%B3%E4%BA%8E%E8%B4%9D%E5%A1%9E%E5%B0%94%E6%9B%B2%E7%BA%BF%E9%97%AE%E9%A2%98/





Android自定义view进阶-- 神奇的贝塞尔曲线**********博主牛B裡面還有很多自定義view案例
http://blog.csdn.net/wingichoy/article/details/50492828

https://github.com/githubwing/LoadingView

wing带你玩转自定义view系列（1） 仿360内存清理效果
http://blog.csdn.net/wingichoy/article/details/50500479




使用地方總結

Android-贝塞尔曲线
http://itfish.net/article/61906.html




實例——一圖繪製多部分

> [Android - Animation 贝塞尔曲线之美](http://gavinliu.cn/2015/03/30/Android-Animation-%E8%B4%9D%E5%A1%9E%E5%B0%94%E6%9B%B2%E7%BA%BF%E4%B9%8B%E7%BE%8E/)









相關——動畫

> [基于贝塞尔曲线的Android动画差值器](http://ivonhoe.github.io/2015/04/17/%E5%9F%BA%E4%BA%8E%E8%B4%9D%E5%A1%9E%E5%B0%94%E6%9B%B2%E7%BA%BF%E7%9A%84Android%E5%8A%A8%E7%94%BB%E5%B7%AE%E5%80%BC%E5%99%A8/)

相關——svg

> [深度掌握SVG路径path的贝塞尔曲线指令](http://www.zhangxinxu.com/wordpress/2014/06/deep-understand-svg-path-bezier-curves-command/)


相關——指定點平滑連接ios版實現

> [开源：破解绘制贝塞尔曲线定位控制点难题](http://geek.csdn.net/news/detail/35668)


相關——html實現可以拖放兩個控制點，然後顯示四個點坐標
> [前段时间鼓捣bootstrap去了,最近看到贝塞尔曲线,就打算折腾折腾.](http://www.w3cfuns.com/notes/17515/59ef54e22c16b2010d696a1259a6c036.html)




怎样才能知道所要画贝塞尔曲线的控制点坐标?

http://zhidao.baidu.com/link?url=4ZnplSBfISxxG7oemrGSDgRWTkywhELZgeCFA6HvUuBNbpgT8BHFqCzhC-ebCF-GXj_OEUZDnb3vdiQkqLPcC_

寻找贝塞尔曲线控制点，画曲线 

用软件绘制贝塞尔曲线的时候，最简单的一种是点三个点出来一条曲线，我想知道的是在按贝塞尔曲线公式求解的时候，这三个控制点的坐标分别是怎样确定的？（当然你点的第二点肯定不是公式中的控制点，但是也许该坐标参与了运算，所以才会有曲线经过该点的效果）

以此类推在绘制双线曲线箭头的时候，这个控制点又该如何计算来影响两条曲线的生成呢？如果是Cubic Bezier spline（四个控制点）又该如何根据鼠标的选点计算出贝塞尔的控制点？

http://bbs.csdn.net/topics/330234380



相關——有疑問點1的答案參考文章翻譯

> [穿过已知点画平滑曲线（3次贝塞尔曲线）](http://blog.csdn.net/microchenhong/article/details/6316332)



完美解決疑問1

> [设计师教你怎么用最偷懒的方式画贝塞尔曲线](http://www.guokr.com/post/695800/)




