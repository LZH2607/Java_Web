# 【JSP】笔记



[toc]



JSP（Java Server Pages）：Java服务端页面

JSP容器（Tomcat）：JSP文件 → Java文件（Servlet） → 字节码文件



## 示例

相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P112 01-JSP概述&快速入门&原理](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=112)



### 项目文件

```
project
│  pom.xml
│  project.iml
│
├─.idea
├─src
│  ├─main
│  │  ├─java
│  │  ├─resources
│  │  └─webapp
│  │      │  demo.jsp
│  │      │
│  │      └─WEB-INF
│  │              web.xml
│  │
│  └─test
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



### demo.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>Hello, World!</h1>
<% System.out.println("Hello, World!"); %>
</body>
</html>
```



### 访问链接

```
http://localhost:8080/project/demo.jsp
```



## 演进过程

Servlet
↓
JSP
↓
Servlet + JSP
↓
Servlet + HTML + AJAX

不直接在JSP里写Java代码：**EL表达式**、**JSTL标签**
	Servlet：处理数据、封装数据
	JSP：获取数据、展示数据



## EL表达式

EL（Expression Language）表达式：
	主要功能：获取数据
	语法：${···}



### 示例

#### 项目文件

```
project
│  pom.xml
│  project.iml
│
├─.idea
├─src
│  ├─main
│  │  ├─java
│  │  │  └─com
│  │  │      └─test
│  │  │          └─web
│  │  │                  Person.java
│  │  │                  ServletDemo.java
│  │  │
│  │  ├─resources
│  │  └─webapp
│  │      │  demo.jsp
│  │      │
│  │      └─WEB-INF
│  │              web.xml
│  │
│  └─test
└─target
```



#### Person.java

```java
package com.test.web;

public class Person {
    String name;
    char gender;
    int age;

    Person(String name, char gender, int age) {
        this.name = name;
        this.gender = gender;
        this.age = age;
    }

    public String toString() {
        return "[Name: " + name + ", Gender: " + gender + ",  Age: " + age + "]";
    }
}
```



#### ServletDemo.java

```java
package com.test.web;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

@WebServlet("/demo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 准备数据
        List<Person> people = new ArrayList<Person>();
        people.add(new Person("Tom", 'M', 18));
        people.add(new Person("Linda", 'F', 19));
        people.add(new Person("Jack", 'M', 20));

        // 存储到request域
        req.setAttribute("people", people);

        // 转发到demp.jsp
        req.getRequestDispatcher("demo.jsp").forward(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



#### demo.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
${people}
</body>
</html>
```



#### 访问链接

```
http://localhost:8080/project/demo
```



#### 页面输出

```
[[Name: Tom, Gender: M, Age: 18], [Name: Linda, Gender: F, Age: 19], [Name: Jack, Gender: M, Age: 20]]
```



## 域对象

域对象：
	page：当前页面有效
	request：当前请求有效
	session：当前会话有效
	application：当前应用有效

寻找顺序：page → request → session → application



## JSTL标签

JSTL（Java Standarded Tag Library）标签



### 示例

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
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
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
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<c:forEach items="${people}" var="person">
    ${person}
</c:forEach>
</body>
</html>
```



#### 访问链接

```
http://localhost:8080/project/demo
```



#### 页面输出

```
[Name: Tom, Gender: M, Age: 18] [Name: Linda, Gender: F, Age: 19] [Name: Jack, Gender: M, Age: 20]
```

