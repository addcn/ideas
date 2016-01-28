发布library到Maven仓库
==================================================

> 本文是将library发布到jcenter的一次记录。


对开发者更友好的android library仓库有`jcenter`和`Maven Central`，但是它们维护在完全不同的服务器上，由不同的人提供内容，两者之间毫无关系。在jcenter上有的可能Maven Central上没有，反之亦然。

除了两个标准的服务器之外，我们还可以把该library放在自己的的Maven仓库服务器，此时需要自己如下定义仓库的url,

```java
repositories {
    maven { url 'https://maven.fabric.io/public' }
}
```

然后在里面使用相同的方法获取一个library。

```java
dependencies {
    compile 'com.crashlytics.sdk.android:crashlytics:2.2.4@aar'
}
```

##发布环境

- JDK版本：`jdk1.7.0_75`
- Android Studio版本：`1.5.1`
- compileSdkVersion `23`, buildToolsVersion `"23.0.2"`

##具体步骤

- 注册[Bintray账号](https://bintray.com/)（我直接用google账号注册登入）。

- 在bintray上创建package。

    登录网站，点击maven——>Add New Package，为要发布的library创建一个package，输入所有需要的信息然后提交。



- 配置Project（最外层）`local.properties`文件API key。

    [Profile页面](https://bintray.com/profile/edit)复制API Key填写。

	完整内容如下：
	
	```java
	sdk.dir=D\:\\android-studio\\sdk	
	bintray.user = dodo
	bintray.apikey = ***********************
	```

- 配置Module（library）`build.gradle`文件。

	上传需要的插件等，完整内容如下：
	
	```java
	buildscript {
	    repositories {
	        jcenter()
	    }
	    dependencies {
	        classpath 'com.android.tools.build:gradle:1.5.0'
	        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
	        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.0'
	
	        // NOTE: Do not place your application dependencies here; they belong
	        // in the individual module build.gradle files
	    }
	}
	
	allprojects {
	    repositories {
	        jcenter()
	    }
	}
	
	task clean(type: Delete) {
	    delete rootProject.buildDir
	}
	```

- 配置Module（library）`build.gradle`文件。

	生成JavaDoc、生成Jar、配置项目的信息等，完整的内容如下：
	
	```java
	apply plugin: 'com.android.library'
	
	apply plugin: 'com.github.dcendents.android-maven'
	apply plugin: 'com.jfrog.bintray'
	
	// 版本号
	version = "1.0.0"
	android {
	    compileSdkVersion 23
	    buildToolsVersion "23.0.2"
	
	    defaultConfig {
	        minSdkVersion 8
	        targetSdkVersion 22
	        versionCode 1
	        versionName version
	    }
	    buildTypes {
	        release {
	            minifyEnabled false
	            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
	        }
	    }
	}
	
	dependencies {
	    compile fileTree(dir: 'libs', include: ['*.jar'])
	    testCompile 'junit:junit:4.12'
	    compile 'com.android.support:appcompat-v7:23.1.1'
	}
	
	def siteUrl = 'https://github.com/addcn/PNEditText'      // 项目的主页
	def gitUrl = 'https://github.com/addcn/PNEditText.git'   // Git仓库的url
	group = "com.uedao.android.pnedittext"                   // Maven Group ID for the artifact，一般填你唯一的包名
	install {
	    repositories.mavenInstaller {
	        // This generates POM.xml with proper parameters
	        pom {
	            project {
	                packaging 'aar'
	                // Add your description here
	                name 'Android EditText With Positive And Negative Button Widget' 	//项目描述
	                url siteUrl
	                // Set your license
	                licenses {
	                    license {
	                        name 'The Apache Software License, Version 2.0'
	                        url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
	                    }
	                }
	                developers {
	                    developer {
	                        id 'dodo'		//填写的一些基本信息
	                        name 'dodo'
	                        email 'lhuibo@gmail.com'
	                    }
	                }
	                scm {
	                    connection gitUrl
	                    developerConnection gitUrl
	                    url siteUrl
	                }
	            }
	        }
	    }
	}
	
	task sourcesJar(type: Jar) {
	    from android.sourceSets.main.java.srcDirs
	    classifier = 'sources'
	}
	task javadoc(type: Javadoc) {
	    source = android.sourceSets.main.java.srcDirs
	    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
	}
	task javadocJar(type: Jar, dependsOn: javadoc) {
	    classifier = 'javadoc'
	    from javadoc.destinationDir
	}
	artifacts {
	    archives javadocJar
	    archives sourcesJar
	}
	Properties properties = new Properties()
	properties.load(project.rootProject.file('local.properties').newDataInputStream())
	
	bintray {
	    user = properties.getProperty("bintray.user")
	    key = properties.getProperty("bintray.apikey")
	    configurations = ['archives']
	    pkg {
	        repo = "maven"
	        name = "PNEditText"	//发布到JCenter上的项目名字
	        websiteUrl = siteUrl
	        vcsUrl = gitUrl
	        licenses = ["Apache-2.0"]
	        publish = true
	    }
	}
	
	```

- 提交library文件到Bintray

	`Terminal`界面执行以下
	```java
	gradlew install
	gradlew bintrayUpload
	```

	如果显示如下你就大喊一声eureka吧！
	```java
	SUCCESSFUL
	```



现在，Bintray网页上版本区域会变化，进入Files选项卡，可以看见我们上传的library文件。


你的library在互联网上任何人都可以使用了！不过library现在只是在你自己的Maven仓库，而不是在jcenter上。如果有人想使用你的library，他必须定义仓库的url，如下：


	```java
	//Project（最外层）build.gradle文件
	allprojects {
	    repositories {
	        jcenter()
	        maven {
	            url  "http://dl.bintray.com/dodo/maven/"
	        }
	    }
	}
	
	//Module的build.gradle文件
	dependencies {
	    compile fileTree(dir: 'libs', include: ['*.jar'])
	    compile 'com.android.support:appcompat-v7:23.1.1'
	    compile 'com.uedao.android.pnedittext:library:1.0.0'
	    //compile project(':library')
	}
	```

注：上面的url可以在项目右上的地方的`SET ME UP`（有个小扳手的地方）找到。



- Add to JCenter

	在[jcenter主页](https://bintray.com/bintray/jcenter)上点击` Include My Package`按纽，或者你的package页面右下角`Linked to面板`有个按钮`Add to JCenter`，填写Comments然后Send即可。


第一次提交审核差不多10小时，在[站内信](https://bintray.com/inbox)可以看到审核通过的信息，而此时`Linked to面板`会有jcenterd的连接`Linked to (1)`。


最后可以不用引入个人仓库的url，直接使用了：

```java
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.uedao.android.pnedittext:library:1.0.0'
    //compile project(':library')
}
```
