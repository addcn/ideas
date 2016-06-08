Android中align
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


`LinearLayout`有两个非常相似的属性：


`android:gravity = center|right`

相对*元素本身*来说的，元素本身的文本对齐方式，默认是左对齐。


`android:layout_gravity = center|right`

相对与它的*父元素*说的，说明元素显示在父元素的什么位置。


用法

1、xml设置 `activity_layout.xml`



	<LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:orientation="vertical" >

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center|right"
            android:gravity="center"
            android:text="text" />

    </LinearLayout>

2、java代码设置 `ActivityLayout.java`


    TextView text  = new TextView(this);
    text.setText("text");

    LinearLayout.LayoutParams lp = new LinearLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
    lp.gravity = Gravity.RIGHT; //android:layout_gravity属性
    text.setLayoutParams(lp);
    text.setGravity(Gravity.CENTER); //android：gravity属性
        
    LinearLayout layout = new LinearLayout(this);
    layout.setOrientation(LinearLayout.VERTICAL);
    lp.gravity = Gravity.RIGHT;  
    layout.addView(text, lp);
    
    layout.addView(text);
    setContentView(layout);


    lp = new RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
    lp.addRule(RelativeLayout.CENTER_IN_PARENT);
    mContainer.addView(text, lp);

`RelativeLayout中`设置要使用`addRule`方法。



显示结果：





`android:layout_centerVertical = true`



