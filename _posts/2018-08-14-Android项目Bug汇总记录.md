---
layout: post
title: "Android项目Bug汇总记录"
date: 2018/8/14 12:02:22 
image: 'https://i.imgur.com/xroiTH7.png'
description: 业精于勤，荒于嬉；<br />行成于思，毁于随。
category: 'Android'
tags:
- Android
- 解决Bug
- 持续更新
introduction: 让Android天下没有解决不了的Bug
---
<div id="Article_catalogue"></div>
<h2>文章目录</h2>
* [前言](#Preface)
* [第一部分：搭建环境（打开项目）](#1)
    * [1.1 AndroidStudio版本](#1_1)
	* [1.2 Gradle自身](#1_2)
	* [1.3 Gradle依赖](#1_3)
	* [1.4 SDK版本](#1_4)
	* [1.5 JDK版本](#1_5)
* [第二部分：编写项目](#2)
	* [2.1 小标题](#2_1)
	* [2.2 小标题](#2_2)
	* [2.3 小标题](#2_3)
	* [2.4 小标题](#2_4)
* [第三部分：运行项目](#3)
	* [3.1 小标题](#3_1)
* [结尾](#ending)

<br />
----------
----------

<div id="Preface"><br /></div>
<h4>前言</h4>
<div id="1"></div>
<h4>第一部分：搭建环境（打开项目）</h4>	
<br />
&emsp;&emsp;这里写可以写一下对接下来的第一部分要写东西的概述。
<br />
&emsp;&emsp;[不看第一部分，直接跳转到第二部分：大标题](#2)
<div id="1_1"></div>
<h5>1.1&emsp;AndroidStudio版本</h5>
[预览版本下载地址](https://developer.android.com/studio/preview/?utm_source=android-studio)
<br />
[稳定版本下载地址](https://developer.android.com/studio/)
<div id="1_2"></div>
<h5>1.2&emsp;Gradle自身</h5>
![Gradle相关配置](https://i.imgur.com/WMpkam8.png)
<br />
&emsp;&emsp;上图是AndroidStudio打开一个项目后的Gradle Script，我圈出了4个文件，对于Gradle Script，只需要了解这四个文件就可以解决99%的问题了。
<br />&emsp;&emsp;Gradle自身的文件是根据上图的第三个红色圈圈的文件进行远程下载的,下面贴一下我的这个文件
```xml
#Tue Aug 14 11:42:13 CST 2018
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-4.9-all.zip

```
可以看到在文件的最后一行末尾是可以看出来远程gradle的版本号的，如果本地没有这个版本的gradle文件，那么AndroidStudio就会自动下载。
<br />&emsp;&emsp;Gradle自身的文件在本地存放的路径为：
<br />&emsp;&emsp;C:\Users\acer\.gradle\wrapper\dists
<br />&emsp;&emsp;其中第三层的acer是我电脑主机的名字。
<br />&emsp;&emsp;我使用Gradle从4.4到4.6到2018-08-14的4.9，版本一直在不断的更新，每更新一次都需要下载一次。![Gradle版本号.png](https://i.imgur.com/h6qsU0y.png)&emsp;&emsp;有时候由于某某防火墙存在的原因，导致下载一半之后下载失败，然而AndroidStudio不会断点续传或者自动本地删除重新下载，所以需要手动到本地进行删除，让后重新下载(记得搬梯子，否则还是下载失败)，例如我的Gradle本地位置为：<br />
C:\Users\acer\.gradle\wrapper\dists
<div id="1_3"></div>
<h5>1.3&emsp;Gradle依赖</h5>
![Gradle相关配置](https://i.imgur.com/WMpkam8.png)
&emsp;&emsp;再来看这个图，第一个红圈圈的文件里面内容如下：
```xml
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.3.0-alpha05'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://jitpack.io" }
    }
}
task clean(type: Delete) {
    delete rootProject.buildDir
}
```
&emsp;&emsp;在中间有一个dependencies，花括号面有一个classpath，最后面有build:gradle的版本号。build:gradle文件在本地存放的路径为：
<br />&emsp;&emsp;C:\Users\acer\.gradle\caches\modules-2\files-2.1\com.android.tools.build\gradle
<br />&emsp;&emsp;其中第三层的acer是我电脑主机的名字。
其中的道理通Gradle一样，都是由于某某防火墙存在导致下载半截失败无法而又无法重新下载的问题，解决方法类似。
<br />&emsp;&emsp;图片中第二个红色圈圈里面有项目的外部依赖，由于我现在是暑假，一直没有实践Android项目，这里先不写，等到搞Android的时候遇到Bug了再来补充。
<div id="1_4"></div>
<h5>1.4&emsp;SDK版本</h5>
<div id="1_5"></div>
<h5>1.5&emsp;JDK版本</h5>
<div id="2"></div>
<h4>第二部分：编写项目</h4>
<br />
&emsp;&emsp;这里写可以写一下对接下来的第二部分要写东西的概述。
<br />
&emsp;&emsp;[不看第二部分，直接跳转到第三部分：大标题](#3)
<div id="2_1"></div>	
<h5>2.1&emsp;小标题</h5>
<div id="2_2"></div>
<h5>2.2&emsp;小标题</h5>
<div id="2_3"></div>	
<h5>2.3&emsp;小标题</h5>
<div id="2_4"></div>	
<h5>2.4&emsp;小标题</h5>
<div id="3"></div>	
<h4>第三部分：运行项目</h4>
&emsp;&emsp;如果这篇博客没有第三部分，那这就是一片垃圾文章！
<br />
&emsp;&emsp;这里写可以写一下对接下来的第三部分要写东西的概述。
<br />
<div id="3_1"></div>	
<h5>3.1&emsp;扩展功能</h5>
<br />
<div id="ending"></div>
<h4>结尾</h4>
<br />
[正文结束，回到目录看一眼](#Article_catalogue)
<br />
<br />
<br />
<br />
这里列出一些曾经帮助过我的文章，表示感谢（排名不分先后）：
0. [T_yoo_csdn的博客](https://blog.csdn.net/T_yoo_csdn/article/details/80016601)
1. [廖雪峰的官方网站](https://www.liaoxuefeng.com/)
2.  
3.  
4. 还有一些没有记录的CSDN博客和简书、知乎等人的文章。
<br />
<br />
<br />
----------
----------
<br />
**万事需坚持，需技巧，虚心请教。<br />走过需担当，需分享，助人助己。**
<br />
----------
----------
<br />
<br />
<br />