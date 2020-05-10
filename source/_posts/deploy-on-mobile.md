---
title: 在移动设备上进行 Hexo 博客编辑和部署
copyright: true
date: 2020-05-10 10:09:12
tags: [博客, 教程]
categories: 教程
description: "我不是鸽王！"
sticky: 1
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

> 我找资料的时候发现没有root的手机也有[解决办法](https://zhuanlan.zhihu.com/p/35668237)，在此列出作为参考：
>
>  先执行```$ pkg install proot```，然后执行 ```$ termux-chroot``` 就可以模拟出root权限。详情见链接↑
>
> 获取完成后就可以用Termux编辑，但是无法用文件管理器看到。

## 配置环境

### 初始化

`$ apt update`

``$ apt upgrade``

### 安装 node.js

```bash
$ apt install nodejs-lts
```

此处安装的是<u>长期支持版</u>，因为node.js的最新版在博客generate时容易出现如下错误：

~~~bash
TypeError [ERR_INVALID_ARGTYPE]: The "mode" argument mast be integer. Received an instance of Object
~~~

[👉nodejs新版的报错截图👈](/images/deploy-on-mobile/error-node-too-new.jpg)

![](/images/deploy-on-mobile/install-nodejs.jpg)

### 安装 git

```bash
$ apt install git
```

![](/images/deploy-on-mobile/install-git.jpg)

### 建立博客文件夹

给文件管理器授予root权限；

进入手机根目录，在 ``/data/data/com.termux/files/``新建一个存放博客的文件夹，如“Blog”。

> 或者Termux使用命令：```$ mkdir Blog```直接创建

### 定位到 Blog

```bash
$ cd Blog
```

### 安装 hexo-cli

> 使用淘宝的镜像：```$ npm config set registry http://registry.npm.taobao.org```

**安装Hexo**：```$ npm install hexo-cli -g```

**Hexo初始化**：```$ hexo init```

安装必要组件：```$ npm install```

完成。

>  如果你的博客在git上有备份：
>
>  克隆→定位→安装Hexo→安装组件→安装主题→生成、部署。
>
>  举例：
>
>  ```bash
>  $ git clone https://e.coding.net/xxx/xxx.git
>  $ cd xxx
>  $ npm install hexo --save
>  $ npm install
>  $ git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/Butterfly
>  $ hexo g -s
>  ```
>

## 开始编辑

因为Hexo支持跨平台，所以手机端编辑和部署操作与电脑端基本一致。这里讲一下大概的操作。

### 文件操作

#### 新建博文

```bash
$ hexo new "title"
```

新的文章在 `/source/_posts/xxxxx.md`

#### 新建页面

```bash
$ hexo new page title
```

新的页面在`/source/title`，页面文件在`/source/title/index.md`

文件可以手动删除。

### 生成 | 预览 | 部署

生成、预览、部署

```bash
$ hexo g
INFO  Start processing
INFO  Files loaded in x s
INFO  Generated: xxx
INFO  Generated: xxx
....
INFO  xx files generated in x.x s

$ hexo s
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.

$ hexo d
...
INFO  Deploy done: git
```

或者使用组合命令：

**生成并本地预览：**

```bash
$ hexo s -g
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

**生成并部署：**

```bash
$ hexo d -g
INFO  Start processing
...
INFO  Deploy done: git
```

## 备份与恢复

### 将博客备份到 git（以Coding为例）

如果你的博客文件夹是从git克隆下来的，那么会自动设置远程仓库，不需要手动设置。

输入 ``git remote -v``查看已经存在的远程仓库，应该会有以下提示：

```bash
$ git remote -v
origin  https://e.coding.net/cross-street/Blog.git (fetch)
origin  https://e.coding.net/cross-street/Blog.git (push)
```

默认生成的远程仓库会被归为“origin”类。

#### 设置新的远程仓库

输入`git remote add <简称> <地址>`新增一个远程仓库

```bash
$ git remote add BlogBackup https://e.coding.net/cross-street/xxxxx.git

$ git remote -v
origin  https://e.coding.net/cross-street/Blog.git (fetch)
origin  https://e.coding.net/cross-street/Blog.git (push)
BlogBackup https://e.coding.net/cross-street/xxxxx.git (fetch)
BlogBackup https://e.coding.net/cross-street/xxxxx.git (push)
```

#### 推送到远程仓库

查看当前仓库有哪些分支（前面带*的是当前定位的分支，所有的相关操作在这个分支下执行）

```bash
$ git branch
*master
backup
```

创建并定位到新分支：

```bash
$ git checkout -b sample
Switched to a new branch "sample"
```

搜索更新文件：``git add .``

输入更新内容（显示在远程仓库的日志里）：```git commit -m "更新内容"```

推送：`git push <简称> <分支>`

可能会要求输入你在托管方的账号密码。

```bash
$ git add .
$ git commit -m "Add new posts & debug"
$ git push origin master

```

### 从远程仓库同步（恢复）

```bash
$ git clone 仓库地址
```

恢复的时候别忘了重新安装主题。

_________________________________________________________

**原作者：[Anotia](https://anotiawang.tk)，转载请标明出处。**

原博客：https://anotiawang.tk

------------------------------------

# 参考资料

这个大佬写得非常全面，从准备到部署到debug都有（不是恰饭）：https://zhuanlan.zhihu.com/p/35668237

https://lanlan2017.github.io/blog/4a95e633/