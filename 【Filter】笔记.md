# 【Filter、Listener】笔记



[toc]



Java Web三大组件：Servlet、Filter、Listener



## Filter

Filter：过滤器
	完成操作：权限控制、编码处理、字符处理、······



### 示例

#### 项目文件

```
project
│  pom.xml
│
├─.idea
├─src
│  └─main
│      ├─java
│      │  └─com
│      │      └─test
│      │          └─web
│      │              └─filter
│      │                      FilterDemo.java
│      │
│      ├─resources
│      └─webapp
│          │  demo.jsp
│          │
│          └─WEB-INF
│                  web.xml
│
└─target
```



#### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>project</artifactId>
  <version>1.0-SNAPSHOT</version>

  <packaging>war</packaging>

  <properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
      </plugin>
    </plugins>
  </build>

</project>
```



#### demo.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>Hello, World!</h1>
<% System.out.println(2); %>
</body>
</html>
```



#### FilterDemo.java

```java
package com.test.web.filter;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

@WebFilter("/*")
public class FilterDemo implements Filter {
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain filterChain) throws IOException, ServletException {
        // 放行前逻辑（一般为处理request数据）
        System.out.println(1);

        // 放行
        filterChain.doFilter(request, response);

        // 放行后逻辑（一般为处理response数据）
        System.out.println(3);
    }

    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void destroy() {

    }
}
```



#### 访问链接

```
http://localhost:8080/project/demo.jsp
```



#### 运行结果

```
1
2
3
```



#### Filter的执行流程

执行：放行前逻辑
↓
放行
↓
访问资源
↓
执行：放行后逻辑



### 过滤器链

略



## Listener

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P137 04-Listener](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=137)

Listener：监听器
	在application、session、request创建、销毁、添加/修改/删除属性时 → 自动执行代码

Listener：8个监听器
	监听ServletContext：
		ServletContextListener：监听ServletContext（创建、销毁）
		ServletContextAttributeListener：监听ServletContext的属性（增、删、改）
	监听Session：
		HttpSessionListener：监听Session（创建、销毁）
		HttpSessionAttributeListener：监听Session的属性（增、删、改）
		HttpSessionBindingListener：监听Session的绑定、解除
		HttpSessionActivationListener：监听Session的钝化、活化
	监听Request：
		ServletRequestListener：监听Request（创建、销毁）
		ServletRequestAttributeListener：监听Request的属性（增、删、改）



### 示例

略

