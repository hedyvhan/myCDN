---

title: JavaScript
date: '2024-01-03 15:49'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 51733
---
# JavaScript

## 1. JavaScript的引入方式

内部脚本：将JS代码定义在HTML页面中

- 代码位于\<script>\</script>标签之间
- 在html文档中，可以在任意位置，防止任意数量的\<script>
- 一般把脚本放置于\<body>元素的底部，可以改善显示速度

```html
<script>
	alert("hello world")
</script>
```



外部脚本：将JS代码定义在外部JS文件中，然后引入到HTML页面中

```javascript
// demo.js
alert("hello world")
```

- 外部JS文件中，只包含JS代码，不包含\<script>标签

- \<script>标签不能自闭合

  ```html
  <script src="js/demo.js"></script>
  //不能自闭合，即
  <script src="js/demo.js"/>
  ```

  

------

eg：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
    
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>JS-引入方式</title></head>

    <script>
        alert("hello");
    </script>

<style>


</style>

<body>

</body>

</html>

```

## 2. js基础语法

### 2.1 语法（与Java雷同）

- 区分大小写

- 分号可有可无（建议带上）

- 注释

  - 单行：//
  - 多行：/*  */

- 大括号表示代码块

  ```javascript
  if (count == 3){
  	alert(count)
  }
  ```

输出语句：

- 使用 window.alert() 写入警告框
- 使用 document.write() 写入 HTML输出
- 使用 console.log() 写入浏览器控制台

```javascript
<script>
       window.alert("hello JavaScript")
	   document.write("hello JavaScript")
	   console.log("hello JavaScript")
</script>
```

效果：

![image-20240104152117945](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162250440.png)

### 2.2 变量（与Java雷同）

- JavaScript中用var关键字(variable 的缩写)来声明变量。
- JavaScript 是一门弱类型语言，变量可以存放不同类型的值
- 变量名需要遵循如下规则:
  - 组成字符可以是任何字母、数字、下划线()或美元符号(S)
  - 数字不能开头
  - 建议使用驼峰命名

var变量特点：

1. 全局变量

   ```javascript
   <script>
       {
           var a = 10
       }
       alert(a) // 10
   
   </script>
   ```

   

2. 可以重复定义

   ```javascript
   <script>
       {
           var a = 10
       	var a = 'a' // 覆盖
       }
   </script>
   ```



**新增let、const关键字**

let所声明的变量，只在 let 关键字所在的代码块内有效，且不允许重复声明。

const用来声明一个只读的**常量**。一旦声明，常量的值就不能改变。

```javascript
<script>
    {
        let a = 10
        alert(a) // 10
    }
	//let局部变量，代码块外面的无法使用a
    
    {
        const pi = 3.14
        //不能再次定义名字为b的变量，不能改变
        // 浏览器控制台报错
         pi = 3.2
       
    }
</script>
```



### 2.3 数据类型、运算符、流程控制语句

#### 2.3.1 数据类型

虽然定义变量的时候不用指定数据类型，但是js依旧有数据类型

**基本数据类型：**

- number：数字（整数、小数、NaN）
- string：字符串（单双引号都可）
- boolen
- null：对象为空
- undefined：当声明的变量未初始化时，该变量的默认值是undefined

```javascript
<script>
	    //原始数据类型
    alert (typeof 3); //number
    alert (typeof 3.14); //number
    alert(typeof "A"); //string
    alert(typeof 'Hello');//string
    alert(typeof true); //boolean
    alert (typeof false);//boolean
    alert (typeof nul1); //null是object
    
    var a ;
    alert (typeof a); //未定义是undefined

