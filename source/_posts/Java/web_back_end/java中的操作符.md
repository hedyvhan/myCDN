---
title: Java中的操作符
date: '2021-05-24 10:14'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 53673
---
<meta name="referrer" content="no-referrer" />

# Java中的操作符

## 一、基础操作符

注意除法，要想得到正确的结果，需要进行类型转换。

```java
package operator;

public class Demo1 {
    public static void main(String[] args) {
        int a =10;
        int b =20;
        int c =25;
        int d =25;
        System.out.println(a+b);
        System.out.println(a-b);
        System.out.println(a*b);
        System.out.println(a/b);//0
        System.out.println((double)a/b);//0.5
        System.out.println(a/(double)b);//0.5
    }
}

```

不同的数据类型相加，结果的数据类型为混合类型中最高类型

```java
package operator;

public class Demo2 {
    public static void main(String[] args) {
        long a = 121413125432532L;
        int b = 123;
        short c = 10;
        byte d = 8;
        System.out.println(a+b+c+d);//long
        System.out.println(b+c+d);//int
        System.out.println(c+d);//int
        //有一个为long，加起来结果就为long
        //没有long，无论有没有int，比如c+d，结果还是为int
        //自动转为混合类型中的最高类型
    }
}

```



## 二、++，-- ！！！

- b=++a：先自加，后赋值。
- c=a++：先赋值，再自加。

```java
package operator;
public class Demo3 {
    public static void main(String[] args) {
        // ++  -- 运算符
        int a = 5;
        int b = a++;//先 b=a ，再a=a+1。此时a=6，b=5

        System.out.println(a);
        System.out.println(b);

        int c = ++a ;//先 a=a+1,再 c=a。此时a=7，c=7

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);


        //幂运算
        double pow = Math.pow(2, 3);
        System.out.println(pow);


    }
}

```



## 三、逻辑运算符

&&、||、！（两位）

值得注意的是：&&逻辑与，当前一个表达式为假，不再计算后一个

```java
package operator;

public class Demo4 {
    public static void main(String[] args) {
        // &&逻辑与
        //当前一个为假，不再计算后一个
        int a = 5;
        boolean b = (a<4)&&(a++<4);
        System.out.println(a);
        System.out.println(b);
        //a++<4 没有计算，a依旧为5
    }
}

```



## 四、位运算符

&、|、^（一位）

值得注意的是，左移相当于*2，右移相当于/2，效率极高。

## 五、连接符 ：+

```java
package operator;

public class Demo5 {
    public static void main(String[] args) {
        //字符串连接符   +  String
        int a = 10;
        int b = 20;
        System.out.println(a+b+"");//计算结果之后拼接上字符串
        System.out.println(""+a+b);//当字符串在前面，将后面的全都转化为字符串
    }
}
```

## 六、条件运算符

```java
package operator;

public class Demo6 {
    //三元运算符
    //x ? y : z
    // 如果x为真，结果为y，否则结果为z
    public static void main(String[] args) {

        int score = 60;
        String type = score >= 60 ? "及格": "不及格";
        System.out.println(type);
    }


}

```

