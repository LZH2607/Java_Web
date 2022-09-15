# 【AJAX】笔记



[toc]



AJAX（Asynchronous JavaScript and XML）：异步的JavaScript和XML
	用HTML、AJAX替换JSP（主流方式）
	异步交互：不用重新加载整个页面即可与服务器交换数据并更新部分网页（如：搜索联想、用户名是否可用校验）

![](D:\Notes\Java_Web\img\AJAX.png)



## 示例

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P139 02-AJAX-快速入门](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=139)

相关网页：
[AJAX 简介 - w3school 在线教程](https://www.w3school.com.cn/js/js_ajax_intro.asp)



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
│      │              └─servlet
│      │                      AjaxDemo.java
│      │
│      ├─resources
│      └─webapp
│          │  demo.html
│          │
│          └─WEB-INF
│                  web.xml
│
└─target
```



### pom.xml

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



### AjaxDemo.java

```java
package com.test.web.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/ajax_demo")
public class AjaxDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException, IOException {
        // 响应数据
        resp.getWriter().write("Hello, World!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



### demo.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    // 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    // 发送请求
    xhttp.open("GET", "http://localhost:8080/project/ajax_demo");
    xhttp.send();
    // 获取响应
    xhttp.onreadystatechange = function () {
        if (this.readyState == 4 && this.status == 200) {
            console.log(this.responseText);
        }
    };
</script>
</body>
</html>
```



### 访问链接

```
http://localhost:8080/project/demo.html
```



### 运行结果

页面的Console：

```
Hello, World!
```



## Axios

Axios：异步框架



### 示例一

#### AxiosDemo.java

```java
package com.test.web.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/axios_demo")
public class AxiosDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException, IOException {
        // 接收请求参数
        String username = req.getParameter("username");
        System.out.println(username);
        // 响应数据
        resp.getWriter().write("Hello, World!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### demo.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script src="js/axios-0.18.0.js"></script>
<script>
    // get
    axios({
        method: "get",
        url: "http://localhost:8080/project/axios_demo?username=Tom"
    }).then(function (resp) {
        console.log(resp.data);
    })
</script>
</body>
</html>
```



#### 访问链接

```
http://localhost:8080/project/demo.html
```



#### 运行结果

```
Tom
```

页面的Console：

```
Hello, World!
```



### 示例二

#### demo.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script src="js/axios-0.18.0.js"></script>
<script>
    // post
    axios({
        method: "post",
        url: "http://localhost:8080/project/axios_demo/",
        data: "username=Tom"
    }).then(function (resp) {
        console.log(resp.data);
    })
</script>
</body>
</html>
```



#### 访问链接

```
http://localhost:8080/project/demo.html
```



#### 运行结果

```
Tom
```

页面的Console：

```
Hello, World!
```

