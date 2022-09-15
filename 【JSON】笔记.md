# 【JSON】笔记



[toc]



JSON（JavaScript Object Notation）



## 导入依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.62</version>
</dependency>
```



## Java对象 → String

```java
import com.alibaba.fastjson.JSON;

public class Test {
    public static void main(String[] args) {
        Person p = new Person("Tom", 'M', 20);
        String s = JSON.toJSONString(p);
        System.out.println(p);
        System.out.println(s);
    }
}

class Person {
    private String name;
    private char gender;
    private int age;

    public String getName() {
        return name;
    }

    public char getGender() {
        return gender;
    }

    public int getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }

    public void setAge(int age) {
        this.age = age;
    }

    Person() {

    }

    Person(String name, char gender, int age) {
        this.name = name;
        this.gender = gender;
        this.age = age;
    }

    public String toString() {
        return "{Name: " + name + ", Gender: " + gender + ", Age: " + age + "}";
    }
}
```

运行结果：

```
{Name: Tom, Gender: M, Age: 20}
{"age":20,"gender":"M","name":"Tom"}
```



相关文章：
[使用JSON.toJSONString()返回{}的原因](https://www.it145.com/9/177064.html)



## String → Java对象

```java
import com.alibaba.fastjson.JSON;

public class Test {
    public static void main(String[] args) {
        String s = "{\"age\":20,\"gender\":\"M\",\"name\":\"Tom\"}";
        Person p = JSON.parseObject(s, Person.class);
        System.out.println(s);
        System.out.println(p);
    }
}

class Person {
    private String name;
    private char gender;
    private int age;

    public String getName() {
        return name;
    }

    public char getGender() {
        return gender;
    }

    public int getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }

    public void setAge(int age) {
        this.age = age;
    }

    Person() {
        
    }

    Person(String name, char gender, int age) {
        this.name = name;
        this.gender = gender;
        this.age = age;
    }

    public String toString() {
        return "{Name: " + name + ", Gender: " + gender + ", Age: " + age + "}";
    }
}
```

运行结果：

```
{"age":20,"gender":"M","name":"Tom"}
{Name: Tom, Gender: M, Age: 20}
```

