# 【Request、Response】笔记



[toc]



Request：请求数据
Response：响应数据



## Request

### 继承体系

ServletRequest：请求对象根接口（Java提供）
↓
HttpServletRequest：对HTTP协议封装的请求对象接口（Java提供）
↓
RequestFacade：实现类（Tomcat提供）



### 处理请求数据

#### 请求数据

HTTP请求：
	请求行：请求方法、URL、协议版本
	请求头：键值对（User-Agent、Content-Type、······）
	（空行）
	请求体（POST、PUT）：表单类型、json类型、······

请求方法：
	GET：查询
	POST：新增
	PUT：修改
	DELETE：删除
	······



#### 请求行

```java
String method = req.getMethod();
String contextPath = req.getContextPath();
StringBuffer requestURL = req.getRequestURL();
String requestURI = req.getRequestURI();
String queryString = req.getQueryString();
```



#### 请求头

```java
String agent = req.getHeader("User-Agent");
String connection = req.getHeader("Connection");
···
```



#### 请求体

获取字符输入流：请求参数

```java
BufferedReader getReader();
```



获取字节输入流：字节数据（图片、文件、······）

```java
ServletInputStream getInputStream();
```



#### 示例

##### 项目文件

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
│      │                  Demo.java
│      │
│      ├─resources
│      └─webapp
│          │  post_demo.html
│          │
│          └─WEB-INF
│                  web.xml
│
└─target
```



##### pom.xml

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



##### web.xml

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <!-- Servlet类名 -->
  <servlet>
    <servlet-name>demo</servlet-name>
    <servlet-class>com.test.web.Demo</servlet-class>
  </servlet>
  <!-- Servlet访问路径 -->
  <servlet-mapping>
    <servlet-name>demo</servlet-name>
    <url-pattern>/demo</url-pattern>
  </servlet-mapping>
</web-app>
```



##### post_demo.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/project/demo" method="post">
    <input type="text" name="username"><br>
    <input type="text" name="password"><br>
    <input type="submit">
</form>
</body>
</html>
```



##### Demo.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.BufferedReader;
import java.io.IOException;

@WebServlet("/demo/")
public class Demo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getMethod();
        String contextPath = req.getContextPath();
        StringBuffer requestURL = req.getRequestURL();
        String requestURI = req.getRequestURI();
        String queryString = req.getQueryString();

        String agent = req.getHeader("User-Agent");
        String connection = req.getHeader("Connection");

        System.out.println("get");

        System.out.println(method);
        System.out.println(contextPath);
        System.out.println(requestURL);
        System.out.println(requestURI);
        System.out.println(queryString);

        System.out.println(agent);
        System.out.println(connection);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getMethod();
        String contextPath = req.getContextPath();
        StringBuffer requestURL = req.getRequestURL();
        String requestURI = req.getRequestURI();

        String agent = req.getHeader("User-Agent");
        String connection = req.getHeader("Connection");

        BufferedReader reader = req.getReader();
        String line = reader.readLine();

        System.out.println("post");

        System.out.println(method);
        System.out.println(contextPath);
        System.out.println(requestURL);
        System.out.println(requestURI);

        System.out.println(agent);
        System.out.println(connection);

        System.out.println(line);
    }
}
```



##### 运行结果

访问：

```
http://localhost:8080/project/demo?username=Tom&password=1234
```

运行结果：

```
get
GET
/project
http://localhost:8080/project/demo
/project/demo
username=Tom&password=1234
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36
keep-alive
```



访问：

```
http://localhost:8080/project/post_demo.html
```

运行结果：

```
post
POST
/project
http://localhost:8080/project/demo
/project/demo
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36
keep-alive
username=Tom&password=1234
```



#### 获取请求参数

GET方式：

```java
String getQueryString();
```

POST方式：

```java
BufferedReader getReader();
```

通用方式：

```java
Map<String, String[]> getParameterMap();
String[] getParameterValues(String name);
String getParameter(String name);
```

示例（Demo.java）：

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Map;

