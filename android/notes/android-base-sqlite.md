Android中的sqlite
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



1、```SQLiteOpenHelper```

SQLiteOpenHelper类是一个抽象类，借助这个类就可以简单地对数据库进行创建和升级。

SQLiteOpenHelper类中有两个抽象方法：

```onCreate()```方法是实现创建数据库的逻辑，数据库文件会存放在```/data/data/<packageName>/database/```目录下。

```onUpgrade()```方法是实现升级数据库的逻辑，当实例化```SQLiteOpenHelper```子类对象时，传入的参数```version```大于当前数据库的 版本号时，当调用```getReadableDatabase()```或```getWritableDatabase()```时，就会调用此升级方法。



2、数据库操作

**增加**

**删除**

**修改**



3、升级数据库



典型用法：

		
	import android.content.Context;
	import android.database.sqlite.SQLiteDatabase;
	import android.database.sqlite.SQLiteOpenHelper;
	
	/**
	 * 數據庫輔助類
	 * 
	 * @author <a href="mailto:lhuibo@gmail.com">dodo</a> 2012/12/24
	 * @version ${Id}
	 * 
	 */
	
	public class DatabaseHelper extends SQLiteOpenHelper {
			
		private static final String DB_NAME = "myApp.db";
		private static final int DB_VERSION = 1;
		private static DatabaseHelper mInstance;
		
		protected DatabaseHelper(Context context) {
			super(context, DB_NAME, null, DB_VERSION);
		}
		
		public static DatabaseHelper getInstance(Context context) {
			mInstance = new DatabaseHelper(context);
			return mInstance;
		}
	
		public static void destoryInstance() {
			mInstance.close();
		}
	
		@Override
		public void onOpen(SQLiteDatabase db) {
			super.onOpen(db);
		}
	
		@Override
		public void onCreate(SQLiteDatabase db) {
			String sql;
			sql = "CREATE TABLE house_fav ("
	        + "fav_id INTEGER PRIMARY KEY AUTOINCREMENT,"
	        + "user_id INTEGER NOT NULL DEFAULT (0),"
	        + "type INTEGER NOT NULL DEFAULT (0),"
	        + "post_id INTEGER NOT NULL DEFAULT (0),"
	        + "source VARCHAR(255) NOT NULL DEFAULT 'android',"
	        + "is_sync INTEGER NOT NULL DEFAULT (0),"
	        + "is_del INTEGER NOT NULL DEFAULT (0),"
	        + "posttime TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP"
	        + ");";
			db.execSQL(sql);
		}
	
		@Override
		public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) 
		{	
			
		}
	}



创建数据库


参考文章

