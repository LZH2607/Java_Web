# 【Servlet】笔记



[toc]



## 概念

Servlet的生命周期：运行在容器/服务器（Tomcat）中
	加载、实例化：创建对象
	初始化：init()
	处理请求：service()
	终止服务：destory()



## 示例

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P94 11-Servlet简介&快速入门](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=94)



### 项目文件

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
│      │                  ServletDemo.java
│      │
│      ├─resources
│      └─webapp
│          │  index.jsp
│          │
│          └─WEB-INF
│                  web.xml
│
└─target
```



### pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.example</groupId>
  <artifactId>project</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>project Maven Webapp</name>
  <url>http://maven.apache.org</url>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <build>
    <finalName>project</finalName>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>6</source>
          <target>6</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```



### ServletDemo.java

```java
package com.test.web;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;

@WebServlet("/demo")
public class ServletDemo implements Servlet {
    private ServletConfig servletConfig;
    /**
     * 初始化
     * @param servletConfig
     * @throws ServletException
     */
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("init");
        this.servletConfig = servletConfig;
    }

    /**
     * 处理请求
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("service");
    }

    /**
     * 终止服务
     */
    @Override
    public void destroy() {
        System.out.println("destroy");
    }

    @Override
    public ServletConfig getServletConfig() {
        return servletConfig;
    }

    @Override
    public String getServletInfo() {
        return null;
    }
}
```



### 访问链接

```
http://localhost:8080/project/demo
```



## HttpServlet

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("get");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("post");
    }
}
```



## urlPattern配置

### 精确匹配

匹配路径：

```java
@WebServlet("/demo")
```

访问路径：

```
http://localhost:8080/project/demo
```



### 目录匹配

匹配路径：

```java
@WebServlet("/*")
```

访问路径：

```
http://localhost:8080/project/
http://localhost:8080/project/a
http://localhost:8080/project/b
···
```



### 扩展名匹配

匹配路径：

```java
@WebServlet("*.do")
```

访问路径：

```
http://localhost:8080/project/.do
http://localhost:8080/project/a.do
http://localhost:8080/project/b.do
···
```



### 任意匹配

```java
@WebServlet("/")
```

或：

```java
@WebServlet("/*")
```

访问路径：

```
http://localhost:8080/project/a
http://localhost:8080/project/b
···
```



### 匹配优先级

精确匹配 ＞ 目录匹配 ＞ 扩展名匹配 ＞ /* ＞ /



## 注解配置

### web.xml


```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <!-- Servlet类名 -->
  <servlet>
    <servlet-name>demo</servlet-name>
    <servlet-class>com.test.web.ServletDemo</servlet-class>
  </servlet>
  <!-- Servlet访问路径 -->
  <servlet-mapping>
    <servlet-name>demo</servlet-name>
    <url-pattern>/demo</url-pattern>
  </servlet-mapping>
</web-app>
```



### ServletDemo.java

```java
package com.test.web;

import javax.servlet.*;
import java.io.IOException;

public class ServletDemo implements Servlet {
    private ServletConfig servletConfig;

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("init");
        this.servletConfig = servletConfig;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("service");
    }

    @Override
    public void destroy() {
        System.out.println("destroy");
    }

    @Override
    public ServletConfig getServletConfig() {
        return servletConfig;
    }

    @Override
    public String getServletInfo() {
        return null;
    }
}
```

