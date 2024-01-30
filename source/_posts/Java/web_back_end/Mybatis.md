---
typora-copy-images-to: upload
title: MyBatis
tags: Java
categories: 
- Java
- Web后端
description: 描述
comments: 是否开启评论(true or false)
abbrlink: 61918
date: 2023-10-12 16:46:07
---

# MyBatis

## 1.什么是MyBatis？
![](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311222144579.webp)

## 2.MyBatis入门

### 2.1 快速入门

[黑马程序员2023新版JavaWeb开发教程，实现javaweb企业开发全流程（涵盖Spring+MyBatis+SpringMVC+SpringBoot等）](https://www.bilibili.com/video/BV1m84y1w7Tb?p=117&ziyu)

- 图形化工具查询数据库
![ziyunote-20230904_102155_c](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311250038031.webp)
- MyBatis查询数据库

  ![ziyunote-20230904_102259_c](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311250038501.webp)

  ![ziyunote-20230904_102634_c](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311250038016.webp)
重点是3编写SQL语句。

[黑马程序员2023新版JavaWeb开发教程，实现javaweb企业开发全流程（涵盖Spring+MyBatis+SpringMVC+SpringBoot等）](https://www.bilibili.com/video/BV1m84y1w7Tb?p=118&ziyu)


### 2.2 JDBC介绍

### 2.3 数据库连接池

### 2.4 lombok小工具
引入依赖
![ziyunote-20230911_100017](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311250038239.webp)


## 3.MyBatis基础增删改查！！！

![ziyunote-20230911_100058_c](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202311250038861.webp)

```
返回新增员工，会自动将生成的主键值，赋值给emp对象的id属性
@Options (useGeneratedKeys = true,keyProperty = "id")
```

## 4. MyBatis动态XML映射文件

三点规范：

- 同包同名，mapper和xml的包和名字要一样
- namespace是接口mapper的全限定名，在mapper类名右键，copy reference。
- id 是 mapper函数名，通过id来定位执行的函数。如果sql语句是查询，有结果返回，返回的结果的类型resultType为返回的实体类的全限定名。

![image-20231214203048487](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202312142030294.webp)

xml文件有约束，可以去[官方文档-入门](https://mybatis.net.cn/getting-started.html)拷贝。

```xml
约束
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

可以下载mybatisX插件，更加方便的操作xml。

## 5. MyBatis动态SQL

![image-20231214203925550](https://hedy-1321816972.cos.ap-guangzhou.myqcloud.com/img/blog202312142039943.webp)

当查询条件为多个时，只输入一个的话，就查不出来，这时候需要动态来查询。



### 5.1 if标签（where）

**<if>**: 用于判断条件是否成立。使用test属性进行条件判断，如果条件为true，则拼接SQL。

```xml
<if test = "name != null">
	name like concat('%', #{name}, '%')
</if>
-- 如果name 不为null，则拼接后面sql
```

将上述三个条件查询改为动态查询：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.EmpMapper">
	<!--resultType: 单条记录所封装的类型-->
	<select id="list” resultType="com.itheima .pojo.Emp">
		select * 
         from emp 
		where name like concat('%',#{name}，'%') and gender = #{gender} and entrydate between #{begin} and #{end} order by update—_time desc
	</select>
</mapper>
```



改为

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.EmpMapper">
	<!--resultType: 单条记录所封装的类型-->
	    <!--条件查询-->
    <select id="list" resultType="com.hedy.Entity.Emp">
        select *
        from emp
        where
            <if test="name != null and name != '' ">
                name like concat('%', #{name}, '%')
            </if>
            <if test="gender!= null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end!= null">
                entrydate between #{begin} and #{end}
            </if>
        order by update_time desc
    </select>
</mapper>
```

此时，如果没有输入name，输入了gender，sql语句为：where and gender = ...，显然多了一个and。xml使用**<where></where>**动态判断，前一个没有输入，将不会拼接and或者or，全部参数都没有也不会生成where关键字。将上述xml语句再次修改为：

```xml
    <!--条件查询-->
    <select id="list" resultType="com.hedy.Entity.Emp">
        select *
        from emp
        <where>
            <if test="name != null and name != '' ">
                name like concat('%', #{name}, '%')
            </if>
            <if test="gender!= null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end!= null">
                entrydate between #{begin} and #{end}
            </if>
        </where>
        order by update_time desc
    </select>
```



### 5.2 foreach标签

例如需要批量删除

```xml
<!--批量删除员工-->
/*
collection: 遍历的集合
item：元素
separate：分隔符
open/close：遍历前/后拼接的sql片段
*/
<delete id = "deleteById">
    delete
    from emp
    where id in
    <foreach collection="ids" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
</delete>
```



### 5.3 sql-include标签

在查询信息时，一般不推荐使用select *，这样性能比较差。应该将所有字段全部列出来。当多个地方都需要查询这些信息时，复用度比较低。这时可以将这个查询语句封装。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.hedy.Mapper.EmpMapper">
   <!--条件查询-->
    <select id="list" resultType="com.hedy.Entity.Emp">
        select id,username, gender, image, job, entrydate, dept id, create_time, update_time
        from emp
        <where>
            <if test="name != null and name != '' ">
                name like concat('%', #{name}, '%')
            </if>
            <if test="gender!= null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end!= null">
                entrydate between #{begin} and #{end}
            </if>
        </where>
        order by update_time desc
    </select>
    
    <select id="getById" resultType="com.hedy.Entity.Emp">
        select id,username, gender, image, job, entrydate, dept id, create_time, update_time
        from emp
        where id = #{id}
    </select>
    
</mapper>
```

改为

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.hedy.Mapper.EmpMapper">
    
    <sql id = "commonSelect">
    	select id,username, gender, image, job, entrydate, dept id, create_time, update_time
        from emp
    </sql>
    
   <!--条件查询-->
    <select id="list" resultType="com.hedy.Entity.Emp">
        
        <include refid = "commonSelect"/>
        
        <where>
            <if test="name != null and name != '' ">
                name like concat('%', #{name}, '%')
            </if>
            <if test="gender!= null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end!= null">
                entrydate between #{begin} and #{end}
            </if>
        </where>
        order by update_time desc
    </select>
    
    <select id="getById" resultType="com.hedy.Entity.Emp">
        
        <include refid = "commonSelect"/>
        
        where id = #{id}
    </select>
    
</mapper>
```