</script>
```

**引用类型：**

#### 2.3.2 运算符（与Java雷同）

特殊：===

== 会进行类型转换。

=== 不会进行类型转换，类型不同就是false，类型和值都相同才true

```javascript
<script>
    var a = 10;
    alert(a == "10"); //true
    alert(a === ""10"); //false
    alert(a === 10); //true
</script>
```

#### 2.3.3 类型转换

**字符串to数字parseInt：**

在转换时，逐个字符串比较，碰到不是数字的就停止。

```javascript
<script>
    
    alert(parseInt("12"))  // 12
    alert(parseInt("12A45"))  // 12
    alert(parseInt("A45"))  // NaN,not a number

</script>
```

**其他类型to布尔类型：**

- Number：0和NaN为false，其他均转为true。
- String：空字符串为false，其他均转为true。
- Null和undefined：均转为false。

```javascript
//数字to布尔   
if (0) { //false
        alert("0 自动转换为false");
    }
    if (NaN) {  //false
        alert("NaN自动转换为false");
    }

    if (1) {  //true
        alert("除0和Nan其他数字都转为 true");
    }
```



```javascript
//字符串to布尔 
if ("") {  //false
        alert("空字符串为 false，其他都是true");
    }
    if ("12") {  //true
        alert("空字符串为 false，其他都是true");
    }
	if (" ") {  //空格，true
        alert("空字符串为 false，其他都是true");
    }
    
```



```javascript
//null、undefined to布尔     
if(null){
        //false
        alert("null 转化为false");
    }
    if(undefined) { //false
        alert("undefined 转化为false");
    }
```

 

#### 2.3.4 流程控制语句

与Java雷同



## 3. js函数

语法

```html
<script>
    function functionName(arg1, arg2,...){
        //code
    }

    function add(a, b){
        return a+b;
    }
    
    var result = add(10,20);
    alert(result);
</script>
```



js是弱类型语言，**参数和返回值 **都不用定义类型。



另外

```html
<script>

    function add(a, b){
        return a+b;
    }
    
    var result = add(10, 20,30,40);//实际上只接受10,20
    alert(result);//30
</script>
```

js中函数调用可以传递任意个数的参数，但是实际还是只接收有限个。



## 4. js对象

### 4.1 基础对象

- array

  ```javascript
  var arr =  [1,2,3];
  //或者 var arr = new Array(1,2,3);
  arr[0] = 0;
  ```

  特点：长度可变，元素类型可变

  ```javascript
  var arr =  [1,2,3];
  arr[4] = 50;
  // 此时arr = [1,2,3,undefined, 50],即长度可变
  
  
  arr[5] = “hello”;
  arr[6] = true;
  // 此时arr = [1,2,3,undefined, "hello", true],即元素类型可变。
  
  ```

  array常见的属性：

  ```javascript
  
  //遍历：数组中 所有 的元素
  var arr = [1, 2, 3, 4];
  for (let i = 0; i< arr.length; i++){
      console.log(arr[i]);
  }
  
  //遍历：数组中 有值 的元素
  arr.forEach(
      function (e) {
      console.log(e)
  }
  )
  // 简化写法，箭头函数
  arr.forEach(
       (e) => {
          console.log(e)
      }
  )
  
  // push尾部追加
  arr.push(100,200,300)
  console.log(arr)
  //[1,2,3,4,100,200,300]
  
  // splice删除。从0开始删除，删除3个
  arr.splice(0,3)
  console.log(a
  
  ```

  

- string

   

  ```javascript
  // 定义
  var str1 = new String("hello string1");
  var str2 = "    hello string2           ";
  console.log(str1);
  console.log(str2);
  // 属性length
  console.log(str1.length);  // 13
  
  /* 方法 */
  
  // charAt指定位置的字符
  console.log(str1.charAt(4)); //  o
  // 检索字符串
  console.log(str1.indexOf("lo")); // 3
  // 去除字符串两边的空格
  s = str2.trim();
  console.log(s);  // hello string2
  // 提取子字符串
  console.log( str1.substring(1,7)  ); // [1,7)  "ello s"
  
  ```

  

- json

  自定义对象：

  ```javascript
  //自定义对象
  var user = {
      name: "Tom",
      age: 10,
      gender: "male",
      //方法定义1
     	/*eat: function () {
          alert("用膳~");
      }*/
      //方法定义2
      eat(){
              alert("用膳~");
          }
  }
  alert(user.name);
  user.eat();
  ```

  json对象：

  概念：JavaScript object Notation，JavaScript**对象标记法**。JSON是通过JavaScript 对象标记法书写的**文本**。实质是一个字符串。

  由于其语法简单，层次结构鲜明，现多用于作为数据载体，在网络中进行数据传输。

  

  json格式的key都需要**双**引号。

  ```javascript
  //定义
  var jsonstr = '{"name":"Tom", "age":18, "addr": ["beijing", "shanghai", "wuhan"]}';
  // json字符串转为json对象
  var jsonOb = JSON.parse(jsonstr);
  alert(jsonOb.name); // Tom
  
  // json对象转为json字符串
  var jsonstr2 = JSON.stringify(jsonstr);
  alert(jsonstr2);
  ```

  

### 4.2 浏览器对象Bom

概念：Browser Obiect Model 浏览器对象模型，允许JavaScript与浏览器对话，JavaScript 将浏览器的各个组成部分封装为对象

组成：

- **Window**：浏览器窗口对象
- Navigator：浏览器对象
- Screen：屏幕对象
- History：历史记录对象
- **Location**：地址栏对象

------



**window对象：**

获取: 直接使用window，其中 **window.可以省略。**

```javascript
window.alert("Hello window");
alert("Hello window");
```

属性：

- history：对history对象的只读引用。
- location：用于窗口或框架的Location 对象。
- navigator：对navigator对象的只读引用。

方法：

- alert()：显示带有一段消息和一个确认按钮的警告框。
- confirm()：显示带有一段消息以及确认按钮和取消按钮的对话框。返回值boolean。
- setInterval()：按照指定的周期(以毫秒计)来调用函数或计算表达式。
- setTimeOUT()：在指定的毫秒数后调用函数或计算表达式。

```javascript
    // BOM获取
    window.alert("hello window");
    alert("hello");

    //方法,
    var flag = confirm("确定要删除吗");
    alert(flag);

    //周期性执行函数，2000ms执行一次
    setInterval(function (){
        console.log("setInterval执行了一次");
    }, 2000);

    // 延迟5000ms执行函数，只执行一次
    setTimeout(function (){
        console.log("setTimeout");
    },5000);
```



**Location对象：**

地址栏对象。使用window.location获取，其中 **window.可以省略。

属性：

- href：设置或返回完整的URL。

```javascript
    // 获取地址栏url
    alert(location.href);
    // 设置地址栏url，即跳转。
    location.href = "https://baidu.com";
```



### 4.3 文档对象DOM

概念: Document Object Model，文档对象模型。将标记语言的各个组成部分封装为对应的对象：

- Document:整个文档对象
- Element:元素对象
- Attribute:属性对象
- Text:文本对象
- Comment:注释对象

即html文档被加载并解析之后，会封装成以上几个对象。同时在浏览器的缓存中会形成一个DOM树结构。

![image-20240108092734621](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162250441.png)



Javascript通过DOM，就能够对HTML进行操作：

- 改变HTML元素的内容
- 改变HTML元素的样式(CSS)
- 对HTML DOM 事件作出反应
- 添加和删除HTML元素

比如通过删除按键，可以删除表格的数据。在前端页面显示上就是对html元素进行了删除。

同时也可以实现通过点开按键，改变文字、文字的颜色等等。

------

如何实现上述功能？

1. 获取Element元素

   ```html
   <!DOCTYPE html>
   <html lanq="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width,initial-scale=l.0">
       <title>JS</title>
   </head>
   
   
   
   <style>
   
   
   </style>
   
   
   <body>
   
   <img id = "h1" src = "img.jpg"> <br><br>
   
   <div class="cls">鼠标</div>  <br>
   <div class="cls">键盘</div>  <br>
   <div class="cls">显示器</div>  <br>
   
   <input type="checkbox" name="编程语言"> C
   <input type="checkbox" name="编程语言"> java
   <input type="checkbox" name="编程语言"> python
   
   </body>
   
   
   <script>
   
       // 获取元素
       //1. 根据id获取
       var img = document.getElementById("h1");
       alert(img);
   
       //2. 根据标签获取
       var divs = document.getElementsByTagName('div');
       alert( divs.length );
       for (let i = 0; i < divs.length; i++) {
           alert( divs[i] );
       }
       // 3.根据name属性获取
       var results = document.getElementsByName("编程语言")
       alert( results.length );
       for (let i = 0; i < results.length; i++) {
           alert( results[i] );
       }
   
       //4. 根据class属性获取
       var cls = document.getElementsByClassName("cls")
       alert( cls.length );
       for (let i = 0; i < cls.length; i++) {
           alert( cls[i] );
       }
   
   </script>
   
   
   </html>
   ```

   

2. [查询参考手册](w3school.com.cn/jsref/index.asp)，使用属性、方法来改变html元素。

   ```javascript
   cls[0].innerHTML = "主机";
   ```

   

------

eg：

```javascript
/*
需求：
1. 所有div标签后面加上huawei，并标为红色。

2. 所有复选框都选中。
*/

// 1.  所有div标签后面加上huawei，并标为红色。
var divs = document.getElementsByTagName("div");
for (let i = 0; i < divs.length; i++) {
    div = divs[i];
    div.innerHTML += "<font color='red '>huawei<font>";
}
// 2. 所有复选框都选中。
var results = document.getElementsByName("编程语言");
for (let i = 0; i < results.length; i++) {
    result = results[i];
    result.checked = true;
}
```





## 5. js事件监听

事件：HTML事件是发生在HTML元素上的“事情”。比如:

- 按钮被点击
- 鼠标移动到元素上
- 按下键盘按键
- 鼠标悬浮提示

事件监听：JavaScript可以在事件被侦测到时执行代码。

### 5.1 事件绑定

两种方法：

- 通过HTML标签中的事件属性进行绑定
- 通过DOM元素进行绑定

eg：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>JS</title>
</head>

<body>

<input type="button" id = "btn1" value="事件绑定1" onclick="on()">
<input type="button" id = "btn2" value="事件绑定2">
    
</body>

<script>
    function on(){
        alert("按键1被点击了")
    }

    document.getElementById("btn2").onclick = function (){
        alert("按键2被点击了")
    }

</script>


</html>
```



### 5.2 常见事件

 ![image-20240108163345846](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162250442.png)



eg：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS-事件-常见事件</title>
</head>

<body onload="load()">

    <form action="" style="text-align: center;" onsubmit="subfn()">
        <input type="text" name="username" onblur="bfn()" onfocus="ffn()" onkeydown="kfn()">
        
        <input id="b1" type="submit" value="提交">

        <input id="b1" type="button" value="单击事件" onclick="fn1()">
    </form>  

    <br><br><br>

    <table width="800px" border="1" cellspacing="0" align="center" onmouseover="over()" onmouseout="out()">
        <tr>
            <th>学号</th>
            <th>姓名</th>
            <th>分数</th>
            <th>评语</th>
        </tr>
        <tr align="center">
            <td>001</td>
            <td>张三</td>
            <td>90</td>
            <td>很优秀</td>
        </tr>
        <tr align="center">
            <td>002</td>
            <td>李四</td>
            <td>92</td>
            <td>优秀</td>
        </tr>
    </table>

</body>

<script>
    //onload : 页面/元素加载完成后触发
    function load(){
        console.log("页面加载完成...")
    }

    //onclick: 鼠标点击事件
    function fn1(){
        console.log("我被点击了...");
    }

    //onblur: 失去焦点事件
    function bfn(){
        console.log("失去焦点...");
    }

    //onfocus: 元素获得焦点
    function ffn(){
        console.log("获得焦点...");
    }

    //onkeydown: 某个键盘的键被按下
    function kfn(){
        console.log("键盘被按下了...");
    }

    //onmouseover: 鼠标移动到元素之上
    function over(){
        console.log("鼠标移入了...")
    }

    //onmouseout: 鼠标移出某元素
    function out(){
        console.log("鼠标移出了...")
    }

    //onsubmit: 提交表单事件
    function subfn(){
        alert("表单被提交了...");
    }

</script>
</html>
```



### 5.3 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS-事件-案例</title>
</head>
<body>

    <img id="light" src="img/off.gif"> <br>

    <input type="button" value="点亮" onclick="on()"> 
    <input type="button"  value="熄灭" onclick="off()">

    <br> <br>

    <input type="text" id="name" value="ITCAST" onfocus="lower()" onblur="upper()">
    <br> <br>

    <input type="checkbox" name="hobby"> 电影
    <input type="checkbox" name="hobby"> 旅游
    <input type="checkbox" name="hobby"> 游戏
    <br>

    <input type="button" value="全选" onclick="checkAll()"> 
    <input type="button" value="重置" onclick="reverse()">

</body>

<script>

    //1. 点击 "点亮" 按钮, 点亮灯泡; 点击 "熄灭" 按钮, 熄灭灯泡; -- onclick
    function on(){
        //a. 获取img元素对象
        var img = document.getElementById("light");

        //b. 设置src属性
        img.src = "img/on.gif";
    }

    function off(){
        //a. 获取img元素对象
        var img = document.getElementById("light");

        //b. 设置src属性
        img.src = "img/off.gif";
    }



    //2. 输入框聚焦后, 展示小写; 输入框离焦后, 展示大写; -- onfocus , onblur
    function lower(){//小写
        //a. 获取输入框元素对象
        var input = document.getElementById("name");

        //b. 将值转为小写
        input.value = input.value.toLowerCase();
    }

    function upper(){//大写
        //a. 获取输入框元素对象
        var input = document.getElementById("name");

        //b. 将值转为大写
        input.value = input.value.toUpperCase();
    }



    //3. 点击 "全选" 按钮使所有的复选框呈现选中状态 ; 点击 "反选" 按钮使所有的复选框呈现取消勾选的状态 ; -- onclick
    function checkAll(){
        //a. 获取所有复选框元素对象
        var hobbys = document.getElementsByName("hobby");

        //b. 设置选中状态
        for (let i = 0; i < hobbys.length; i++) {
            const element = hobbys[i];
            element.checked = true;
        }

    }
    
    function reverse(){
        //a. 获取所有复选框元素对象
        var hobbys = document.getElementsByName("hobby");

        //b. 设置未选中状态
        for (let i = 0; i < hobbys.length; i++) {
            const element = hobbys[i];
            element.checked = false;
        }
    }



</script>
</html>
```

 













































