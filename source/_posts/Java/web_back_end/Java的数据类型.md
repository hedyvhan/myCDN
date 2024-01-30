---
title: Java的数据类型
date: '2021-05-23 21:36'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 3637
---

# Java的数据类型

> 2021-05-23

## 一、基本类型（8个）

### 1. 数值类型（8大数据类型）

#### 1）整数类型

​		byte：1字节（-128-127）2**8

​		short：2字节

​		int：4字节

​		long：8字节

#### 2）浮点类型

​		float：4字节

​		double：8字节

#### 3）字符类型

​		char：2字节

### 2. 布尔类型

​		flase or true: 1 **位**

```Java
public class Demo2 {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 10.1; //报错, int 不能为小数
        int num3 = 100000000;

        byte num4 = 20;
        byte num5 = 128; //报错, byte最大127

        short num6 =  32767;
        short num7 =  32768; //报错,  short最大32767

        long num8 = 30L;

        float num9 = 10F;
        double num10 = 3.14159;

        char name = 'a';
        char name2 = 'ab'; //报错, char 一个字符

        //String不是关键字，是一个类
        String s1 = 'ab';  //报错, String ""
        String s2 = "ab";

        boolean flag = true;
    }
}

```

　　注意String是一个类,不是基本数据类型,基本数据类型只有八个 .

##  二、引用类型 reference

对象是通过引用来操作的，栈-->堆（地址），引用在栈中，真实的对象在堆中。

1. 类
2. 接口
3. 数组

### 三、默认值

|   类型   |      默认值      |
| :------: | :--------------: |
|   数字   |      0、0.0      |
|   char   |      u0000       |
| boolean  |      false       |
| 引用类型 | null，比如String |

