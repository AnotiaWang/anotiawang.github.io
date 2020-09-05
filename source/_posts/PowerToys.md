---
title: PowerToys - 低调的神器
copyright: true
description: '微软推出的鲜为人知的工具，提高了Windows不少实用性。'
sticky: 
date: 2020-05-16 11:54:38
tags: [分享]
categories: 分享
comments: true
cover: https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/cover.jpg
---

尽管Windows占有PC市场的半壁江山，但它的特色功能一直是平淡无奇，没有多少亮点，只是默默跟着大势。反观Mac，从一开始就因为一些令人眼前一亮的设计十分讨喜。

然而前段时间，~~微软~~巨硬的一款软件开始**重新**进入人们的视线，那就是“PowerToys”。

![Power Toys的logo](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/cover.png)

为什么是“重新”？

微软曾经在Windows 95时代就开发出了这个软件，作为系统工具使用，但是后来抛弃了它，直到去年底才重新开始更新。

这次的PowerToys有这些亮点：

* FancyZone 窗口布局
* Shortcut Guide 快捷键速览
* PowerRename 批量重命名
* 扩展的文件预览
* 一键重设图片尺寸

官网：https://github.com/microsoft/PowerToys

PowerToys的设置界面有详细的配置（英文）。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/settings.png)

安装后，PowerToys会在后台运行，系统托盘显示图标。**对应的操作通过右键菜单完成。**

# FancyZone

顾名思义，它能一键设置窗口布局。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/FancyZone.png)

在拖拽窗口的时候按住Shift，就会显示出窗口布局位置，直接拖动到相应的位置即可放置。

按住`` Win+` ``配置布局方式。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/FancyZoneSettings.png)

可以手动设置的选项：

* 覆盖Windows自带的热键；
* 当分辨率改变时保持窗口布局；
* 当新的布局生效时，自动编排窗口到新的布局模式；
* 记忆每个应用上一次的窗口位置；
* 在当前/全部显示器上显示布局网格；
* 示意区域的颜色可以调节。

# Shortcut Guide

Windows有丰富的快捷键，但是要花不少时间去学习和记忆。PowerToys提供了一个向导，长按Windows键就会弹出与其相关的快捷键。默认的呼出时值是900毫秒，根据自己的需要调整。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/startmenu.png)

# PowerRename

给文件批量重命名的工具，应该不用多说🤪

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/PowerRename.png)

# Preview Panes

实际上是一个扩展，增加了文件资源管理器中可以在侧边栏预览的文件格式，新增了Markdown (.md) 和 SVG (.svg)。

在文件管理器的**顶栏 - 查看 - 预览窗格**启用预览就行。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/PreviewPanes.png)

>  我这里的图片使用了相对路径，所以有显示错误提示

# Images Resizer

这个功能其实在Microsoft Office里有，微软把它拎出来做了一个单独的功能，根据需要在哪种设备上显示，压缩图片尺寸，从而节约大小。

![](https://cdn.jsdelivr.net/gh/AnotiaWang/jscdn@1.0.0.7/images/blog/PowerToys/Resizer.png)

# 其他配置

* 应用支持浅色和深色主题，可以根据系统自动切换；
* 可以开机启动、以管理员模式启动；
* 每一个功能都有演示页面（会打开相应的GitHub链接）

------------------------

工具可以在微软的[GitHub Release](https://github.com/microsoft/PowerToys/releases)页下载到。

> 封面图片来自PowerToys GitHub页面，PowerToys的图标来自网络。