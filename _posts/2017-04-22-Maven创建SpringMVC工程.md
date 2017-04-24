---
layout: post 
title: "Maven创建SpringMVC项目" 
date: 2017-04-22 
description: "Maven创建SpringMVC项目" 
tag: Maven SpringMVC 
---

#### 创建新的maven工程

<img src="/images/posts/maven-springmvc/maven-springmvc-1.png" height="494" width="513"> 

#### 选择项目目录（默认使用Eclipse的目录）

<img src="/images/posts/maven-springmvc/maven-springmvc-2.png" height="582" width="641"> 

#### 搭建web工程，选择maven-archetype-webapp类型

<img src="/images/posts/maven-springmvc/maven-springmvc-3.png" height="582" width="641">

#### 填入mavne工程相关信息,点击“Finish”按钮

<img src="/images/posts/maven-springmvc/maven-springmvc-4.png" height="579" width="734">

#### 生成的工程目录如下

<img src="/images/posts/maven-springmvc/maven-springmvc-5.png" height="355" width="895">
可以看到生成的index.jsp出现异常，异常信息为<span style='color:red'>The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build path</span>.导致这个问题的原因是因为，没有引入servlet-api的包，后续会在pom.xml中添加。

