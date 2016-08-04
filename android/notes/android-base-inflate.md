Android中的inflate
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

LayoutInflater技术广泛应用于需要动态添加View的时候，比如在ScrollView和ListView中，经常都可以看到LayoutInflater的身影。

LayoutInflater其实就是使用Android提供的pull解析方式来解析布局文件的。


#### 1、LayoutInflater的获取

获取到LayoutInflater的实例，有两种方法可以获取。

第一种：

	LayoutInflater layoutInflater = LayoutInflater.from(context);

第二种：

	LayoutInflater layoutInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);


其实第一种就是第二种的简单写法，只是Android做了一下封装而已。



	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, null);
	
	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, null, false);
	
	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, container);
	
	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, container, false);


#### 2、inflate的使用

	inflate(int resource, ViewGroup root, boolean attachToRoot)  

- 如果root为null，attachToRoot将失去作用，设置任何值都没有意义。

- 如果root不为null，attachToRoot设为true，则会给加载的布局文件的**指定一个父布局**，即root。

- 如果root不为null，attachToRoot设为false，则会**将布局文件最外层的所有layout属性进行设置**，当该view被添加到父view当中时，这些layout属性会**自动生效**。

- 在不设置attachToRoot参数的情况下，如果root不为null，attachToRoot参数默认为true。



#### 3、注意事项

一般情况下，我们在fragment或是adapter中加载布局都是如此使用：


	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, container, false);


其中 ```false``` 意思为：把布局添加到父视图中，并保留父视图中的其他视图；

而 infate 方法也可以省略 boolean 参数，而如果省略了boolean变量，而 container 不为空的情况下，第三个参数默认是为 ```true``` 的，即：

	public View inflate(@LayoutRes int resource, @Nullable ViewGroup root) {
    	return inflate(resource, root, root != null);
	}


这个时候如果我们调用


	View row = LayoutInflater.from(context).inflate(R.layout.item_scroll_content, container)


则表示，要删除父视图中其他子视图。于是可能就会报如下的错误了。

```java.lang.IllegalStateException: The specified child already has a parent. You must call removeView() on the child's parent first.```


#### 4、使用例子

xml

	<LinearLayout
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:orientation="vertical"
	        android:paddingBottom="5.0dip"
	        android:paddingLeft="5.0dip"
	        android:paddingRight="5.0dip"
	        android:paddingTop="12.0dip" >
	
	        <HorizontalScrollView
		        android:layout_width="fill_parent"
		        android:layout_height="wrap_content"
		        android:scrollbars="none" >

	                <LinearLayout
		                android:id="@+id/ll_agent_ads_list"
		                android:layout_width="wrap_content"
		                android:layout_height="wrap_content"
		                android:orientation="horizontal" >
	                </LinearLayout>

	        </HorizontalScrollView>
	</LinearLayout>



java

	/**
	 * 打勾點擊事件綁定
	 */
	private void initAentAdsListClick(ArrayList<HashMap<String, String>> agentAds) 
	{
        // 初始不選
        final RelativeLayout rl_pay_exist_agent = (RelativeLayout) findViewById(R.id.rl_pay_exist_agent);
        final ImageView iv_pay_exist_agent = (ImageView) findViewById(R.id.iv_pay_exist_agent);
        rl_pay_exist_agent.setTag("off");
        iv_pay_exist_agent.setVisibility(View.GONE);
        
        // 廣告列表
        LinearLayout ll_agent_ads_list = (LinearLayout) findViewById(R.id.ll_agent_ads_list);
        houseLinearLayoutAlls.clear(); //清空
        ll_agent_ads_list.removeAllViews();
        if(agentAds.size()>0){
                for (int i = 0; i < agentAds.size(); i++){
                        FrameLayout root = (FrameLayout) mInflater.inflate(R.layout.item_house_open, ll_agent_ads_list, false);
                        final ImageView ivIsVip = (ImageView) root.findViewById(R.id.iv_is_vip);				
                        final LinearLayout view = (LinearLayout) root.findViewById(R.id.ll_wrapper);
                        view.setOnClickListener(new OnClickListener() {
                                        public void onClick(View v) {
                                                String tagto = (view.getTag()!=null) && ((String) view.getTag()).equals("off") ? "on" : "off";
                                                unSelectAgentAds(); //清空物件選擇，一定要在tagto之後
                                                unSelectPayTicks(); //全部不選
                                                ImageView iv_pay_exist_agent = (ImageView) findViewById(R.id.iv_pay_exist_agent);
                                                final int padding = view.getPaddingTop();
                                                if(tagto.equals("on")){
                                                        mCurrentSelectPlanId = R.id.rl_pay_exist_agent;
                                                        mCurrentSelectAgentAdId = (view.findViewById(R.id.tv_title)!=null) && (((TextView) view.findViewById(R.id.tv_title)).getTag()!=null)  ? (String) ((TextView) view.findViewById(R.id.tv_title)).getTag(): "";
                                                        iv_pay_exist_agent.setVisibility(View.VISIBLE);
                                                        view.setBackgroundResource(R.drawable.bg_rectangle_p);
                                                        view.setPadding(padding, padding, padding, padding);
                                                }else{
                                                        mCurrentSelectPlanId = -1;
                                                        iv_pay_exist_agent.setVisibility(View.GONE);
                                                        view.setBackgroundResource(R.drawable.bg_rectangle_n);
                                                        view.setPadding(padding, padding, padding, padding);
                                                }
                                                view.setTag(tagto);
                                                
                                                calTotal(R.id.rl_pay_exist_agent, tagto);
                                        }
                                });
                TextView tv_title = (TextView) view.findViewById(R.id.tv_title);
                TextView tv_desc = (TextView) view.findViewById(R.id.tv_desc);
                String title = agentAds.get(i).containsKey("title") ? agentAds.get(i).get("title") : "";
                String desc = agentAds.get(i).containsKey("desc") ? agentAds.get(i).get("desc") : "";
                String id = agentAds.get(i).containsKey("id") ? agentAds.get(i).get("id") : "";
                //是否vip
                String isvip = agentAds.get(i).containsKey("isvip") ? agentAds.get(i).get("isvip") : "0";
                if(isvip!=null && isvip.equals("1")){
                        ivIsVip.setVisibility(View.VISIBLE);
                }else{
                        ivIsVip.setVisibility(View.GONE);
                }
                tv_title.setText(Html.fromHtml(title));
                tv_title.setTag(id);
                tv_desc.setText(desc);	        
                ll_agent_ads_list.addView(root);
                houseLinearLayoutAlls.add(view);
            }  
        }
}


#### 参考文章

> [Android LayoutInflater原理分析，带你一步步深入了解View(一)](http://blog.csdn.net/guolin_blog/article/details/12921889)

> [LayoutInflater&LayoutInflaterCompat源码解析](https://github.com/peerless2012/SourceAnalysis/blob/master/Android/FrameWork/LayoutInflater%26LayoutInflaterCompat%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90.md)