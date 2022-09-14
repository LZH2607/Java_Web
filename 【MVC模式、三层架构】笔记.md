# 【MVC模式、三层架构】笔记



[toc]



相关视频：
[黑马程序员最新版JavaWeb基础教程，Java web从入门到企业实战完整版 P117 06-MVC模式和三层架构](https://www.bilibili.com/video/BV1Qf4y1T7Hx?p=117)



## MVC模式

MVC模式：
	M（Model）：业务模型 → 处理业务
	V（View）：视图 → 展示界面
	C（Controller）：控制器 → 处理请求、调用模型、调用视图

![](D:\Notes\Front-end\img\MVC模式.png)



## 三层架构

三层架构：
	表现层：接收请求、封装数据、调用业务逻辑层、响应数据
	业务逻辑层：对业务逻辑进行操作
	数据访问层 / 持久层：对数据库进行CRUD操作

![](D:\Notes\Front-end\img\三层架构.png)

|  三层架构  |      包名称      |  主流框架  |
| :--------: | :--------------: | :--------: |
|   表现层   | web / controller | Spring MVC |
| 业务逻辑层 |     service      |   Spring   |
| 数据访问层 |   dao / mapper   |  MyBatis   |

三大框架：SSM（Spring MVC、Spring、MyBatis）



## MVC模式与三层架构

![](D:\Notes\Front-end\img\MVC模式与三层架构.png)
