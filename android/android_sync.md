android异步
==============

- [android开发规范](https://github.com/addcn/ideas/blob/master/android/code_style.md)
- [android异步](https://github.com/addcn/ideas/blob/master/android/android_sync.md)




熟悉Windows编程的朋友知道Windows程序是消息驱动的，并且有全局的消息循环系统。Google参考了Windows的消息循环机制，也在Android系统中实现了消息循环机制。Android通过Looper、Handler来实现消息循环机制。Android的消息循环是针对线程的，每个线程都可以有自己的消息队列和消息循环。

Android系统中的Looper负责管理线程的消息队列和消息循环。通过Looper.myLooper()得到当前线程的Looper对象，通过Looper.getMainLooper()得到当前进程的主线程的Looper对象。

Android的消息队列(MessageQueue)和消息循环(Looper)都是针对具体线程的，一个线程可以存在一个消息队列和消息循环，特定线程的消息只能分发给本线程，不能跨线程和跨进程通讯。但是创建的工作线程默认是没有消息队列和消息循环的，如果想让工作线程具有消息队列和消息循环，就需要在线程中先调用Looper.prepare()来创建消息队列，然后调用Looper.loop()进入消息循环。

Activity是一个UI线程，运行在主线程中，Android系统会在Activity启动时为其创建一个消息队列和消息循环，每个消息处理的地方都有Handler的存在，它是做什么的呢？Handler的作用是把消息加入特定的Looper所管理的消息队列中，并分发和处理该消息队列中的消息。构造Handler的时候可以指定一个Looper对象，如果不指定则利用当前线程的Looper对象创建。




##名词术语

- 消息(Message)
    包含了消息id，数据，等信息，由MessageQueue队列控制。

- 消息队列(MessageQueue)

    消息队列，用链表的方式存储Message，按照FIFO（队列先进先出规则）让Looper来   抽取Message，进行处理。

- 消息循环(Looper)

    一个线程只有一个Looper对象，负责不断从MessageQueue 抽取Message进行处理。

- Handler

    Handler的作用：（1）在工作线程中发送消息。（2）在UI线程中获取、处理消息(Handler)。

- Runnable

    Runnable是接口。

- AsyncTask

    Android团队关于AsyncTask执行策略进行了多次修改，修改大致如下：

    - 自最初引入到Donut(1.6)之前，任务串行执行
    - 从Donut到GINGERBREAD_MR1(2.3.4),任务被修改成了并行执行
    - 从HONEYCOMB（3.0）至今，任务恢复至串行，但可以设置executeOnExecutor()实现并行执行。



- HandlerThread

    封装了Thread和Looper、MessageQueue。

- Executors

    Executors是Java API中一个快速创建线程池的工具类。






## 使用方法

###直接Thead

Thread 是一个类。Thread本身就实现了Runnable接口。它的声明如下：public class Thread implements Runnable {}。

创建Thread子类的一个实例并重写 run 方法，run 方法会在调用start()方法之后被执行。

```java
Thread thread = new Thread(){
    public void run(){
        System.out.println( "Thread Running" );
    }
};
thread.start(); //局限，一个类只能继承一个父类
```

###Thead+Runable

Runnable是接口。

实现Runnable接口，但是在使用Runnable定义的子类中没有start()方法，只有Thread类中才有，因此通过Thread类来启动Runnable实现的多线程。

```java
Runnable myRunnable = new Runnable(){
    public void run(){
        System.out.println( "Runnable running" );
    }
};

Thread thread = new Thread( myRunnable);
thread.start();
```
###Handler+Runable

new Handler.post(new Runnable(){})，如果使用匿名内部类是运行在UI主线程的，使用实现Runnable接口的线程类，则是运行在对应线程的。这种情况下，由于不是在新的线程中使用，所以千万别做复杂的计算逻辑。

```java
final Handler myHandler = new Handler() ;
//myHandler = new Handler(Looper. getMainLooper()) ;
myHandler.post( new Runnable() {
    @Override
    public void run() {
        // TODO Auto-generated method stub
        try {
            for (int i = 0; i < 10; i++) {
                Thread.sleep(1000 );
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        //與 Thread 不同的是，我們可以在Runnble直接更新介面
        mTitle .setText( "Update My UI");
    }
});

@Override
protected void onPause () {
    super .onPause() ;
    if (myHandler != null ) {
        myHandler .removeCallbacks(myRunnable) ;
    }
}
```
###Handler+Message

1、在主线程创建Handler

```java
//主线程创建Handler 
// final Handler myHandler = new Handler();
final Handler myHandler = new Handler(Looper.getMainLooper()){//或者直接主线程new Handler()
    @Override
    public void handleMessage (Message msg) {
        super .handleMessage(msg) ;
        if (!Thread. currentThread().isInterrupted()) { //Activity 結束時中斷它
            if (msg.what == 0x123){
                String txt = (String)msg. obj;
                if(txt!= null && !txt.equals("")){
                    //TODO:action txt
                }
            }
        }
    }
};

//  发送消息
// （1）new Handler.post(new Runnable(){})
// 其实内部实现也是sendMessageDelayed()，见
//  public final boolean post (Runnable r)
//  {
//     return  sendMessageDelayed( getPostMessage(r) , 0 ) ;
//  }
myHandler.post( new Runnable() {
    @Override
    public void run() {
        // TODO Auto-generated method stub
        mTitleTv.setText( "Update My UI");
    }
});

// （2）new Handler.sendMessage(msg) 
Message msg = new Message(); //发送通知，加入线程
// Message msg = Message.obtain();
// Message msg = myHandler.obtainMessage();
msg. what = 0x123;
msg. obj = "" ; //參數txt
myHandler .sendMessage(msg) ;

```

2、在子线程创建Handler

```java
// 子线程创建Handler
class Background extends Thread{
    public Handler myHandler;
    public void run (){
        Looper.prepare () ; // （1）调用Looper.prepare()方法为当前线程创建Looper对象,而它的构造器会创建配套的MessageQueue。在非主线程中是没有looper的所以在创建handler前一定要使用prepare()创建一个Looper
        myHandler = new Handler(){ // TODO:fix leaks warning
            @Override
            public void handleMessage (Message msg){

            }
        };
        Looper. loop() ; // （2）调用Looper.loop()方法启动Looper。建立一个消息循环，支持该线程将不会退出，不断进行循环
    }
}
Background background = new Background() ;
background .start() ;// 启动新线程

//  发送消息
Message msg = new Message();
msg.what = 0x123;
Bundle bundle = new Bundle();
bundle.putInt( "id" , 1001 );
msg.setData(bundle) ;
msg.sendToTarget() ; //?????Message对象池中获取到Message对象
background. myHandler.sendMessage(msg) ; // 向子线程中的Handler发送消息

```
###Activity.runOnUiThread(Runnable)

（注：见 [http://blog.csdn.net/caiwenfeng_for_23/article/details/37579653](http://blog.csdn.net/caiwenfeng_for_23/article/details/37579653)）

```java
// 具体见内部实现
//     public final void runOnUiThread(Runnable action) {
//    //如果当前线程不为Ui主线程则使用定义好的mHandler
//         if (Thread.currentThread() != mUiThread) {
//             mHandler.post(action);
//        } else {
//            action.run();
//         }
//    }
BrowserActivity.this.runOnUiThread(new Runnable() {
    public void run() {
        Toast.makeText( mContext, "Update My UI" , Toast.LENGTH_LONG).show() ;
    }
});

```
###HandlerThread

封装了Thread和Looper、MessageQueue

```java
public class UserLoginActivity extends AppCompatActivity {

    private Handler mHandler;
    int what = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super .onCreate(savedInstanceState) ;
        setContentView(R.layout. activity_user_login );

         // 因为HandlerThread()里面已经封装好了Looper.prepare()和Looper.loop(); 
        HandlerThread thread = new HandlerThread("自定义消息队列" ) ;
        thread.start() ;
        //thread.getLooper()如果换成Looper.myLooper()就是得到主线程的looper 
        mHandler = new Handler(thread.getLooper()) { // TODO:fix leaks warning
            //handler在哪个线程处理消息，取决于Looper在哪个线程创建 
            @Override 
            public void handleMessage (Message msg) {
                String content = "当前线程：" + Thread.currentThread ().getName() + "msg:" + msg. what; 
                Toast.makeText (UserLoginActivity.this, content , Toast. LENGTH_SHORT ).show(); //提示：  当前线程：自定义消息队列 0/当前线程：自定义消息队列 1 
            } 
        }; 

        /**
        * 点击事件
        */
        findViewById(R.id. btn_user_login).setOnClickListener(new View.OnClickListener() {

            @Override
            public void onClick(View v) {
                mHandler.sendEmptyMessage( what++); //主线程发送
                new Thread( "thread-a") {
                    public void run () {
                        mHandler.sendEmptyMessage(what ++);//“thread-a”子线程发送
                    }
                }.start();
            }
        });
        
    }
}

```

###AsyncTask

Android团队关于AsyncTask执行策略进行了多次修改，修改大致如下：

 - 自最初引入到Donut(1.6)之前，任务串行执行
 - 从Donut到GINGERBREAD_MR1(2.3.4),任务被修改成了并行执行
 - 从HONEYCOMB（3.0）至今，任务恢复至串行，但可以设置executeOnExecutor()实现并行执行。

###Executors

Executors是Java API中一个快速创建线程池的工具类。




