---
title: Valine 评论系统保活
copyright: true
description: 白嫖党的胜利
sticky: 
date: 2020-05-25 17:43:21
tags: [教程, 白嫖]
categories: 教程
cover: /images/lean/cover.jpeg
---

Valine 评论系统需要 LeanCloud 的云引擎作为支持，但是 LC 的限流措施让 <font color=grey>~~白嫖版~~</font> Valine运行断断续续，热心网友们也想出了不少办法。
> LeanCloud官方文档：
> 体验实例在进行部署等管理操作时会暂停服务；同时**体验实例会执行休眠策略**，没有请求时会休眠***（约半个小时后）***，有请求时启动（首次启动可能需要十几秒的时间），**每天最多运行 18 个小时**。

我在这里列出几个有效的方法。

# 1. 钞能力
<font color=grey>~~Pony Ma 曾经说过，没有什么是💰解决不了的，如果有，那就加大力度~~</font>
每天几块钱，就可以让实例全天运行，没有流控、没有限时。不过对于白嫖玩家来说，氪金是不可能的，一辈子都不会氪金的。

# 2. 定时任务
在实例设置里设置两个定时任务，一个叫```self_wake```，一个叫```resend_mails```。两种方法：
* 可以设置 Cron 表达式，好处是可以设置运行区间，不过容易跟别人的撞车。
* 也可以设置间隔时长，以秒为单位。随意设置，别让运行时间超过免费版的每天限制就行。
![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.2/images/lean/autowake.jpg)

这种方法目前不太行，LeanCloud 加强了流控。

# 3. UptimeRobot

此方法适用于使用国际版 LC，设置了独立主机域名的玩家。
![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.2/images/lean/域名1.jpg)
![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.2/images/lean/域名2.jpg)
Uptime Robot（简称UR）的作用，简单来说就是**存活测试**，看网站是否正常运行。
而 LC 云引擎的运行策略是，如果主机域名被访问了，实例就会启动，半个小时无活动之后再关闭。
* 注册一个 UR 账号
* 给你的**后台网址**添加一个监视器
* 设置检查时间间隔

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.2/images/lean/ur.jpg)
但是超过每天的时间上限之后就会出现 Bad Request，而且这个没法设置运行区间，所以记得把时间弄明白。

# Wake LeanCloud
目前为止最有效的方案，用 GitHub Workflow 实现定时唤醒。我试了一下，好像有用。
https://github.com/blogimg/WakeLeanCloud