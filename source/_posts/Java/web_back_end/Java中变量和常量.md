---
title: Java中变量和常量
date: '2021-05-23 21:36'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 53671
---

# Java中变量和常量

- 每个变量必需有类型,可以是基本类型,也可以是引用类型
- 必需是合法的标识符
- 分号结束

## 一、变量的作用域

### 1. 类变量：

类里定义的变量，相当于全局变量

### 2. 实例变量：

需要实例化才能使用

### 3. 局部变量：

方法里面定义、使用的变量

```java
//变量：类变量、实例变量、局部变量
public class demo3 {

    //3. 类变量  static, 从属于类
    //相当于 全局变量
    //可以直接使用
    static double salary = 1000;

    //1. 实例变量,从属于对象
    //实例化才能使用
    // 可以不初始化,是这个类型的默认值
    String name;
    int age ;
    boolen flag;

    public static void main(String[] args) {
        //2. 局部变量：必须声明和初始化，直接使用
        //作用范围: 在函数里面声明、在函数里面使用。
        int i = 10;
        System.out.println(i);

        //实例变量的使用,需要先实例化再使用
        demo3 TOM = new demo3();
        System.out.println(TOM.age);//0,int的默认值
        System.out.println(TOM.name);//null,string的默认值
        System.out.println(TOM.flag);//FALSE,布尔值的默认值
        
        //所有的类型默认值是0或者0.0
        //布尔值默认为FALSE
        //除了基本类型，其余的默认为null
        
    }
    
}

```

## 二、常量

使用大写，修饰符不区分顺序。

```java
//常量：
//final ，变量名一般使用大写字母
public class demo4 {
    static final double PI_1 = 3.14;
    final static double PI_2 = 3.1415;
    //类型前面的 final static 都为修饰符，不区分顺序
    public static void main(String[] args) {
        System.out.println(PI_1);
        System.out.println(PI_2);
    }
}

```

## 三、变量命名规范：

- 所有变量、方法、类名：见名知意。
- 类成员变量：首字母小写和驼峰原则，例如：lastName。
- 局部变量：首字母小写和驼峰原则。
- 常量：全部大写字母和下划线：MAX_VALUE。
- 类名：首字母大写和驼峰原则。GoodMan。
- 方法名：首字母小写和驼峰原则