Android中的常用布局
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



工作中常用的布局整理



## 1、左右布局
## 1、等分布局
## 1、上下布局
## 1、上中下布局

## 1、左中右布局



### 1.1 `RelativeLayout`实现

>   实现方法：内容分别居左右，中间内容居中。
>   
>   优点缺点：不可换行。



```


左中右布局




```

### 1.2 `LinearLayout`实现

>   实现方法：内容分别居左右，中间内容居中。
>   
>   优点缺点：不可换行。


    
``` 

		<RelativeLayout style="@style/p_layout_style" >

            <LinearLayout
                android:id="@+id/title_ll"
                style="@style/p_left_layout_style" >

                <TextView
                    style="@style/p_left_text_style"
                    android:text="@string/house_post_text_item_title" />

                <TextView
                    style="@style/p_required_style"
                    android:text="*" />
            </LinearLayout>

            <View
                android:id="@+id/title_line"
                style="@style/p_line_style"
                android:layout_toRightOf="@+id/title_ll" />



            <EditText
                android:id="@+id/title_et"
                style="@style/p_right_text_style2"
                android:layout_toLeftOf="@+id/title_line"
                android:hint="@string/house_post_hint_title"
                 android:clickable="false"
                    android:focusable="true"
                android:maxLength="20" />
        </RelativeLayout>




```




```

	<LinearLayout
        android:id="@+id/price_add_layout"
        style="@style/table_tr"
        android:background="@drawable/drawable_preference_middle_item"
        android:focusable="true" >

        <LinearLayout style="@style/table_th" >

            <TextView
                style="@style/table_th_txt"
                android:text="@string/house_post_text_item_price_add" />
        </LinearLayout>

        <RelativeLayout style="@style/table_td" >

            <TextView
                android:id="@+id/price_add_tv"
                style="@style/table_td_txt"
                android:text="@string/house_post_text_default_price_add" />

            <ImageView
                android:id="@+id/icon_arrow"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_alignParentRight="true"
                android:layout_centerVertical="true"
                android:layout_marginRight="5.0dip"
                android:scaleType="matrix"
                android:src="@drawable/arrow_icon_small" />
        </RelativeLayout>
    </LinearLayout>

```