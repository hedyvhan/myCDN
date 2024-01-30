---
title: Vue
date: '2024-01-03 15:49'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 3
---
# Vue

官网: https://v2.cn.vuejs.org/

Vue 是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。

基于**MVVM**(Mqdel-View-ViewModel)思想，实现数据的**双向绑定**，将编程的关注点放在数据上。

![image-20240111093035328](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252443.png)

Model：数据模型，包含了很多业务数据，数据方法。

View：视图层，负责数据的展示，即html页面的标签，可以理解为DOM元素。

ViewModel：View和Model通信的桥梁，通过完成数据绑定，数据改变，视图显示也会改变；视图层数据改变，数据层也会改变。

## 1. Vue快速入门

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-快速入门</title>
    <script src="js/vue.js"></script>
</head>
<body>

    <div id="app">
        <input type="text" v-model="message">
        {{message}}
    </div>

</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
            message: "Hello Vue"
        }
    })
</script>
</html>
```

## 2. Vue的常用指令

![image-20240111095029643](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252444.png)



### 2.1 v-bind

```html
<a v-bind:href="url">绑定指令</a>
//简写：
<a :href="url">绑定指令</a>
```

**v-bind:href 冒号后不能有空格**

### 2.2 v-model

```html
<inut type="text" v-model="url">
```



eg：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-v-bind</title>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">

        <a v-bind:href="url">链接1</a>
        <a :href="url">链接2</a>

        <input type="text" v-model="url">

    </div>
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           url: "https://www.baidu.com"
        }
    })
</script>
</html>
```

两个超链接都指向URL，文本输入框绑定URL接收输入。

通过v-bind或者v-model绑定的变量，必须在数据模型中声明，即在data中声明。

```html
new Vue({
    el: "#app", //vue接管区域
    data:{
       url: "https://www.baidu.com"
    }
})
```

### 2.3 v-on

```html
<input type="button" value="按钮” v-on:click="handle()">
//简写
<input type="button" value="按钮” @click="handle()">
```

​		 eg：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-v-on</title>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">

        <input type="button" value="点我一下" v-on:click="handle()">

        <input type="button" value="点我一下" @click="handle()">

    </div>
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           
        },
        methods: {
            handle: function(){
                alert("你点我了一下...");
            }
        }
    })
</script>
</html>
```

### 2.4 v-if

```html
// 年龄{{age]},经判定为:
<span V-if="age <= 35">年轻人</span>
<span v-else-if="age > 35 && age < 60">中年人</span>
<span V-else>老年人</span>
```



### 2.5 v-show

```html
// 年龄{{age}},经判定为:
<span V-show="age <= 35">年轻人</span>
```

v-if 和v-show的区别：

- v-if条件不成立浏览器不渲染

- v-show浏览器全部渲染，但是通过控制CSS的样式，将display设置为关闭，实现不展示的功能。

eg：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-v-if与v-show</title>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">
        
        年龄<input type="text" v-model="age">经判定,为:
        <span v-if="age <= 35">年轻人(35及以下)</span>
        <span v-else-if="age > 35 && age < 60">中年人(35-60)</span>
        <span v-else>老年人(60及以上)</span>

        <br><br>

        年龄<input type="text" v-model="age">经判定,为:
        <span v-show="age <= 35">年轻人(35及以下)</span>
        <span v-show="age > 35 && age < 60">中年人(35-60)</span>
        <span v-show="age >= 60">老年人(60及以上)</span>

    </div>
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           age: 20
        },
        methods: {
            
        }
    })
</script>
</html>
```

### 2.6 v-for

```html
<div v-for="addr in addrs">{{addr}}</div>

<div v-for="(addr,index) in addrs">{{index + 1}} : {{addr}}</div>


data:{
	...
	addrs:[ ... ]
}
```



eg：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-v-for</title>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">

        <div v-for="addr in addrs">{{addr}}</div>

        <hr>

        <div v-for="(addr,index) in addrs">{{index + 1}} : {{addr}}</div>

    </div>
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           addrs:["北京", "上海", "西安", "成都", "深圳"]
        },
        methods: {
            
        }
    })
</script>
</html>
```





## 3. 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-案例</title>
    <script src="js/vue.js"></script>
</head>
<body>
    
    <div id="table">
        
        <table border="1" cellspacing="0" width="60%">
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>性别</th>
                <th>成绩</th>
                <th>等级</th>
            </tr>

            <tr align="center" v-for="(user,index) in users">
                <td>{{index + 1}}</td>
                <td>{{user.name}}</td>
                <td>{{user.age}}</td>
                <td>
                    <span v-if="user.gender == 1">男</span>
                    <span v-if="user.gender == 2">女</span>
                </td>

                <td>{{user.score}}</td>

                <td>
                    <span style="color: green;" v-if="user.score >= 85">优秀</span>
                    <span style="color: greenyellow;" v-else-if="user.score >= 60">及格</span>
                    <span style="color: red;" v-else>不及格</span>
                </td>

            </tr>

        </table>

    </div>

</body>

<script>
    new Vue({
        el: "#table",
        data: {
            users: [{
                name: "Tom",
                age: 20,
                gender: 1,
                score: 78
            },{
                name: "Rose",
                age: 18,
                gender: 2,
                score: 86
            },{
                name: "Jerry",
                age: 26,
                gender: 1,
                score: 90
            },{
                name: "Tony",
                age: 30,
                gender: 1,
                score: 52
            }]
        },
        methods: {
            
        },
    })
</script>
</html>
```





## 4. 生命周期

生命周期：指一个对象从创建到小会的整个过程。

vue的生命周期八个阶段：每触发一个生命周期时间，会自动执行一个生命周期方法（钩子）。

![image-20240111143322292](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252445.png)



![image-20240111143524319](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252446.png)



其中我们关注**mounted阶段**，在这个阶段挂完成，Vue初始化成功，HTML页面渲染成功。发送请求到服务端，加载数据。

可以在method平级定义一个状态同名函数，当执行到当前状态时，自动执行该函数。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue-指令-v-for</title>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">

    </div>
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           
        },
        methods: {
            
        },
        mounted () {
            alert("vue挂载完成,发送请求到服务端")
        }
    })
</script>
</html>
```

