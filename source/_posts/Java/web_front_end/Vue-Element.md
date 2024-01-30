---
title: Vue-Element
date: '2024-01-03 15:49'
tags: Java
categories:
  - Java
  - Web前端
abbrlink: 2

---
# Vue-Element

## 1. Ajax

概念：Asynchronous JavaScript And XML，异步的JavaScript和XML。

作用：

- 数据交换：通过Aiax可以给服务器发送请求，并获取服务器响应的数据

  ![image-20240112094528549](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162217336.webp)

- 异步交互：可以在不重新加载整个页面的情况下，与服务器交换数据并更新部分网页的技术，如:搜索联根、用户名是否可用的校验等等。

  ![image-20240112094546788](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162218801.webp)



其中同步与异步：	

同步：必须等待浏览器全部加载完成，才能进行后续请求。	![image-20240112094750863](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252951.png)

### 1.1 原生的Ajax请求

![image-20240112103011444](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252952.png)

### 1.2 Axios

Axios 对原生的Ajax进行了封装，简化书写，快速开发。

**作用：**可以在vue生命周期的mounted函数中发送请求，获取页面展示数据。

官网：https://www.axios-http.cn/

入门：

1. 引入Axios的js文件
2. 使用Axios发送请求，比国内获取响应结果。



Axios请求方式别名

- axios.get(url[, config])
- axios.delete(url[, config])
- axios.post(url[ datal, config]])
- axios.put(url[ datal, config]])

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajax-Axios</title>
    <script src="js/axios-0.18.0.js"></script>
</head>
<body>
    
    <input type="button" value="获取数据GET" onclick="get()">

    <input type="button" value="删除数据POST" onclick="post()">

</body>
<script>
    function get(){
        //通过axios发送异步请求-get
        // axios({
        //     method: "get",
        //     url: "http://yapi.smart-xwork.cn/mock/169327/emp/list"
        //  箭头函数
        // }).then(result => {
        //     console.log(result.data);
        // })


        axios.get("http://yapi.smart-xwork.cn/mock/169327/emp/list").then(result => {
            console.log(result.data);
        })
    }

    function post(){
        //通过axios发送异步请求-post
        // axios({
        //     method: "post",
        //     url: "http://yapi.smart-xwork.cn/mock/169327/emp/deleteById",
        //     data: "id=1"
        // }).then(result => {
        //     console.log(result.data);
        // })

        axios.post("http://yapi.smart-xwork.cn/mock/169327/emp/deleteById","id=1").then(result => {
            console.log(result.data);
        })
    }
</script>
</html>
```



### 1.3 案例

数据动态加载，浏览器加载，自动展示数据。mounted（）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajax-Axios-案例</title>
    <script src="js/axios-0.18.0.js"></script>
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app">
        <table border="1" cellspacing="0" width="60%">
            <tr>
                <th>编号</th>
                <th>姓名</th>
                <th>图像</th>
                <th>性别</th>
                <th>职位</th>
                <th>入职日期</th>
                <th>最后操作时间</th>
            </tr>

            <tr align="center" v-for="(emp,index) in emps">
                <td>{{index + 1}}</td>
                <td>{{emp.name}}</td>
                <td>
                    <img :src="emp.image" width="70px" height="50px">
                </td>
                <td>
                    <span v-if="emp.gender == 1">男</span>
                    <span v-if="emp.gender == 2">女</span>
                </td>
                <td>{{emp.job}}</td>
                <td>{{emp.entrydate}}</td>
                <td>{{emp.updatetime}}</td>
            </tr>
        </table>
    </div>
</body>
<script>
    new Vue({
       el: "#app",
       data: {
         emps:[]
       },
       mounted () {
          //发送异步请求,加载数据
          axios.get("http://yapi.smart- xwork.cn/mock/169327/emp/list").then(result => {
            this.emps = result.data.data;
          })
       }
    });
</script>
</html>
```





## 2. 前后端分离开发

![image-20240112105736018](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252953.png)





YApi介绍:

YApi 是高效、易用、功能强大的 api 管理平台，旨在为开发、产品、测试人员提供更优雅的接口管理服务.

