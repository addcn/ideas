Android中的selector
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


`selector`常用属性：

- `android:state_selected` 是否选中状态，true或false
- `android:state_focused` 是否聚焦状态，true或false
- `android:state_pressed` 是否按压状态，true或false
- `android:state_enabled` 是否可用状态，true或false
- `android:state_checkable` 是否可勾选状态，true或false
- `android:state_checked` 是否勾选状态，true或false
- `android:state_active`  是否被激活状态，true或false
- `android:window_focused` 应用程序窗口焦点状态，true或false
- `android:state_hovered` 是否鼠标在上面滑动的状态，true表示鼠标在上面滑动，默认为false。必须在`API Level 14`及以上才支持

- `android:color` 定义特定状态的颜色，16进制颜色

注意：在状态描述中，第一个匹配当前状态的item会被使用。 因此，如果第一个item没有任何状态特性的话，那么它将每次都被使用，所以默认的值必须总是在最后。


另外，`selector`标签下有两个在状态改变时出现淡入淡出效果的属性，但必须在`API Level 11`及以上才支持：

- `android:enterFadeDuration` 状态改变时，新状态展示时的淡入时间，以毫秒为单位
- `android:exitFadeDuration`  状态改变时，旧状态消失时的淡出时间，以毫秒为单位 

典型用法： `selector_corner_border.xml`

	<?xml version="1.0" encoding="UTF-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android">
		<!-- 不可用时 -->
	    <item android:drawable="@drawable/corner_border_d" android:state_enabled="false" />
		<!-- 聚焦时 -->
	    <item android:drawable="@drawable/corner_border_p" android:state_focused="true" />		
		<!-- 按压时 -->
	    <item android:drawable="@drawable/corner_border_p" android:state_pressed="true" />
		<!-- 默认 -->
	    <item android:drawable="@drawable/corner_border_n" />	    
	</selector>

