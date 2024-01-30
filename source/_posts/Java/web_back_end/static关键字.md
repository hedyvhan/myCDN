---
title: static关键字
date: '2023-12-18 20:40'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 53677
---
<meta name="referrer" content="no-referrer" />

# static关键字

## static关键字

静态变量多个类共享，在多线程中会更多的使用

静态变量通过类可以访问，比如以下Student.age，也叫类变量。

```java
public class Student{
    private static int age;  // 非静态变量
    private double score; // 静态变量
    
    public static void main (String[] args){
        Student s1 = new Student;
        System.out.println(Student.age);
        System.out.println(Student.score);  // 无法调用      
        System.out.println(s1.age);
        System.out.println(s1.score); 
    }
}
```

静态变量、方法在类创建时一起加载（类的加载机制），因此可以在飞静态方法中调用静态方法，反之不可以。

## 静态代码块

可以定义一些初始化设置。

静态代码块、匿名代码块、构造器三者，注意看加载顺序

![image](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202312192142106.webp)

并且，静态代码块只执行一次。