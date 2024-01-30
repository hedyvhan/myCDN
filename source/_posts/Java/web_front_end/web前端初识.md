---
title: web前端初识
date: '2024-01-03 15:49'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 4
---
# web前端初识

## 1. 标准

为了让不同的浏览器解析渲染得到的网页都相同，需要指定web标准。

三个部分组成：

- HTML：负责网页的结构（页面元素和内容）
- CSS：负责网页的表现（页面元素的外观、位置等页面样式，如:颜色、大小等)
- JavaScript：负责网页的行为 (交互效果）

vue是基于JavaScript的高级框架

## 2. HTML

**超文本标记语言**，hyper Text Markup Language，除了文字信息，还可以定义图片、视频、超链接等内容。

**标记语言**：由标签构成的语言

- HTML标签都是预定义好的。例如: 使用\<a>展示超链接，使用\<img>展示图片，\<video>展示视频。
- HTML代码直接在浏览器中运行，HTML标签由浏览器解析。

主要是常用的标签

### 2.1 快速入门

一个简单的html

![快速入门](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252449.png)

```html
<html>
	<head>
		<title>HTML 快速入门</title>
	</head>    
    <body>    
    	<h1>Hello HTML</h1>
        <img src="1.jpg"/>
    </body>
</html>

```

```html
自闭和：<img src="1.jpg"/>
也可以：<img src="1.jpg"></img>
```

- 语法不区分大小写。
- 属性值可以使用单引号也可以双引号。
- 语法结构比较松散。少一个括号、少了\</html>依旧可以显示，但不推荐。

## 3. CSS

**层叠样式表**，Cascading Style Sheet, 用于控制页面的样式(表现)

主要是常见的样式