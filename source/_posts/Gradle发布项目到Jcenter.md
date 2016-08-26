title: Gradle发布项目到Jcenter

category: android

date: 2016-08-25 11:02:19

tags: [ android,gradle ]

description: Gradle 发布项目到 Maven / Jcenter

---
## Gradle发布项目到 Maven / Jcenter
自己写了一些工具类，每次用的时候都要导入一个 Module 感觉有点麻烦，就想把项目发布到 Jcenter 上，方便自己使用，同时别人也可以拉下来使用。 经过一天的采坑，终于把项目发不上去了。在这里总结一下遇到的坑。
发布项目到 Maven/Jcenter , 网上教程一大堆。但是真正到用的时候发现使用的一些插件和依赖都过时了，不能使用了。 

### 下面记录一下发布的流程吧

1. 首先注册Bintray账号,不注册账号发布到哪里去啊。[点击这里去注册](https://bintray.com/)

2. 登陆之后拿到两个参数 一个是你的用户名，一个是api key (这个在你的个人信息里面有);

3. 然后重点来了 ，先看一下我的项目结构。需要注意的三个地方我都给了标记。下面我们关注这三个文件就可以了。JLibary 就是我们要发布的库文件。![](http://jiayaguang.oss-cn-shanghai.aliyuncs.com/%E4%B8%8A%E4%BC%A0%E9%A1%B9%E7%9B%AE%E5%88%B0Jcenter.png)

4. 首先我们在项目的 build.gradle 文件中添加两个依赖

		classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.6'
    	classpath 'com.github.dcendents:android-maven-gradle-plugin：1.3'
    	
	这里注意了，在 Gradle 之前的版本确实是这样写的，但是 gradle 工具升级了之后，	这样写是不对的。>>> [可以参见这里](https://docs.gradle.org/current/userguide/plugins.html)

	按照官方模板写之后： 项目最外层的 build.gradle 文件现在就是这个样子：
		
	buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.1.3'
    }
	}

	plugins {
    id "com.jfrog.bintray" version "1.7"
    id "com.github.dcendents.android-maven" version "1.5"
	}

	allprojects {
    repositories {
        jcenter()
    }
	}

	task clean(type: Delete) {
    delete rootProject.buildDir
	}

5. 然后我们配置 Module 里面的 build.gradle ,就是第一条红线标示出来的地方。

	```
	apply plugin: 'com.android.library'
	apply plugin: 'com.github.dcendents.android-maven'
	apply plugin: 'com.jfrog.bintray'

	def siteUrl = 'https://github.com/ovwvwvo/JLibary' ****
	def gitUrl = 'https://github.com/ovwvwvo/JLibary.git' ****
	group = "cn.ovwvwvo.android" ****
	version = "0.1.0" ****

	android {
	    compileSdkVersion 23
	    buildToolsVersion "23.0.3"
	
	    resourcePrefix "****"
	
	    defaultConfig {
	        minSdkVersion 15
	        targetSdkVersion 24
	        versionCode 1
	        versionName "1.0"
	    }
	    buildTypes {
	        release {
	            minifyEnabled false
	            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
	        }
	    }
	    lintOptions {
	        abortOnError false
	    }
	}
	
	dependencies {
	    compile fileTree(dir: 'libs', include: ['*.jar'])
	    testCompile 'junit:junit:4.12'
	}
	
	install {
	    repositories.mavenInstaller {
	        // This generates POM.xml with proper parameters
	        pom {
	            project {
	                packaging 'aar'
	                name '****'
	                url siteUrl
	                licenses {
	                    license {
	                        name 'The Apache Software License, Version 2.0'
	                        url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
	                    }
	                }
	                developers {
	                    developer {
	                        id '***'
	                        name '***'
	                        email '****'
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
	//    source = android.sourceSets.main.java.srcDirs
	//    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
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
	        name = "****"
	        websiteUrl = siteUrl
	        vcsUrl = gitUrl
	        licenses = ["Apache-2.0"]
	        publish = true
	    }
	}
	```

	1. 标注 **** 的地方是需要填写的一些信息
	
	2. 注意以上代码要是提示  javadoc 字符集错误 可以添加以下代码
  
  ```
  javadoc {
	    options {
	        encoding "UTF-8"
	        charSet 'UTF-8'
	        author true
	        version true
	        links "http://docs.oracle.com/javase/7/docs/api"
	    }
	}
	```
6. 之后在项目的 local.properties 文件中（就是最后一处红线的位置），添加我们第二步注册网站是拿到的两个参数。

	```
	bintray.user = username
	bintray.apikey =api key
	```

7. 一切就绪之后，在根目录的控制台执行

	`gradle build`

	`gradle bintrayUpload`

	就可以上传了我们的JLibary

8. 然后登陆 bintray.com 就可以看到我们项目了，然后在项目里点击 add to Jcenter 按钮就可以发布到 Jcenter . 发布成功会有邮件通知你。

## 使用我们发布的项目
我们刚才发布的项目现在就可以使用了。

1. 在没有提交到 Jcenter 的时候，我们的项目是存在于 Maven 仓库的，我们可以这样引用我们的项目：

 	```
 	<dependency>
  		<groupId>cn.ovwvwvo.android</groupId>
  		<artifactId>JLibary</artifactId>
  		<version>0.1.0</version>
  		<type>pom</type>
	</dependency>
	```

  这样写着比较麻烦，我们可以写成我们经常使用的写法，像  compile '';
  首先我们在项目根目录的 build.gradle 添加
  
	```
  	allprojects {
    	repositories {
        	jcenter()
        	maven {
            	url 'https://dl.bintray.com/ovwvwvo/maven/'
        	}
    	}
  	}
	```
	其中，url 在 bintray.com/ 项目仓库页面的右上角有显示，然后我们在项目的 	build.gradle 依赖里面添加就可以了，具体格式参照上面的 <dependency>包含的内容

	`compile 'cn.ovwvwvo.android:JLibary:0.1.0' `
	
		
2. 当项目添加到 Jcenter 之后我们就直接使用 
 
 `compile 'cn.ovwvwvo.android:JLibary:0.1.0' `
 
 对项目进行引用。










 