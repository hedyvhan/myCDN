---
title: Java数据类型中常见的类型（面试笔试容易考）
date: ' 2021-05-23 21:36'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 8073
---



# Java数据类型中常见的类型（面试笔试容易考）

> 2021-05-23

# 1. 各个类型的简单使用

```java
public class Demo1 {
    public static void main(String[] args) {
        //整数扩展：进制
        
        //二进制0b
        //十进制
        //八进制0
        //十六进制0x
        int i = 10;
        int i2 = 010;//八进制
        int i3 = 0x10;//十六进制
        System.out.println(i); // 10 
        System.out.println(i2); //8 
        System.out.println(i3); //16

        System.out.println("****************************");
        //浮点数扩展,银行业务使用BigDecimal数学工具类
        
        // float	有限,离散,舍入误差,接近但不等于
        // double
        float f = 0.1f;  // 0.1
        double d = 1.0/10; // 0.1
        
        System.out.println(f); // 0.1
        System.out.println(d); // 0.1
        System.out.println(f==d); //false 
        //为什么?
        
        System.out.println("****************************");
        
        float d1 = 12312312123f;
        float d2 = d1 + 1;
        float d3 = 123f;
        float d4 = d3 + 1 ;
        System.out.println(d1 == d2 ); // true
        // 为什么?
        
        System.out.println(d3 == d4 );//false
        
 
        //最好完全避免使用浮点数进行比较
        //最好完全避免使用浮点数进行比较
        //最好完全避免使用浮点数进行比较

        
        
        System.out.println("****************************");

        
        
        
        //字符扩展
        char c1 = 'a';
        char c2 = '中';
        System.out.println(c1);
        System.out.println(c2);
        System.out.println((int)c1); // 强制转换为int
        System.out.println((int)c2);
        // 所有的字符本质都是数字
        // unicode 编码  2字节 0-65536

        System.out.println("****************************");

        String sa = new String("hello world");
        String sb = new String("hello world");
        System.out.println(sa == sb ); // false

        String sc = "hello world";
        String sd = "hello world";
        System.out.println(sc == sd ); // true
        // 从内存分析

        // 布尔值扩展
        boolean flag = true;
        if (flag == true){}
        if (flag){}
        //一个意思
    }
}


```

# 2. 类型转换问题

低------------------------------------------------------------>高 ( 小数的优先级大于整数 )

byte, short, char  -->  int -->  long -->  float -->  double

| 强制转换: 高-->低 | 自动转换: 低-->高 |
| ----------------- | ----------------- |

但不能对bool进行转换

- 精度问题

- 溢出问题

```java
public class demo2 {
    public static void main(String[] args) {
        // 强制类型转换  高----低
        // 自动类型转换  低----高


        // 高----低： int----byte
        int i = 128;
        byte b = (byte)i; // 强制转换
       
        //将int强制转换为byte，但是byte：0-127,补码
        System.out.println(i); // 128
        System.out.println(b); // 最大值127,一般转换避免内存溢出


        //低----高：int----double
        double d = i;
        System.out.println(d);

        //精度问题
        System.out.println("********************");
        System.out.println((int)23.7);
        System.out.println((int)-45.86f);

        //溢出问题
        System.out.println("********************");
        int money = 10_0000_0000;
        int years  =  20;
        int total = money*years; // -1474836480 已经溢出
        System.out.println(total);

        long total2 = money*years; //money和years都是int，默认total2也是int，相当于计算结果默认为int，再转化为long
        System.out.println(total2);

        long total3 = money*(long)years; // 解决办法:计算前先解决精度,再计算
        System.out.println(total3);


    }
}

```

