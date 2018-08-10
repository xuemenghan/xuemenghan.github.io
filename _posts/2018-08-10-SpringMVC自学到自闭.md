---
layout: post
title: "SpringMVC自学到自闭"
date: 2018/8/10 0:15:34 
image: 'https://i.imgur.com/GSNw8Bn.png'
description: 万事需坚持，需技巧，虚心请教。<br />走过需担当，需分享，助人助己。
category: 'Java'
tags:
- SpringMVC
- 解决Bug
- 经验分享
introduction: 自学SpringMVC之后的“忏悔”。
---
<div id="Article_catalogue"></div>
<h2>文章目录</h2>
* [前言](#Preface)
* [第一部分：真正手把手带你入门](#1)
    * [1.1 环境准备](#1_1)
	* [1.2 新建项目](#1_2)
	* [1.3 五件事情](#1_3)
* [第二部分：解决让人自闭的Bug](#2)
	* [2.1 发生“灵异事件”导致404](#2_1)
	* [2.2 新建项目卡死](#2_2)
	* [2.3 ClassNotFound](#2_3)
	* [2.4 web.xml中的springMVC配置文件名称](#2_4)
	* [2.5 web.xml中的url-pattern](#2_5)
	* [2.6 SpringMVC配置文件的命名空间有红叉](#2_6)
	* [2.7 SpringMVC配置自动扫描包名不一致](#2_7)
	* [2.8 SpringMVC配置jsp路径与实际不一致](#2_8)
	* [2.9 SpringMVC配置文件忘写注解驱动](#2_9)
	* [2.10 Controller类返回信息错误](#2_10)
	* [2.11 Controller注解url与实际url不一致导致404](#2_11)
	* [2.12 jsp文件名称与Controller类返回名称不一致导致404](#2_12)
	* [2.13 Tomcat端口号被占用导致无法启动](#2_13)
	* [2.14 Tomcat报context相关错误](#2_14)
	* [2.15 Tomcat运行项目无法生成.class文件导致404](#2_15)
* [第三部分：尽管走下去，不必逗留着](#3)
	* [3.1 莫愁前路无知己，天下谁人不识君](#3_1)
* [结尾](#ending)

<br />
----------
----------

<div id="Preface"><br /></div>
<h4>前言</h4>
<div id="1"></div>
&emsp;&emsp;起初是因为学习Android，我想整一个App，能够实现上传和下载的功能，然后就去网上搜资料，有人说FTP可以实现，我就去学了一下FTP，可是只实现了电脑与电脑之间的资源传递，并没有实现手机与服务器之间的传递。然后又听说SpringMVC可以实现上传与下载，接着就走上了自学SpringMVC的道路，差点自闭！好在我天资聪颖，外加勤奋刻苦，终于还是没有自闭。
&emsp;&emsp;这篇文章就来讲讲我与SpringMVC之间的爱恨情仇！
<h4>第一部分：真正手把手带你入门</h4>	
<br />
&emsp;&emsp;要做到手把手，最直接的就是上视频，但是录制一个视频，不易呈现，而且视频的资源占用特别大，所以我倾向使用截图的方式，每一步操作都有截图，每一步操作都有解释，就连xml文件中的命名空间都给你说道说道。我还写了较为详细的目录来定位文章，读者可以根据目录快速跳转到自己需要的地方。
<br />
&emsp;&emsp;[不看第一部分，直接跳转到第二部分：大标题](#2)
<div id="1_1"></div>
<h5>1.1&emsp;环境准备</h5>
&emsp;&emsp;既然你都来学习SpringMVC了（这属于JavaEE的内容），那你Java环境肯定已经搭建好了，比如说JDK、环境变量、Eclipse、MyEclipse都已经安装且配置了（这属于JavaSE的内容）。
&emsp;&emsp;JavaSE的资源我就不给你贴链接了，有需要的可以给我发邮箱联系我。这里我把SpringMVC所用的一些资源贴给你，点击下图或者链接进行下载：<br />
[百度网盘资源](https://pan.baidu.com/s/15NT9M4B8WMmeBryN2lNn0w)
[![四个资源文件.png]({{site.baseurl}}/assets/img/image/四个资源文件.png)](https://pan.baidu.com/s/15NT9M4B8WMmeBryN2lNn0w)
<h6>资源解释</h6>
&emsp;&emsp;前两个是Tomcat7和9，两个不同版本，任意挑一个，或者两个都下载，Tomcat是免安装的，解压到本地，然后Eclipse或者MyEclipse中配置一下就能使用了。Eclipse中配置Tomcat键具体步骤链接(MyEclipse同理)：[百度经验](https://jingyan.baidu.com/article/3065b3b6efa9d7becff8a4c6.html)
<br />
&emsp;&emsp;第三个文件是运行SpringMVC框架入门程序所需要的全部jar包，几乎是全部，我是从这个链接下载的：[SpringMVC使用的Jar包集合](http://repo.spring.io/release/org/springframework/spring/)但是，很不幸，这个链接是在墙外的，考虑到有些小伙伴没有梯子，我就把这些Jar包都打包一起传到百度网盘里了。
<br />
&emsp;&emsp;第四个文件是一本书，具体作用：留得青山在，不怕没柴烧。你懂的！
<div id="1_2"></div>
<h5>1.2&emsp;新建项目</h5>
&emsp;&emsp;我用的是MyEclipse具体步骤：File->new->web project(Eclipse中是Dynamic Web Project)->填写项目信息->Next->Next->Finish  如下图：<br />
![newWebProject.png]({{site.baseurl}}/assets/img/image/newWebProject.png)
![填写信息.png]({{site.baseurl}}/assets/img/image/填写信息.png)
![继续Next.png]({{site.baseurl}}/assets/img/image/继续Next.png)
![勾上web继续Next.png]({{site.baseurl}}/assets/img/image/勾上web继续Next.png)
![直接Finish.png]({{site.baseurl}}/assets/img/image/直接Finish.png)
![有时候需要断网.png]({{site.baseurl}}/assets/img/image/有时候需要断网.png)
<div id="1_3"></div>
<h5>1.3&emsp;五件事情</h5>
&emsp;&emsp;在做接下来的五件事之前，先看一眼新建项目的目录树：
![新建目录树.png]({{site.baseurl}}/assets/img/image/新建目录树.png)
&emsp;&emsp;第一件事，添加Jar包：
![buildpath.png]({{site.baseurl}}/assets/img/image/buildpath.png)
![ExternalJAR.png]({{site.baseurl}}/assets/img/image/ExternalJAR.png)
![全选JAR.png]({{site.baseurl}}/assets/img/image/全选JAR.png)
![Apply-OK.png]({{site.baseurl}}/assets/img/image/Apply-OK.png)
![添加好依赖库之后的目录树.png]({{site.baseurl}}/assets/img/image/添加好依赖库之后的目录树.png)
&emsp;&emsp;第二件事，配置web.xml（完整代码如下）：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>SpringMVCTest</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
  <!-- 前端控制器 -->
  <servlet>
  	<servlet-name>springmvc</servlet-name>
  	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  	<!-- contextConfigLocation配置SpringMVC的配置文件 -->
  	<init-param>
  		<param-name>contextConfigLocation</param-name>
  		<param-value>classpath:springmvc.xml</param-value>
  	</init-param>
  </servlet>
  <servlet-mapping>
  	<servlet-name>springmvc</servlet-name>
  	<url-pattern>/</url-pattern>
  </servlet-mapping>
  
</web-app>
```
web.xml在我项目中的截图:
![webxml文件.png]({{site.baseurl}}/assets/img/image/webxml文件.png)
&emsp;&emsp;第三件事，配置springmvc.xml（完整代码如下）：
```xml
<!-- 
底下这些命名空间以及schemaLocation的配置方式：
Windows->Preferences->XML->XML Catalog->Add->Catalog Entry->
选择Location处：FileSystem->找到路径：G:\Workspaces\JavaEE\spring-framework-4.3.1.RELEASE\schema->选择对应目录下对应版本号的 .xsd文件打开
修改Key type处：选择schemaLocation
Key处：Key是自动生成的，不用改动，类似于http://www.springframework.org/schema/tx
注意下面一大堆命名空间都在<beans>一个起始标签里，我起初忘记了敲右尖括号>，结果配了半天还是红叉！！
 -->
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:mvc="http://www.springframework.org/schema/mvc"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:tx="http://www.springframework.org/schema/tx"
xsi:schemaLocation="http://www.springframework.org/schema/beans
					http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
					http://www.springframework.org/schema/mvc
					http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
					http://www.springframework.org/schema/context
					http://www.springframework.org/schema/context/spring-context-4.3.xsd
					http://www.springframework.org/schema/aop
					http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
					http://www.springframework.org/schema/tx
					http://www.springframework.org/schema/tx/spring-tx-4.3.xsd"   >

		<!-- 配置自动扫描包 -->
		<context:component-scan base-package="springmvc.controller"></context:component-scan>

		<!-- 处理器适配器 -->
		<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter" />
		
		<!-- 处理器映射器 -->
		<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping" />
		
		<!-- 视图解析器  InternalResourceViewResolver.class源码中用到了JSTL，所以SpringMVC需要加入JSTL的jar包 -->
		<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
			<property name="viewClass"  value="org.springframework.web.servlet.view.JstlView"></property>
			<property name="prefix" value="/WEB-INF/jsp/"></property>
			<property name="suffix" value=".jsp"></property>
		</bean>
		
		<!-- 配置mvc：annotation-driven -->
		<mvc:annotation-driven></mvc:annotation-driven>	

</beans>

```
springmvc.xml在我项目中的截图:
![SpringMVC命名空间.png]({{site.baseurl}}/assets/img/image/SpringMVC命名空间.png)
![配置5个工具.png]({{site.baseurl}}/assets/img/image/配置5个工具.png)
&emsp;&emsp;第四件事，新建包，写java文件（完整代码如下）：
```java
package springmvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class TestController {
	@RequestMapping("/test")
	public String hello(){
		System.out.println("hello springMVC");
		return "success";
	}
}
```
具体步骤截图：
![根据自动扫描包建包.png]({{site.baseurl}}/assets/img/image/根据自动扫描包建包.png)
![包名.png]({{site.baseurl}}/assets/img/image/包名.png)
![建类.png]({{site.baseurl}}/assets/img/image/建类.png)
![类名随意起.png]({{site.baseurl}}/assets/img/image/类名随意起.png)
![写Controller类.png]({{site.baseurl}}/assets/img/image/写Controller类.png)
&emsp;&emsp;第五件事，写jsp文件（完整代码如下）：
```jsp
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">  
    <title>My JSP 'success.jsp' starting page</title>    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->
  </head>
  
  <body>
    success!!! <br>
  </body>
</html>

```
步骤如下图所示：
![写jsp页面.png]({{site.baseurl}}/assets/img/image/写jsp页面.png)
&emsp;&emsp;五件事做完之后就是右键项目->Run As->...,具体如下图：
![RunAs.png]({{site.baseurl}}/assets/img/image/RunAs.png)
&emsp;&emsp;接着MyEclipse会弹出一个网页，在地址栏末尾写上test，然后回车，大功告成！
![大功告成.png]({{site.baseurl}}/assets/img/image/大功告成.png)
<div id="2"></div>
<h4>第二部分：解决让人自闭的Bug</h4>
<br />
&emsp;&emsp;这一部分我会写一些在自学SpringMVC过程中遇到过的各种Bug以及我是如何解决的。在遇到数十个Bug并全部解决之后，我最后总结的经验就是，小bug问百度，疑难杂症先弄通原理，然后再一个一个文件排查，包括导入的jar包，要能清除知道自己导入了哪些jar包，这些jar包都到哪了，是一什么形式来起作用的，是.html或者是.xsd还是.class等等。
<br />
&emsp;&emsp;[不看第二部分，直接跳转到第三部分：尽管走下去，不必逗留着](#3)
<div id="2_1"></div>	
<h5>2.1&emsp;发生“灵异事件”导致404</h5>
&emsp;&emsp;404有很多种情况，有的可能是因为Jar包导入的不对，有次我的项目就发生“灵异事件”了，我新建第一个项目，一切jar包都是导入的，可以运行，等我新建第二个项目的时候，我是复制第一个项目lib下的文件，本来一个jar包是分三种的，有.jar、javadoc.jar、sources.jar：
![三种jar包.png]({{site.baseurl}}/assets/img/image/三种jar包.png)
&emsp;&emsp;可是我复制过去之后myeclipse竟然就自动给我导入了，我还欣喜，MyEclipse就是高级啊，结果我那个项目折腾了一上午无论如何也是跑不起来，我还纳闷呢，第一个项目咋就能跑起来呢？在我快要自闭的时候，我一个文件一个文件审查，连导入的jar文件也审查一遍，结果当我打开jar依赖库的时候，吓出了一身冷汗，本来只有javadoc.jar和javasource.jar这两种jar包里面是.html文件，很奇怪的是，就连单纯.jar这种jar包里面的文件也都是.html。最后我把这个依赖库删除，然后把lib目录下从上个项目里复制的jar文件删除，乖乖的从我让你下载的那四个资源中解压出来的jar包集合中复制jar文件到lib目录下，myeclipse竟然又自动给我导入了，我把它自动导入的依赖库删除，然后自己手动配置buildpath，就像第一个新建的项目一样。再次运行，这次这个Bug就解决了。.
<br />
&emsp;&emsp;除了这个灵异事件导致404之外，还有很多种情况都能导致404，我在下面有具体细分。
<div id="2_2"></div>
<h5>2.2&emsp;新建项目卡死</h5>
&emsp;&emsp;这个Bug在新建项目的时候我说过了，解决办法就是先断网，然后任务管理器强制关闭MyEclipse，再重启MyEclipse，在断网的环境下来新建项目，具体原因未知。
<div id="2_3"></div>	
<h5>2.3&emsp;ClassNotFound</h5>
&emsp;&emsp;所有的ClassNotFound原因都和jar包有关系，具体情况如下：<br />
1. jar包导入出现灵异事件，比如我上面写到的经历，不要复制已有项目的（平常情况下是可以复制的，不知道那次为啥就出事了），从我让你下载的资源文件里面复制，然后重新粘贴到lib目录下，重新配置Build path
2. jar包导入包不完整（写个SpringMVC基本入门程序用我给发的资源就绝对够了，按照我在第一部分写的步骤导入jar包，应该不会出错）
3. 只在Build path中Add External JAR，项目的WebRoot/WEB-INF/lib目录下没有jar文件（平常情况下如果在Build path中配置之后，这里没有也没关系，也是不知道为啥有时候lib下没有就会出事）
<div id="2_4"></div>	
<h5>2.4&emsp;web.xml中的springMVC配置文件名称</h5>
&emsp;&emsp;如果你再web.xml中没有写<init-param>相关内容，那么SpringMVC的配置文件名称是“ ***-servlet.xml ”，后面的-servlet是必须的，而且是小写。当然如果你配置了<init-param>相关内容，那么你自己起什么名，就叫什么名。而classpath默认是对应src目录的，当然也可以右键项目名->build path->config...->source->Add进行添加。可有时候，myeclipse只认第一个path，所以把SpringMVC配置文件放到src目录下就行。如果想新在项目根目录下建一个config文件夹来存放配置文件，也可以试试，有时候行，有时候不行。
<!--
![]({{site.baseurl}}/assets/img/image/)
-->
<div id="2_5"></div>
<h5>2.5&emsp;web.xml中的url-pattern</h5>
<div id="2_6"></div>
<h5>2.6&emsp;SpringMVC配置文件的命名空间有红叉</h5>
<div id="2_7"></div>
<h5>2.7&emsp;SpringMVC配置自动扫描包名不一致</h5>
<div id="2_8"></div>
<h5>2.8&emsp;SpringMVC配置jsp路径与实际不一致</h5>
<div id="2_9"></div>
<h5>2.9&emsp;SpringMVC配置文件忘写注解驱动</h5>
<div id="2_10"></div>
<h5>2.10&emsp;Controller类返回信息错误</h5>
<div id="2_11"></div>
<h5>2.11&emsp;Controller注解url与实际url不一致导致404</h5>
<div id="2_12"></div>
<h5>2.12&emsp;jsp文件名称与Controller类返回名称不一致导致404</h5>
<div id="2_13"></div>
<h5>2.13&emsp;Tomcat端口号被占用导致无法启动</h5>
<div id="2_14"></div>
<h5>2.14&emsp;Tomcat报context相关错误</h5>
<div id="2_15"></div>
<h5>2.15&emsp;Tomcat运行项目无法生成.class文件导致404</h5>
<div id="3"></div>	
<h4>第三部分：尽管走下去，不必逗留着</h4>
&emsp;&emsp;如果这篇博客没有第三部分，那这就是一片垃圾文章！
<br />
emsp;&emsp;分享一句话：<br />
emsp;&emsp;尽管走下去，不必逗留着，去采鲜花来保存，因为在这一路上，花自然会继续开放。----泰戈尔
<br />
<div id="3_1"></div>	
<h5>3.1&emsp;莫愁前路无知己，天下谁人不识君</h5>




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
0. [阮一峰的博客](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
1. [廖雪峰的官方网站](https://www.liaoxuefeng.com/)
2. [美美王子的博客园](https://www.cnblogs.com/yehui-mmd/p/6286271.html)
3. [廖柯宇的GitHub主题](https://github.com/kaeyleo/jekyll-theme-H2O)
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