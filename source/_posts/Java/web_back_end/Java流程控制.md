---
title: Java流程控制
date: ' 2021-05-23 21:36'
tags: Java
categories: 
- Java
- Web后端
abbrlink: 13069
---

# Java流程控制

## 一、用户交互scanner

### 1. 基本语法：

```java
Scanner s = new Scanner（System.in）;
```

通过Scanner类的next()和nextLine()方法获取输入的字符串，在读取前我们一般需要使用hasNext()和hasNextLine（）判断是否还有输入的数据。

### 2. 接收用户输入的两种方式：

- next():

  以空格作为结束符，不能得到带有空格的字符串。

- nextLine():

  以Enter作为结束符，可以获取空格字符串，一般使用这个。

  ```java
  package Scanner;
  
  import java.util.Scanner;
  
  public class Demo1 {
      public static void main(String[] args) {
          //创建一个扫描器对象，用于键盘接受数据
          Scanner scanner = new Scanner(System.in);
          System.out.println("input : ");
          // 判断用户有没有输入
          if (scanner.hasNext())
          {
              // 使用next接收输入数据
              String str1 = scanner.next();
              System.out.println("用户输入为： "+str1);
  
          }
          //io流,一定要记得关闭！！！！！！！
          scanner.close();
  
      }
  }
  
  ```

  ```java
  package Scanner;
  
  import java.util.Scanner;
  
  public class Demo2 {
      public static void main(String[] args) {
          //创建一个扫描器对象，用于键盘接受数据
          Scanner scanner = new Scanner(System.in);
          System.out.println("input : ");
          // 判断用户有没有输入
          if (scanner.hasNext())
          {
              // 使用nextLine接收输入数据
              String str2 = scanner.nextLine();
              System.out.println("用户输入为： "+str2);
          }
  
          //一定要记得关闭！！！！！！！
          scanner.close();
      }
  }
  
  ```

  另外还有接收整数小数：

  ```java
  package Scanner;
  
  import java.util.Scanner;
  
  public class Demo4 {
      public static void main(String[] args) {
          int i = 0;
          float f = 0.0f;
  
          Scanner scanner = new Scanner(System.in);
          System.out.println("请输入一个数 ：");
  
          //接收更加细致
          if (scanner.hasNextInt())
          {
              i = scanner.nextInt();
              System.out.println("整数数据为："+i);
          }
          else
              System.out.println("输入的不是整数！");
  
  
          if (scanner.hasNextFloat())
          {
              f = scanner.nextFloat();
              System.out.println("小数数据为："+f);
          }
          else
              System.out.println("输入的不是小数！");
  
          scanner.close();
      }
  }
  
  ```

  一个小栗子：

  ```java
  package Scanner;
  
  import java.util.Scanner;
  
  public class Demo5 {
      public static void main(String[] args) {
          Scanner scanner = new Scanner(System.in);
  
          double sum = 0;
          int n = 0;
          System.out.println("请输入数据： ");
          while (scanner.hasNextDouble())
          {
              double x = scanner.nextDouble();
              sum += x;
              n ++;
              System.out.println("第"+n+"个数"+"，当前输入为："+x+",当前总和为："+sum);
          }
  
          System.out.println("输入总和为："+sum);
          System.out.println("输入的平均数为："+sum/n);
  
  
  
          scanner.close();
  
  
      }
  }
  
  ```
  


## 二、顺序结构

## 三、选择结构

switch case 语句里的break用法：

（case穿透现象）如果没有break，将输出“良好”以及后面的所有；如果加上break，只会输出“良好”。

无法匹配到,输出default的内容.



这里反编译发现,是通过哈希值进行匹配的.

```java
package struct;

public class SwitchDemo1 {
    public static void main(String[] args) {
        char grade = 'B';
        switch (grade)
        {
            case 'A':
                System.out.println("优秀");
                break;
            case 'B':
                System.out.println("良好");
                break;
            case 'C':
                System.out.println("及格");
                break;
            case 'D':
                System.out.println("不及格");
                break;
            default:
                System.out.println("未知等级");

        }

    }
}

```



## 四、循环结构

## 五、break和continue

break：用于强制退出循环，不执行循环中剩余语句，但是会执行循环外的语句。（也可以用于switch语句）

continue：终止某次循环过程，即跳过循环体中尚未执行的语句，接着进行下一次是否执行循环的判定。

```java
package struct;

public class BreakContinueDemo5 {
    public static void main(String[] args) {
        int i = 0;
        while (i<100)
        {
            i = i+10;
            if(i==30)
                break;
            System.out.println(i);//输出10，20
        }
        System.out.println("break会执行这一句！！！");

        System.out.println("====================================");

        i=0;
        while(i<100)
        {
            i = i+10;
            if(i==30)
                continue;
            System.out.println(i);//输出10，20，40，50，60，70，80，90，100，跳过了30
        }
        System.out.println("continue会执行这一句！！！");
    }
}

```

[反编译看源码](【【狂神说Java】Java零基础学习视频通俗易懂】 https://www.bilibili.com/video/BV12J41137hu/?p=37&share_source=copy_web&vd_source=b14289245d1bcfac80afa07855c1c799)

