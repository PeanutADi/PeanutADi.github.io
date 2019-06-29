---
layout: post
title: 提高团队协作效率
categories: Blog
description: Using rarious tools to promote teamwork efficiency
keywords: swsad, github issue
---

这是我第一次参加这样一个过程相对完善规范、持续时间相对较长的项目。在项目过程中，我发现如下团队协作工具可以有效提高团队工作效率：

## Github Issues

仓库的Issue在这里不仅可以提出疑问，也可用于前后端交流窗口。前后端有Bug或需要什么接口时，如果在社交媒体沟通很容易就被大量的消息刷过去了。使用Issue并标明优先级等是一种合理的沟通方式。

另一方面，Issue还可用于分发细分的任务。比如某个组件的开发、某个逻辑的完善，使用Issue更简单明了，相关问题也可以在Issue中更新回复。

## 腾讯 / 石墨文档

使用Github更新Readme或API接口文档时常常会出现同时编辑的情况，那么在Merge时不慎就会出现Conflicts。使用腾讯文档在线协同编辑时所有用户看到的界面都是一样的，即它是实时更新的。虽然腾讯文档不能用于编辑Markdown，在编写用户手册等doc文档时十分方便。

## Git Bash SSH

使用Git bash自带的ssh功能，小组成员均可连接服务器进行部署等操作。

对服务器的数据库使用SSH做转发后，即使不是服务器的拥有者也可以查看、编辑云端数据库信息。

## Linux Screen命令

使用Screen命令可以同时连接多个本地或远程的命令行会话，并在其间自由切换。

**GNU Screen**是一款由GNU计划开发的用于命令行终端切换的自由软件。

假如后端增加了ssl与前端链接，那么在本地测试后端就是不可行的了，除非也申请一个ssl证书。但是团队开发过程中后端的小组成员经常有测试或查看log的需求，那么通过ssh链接到服务器后，服务器管理者再为他们分别开不同的screen即可测试。

### Reference：

[Linux Screen命令详解](https://www.cnblogs.com/yangliheng/p/6173530.html)