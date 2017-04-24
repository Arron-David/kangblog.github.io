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

#### pom.xml

```xml 
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>practice</groupId>
  <artifactId>springmvc</artifactId>
  <packaging>war</packaging>
  <version>0.0.1-SNAPSHOT</version>
  <name>springmvc Maven Webapp</name>
  <url>http://maven.apache.org</url>
  
  <properties>
  	<spring.version>4.3.5.RELEASE</spring.version>
  </properties>
  
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    
    <!-- 增加servlet api解决jsp报错问题 -->
	<dependency>
	    <groupId>javax.servlet</groupId>
	    <artifactId>javax.servlet-api</artifactId>
	    <version>3.1.0</version>
	</dependency>
	
	<dependency>  
        <groupId>org.springframework</groupId>  
        <artifactId>spring-web</artifactId>  
        <version>${spring.version}</version>  
    </dependency>
    
    <dependency>  
        <groupId>org.springframework</groupId>  
        <artifactId>spring-webmvc</artifactId>  
        <version>${spring.version}</version>  
    </dependency>

  </dependencies>
  <build>
    <finalName>springmvc</finalName>
  </build>
</project>
```

#### web.xml


```xml
<?xml version="1.0" encoding="UTF-8"?>  
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee   
    http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
	<display-name>Archetype Created Web Application</display-name>
		<welcome-file-list>
		<welcome-file>index.jsp</welcome-file>
	</welcome-file-list>
  
	<listener>
		<listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>
	</listener>
  
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
  
	<servlet>
		<servlet-name>springmvc</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>/WEB-INF/applicationContext.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
  
	<servlet-mapping>
		<servlet-name>springmvc</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
</web-app>
```

#### applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"   
       xmlns:context="http://www.springframework.org/schema/context"  
       xmlns:mvc="http://www.springframework.org/schema/mvc"   
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="  
        http://www.springframework.org/schema/beans   
        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd   
        http://www.springframework.org/schema/context   
        http://www.springframework.org/schema/context/spring-context-3.0.xsd   
        http://www.springframework.org/schema/mvc   
        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd   
       ">  
  
    <mvc:annotation-driven />  
    <context:component-scan base-package="com.xuefei.springmvc" />  
  
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
        <property name="prefix" value="/" />  
        <property name="suffix" value=".jsp" />  
    </bean>  
  
</beans> 
```

#### 配置文件配置完成之后，编写一个controller测试
```java
package com.xuefei.springmvc;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

/**
 * @author Administrator
 *
 */
@Controller
public class SpringMVCController {

	@RequestMapping("/")
	public String index(){
		return "index";
	}
}
```
#### 用tomcat9部署之后，浏览器访问http://localhost:8080/springmvc/进行测试，截图如下：
<img src="/images/posts/maven-springmvc/maven-springmvc-5.png" height="219" width="511">

到此为止，一个新的springmvc工程就算搭建完成，后面会继续讲解springmvc的注解。
