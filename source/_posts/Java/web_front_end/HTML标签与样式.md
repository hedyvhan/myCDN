---
title:  HTML标签与样式
date: '2024-01-03 15:49'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 51733
---
# HTML标签与样式

## 1. 标签-新闻标题

- 图片标签：\<img>

  - src：指定图像的url(绝对路径/相对路径)
  - width：图像的宽度(像素px/相对于父元素的百分比%)
  - height：图像的高度(像素px/相对于父元素的百分比%)

  长宽只指定一个，另一个可以自动按比例缩放。

- 标题标签:\<h1> - \<h6>

- 水平线标签:\<hr>

- 超链接标签

  ```html
  <a href="...” target="..."> 央视网</a>
  ```

  ```html
  href:指定资源访问的url
  target:指定在何处打开资源链接
  	_self:默认值，在当前页面打开
  	_blank:在空白页面打开
  ```

- 视频标签：\<video>

  - src：规定视频的ur1
  - controls：显示播放控件
  - width：播放器的宽度
  - height：播放器的高度

- 音频标签：\<audio>

  - src：规定音频的url
  - controls：显示播放控件

- 段落标签：\<p>

- 文本加粗标签：\<b>或者\<strong>

------

新闻标题最终代码：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>
<body>
	<img src="img/news logo.png"> <a href="http://gov.sina.com.cn" target= "_self">新浪政务</a> > 正文
	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
	<hr>
	2023年03月02日 21:50 央视网
	<hr>
</body>
</html>
```



## 2. 样式-标题的样式

### 2.1 CSS引入方式：

- 行内样式：写在标签style属性中**（不推荐）**

  ```html
  			属性名: 属性值
  <h1 style="xxx: xxx; xxx: xxx;"中国新闻网</h1>
  ```

- 内嵌样式：写在style标签中 (可以写在页面任何位置，但通常约定写在head标签中)

  ```html
  <style> 
  	h1 {
  		xxx: xxx;
          xxx: xxx;
  </style>
  ```

- 外联样式：写在一个单独的.css文件中(需要通过 link 标签在网页中引入)

  ```html
  h1 {
  		xxx: xxx;
          xxx: xxx;
  }
  ```

  ```html
  <link rel="stylesheet" href="css/news.css">
  ```

例如改标题颜色：

![颜色表示形式](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242081.png)



改标题颜色，最终代码：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>
    方式二：内嵌样式
    <style>
        h1{
            color: red;
        }
    </style>
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文
    
    方式一：行内样式
	<h1 style = "color: red">焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
	2023年03月02日 21:50 央视网
	<hr>
</body>
</html>
```

方式三：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>
    
    方式三：外联样式
    <link rel = "stylesheet" href="css/news.css">
    
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文

	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
	2023年03月02日 21:50 央视网
	<hr>
</body>
</html>
```

```html
css/news.css文件
h1{
    color: red;
}

```



------

使用方式二，最终代码：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
    </style>
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文

	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
	2023年03月02日 21:50 央视网
	<hr>
</body>
</html>
```

如果需要修改同一行文字为不同的字体颜色，比如“2023年03月02日”和“21:50 央视网”为不同颜色，需要使用css选择器。

### 2.2 CSS选择器

CSS选择器：用来选取需要设置样式的元素(标签）

- 元素选择器

  ```html
  h1{
  	color: red;
  }
  ```

  ```html
  <h1> hello </h1>
  ```

- id选择器

  ```html
  #hid{    	
  	color: red;
  }
  ```

  ```html
  <h1 id="hid"> hello </h1>
  ```

  一个页面中，id不能重复



- 类选择器

  ```html
  .cls{
  	color:red;
  }
  ```

  ```html
  <h1 class="cls"> hello </h1>
  ```

  class可以重复


------

实现“2023年03月02日”和“21:50 央视网”为不同颜色，使用元素选择器：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        span{
            color: #968B92;
        }
        
    </style>
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文

	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
    <span>2023年03月02日 21:50</span> <span>央视网</span>
	<hr>
</body>
</html>
```

\<span>\</span>标签没有任何语意。这里两部分的颜色完全相同。

使用类选择器：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        .cls{
            color: #968B92;
        }
        
    </style>
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文

	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
    <span class = "cls">2023年03月02日 21:50</span>   <span>央视网</span>
	<hr>
</body>
</html>
```

这里在时间加了一个class，并规定class的颜色，所以时间和“央视网”的颜色不同。

使用id选择器：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        #time{
            color: #968B92;
        }
        
    </style>
<body>
	<img src="img/news logo.png"> 新浪政务 > 正文

	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
    <span class = "cls" id = "time">2023年03月02日 21:50</span>   <span>央视网</span>
	<hr>
</body>
</html>
```

时间使用了id标签，改变了颜色。

作用优先级：**元素选择器 < 类选择器 < id选择器**。

------



将超链接不显示为蓝色字体和下划线，改a标签的样式即可：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        #time{
            color: #968B92;
        }
        
        a{
            color: black;
            text-decoration:none;设置文本为标准文本
        }
        
    </style>
<body>
	<img src="img/news logo.png"> <a href="http://gov.sina.com.cn" target= "_self">新浪政务</a> > 正文
	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
    <span class = "cls" id = "time">2023年03月02日 21:50</span>   <span>央视网</span>
	<hr>
</body>
</html>
```

## 3.标签-新闻正文

换行：\<br>

段落：\<p>-\</p>

首行缩进、行高、对齐方式：通过css

```html
p{
	text-indent：35px;
	line-heigt: 40px ;
	text-align:right;
}
```

------

最终正文排版：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        #time{
            color: #968B92;
        }
        
        a{
            color: black;
            text-decoration:none;设置文本为标准文本
        }
        
        p{
			text-indent：35px; /*首行缩进*/
			line-heigt: 40px; /*行高*/
		}
        #plast{
            text-align:right; /*对齐方式*/
        }
        
    </style>
