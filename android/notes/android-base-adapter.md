Android中的adapter
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


`java`


        public class HousePostCommonActivity extends BaseActivity {

        static final String TAG = "HousePostCommonActivity";
        private Context mContext;
        private BaseApplication mApp;

        private ImageButton headLeftBtn;
        private TextView headLayoutTitle;

        private List<Map<String, String>> mList = null;
        private ListView mListView = null;	
        private SimpleAdapter mAdapter = null;

        private int mPostTvId;
        private String mPostKey = "";	

        @Override
        protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                this.requestWindowFeature(Window.FEATURE_NO_TITLE);
                setContentView(R.layout.activity_house_post_type);
                
                // 成員變量
                mContext = this;
                mApp = (BaseApplication) getApplication();
                                
                // 初始視圖
                Bundle extras = getIntent().getExtras();
                if (extras != null) {
                        mPostTvId = extras.getInt("postTvId");
                        mPostKey = extras.getString("postKey");			
                }
                // 初始視圖
                initViews();
        }

        /**
         * 初始視圖
         */
        private void initViews() 
        {
                // 返回按鈕
                headLeftBtn = (ImageButton) findViewById(R.id.head_left_btn);
                headLeftBtn.setOnClickListener(new OnClickListener() {
                        public void onClick(View v) {
                                finish();
                        }
                });
                
                // 列表内容
                headLayoutTitle = (TextView)findViewById(R.id.head_laout_title);
                headLayoutTitle.setText(mContext.getResources().getString(R.string.house_post_common_header_title));
                mListView = (ListView)findViewById(R.id.list_view);
                mList = getList();
                mAdapter = new SimpleAdapter(getApplicationContext(), mList,
                                R.layout.item_house_filter_region,
                                new String[] { "filter_name" },
                                new int[] { R.id.filter_item_text });
                mListView.setAdapter(mAdapter);
                mListView.setOnItemClickListener(new OnItemClickListener() {
                public void onItemClick(AdapterView<?> parent, View view, int position, long id) {	        	
                        Intent intent = new Intent();
                        intent.setClass(HousePostCommonActivity.this, HousePostActivity.class);
                        Bundle bundle = new Bundle();
                        bundle.putInt("postTvId", mPostTvId);
                        bundle.putString("postKey", mPostKey);
                        bundle.putString("postKeyId", mList.get(position).get("filter_val"));
                        bundle.putString("postKeyName", mList.get(position).get("filter_name"));
                        intent.putExtras(bundle);
                        setResult(RESULT_OK, intent);
                        finish();
                }
            });
        }

        /**
         * 設置列表數據
         */
        private ArrayList<Map<String, String>> getList() 
        {
                String keyIndex = mPostKey;
                
                InputStream inputStream = mContext.getResources().openRawResource(R.raw.post);
                HashMap<String, Object> data = XmlParserUtils.parser(inputStream);		
                ArrayList<String> orderMap = XmlParserUtils.geto(data, keyIndex);
                ArrayList<Map<String, String>> listData = new ArrayList<Map<String, String>>();
                for (int i = 0; i < orderMap.size(); i++) {
                        String key = orderMap.get(i);
                        String filterKey = key;
                        String filterName = XmlParserUtils.getValName(data, keyIndex, key);
                        Map<String, String> map = new HashMap<String, String>();
                        map.put("filter_val", filterKey);
                        map.put("filter_name", filterName);
                        listData.add(map);
                }
                return listData;
        }
        }

`xml`

        <?xml version="1.0" encoding="utf-8"?>
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:background="@color/body_bg"
        android:orientation="vertical" >

        <RelativeLayout
        android:id="@+id/head_layout"
        android:layout_width="fill_parent"
        android:layout_height="50.0dip"
        android:background="@drawable/drawable_head_layout_bg" >

        <TextView
            android:id="@+id/head_laout_title"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="@string/post_type_header_title"
            android:textColor="#ffffffff"
            android:textSize="20.0sp" />

        <ImageButton
            android:id="@+id/head_left_btn"
            android:layout_width="50.0dip"
            android:layout_height="fill_parent"
            android:background="@drawable/drawable_head_back_bg"
            android:gravity="center"
            android:scaleType="centerInside"
            android:src="@drawable/left_arrow_icon" />

        <View
            android:id="@+id/head_left_line"
            android:layout_width="2.0dip"
            android:layout_height="fill_parent"
            android:layout_toRightOf="@+id/head_left_btn"
            android:background="@drawable/drawable_head_layout_margin" />
        </RelativeLayout>

        <include layout="@layout/layout_body_loading" />

        <LinearLayout
        android:id="@+id/list_view_layout"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:orientation="vertical"
        android:background="#ffffffff" >
        <ListView
            android:id="@+id/list_view"
            style="@style/corner_listview_style"
            android:layout_alignParentLeft="true" >
        </ListView>
        </LinearLayout>

        </LinearLayout>