@WebServlet("/demo/")
public class Demo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Map<String, String[]> getParameterMap()
        Map<String, String[]> parameterMap = req.getParameterMap();
        for (String key : parameterMap.keySet()) {
            String[] values = parameterMap.get(key);
            System.out.print(key + ": ");
            for (String value : values) {
                System.out.print(value + " ");
            }
            System.out.println();
        }

        // String[] getParameterValues(String name)
        String[] values = req.getParameterValues("value");
        for (String value : values) {
            System.out.println(value);
        }

        // String getParameter(String name)
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println(username);
        System.out.println(password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



### 解决乱码问题

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 06-Request请求参数中文乱码-GET解决方案](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=104)



### 请求转发

#### web.xml

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <!-- Servlet类名 -->
  <servlet>
    <servlet-name>demo1</servlet-name>
    <servlet-class>com.test.web.Demo1</servlet-class>
  </servlet>
  <servlet>
    <servlet-name>demo2</servlet-name>
    <servlet-class>com.test.web.Demo2</servlet-class>
  </servlet>
  <!-- Servlet访问路径 -->
  <servlet-mapping>
    <servlet-name>demo1</servlet-name>
    <url-pattern>/demo1</url-pattern>
  </servlet-mapping>
  <servlet-mapping>
    <servlet-name>demo2</servlet-name>
    <url-pattern>/demo2</url-pattern>
  </servlet-mapping>
</web-app>
```



#### Demo1.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo1/")
public class Demo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Demo1");

        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println(username);
        System.out.println(password);

        req.setAttribute("message", "Hello, World!");
        req.getRequestDispatcher("/demo2/").forward(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### Demo2.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo2/")
public class Demo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Demo2");

        String username = req.getParameter("username");
        String password = req.getParameter("password");
        Object message = req.getAttribute("message");
        System.out.println(username);
        System.out.println(password);
        System.out.println(message);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### 运行结果

访问：

```
http://localhost:8080/project/demo1?username=Tom&password=1234
```

运行结果：

```
Demo1
Tom
1234
Demo2
Tom
1234
```



#### 特点总结

浏览器地址栏的路径不发生改变
只能在内部转发



## Response

### 处理响应数据

#### 响应数据

HTTP响应：
	响应行/状态行：协议版本、状态码（200、403、404、······）、状态码描述（OK、Forbidden、Not Found、······）
	响应头：键值对
	（空行）
	响应体：表单类型、json类型、图片类型（验证码）、······



#### 响应行

```java
resp.setStatus(302);
```



#### 响应头

```java
resp.setHeader("Location", "/project/demo2");
resp.setHeader("Location", "http://www.baidu.com");
```



#### 响应体

获取字符输出流：

```java
PrintWriter getWriter();
```



获取字节输出流：

```java
ServletOutputStream getOutputStream();
```



#### 简化方式

```java
sendRedirect("/project/demo2");
```



### 重定向示例

#### 示例一

Demo1.java：

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo1/")
public class Demo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Demo1");
        resp.setStatus(302);
        resp.setHeader("Location", "/project/demo2");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

Demo2.java：

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo2/")
public class Demo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Demo2");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

访问：

```
http://localhost:8080/project/demo1
```

运行结果：

```
Demo1
Demo2
```



#### 示例二

Demo.java：

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo/")
public class Demo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Demo");
        resp.setStatus(302);
        resp.setHeader("Location", "http://www.baidu.com");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



### 特点总结

浏览器地址栏的路径发生改变
可以重定向到任意资源（内部、外部）



### 字符输出流

#### 示例

Demo.java：

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/demo/")
public class Demo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        PrintWriter writer = resp.getWriter();
        writer.write("<h1>Hello, World!</h1>");
        writer.write("<h1>你好，世界！</h1>");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

访问：

```
http://localhost:8080/project/demo
```



### 字节输出流

#### 示例

pom.xml：

```xml
<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>2.6</version>
</dependency>
```



Demo.java：

```java
package com.test.web;

import org.apache.commons.io.IOUtils;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.FileInputStream;
import java.io.IOException;

@WebServlet("/demo/")
public class Demo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        FileInputStream inputStream = new FileInputStream("D://image.png");
        ServletOutputStream outputStream = resp.getOutputStream();
        IOUtils.copy(inputStream, outputStream);
        inputStream.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