<body>
	<img src="img/news logo.png"> <a href="http://gov.sina.com.cn" target= "_self">新浪政务</a> > 正文
	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>
    
	<hr>
    <span class = "cls" id = "time">2023年03月02日 21:50</span>   <span>央视网</span>
	<hr>
    
    <!-- 正文-->
	<!-- 视频-->
	<video src="video/1.mp4” controls width="950px"></video>
	<!--音频 -->
	<!--<audio src="audio/1.mp3" controls></audio> -->
                                
	<p>
	<strong>天视网消息</strong>(焦点访谈》:党的十人大以来，以习近平同志为核心的党中央始终把解	决粮食安全问题作为治国理政的头等大事，重农抓粮一系列政策举措有力有效，我国粮食产量站稳1.3	万亿斤台阶，实现谷物基本自给、口粮绝对安全。我们把饭碗牢牢端在自己手中，为保障经济社会发展	提供了坚实支撑，为应对各种风险挑战赢得了主动。连续八年1.3万亿斤，这个沉甸甸的数据是如何取得的呢?
	</p>
                                
	<p>
	人勤春来早，春耕农事忙。立春之后，由南到北，我国春耕春管工作陆续展开，春天的田野处处生机盎然。
	</p>

	<p id="plast">
	责任编辑：王树淼 SN42
	</p>                               
                                
</body>
</html>
```

在HTML中无论输入多少个空格，只会显示一个。空格占位符: \&nbsp;

## 4. 盒子模型-新闻布局

- 盒子：页面中所有的元素(标签)，都可以看做是一个 盒子，由盒子将页面中的元素包含在一个矩形区域内，通过盒子的视角更方便的进行页面布局
- 盒子模型组成：内容区域(content)、内边距区域 (padding)、边框区域(border)、外边距区域(margin)

![image-20240104095925753](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242083.png)

**布局标签**：实际开发网页中，会大量频繁的使用div和span 这两个没有语的布局标签。

- div标签：
  - 一行只显示一个(独占一行)
  - 宽度默认是父元素的宽度，高度默认由内容撑开
  - 可以设置宽高(width、height)
- span标签：
  - 一行可以显示多个
  - 宽度和高度默认由内容撑开
  - 不可以设置宽高(width、height)

例子：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
    
		div{
			width: 200px;
			height: 200px;
			box-sizing: border-box; /* 指定width height为盒子的高宽 */
			background-color:  aquamarine; /t 背景色*/
			padding:20px;/* 内边距，上右下左*/
			border: 10px solid red; /* 边框，宽度 线条类型 颜色 */
			margin:30px;/* 外边距，上右下左*/
		}
        
    </style>
<body>


	<div>
		A A A A A A A A A A A A A A A
 	</div>
                                
</body>
</html>
```



可以看到效果：

![image-20240104102838593](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242084.png)



![image-20240104101158447](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242085.png)

border边框200

------



将新闻重新排版：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        h1{
            color: red;
        }
        
        #time{
            color: #968B92;
        }
        
        a{
            color: black;
            text-decoration:none; /*设置文本为标准文本*/
        }
        
        p{
			text-indent:65px; /*首行缩进*/
			line-height:50px; /*行高*/
			font-size: 30px;
		}
        #plast{
            text-align:right; /*对齐方式*/
        }
		div{
			width: 60%;
			/*margin:0 15% 0 15%;!* 外边距，上右下左*!*/
			margin:0 auto;/* 外边距，上右下左*/

		}
        
    </style>
