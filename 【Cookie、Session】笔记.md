# 【Cookie、Session】笔记



[toc]



## Cookie

Cookie：
	保存在客户端
	每次请求都携带Cookie数据

请求头：Cookie
响应头：Set-Cookie



### 发送Cookie

#### ServletDemo.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 创建Cookie
        Cookie cookie = new Cookie("username", "Tom");

        // 发送Cookie
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### 访问链接

```
http://localhost:8080/project/demo
```



### 获取Cookie

#### ServletDemo.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获取Cookie
        Cookie cookies[] = req.getCookies();

        // 遍历数组
        for (Cookie cookie : cookies) {
            String name = cookie.getName();
            String value = cookie.getValue();
            System.out.println(name + ": " + value);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### 访问链接

```
http://localhost:8080/project/demo
```



#### 运行结果

```
username: Tom
```



### setMaxAge

设置Cookie的存活时间：setMaxAge(int seconds)
	正数：到时间自动删除
	负数：当浏览器关闭时删除（默认）
	零：删除



#### 示例

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/demo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 创建Cookie
        Cookie cookie = new Cookie("username", "Tom");

        // 设置存活时间
        cookie.setMaxAge(7 * 24 * 60 * 60);

        // 发送Cookie
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### 访问链接

```
http://localhost:8080/project/demo
```



## Session

Session：
	保存在服务端
	浏览器重启后，Session改变



### 示例

#### ServletDemo1.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.*;
import java.io.IOException;

@WebServlet("/demo1")
public class ServletDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 创建Session
        HttpSession session = req.getSession();

        // 存储数据
        session.setAttribute("username", "Tom");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### ServletDemo2.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.*;
import java.io.IOException;

@WebServlet("/demo2")
public class ServletDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获取Session
        HttpSession session = req.getSession();

        // 获取数据
        Object username = session.getAttribute("username");
        System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### 访问链接

```
http://localhost:8080/project/demo1
http://localhost:8080/project/demo2
```



#### 运行结果

```
Tom
```



### 原理

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P127 05-Session原理&细节](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=127)

钝化、活化：由Tomcat完成
	钝化：将Session数据保存在文件中
	活化：从文件中加载Session数据

销毁：略



## Cookie与Session的区别

|              |      Cookie      |     Session      |
| :----------: | :--------------: | :--------------: |
|   存储位置   | 客户端（浏览器） | 服务端（服务器） |
|    安全性    |      不安全      |       安全       |
|   数据大小   |     最大3KB      |      无限制      |
|   存储时间   |        长        | 短（默认30分钟） |
| 浏览器重启后 |       不变       |       改变       |
|  服务器资源  |      不占用      |       占用       |