地址: [YApi Pro-高效、易用、功能强大的可视化接口管理平台](https://yapi.pro/)



## 3. 前端工程化

### 3.1 环境准备

Vue项目-创建

```
vue ui
```

[Day03-05. 前端工程化-Vue项目_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1m84y1w7Tb/?p=38&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)



vue项目的目录结构

![image-20240115092029047](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252954.png)

首先执行的是index文件，index引用main，main引用APP.vue，最终App.vue的讲集成在index的div中。

![image-20240116110712585](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162226520.webp)



### 3.2 Vue开发流程

[Day03-06. 前端工程化-Vue项目开发流程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1m84y1w7Tb/?p=39&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)

### 3.3 API风格

[实战篇-48_工程化_vue的api风格_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV14z4y1N7pg?p=60&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)

![image-20240116111403914](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252955.png)

### 3.4 代码优化

  请求函数集合在js中

[实战篇-50_工程化_案例代码优化01_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV14z4y1N7pg?p=62&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)

## 4. Element

### 4.1 什么是element

Element:是饿了么团队研发的，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库.

组件:组成网页的部件，例如 超链接、按钮、图片、表格、表单、分页条等等

官网: https://element.eleme.cn/#/zh-CNListener

![html标签构建的网页对比element组件](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252956.png)

### 4.2 快速入门

![image-20240115112819868](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162252957.png)

1. 工程文件右键打开终端,执行指令安装elementUI组件库.
2. 打开element官网-快速上手,引入组件库到main.js
3. 在views文件夹下,新建element文件夹,存放后面要使用的组件.新建组件ElementVue文件,在官网找到需要的组件复制进去.
4. 在主vue文件App.vue中引入ElementVue组件.

### 4.3 常见组件

在官网中查找复制改造即可

```html
<template>
  <div>
    <!--  button按钮 -->
    <el-row>
      <el-button>默认按钮</el-button>
      <el-button type="primary">主要按钮</el-button>
      <el-button type="success">成功按钮</el-button>
      <el-button type="info">信息按钮</el-button>
      <el-button type="warning">警告按钮</el-button>
      <el-button type="danger">危险按钮</el-button>
    </el-row>
    <br />
    <!-- 表格 -->
    <el-table :data="tableData" style="width: 100%">
      <el-table-column prop="date" label="日期" width="180"> </el-table-column>
      <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
      <el-table-column prop="address" label="地址"> </el-table-column>
    </el-table>

    <!-- 分页 -->

    <!-- 加入时间监听： 页码大小和当前页变动时触发函数 -->
    <el-pagination
      background
      layout="total, sizes, prev, pager, next, jumper"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :total="1000"
    >
    </el-pagination>
    <br />
    <br />
    <br />
    <br />


    <!-- dialog对话框:Table：通过dialogTableVisible控制dialog的隐藏与否。默认隐藏，点击显示 -->
    <el-button type="text" @click="dialogTableVisible = true">打开嵌套表格的 Dialog</el-button>

    <el-dialog title="收货地址" :visible.sync="dialogTableVisible">
      <el-table :data="gridData">
        <el-table-column property="date" label="日期" width="150"></el-table-column>
        <el-table-column property="name" label="姓名" width="200"></el-table-column>
        <el-table-column property="address" label="地址"></el-table-column>
      </el-table>
    </el-dialog>

    <br />
    <br />
    <br />
    <br />

    <!-- dialog对话框: form表单 -->
    <el-button type="text" @click="dialogFormVisible = true">打开嵌套表单form的 Dialog</el-button>
    <el-dialog title="form表单" :visible.sync="dialogFormVisible">

      <el-form ref="form" :model="form" label-width="80px">
        <el-form-item label="活动名称">
          <el-input v-model="form.name"></el-input>
        </el-form-item>

        <el-form-item label="活动区域">
          <el-select v-model="form.region" placeholder="请选择活动区域">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="活动时间">
          <el-col :span="11">
            <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
          </el-col>
          <el-col class="line" :span="2">-</el-col>
          <el-col :span="11">
            <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
          </el-col>
        </el-form-item>

        <el-form-item label="即时配送">
          <el-switch v-model="form.delivery"></el-switch>
        </el-form-item>

        <el-form-item label="活动性质">
          <el-checkbox-group v-model="form.type">
            <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
            <el-checkbox label="地推活动" name="type"></el-checkbox>
            <el-checkbox label="线下主题活动" name="type"></el-checkbox>
            <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>

        <el-form-item label="特殊资源">
          <el-radio-group v-model="form.resource">
            <el-radio label="线上品牌商赞助"></el-radio>
            <el-radio label="线下场地免费"></el-radio>
          </el-radio-group>
        </el-form-item>

        <el-form-item label="活动形式">
          <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="onSubmit">提交</el-button>
          <el-button>取消</el-button>
        </el-form-item>
    </el-form>

    </el-dialog>


      


  </div>
</template>


 <script>
export default {
  data() {
    return {
      form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },

      gridData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }],
        dialogTableVisible: false,
        dialogFormVisible: false,

      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],

    };
  },
  methods: {
    onSubmit() {
        alert(JSON.stringify(this.form));
      },
    handleSizeChange: function (val) {
      alert("监听到了每页页码数改变，值为：" + val);
    },

    handleCurrentChange: function (val) {
      alert("监听到了当前页码改变，值为：" + val);
    },
  },
};
</script>

<style>
</style>


```



### 4.4 案例

[Day03-12. Element-案例-基本页面布局_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1m84y1w7Tb?p=45&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)





## 5. 路由

![image-20240115165626234](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162149055.webp)

可以使用官方提供的插件vue router

![image-20240115165854984](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202401162203559.webp)

[Day03-15. vue路由_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1m84y1w7Tb?p=48&spm_id_from=pageDriver&vd_source=da2dcfc57a98c16123113fae8847b6b3)