<body>
<div>
	<img src="img/news logo.png"> <a href="http://gov.sina.com.cn" target="_self">新浪政务</a> > 正文
	<h1>焦点访谈: 中国底气 新思想夯实大国粮仓</h1>

	<hr>
	<span class="cls" id="time">2023年03月02日 21:50</span> <span>央视网</span>
	<hr>

	<!-- 正文-->
	<!-- 视频-->
	<video src="video/1.mp4” controls width=" 950px
	"> </video>
	<!--音频 -->
	<!--<audio src="audio/1.mp3" controls></audio> -->

	<p>
		<strong>天视网消息</strong>(焦点访谈》:党的十人大以来，以习近平同志为核心的党中央始终把解 决粮食安全问题作为治国理政的头等大事，重农抓粮一系列政策举措有力有效，我国粮食产量站稳1.3
		万亿斤台阶，实现谷物基本自给、口粮绝对安全。我们把饭碗牢牢端在自己手中，为保障经济社会发展 提供了坚实支撑，为应对各种风险挑战赢得了主动。连续八年1.3万亿斤，这个沉甸甸的数据是如何取得的呢?
	</p>

	<p>
		人勤春来早，春耕农事忙。立春之后，由南到北，我国春耕春管工作陆续展开，春天的田野处处生机盎然。
	</p>

	<p id="plast">
		责任编辑：王树淼 SN42
	</p>


</div>

</body>
</html>
```



## 5. 表格标签

|   标签   |            描述            |                          属性/备注                           |
| :------: | :------------------------: | :----------------------------------------------------------: |
| \<table> |        定义表格整体        | border：规定表格边框的宽度<br />width：规定表格的宽度<br />cellspacing：规定单元之间的空间 |
|  \<tr>   |          表格的行          |                                                              |
|  \<td>   | 表格的单元格，可以包裹内容 |              如果是表头单元格，**替换为\<th>**               |

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
        table{
            text-align: center;
        }
        
    </style>
<body>

    <table border="1px" cellspacing="0" width="600px">
        <tr>
            <th>序号</th>
            <th>品牌Logo</th>
            <th>品牌名称</th>
            <th>企业名称</th>
        </tr>
        <tr>
            <td>1</td>
            <td><img src="img/huawei.jpg" width="100px"></td>
            <td>华为</td>
            <td>华为技术有限公司</td>
        </tr>
        <tr>
            <td>2</td>
            <td><img src="img/alibaba.jpgwidth=" 100px"></td>
            <td>阿里</td>
            <td>阿里巴巴集团控股有限公司</td>
        </tr>
    </table>
                                
</body>
</html>
```



## 6.表单标签

表单标签：\<form>，指的是整个表单。

- 属性：
  - action：规定提交表单时想何处发送表单数据，url
  - method：规定发送表单数据的方式，get、post



例子：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
   <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">
    <title>焦点访谈: 中国底气 新思想夯实大国粮仓</title></head>

    <style>
    
      div{
         width: 200px;
         height: 200px;
         box-sizing: border-box; /* 指定width height为盒子的高宽 */
         background-color:  aquamarine; /t 背景色*/
         padding:20px;/* 内边距，上右下左*/
         border: 10px solid red; /* 边框，宽度 线条类型 颜色 */
         margin:30px;/* 外边距，上右下左*/
      }
        table{
            text-align: center;
        }
        
    </style>
<body>

    <form action="" method="get">
        用户名:<input type="text" name="uername">
        年龄:<input type="text" name="age">

        <input type="submit" value="提交">
    </form>
                                
</body>
</html>
```



## 7. 表单项标签

一个表单下可以包含多个表单项标签。

表单项目：

- \<input>定义表单项，通过type属性控制输入形式。**必须有name属性才可以提交**
- \<select>定义下拉列表
- \<textarea>定义文本域

通过这三个表单项，可以实现各式各样的表单输入形式。

### 7.1 input：

![image-20240104105655370](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242086.png)

### 7.2 select

![image-20240104105750481](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242087.png)

### 7.3 文本域

![image-20240104105804575](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242088.png)

------

单选框

type="radio"，且使用label包裹，这样点击label中的任何属性都可以聚焦到当前元素上。

比如

![image-20240104111335129](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162242089.png)

选择文字也可以选中。不用label包裹则必须选中圆圈才行。

```html
<!--radio单选框-->
性别: <label><input type="radio" name="gender" value="1">男</label>
	<label><input type="radio" name="gender" value="2"> 女 </label> <br><br>
```

复选框

```html
爱好: <label><input type="checkbox" name="hobby" value="java"> java </label>

             <label><input type="checkbox" name="hobby" value="game"> game </label>

             <label><input type="checkbox" name="hobby" value="sing">sing</label>
```

### 7.4 各种表单项演示：

```html
<!DOCTYPE html>
<html lanq="en">
<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=l.0">

<body>


<!--    value:表单项提交的值&ndash;&gt;-->
    <form action="" method="post">
        姓名: <input type="text" name="name"> <br><br>

        密码: <input type="password" name="password"> <br><br>

        <!--radio单选框-->
        性别: <label><input type="radio" name="gender" value="1">男</label>

             <label><input type="radio" name="gender" value="2"> 女 </label> <br><br>

        爱好: <label><input type="checkbox" name="hobby" value="java"> java </label>

             <label><input type="checkbox" name="hobby" value="game"> game </label>

             <label><input type="checkbox" name="hobby" value="sing">sing</label>

        图像:<input type="file" name="image"><br><br>生日: <input type="date" name="birthday"> <br><br>

        时间:<input type="time" name=" time"> <br><br>

        日期时间: <input type="datetime-local" name="datetime"> <br><br>邮箱: <input type="email" name="email"> <br><br>

        年龄:<input type="number" name="age"> <br><br>

        学历: <select name="degree">
            <option value="">----------- 请选择-----------</option>
            <option value="1">大专</option>
            <option value="2">本科</option>
            <option value="3">硕士</option>
            <option value="4">博士</option>
            </select><br><br>

        描述: <textarea name="description" cols="30" rows="10"></textarea><br><br>
            <input type="hidden" name="id" value="1">
        <!-- 表单常见按钮 -->
            <input type="button" value="按钮">
            <input type="reset"  value="重置">
            <input type="submit" value="提交">
        <br>
    </form>
                                
</body>
</html>
```

