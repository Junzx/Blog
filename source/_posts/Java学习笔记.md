---
title: Java学习笔记
date: 2017-8-31
tags:
	- 笔记
	- Java
description: java
---
***
##### 参考图书：21天学通Java（第六版），人民邮电出版社，[美]Rogers Cadenhead
***
#### 第一章
- 类变量（class variable）：定义类的属性，不同的实例公用这个属性
- 类方法（class method）：适用于类本身
<p>
- 三个重要概念：继承、借口、包
- 继承其他类的叫子类，被继承的叫超类
- 在子类中创建一个防止调用超类中定义的方法。为此，方法的名称、返回值和参数必须与超类方法相同，这称谓**覆盖**
- Java单继承：仅有一个超类

#### 第二章
- 变量命名法：小驼峰
- 数据类型（基本）：
  - 存储整数：byte、short、int、long
  - 浮点数：float、double
  - char、boolean
- 定义常量： 关键字：**final**。如：final float PI = 3.14；
- 输出：System.out.println("str1" + "str2");  // 在输出字符串后面回车，区别于print
- 字符串对象是Java中的真正对象
- 逻辑运算符：& 与 &&。如果用& ，不论两边式子真假，两边都会计算；如果是&&，lazy模式，若左边为true，右边则不会计算。

#### 第三章
- 参数数目和类型是区分构造函数的唯一途径
- 类变量：关键字：**static**，修改它会改变所有的实例。
- System.out.format("Test:$，d%n", data）；  // %，d是十进制数，%n是回车符
- System位于java.lang包中
- System.out 是一个类型，他存储了PrintSteam的一个实例
- 引用是一个地址，指明了对象的变量和方法的存储位置
- 将对象赋值给变量或者作为参数传递给方法的时候，使用的仅仅是对象的引用。

```
Interger dataCount = new Integer(10);
int newCount = dataCount.intValue();
// 这里，dataCount是个Integer对象
```
- 若判断对象所属于的类：

```
1. String Name = key.getClass().getName();
2. 用instanceof
boolean check2 = pt instanceof String;
```
#### 第四章
- 块语句，即{}，但是直接用并不常见
- 在块中声明的局部变量创建了作用域
- if，需要加括号
- 三目运算：test?trueresult : falseresult;
- break & continue 标号，标记要跳到哪里，P65

#### 第五章
- 指定超类：关键字：**extends**
```
class Son extends Father {
pass
}
```
- 类变量：关键字：**static**；例子：static int num；
- this：类似于python中的self
- P80 构造函数相关
- 调用超类的构造函数：super.methodname(arguments)

#### 第六章
- static：创建类方法和类变量
- final：设置常量。常与static一起使用，例如：static final String TITLE = "sss";
- final方法不能被子类覆盖。
- final类不能被继承。在final类中，所有的方法都是final的，无需再次限定。