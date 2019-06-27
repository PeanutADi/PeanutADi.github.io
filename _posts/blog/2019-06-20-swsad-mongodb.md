---
layout: post
title: MongoDB学习记录
categories: Blog
description: MongoDB learning process
keywords: MongoDB
---

在本学期的一个课程项目中，作为一个后端小白，第一次接触并使用了MongoDB。以下为学习记录。

## MongoDB

MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。

MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。

MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

## 为什么使用MongoDB

本项目中，我们后端使用的是koa框架。koa和mongoDB总是在一起提到，本项目中我们也自然使用了这一数据库。那么MongoDB带来了什么实际的好处呢？

我总结了在我们项目实际使用中MongoDB带来的好处：

- MongoDB 是一个面向文档存储的数据库，操作起来比较简单和容易。查询语言非常强大，增删改查API操作简捷易懂。
- 提供的Compass等可视化工具使用方便。
- 我们项目小组作为一个经验较少的小组，数据库开发不够成熟，经常有数据元素的增删。MongoDB作为NoSQL在这方面十分方便。
- MongoDB可以直接输入和输出JSON文件。
- MongoDB读写操作都非常快，查询后可能是因为：MongoDB使用内存映射存储引擎，把磁盘的IO操作转换成为内存的操作。

**在使用MongoDB中发现的不足**

MongoDB给我们的开发带来了很多便利，但是在开发过程中也遇见了一些问题：即复杂的查询，如Join，无法实现。

## Monk

Monk是提供给koa使用的一个操作MongoDB的组件。

使用Monk提供的API，我们在项目中做到了如下：

- 以中间件的形式使用Monk，符合koa框架编程习惯。
- 通过Monk较为简单的连接MongoDB与koa。
- 使用Monk提供的面向对象接口方便操作MongoDB。

## Joi

Joi是一个Shema组件，可以用于将数据转为对象，或将对象转为Json数据，通过这一组件，实现了数据层与应用层之间的数据交换需要。

例如一个用户的标准格式：

```JavaScript
const userRegSchema = Joi.object().keys({
    username: Joi.string().alphanum().min(3).max(30).trim().required(),
    password: Joi.string().regex(/^[a-zA-Z0-9]{3,30}$/).required(),
    email: Joi.string().email({ minDomainSegments: 2, }).required(),
    phone: Joi.string().regex(/^[0-9]{11}$/).required(),
    nickname: Joi.string().min(2).max(20).trim().required()
});
```

## Reference

### Joi

[Joi](<https://github.com/hapijs/joi>)

### Monk

[Monk](https://automattic.github.io/monk/)

### MongoDB
[MongoDB](https://www.runoob.com/mongodb/mongodb-intro.html)