---
title: 在移动设备上进行博客编辑和部署
copyright: true
date: 2020-05-10 10:09:12
tags: 
categories: 教程
description: 
cover: /images/deploy-on-mobile/cover.jpg
---



# 导言

一般来说我们部署博客都是在电脑端，如果出门在外，想要用移动设备进行博客的编辑和部署，应该怎么操作？

### 注意

* Hexo支持跨平台，所以博客的操作基本相同；

* 因为网上已经有很多教程了，我这里就大概讲一下步骤和注意事项😀
* 具体操作因人而异，**请根据自己的状况取舍**，不要全部照抄。

# 正文

## 准备材料

* 一台安卓手机（已 root 且做好防范措施）
* 安装 Termux（前往[官网](https://termux.com/)或者[Google  Play](https://play.google.com/store/apps/details?id=com.termux&hl=zh)下载）
* 能查看系统根目录的文件管理器，如 RE 或 MT 管理器，手机需root。推荐MT
* 【建议】科学上网工具

![Termux 主界面](/images/deploy-on-mobile/termux-1.jpg)

> 我找资料的时候发现没有root的手机也有[解决办法](https://zhuanlan.zhihu.com/p/35668237)，不过我自己没有尝试，在此列出作为参考：
>
>  先执行```$ pkg install proot```，然后执行 ```$ termux-chroot``` 就可以模拟出root权限。详情见链接↑

## 配置环境

### 初始化

`$ apt update`

``$ apt upgrade``

### 安装node.js长期支持版

```
$ apt install nodejs-lts
```

原因：node.js的最新版在博客generate时容易出现如下错误：

~~~
TypeError [ERR_INVALID_ARGTYPE]: The "mode" argument mast be integer. Received an instance of Object
~~~

[nodejs新版的报错截图](/images/deploy-on-mobile/error-node-too-new.jpg)

![](/images/deploy-on-mobile/install-nodejs.jpg)

### 安装 git

```
$ apt install git
```

![](/images/deploy-on-mobile/install-git.jpg)

### 建立博客文件夹

给文件管理器授予root权限；

进入手机根目录，在 ``/data/data/com.termux/files/``新建一个存放博客的文件夹，如“Blog”。

> 或者Termux使用命令：```$ mkdir Blog```直接创建

### 定位到Blog

``` （“Blog”替换成你自己取的名字）
$ cd Blog
```



> 如果你的博客在git上有备份，就直接用``git clone`` 指令克隆，然后```cd 仓库名```，如
>
> ``` $ git clone https://github.com/xxx/xxx.github.io```，克隆到files文件夹下，一个叫做“xxx.github.io”的子文件夹
>
> `$ cd xxx.github.io` 定位到克隆好的文件夹

### 安装 hexo-cli

> 使用淘宝的镜像：```$ npm config set registry http://registry.npm.taobao.org```

**安装Hexo**：```$ npm install hexo-cli -g```

**Hexo初始化**：```$ hexo init```

安装必要组件：```$ npm install```













# 参考资料

