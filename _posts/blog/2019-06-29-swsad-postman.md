---
layout: post
title: 使用Postman测试API接口
categories: [Blog, swsad]
description: Postman使用方法简介
keywords: swsad, Postman
---

在后端开发过程中，常常有需要测试API接口能否正常工作的需要。前端也常常需要测试APiece接口的返回结果，和文档中两相对照。传统的命令行API测试工具curl输入繁琐，无法保存请求历史以及在较难一连串的请求中保持cookie，并且返回结果不够清晰。使用图形化工具 Postman 可以情形明了的展示API的工作以及返回情况，同时具备了小组协作、保存历史以及脚本执行的功能。

## 开始

Postman 的界面非常简单命令。在搜索引擎搜索并进入官网下载。安装、注册后进入使用界面。

![开始界面.png](https://i.loli.net/2019/06/29/5d1721e51291e35927.png)

使用界面非常清晰。您可以在上图标号1处选择要测试的请求方法，在标号2处输入请求的url，点击标号3处以发送请求。当使用POST等方法，需要添加 Request body的时候，您可以点击标号4处，在标号5所示的地方填写JSON数据对应的key-value对。同时，标号6处的Save可以持久化的储存该请求于您的账号中，而标号7处的请求历史则可以看到本地近些天的请求内容，单击即可加载。

## 生成请求集合

![collection.png](https://i.loli.net/2019/06/29/5d1724ddd0f2765576.png)

当您需要测试一系列接口时，首先点击上图1处导航栏的collection项目，并点击标号2处 “New collection”。之后输入该集合的名称及描述后直接点击Create即可。

右键单击生成的 Collection，即标号  3 处，点击 Add Request。

![Add_Request.png](https://i.loli.net/2019/06/29/5d1726331766587292.png)

输入Request的名称描述后点击 Save To...， 即可在该 collection 下看到新的请求。点击该请求，按照 "开始" 中所述更改请求信息，并点击Save，即可保存到 collection 中。

## 生成测试脚本
使用 Postman 可以方便生成API测试脚本。上手容易，并且在脚本执行过程中会保存cookie。

在 collection中 输入好请求的URL并按顺序调整好，如将“登出”设置到“登陆”的URL之后，右键该collection，单击Export，生成Json文件，即测试脚本。

在测试目录通过 node.js 安装 postman 脚本测试工具 newman，您可以根据需求选择 --g --save等参数,：
```sh
$ npm install -g newman
```
要运行脚本文件，输入：
```sh
$ newman run mycollection.json
```
即可由 newman 工具自行执行您创建的测试脚本，并且会将测试结果显示在控制台。

## Team work
小组协作使用 Postman，减轻了前后端沟通压力，省去了每个人各自创建Request的麻烦。推荐使用。

![teamwork.png](https://i.loli.net/2019/06/29/5d172936ebe2f70928.png)

如图，当组长想要创建 Postman 工作小组时，选择页面最上方的My Workspace，在弹出窗口中点击 Team，并点击 Create a team workspace。

![生成Teamspace.png](https://i.loli.net/2019/06/29/5d1729b5306d717832.png)

在该界面中，填入您要邀请人的账号对应的E-mail（或仅仅时E-mail，该用户点击邮件后再进行注册和登陆）。

![Teamspace.png](https://i.loli.net/2019/06/29/5d172a38624c512646.png)

进入Teamspace后，再按照上述步骤生成API测试和测试脚本即可。

## Reference
[Postman docs](https://learning.getpostman.com/docs/postman/launching_postman/installation_and_updates)