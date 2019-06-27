---
layout: post
title: koa学习记录
categories: Blog
description: koa & MongoDB & testing
keywords: swsad, koa, MongoDB, nodejs
---

# 后端小白从零开始之路

## Koa

第一次接触到node.js框架，在这之前从来没用node.js编程…好在同组大佬全程手把手指导开发。
Koa框架拥有很强的兼容性，可以使用node和express的组件，使得开发方便并且弹性强。同时Koa具有轻量化的特点，使用async函数，错误处理简洁。
### 洋葱模型
Koa没有绑定中间件执行，但提供了大量的可选中间件并使用堆栈结构进行函数调用。当级联的下游没有更多的中间件时，堆栈展开且每个中间件执行其上游行为。有大神称其为洋葱模型：
![koa.jpg](https://i.loli.net/2019/06/27/5d14c5741ae7712798.jpg)
使用官网代码作为例子：

```JavaScript
var koa = require('koa');
var app = koa();

// response-time中间件
app.use(function *(next){
  var start = new Date;
  yield next;
  var ms = new Date - start;
  this.set('X-Response-Time', ms + 'ms');
});

// logger中间件
app.use(function *(next){
  var start = new Date;
  yield next;
  var ms = new Date - start;
  console.log('%s %s - %s', this.method, this.url, ms);
});

// 响应中间件
app.use(function *(){
  this.body = 'Hello World';
});

app.listen(3000);
```

那么，请求过程就是：请求进来，先进到response-time中间件，执行 var start = new Date; 然后遇到yield next，则暂停response-time中间件的执行，跳转进logger中间件，同理，最后进入响应中间件，响应中间件中没有yield next代码，则开始逆序执行，也就是再先是回到logger中间件，执行yield next之后的代码，执行完后再回到response-time中间件执行yield next之后的代码。至此，整个Koa的中间件执行完毕 。

### Context

Koa的Context对象将节点的请求和响应对象封装到单个对象中，该对象为编写Web应用程序和API提供了许多有用的方法。
每个 请求都将创建一个 Context，并在中间件中作为接收器引用，或者 ctx 标识符。
可以通过ctx.requeset对象获得请求, ctx.request.body是处理POST请求时常用的API。
ctx.statue可以用于返回状态码。
ctx.body可以用于返还给client的实体。

### 架构设计

这次的项目采用一个完全API化的后端,因为所有前端的页面设计都是承载在微信小程序上,故后端不需要解决静态文件的推送,只需要处理各种逻辑的处理,如管理用户,管理订单,管理任务。
这样的架构就能顺理成章地让某个逻辑的代码落到某个类的的 controller 中,而这个 controller 暴露出其路由,由上层的初始化层进行综合和启动,并插入一些中间件去处理。而 controller 中只包含了每个API所需要的逻辑处理函数,而部分不和API产生直接关联的函数或者中间件,如数据库的初始化,钱包的操作函数,验证请求的 Session 的中间件,这些都放在了对应的 helper 中,这样避免了逻辑混乱和导致非公开函数被恶意调用，同时也实现了后端的解耦。

## MongoDB

MongoDB是我第一次使用的NoSQL，并且安装、使用都十分方便。
NoSQL在使用时不用考虑表格的问题，作为一个数据库设计不那么有经验的团队，我们可能常有属性的增添，MongoDB十分适合。
另一方面，MongoDB能直接导入、导出Json，并且增删改查API简单又易于理解。
但同时，使用MongoDB无法进行Join查询，需要前端自己进行处理又不是很方便。

## Software test

虽然在网上找到了很多用于单元测试的框架，但对于我们这种大量调用中间件的接口测试逻辑太过麻烦，代价太大，所以在写了几个单元测试之后决定只使用Postman提供的 newman 脚本测试工具进行接口测试。

newman进行测试比较简单，在Postman中输入好需要测试的url和http方法即可自动生成。在命令行中利用newman工具即可进行测试。