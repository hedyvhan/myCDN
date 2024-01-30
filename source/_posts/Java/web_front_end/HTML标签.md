---
title: HTML-以新浪新闻为例
date: '2024-01-03 17:24'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 26949
---

# HTML-以新浪新闻为例

## 标签

- 图片标签：\<img>

  - src：指定图像的url(绝对路径/相对路径)
  - width：图像的宽度(像素px/相对于父元素的百分比%)
  - height：图像的高度(像素px/相对于父元素的百分比%)

  长宽只指定一个，另一个可以自动按比例缩放。

- 标题标签：\<h1> - \<h6>

- 水平线标签：\<hr>

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

  

最终代码：

```html
<!DOCTYPE htm1>
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



## 样式

### CSS引入方式：

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

![颜色表示形式](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401032147666.webp)



改标题颜色，最终代码：

```html
<!DOCTYPE htm1>
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
<!DOCTYPE htm1>
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
<!DOCTYPE htm1>
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

### CSS选择器

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
<!DOCTYPE htm1>
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
<!DOCTYPE htm1>
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
<!DOCTYPE htm1>
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
<!DOCTYPE htm1>
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

