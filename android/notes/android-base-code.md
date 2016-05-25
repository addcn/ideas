Android中常用代码
==================================================


Android界面开发

- [Android中的shape]()
- [Android中的selector]()
- [Android中align]()
- [Android中的style]()
- [Android中的inflate]()
- [Android中的常用布局]()
- [Android中的view绘制流程]()
- [Android中常用代码]()

----------



- 设置文本颜色

`title.setTextColor(0xff000000);`


- A-->B-->C连续转跳

`PageAActivity.java`

        protected static final int REQUEST_CODE = 0;

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
                                }
                        }
                }
        }

        //转跳
        Intent intent = new Intent();
        intent.setClass(PageAActivity.this, PageBActivity.class); //A-->B
        Bundle bundle = new Bundle();
        bundle.putInt("position", position);
        intent.putExtras(bundle);
        startActivityForResult(intent, REQUEST_CODE);


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