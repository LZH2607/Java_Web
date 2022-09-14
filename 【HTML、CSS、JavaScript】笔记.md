# 【HTML、CSS、JavaScript】笔记



[toc]



相关链接：
[w3school 在线教程](https://www.w3school.com.cn/)



W3C标准：
	结构：HTML
	表现：CSS
	行为：JavaScript



## HTML

HTML（HyperText Markup Language）：超文本标记语言
	不区分大小写



### 结构标签

|       |      标签       |
| :---: | :-------------: |
| html  |  <html></html>  |
| head  |  <head></head>  |
| meta  |     <meta>      |
| title | <title></title> |
| body  |  <body></body>  |



### 基础标签

|            |       标签        |
| :--------: | :---------------: |
|     h1     |     <h1></h1>     |
|     h2     |     <h2></h2>     |
|     h3     |     <h3></h3>     |
|     h4     |     <h4></h4>     |
|     h5     |     <h5></h5>     |
|     h6     |     <h6></h6>     |
|  ~~font~~  |   <font></font>   |
|     b      |      <b></b>      |
|     i      |      <i></i>      |
|     u      |      <u></u>      |
| ~~center~~ | <center></center> |
|     p      |      <p></p>      |
|     br     |       \<br>       |
|     hr     |       <hr>        |



### 转义字符

| 转义字符 | 显示结果 |
| :------: | :------: |
|  \&lt;   |   &lt;   |
|  \&gt;   |   &gt;   |
|  \&amp;  |  &amp;   |
| \&quot;  |  &quot;  |
|  \&reg;  |  &reg;   |
| \&copy;  |  &copy;  |
| \&trade; | &trade;  |
| \&nbsp;  |  &nbsp;  |



### 图片、音频、视频标签

|       |      标签       |
| :---: | :-------------: |
|  img  |      <img>      |
| audio | <audio></audio> |
| video | <video></video> |



### 超链接标签

|      |  标签   |
| :--: | :-----: |
|  a   | <a></a> |



### 列表标签

|      |   标签    |
| :--: | :-------: |
|  ol  | <ol></ol> |
|  ul  | <ul></ul> |
|  li  | <li></li> |



### 表格标签

|       |      标签       |
| :---: | :-------------: |
| table | <table></table> |
|  tr   |    <tr></tr>    |
|  th   |    <th></th>    |
|  td   |    <td></td>    |



### 布局标签

|      |     标签      |
| :--: | :-----------: |
| div  |  <div></div>  |
| span | <span></span> |



### 表单标签

|          |         标签          |
| :------: | :-------------------: |
|   form   |     <form></form>     |
|  label   |    <label></label>    |
|  input   |        <input>        |
|  select  |   <select></select>   |
|  option  |   <option></option>   |
| textarea | <textarea></textarea> |

form标签的method属性：
	get（默认）：参数在URL中（长度有限制）
	post：参数在HTTP请求体中（长度无限制）

input标签的type属性：
	text（默认值）：文本
	password：密码
	radio：单选框
	checkbox：复选框
	file：上传文件
	hidden：隐藏文本（非用户输入）
	submit：提交按钮
	reset：重置按钮
	button：可点击按钮



### 示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>
<h1>h1</h1>
<h2>h2</h2>
<h3>h3</h3>
<h4>h4</h4>
<h5>h5</h5>
<h6>h6</h6>
<font face="Times" size="10" color="#ff0000">font</font>
<b>b</b>
<i>i</i>
<u>u</u>
<center>center</center>
<p>p</p>
<br>
<hr>
<img src="">
<audio src="" controls></audio>
<video src="" controls></video>
<a href="https://www.google.com/" target="_blank">a</a>
<ol>
    <li>li</li>
    <li>li</li>
    <li>li</li>
</ol>
<ul>
    <li>li</li>
    <li>li</li>
    <li>li</li>
</ul>
<table>
    <tr align="center">
        <th>th1</th>
        <th>th2</th>
        <th>th3</th>
        <th>th4</th>
    </tr>
    <tr align="center">
        <td>td1</td>
        <td>td2</td>
        <td>td3</td>
        <td>td4</td>
    </tr>
    <tr align="center">
        <td>td5</td>
        <td>td6</td>
        <td>td7</td>
        <td>td8</td>
    </tr>
</table>
<div>div</div>
<span>span</span>
<form action="" method="post">
    <label for="username">Name: </label><input type="text" name="username" id="username"><br>
    <label for="password">Password: </label><input type="password" name="password" id="password"><br>
    Gender: <input type="radio" name="gender" value="1" id="male"><label for="male">Male</label>
    <input type="radio" name="gender" value="2" id="female"><label for="female">Female</label><br>
    Hobby: <input type="checkbox" name="hobby" value="1" id="coding"><label for="coding">Coding</label>
    <input type="checkbox" name="hobby" value="2" id="reading"><label for="reading">Reading</label>
    <input type="checkbox" name="hobby" value="3" id="thinking"><label for="thinking">Thinking</label><br>
    Profile: <input type="file"><br>
    City: <select name="city">
    <option value="1">Beijing</option>
    <option value="2">Shanghai</option>
    <option value="3">Guangzhou</option>
    <option value="4">Shenzhen</option>
</select><br>
    Description: <textarea name="description"></textarea><br>
    <input type="reset" value="Reset">
    <input type="submit" value="Submit">
    <input type="button" value="Button">
</form>
</body>
</html>
```



## CSS

CSS（Cascading Style Sheet）：层叠样式表



### 导入方式

#### 内联样式

```html
<div style="color:red">div</div>
```



#### 内部样式

<style></style>

```html
<style>
    div{color:red;}
</style>
```



#### 外部样式

<link>

```html
<link href="../css/demo.css" rel="stylesheet">
```

demo.css：

```css
div{color:red;}
```



### 选择器

#### 元素选择器

```css
div{color:red;}
```

```html
<div>div</div>
```



#### id选择器

```css
#i{color:red}
```

```html
<div id="i">div</div>
```



#### 类选择器

```css
.c{color:red}
```

```html
<div class="c">div</div>
```



## JavaScript

ECMA标准
ECMAScript6（ES6）：2015年



### 引入方式

#### 内部脚本

<script></script>

```html
<script>
    alert("Hello, World!");
</script>
```



#### 外部脚本

<script></script>

```html
<script src="../js/demo.js"></script>
```

demo.js：

```javascript
alert("Hello, World!");
```



### 语法

区分大小写

结尾的分号可省略

注释：
	单行注释：//
	多行注释：/**/

弱类型语言



#### 输出

写入提示框：

```javascript
window.alert("Hello, World!");
```

写入HTML：

```javascript
document.write("Hello, World!");
```

写入控制台：

```javascript
console.log("Hello, World!");
```



#### 变量

全部变量：

```javascript
var v = 1;
console.log(v);
v = "Hello, World!";
console.log(v);
var v = true;
console.log(v);
```

运行结果：

```
1
Hello, World!
true
```



局部变量（ES6）：

```javascript
let l = 1;
console.log(l);
```

运行结果：

```
1
```



常量（ES6）：

```javascript
const c = 1
console.log(c);
```

运行结果：

```
1
```



#### 数据类型

数据类型：
	原始类型：
		number：数字（整数、小数、NaN）
		string：字符、字符串
		boolean：布尔（true、false）
		null：对象为空
		undefined：变量未初始化的默认值
	引用类型

获取数据类型：typeof

```javascript
var v1 = 1;
var v2 = "a";
var v3 = true;
var v4 = null;
var v5;
console.log(typeof(v1));
console.log(typeof(v2));
console.log(typeof(v3));
console.log(typeof(v4));
console.log(typeof(v5));
```

运行结果：

```
number
string
boolean
object
undefined
```



#### 数据类型转换

string → number：
	"" → 0
	只有数字 → number
	有非数字 → NaN

boolean → number：
	true → 1
	false → 0

| → boolean | false  | true |
| :-------: | :----: | :--: |
|  number   | 0、NaN | 其他 |
|  string   |   ""   | 其他 |
|   null    |   √    |      |
| undefined |   √    |      |



#### 运算符

等值判断：==（先类型转换后比较）

```javascript
var v1 = 1;
var v2 = "1";
console.log(v1 == v2);
```

运行结果：

```
true
```



全等于：===

```javascript
var v1 = 1;
var v2 = "1";
console.log(v1 === v2);
```

运行结果：

```
false
```



#### 控制语句

if
switch
for
while
do-while



#### 函数

方式一：

```javascript
function add(a, b) {
    return a + b;
}
var v1 = 1;
var v2 = 2;
var v3 = add(v1, v2);
console.log(v3);
```

运行结果：

```
3
```



方式二：

```javascript
var add = function (a, b) {
    return a + b;
}
var v1 = 1;
var v2 = 2;
var v3 = add(v1, v2);
console.log(v3);
```

运行结果：

```
3
```



#### 对象

对象：
	JavaScript对象：Array、String、RegExp、·····
	Browser对象（BOM）：Window、Navigator、Screen、History、Location
	HTML DOM对象



#### Array

方式一：

```javascript
var v = new Array(0, 1, 2, 3);
console.log(v);
```

运行结果：

```
(4) [0, 1, 2, 3]
```



方式二：

```javascript
var v = [0, 1, 2, 3];
console.log(v);
```

运行结果：

```
(4) [0, 1, 2, 3]
```



访问：

```javascript
var v = [0, 1, 2, 3];
console.log(v[0]);
console.log(v[1]);
console.log(v[2]);
console.log(v[3]);
```

运行结果：

```
0
1
2
3
```



```javascript
var v = [0, 1, 2, 3];
v[5] = true;
v[10] = "Hello, World!";
console.log(v);
```

运行结果：

```
(11) [0, 1, 2, 3, empty, true, empty × 4, 'Hello, World!']
```



```javascript
var v = [0, 1, 2, 3];
console.log(v.length);
```

运行结果：

```
4
```



#### String

方式一：

```javascript
var v = new String("Hello, World!");
console.log(v);
```

运行结果：

```
String {'Hello, World!'}
```



方式二：

```javascript
var v = "Hello, World!";
console.log(v);
```

运行结果：

```
Hello, World!
```



```javascript
var v = "Hello, World!";
console.log(v.length);
```

运行结果：

```
13
```



#### 自定义对象

```javascript
var person = {
    name: "Tom",
    age: 20,
    hello: function() {
        console.log("Hello!");
    }
}
person.hello();
console.log(person.name);
console.log(person.age);
console.log(person);
```

运行结果：

```
Hello!
Tom
20
{name: 'Tom', age: 20, hello: ƒ}
```



### BOM

BOM（Browser Object Model）：浏览器对象模型

Window：
	属性：History、Navigator、Screen、Location
	方法：alert、confirm、setInterval、setTimeout

```javascript
window.alert("alert");

var v = window.confirm("confirm");
console.log(v);

window.setTimeout(function () {
    console.log("timeout");
}, 1000);

window.setInterval(function () {
    console.log("interval");
}, 1000);
```



### DOM

DOM（Document Object Model）：文档对象模型
	核心DOM：任何结构化文档的标准模型
		Document：文档对象
		Element：元素对象
		Attribute：属性对象
		Text：文本对象
		Comment：注释对象
	XML DOM：XML文档的标准模型
	HTML DOM：HTML文档的标准模型
		Image：<img>
		Button：<input type="button">

JavaScript：通过DOM对HTML进行操作

略



### 事件监听

方法一：通过HTML标签绑定

```html
<input type="button" onclick="onclick()" value="button">
```

```javascript
function onclick() {
    window.alert("alert");
}
```



方法二：通过DOM元素属性绑定

```html
<input type="button" id="btn" value="button">
```

```javascript
document.getElementById("btn").onclick = function () {
    window.alert("alert");
}
```

