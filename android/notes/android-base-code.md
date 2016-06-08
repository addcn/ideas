Android中常用代码
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



- 设置文本颜色

`title.setTextColor(0xff000000);`


- indexOf判斷字符

        if(url!=null && url.length()>0){
                if(url.indexOf("?")==-1){
                        url = url + "?";
                }
        }



- A-->B-->C连续转跳

`PageAActivity.java`

        protected static final int REQUEST_CODE = 0;

        //转跳
        Intent intent = new Intent();
        intent.setClass(PageAActivity.this, PageBActivity.class); //A-->B
        Bundle bundle = new Bundle();
        bundle.putInt("position", position);
        intent.putExtras(bundle);
        startActivityForResult(intent, REQUEST_CODE);

        /**
         * 条件选择返回值
         */
        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent intent) 
        {
                super.onActivityResult(requestCode, resultCode, intent);
                if (intent == null) {
                        return;
                }
                if (requestCode == REQUEST_CODE) {
                        if (resultCode == RESULT_OK) {
                                Bundle bundle = new Bundle();
                                bundle = intent.getExtras();
                                if (bundle != null) {
                                        int position = bundle.getInt("position");
                                        //TODO:you code here
                                }
                        }
                }
        }


`PageBActivity.java`

        if(position==0){ // 不限
                Intent intent = new Intent();
                Bundle bundle = new Bundle();
                bundle.putString("regionId", regionId);
                bundle.putString("regionName", regionName);
                intent.putExtras(bundle);
                setResult(RESULT_OK, intent); //B-->A
                finish();
        }else{ // 县市
                Intent intent = new Intent();
                intent.setClass(PageBActivity.this, PageCActivity.class); //B-->C
                Bundle bundle = new Bundle();
                bundle.putString("regionId", regionId);
                bundle.putString("regionName", regionName);
                intent.putExtras(bundle);
                intent.setFlags(Intent.FLAG_ACTIVITY_FORWARD_RESULT); // 直接转跳
                overridePendingTransition(R.anim.remain, R.anim.push_left_out);
                startActivity(intent);
                finish();
        }


`PageCActivity.java`

        Intent intent = new Intent();
        Bundle bundle = new Bundle();
        bundle.putString("regionId", regionId);
        bundle.putString("regionName", regionName);
        intent.putExtras(bundle);
        setResult(RESULT_OK, intent); //B-->C
        finish();

