---
title: 在移动设备上进行 Hexo 博客编辑和部署
copyright: true
date: 2020-05-10 10:09:12
tags: [博客, 教程]
categories: 教程
description: "在任何地方接续你的工作"
sticky: 
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
> 获取完成后可以用Termux操作，但是无法用文件管理器看到。

本文资料来自：华为平板 M6
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

### 设置默认用户信息
设置默认的账户名、邮箱和密码

```bash
$ git config --global user.name "xxx"
$ git config --global user.email "xxx@xmail.com"
$ git config --global user.password "6666666"
```

如果对账号安全不放心，可以不设置密码，在部署和备份的时候手动输入。
### 在托管平台登记密钥
先生成一个SSH密钥。邮箱填自己GitHub或Coding或其他托管平台的注册邮箱。

```bash
$ ssh-keygen -t rsa -C "xxx@xmail.com"
```

输入完成后一路回车，如果对文件安全不放心就在“密码” 那一步设置一个加密密码。
生成密钥信息：

```bash
$ cat ~/.ssh/id_rsa.pub
```

之后程序会生成一个名为"id_rsa.pub"的文件，默认保存在`/files/.ssh/`文件夹，可以手动查看，或者直接复制程序输出的一串密钥。
打开托管平台，在**个人设置里**新建一个SSH公钥，以Coding为例：
![Create new SSH key](/images/deploy-on-mobile/SSH.jpg)

> 注：Coding的公钥分为两种类型，在个人设置里的是**全局公钥**，可以编辑你的所有项目；在每个项目设置里还有单独的SSH私钥，仅对该项目有效。

接下来在设备上“注册”密钥并检查可用性：

```bash
$ ssh -T git@e.coding.net
Warning: Permanently added the RSA host key for IP address '118.xx.xxx.252' to the list of known hosts.
Coding 提示: Hello 艾诺迪亚, You've connected to Coding.net via SSH. This is a personal key.
艾诺迪亚，你好，你已经通过 SSH 协议认证 Coding.net 服务 ，这是一个个人公钥.
公钥指纹：a3:9c:70:xx:xx:xx:xx:xx:xx:xx:xx:72:1e:fe
```

如果出现以上提示则说明成功。GitHub使用``ssh -T git@github.com``即可。

> 6/25 更新：
> 手机端的密钥不好用，容易出错，实际上用 Coding 令牌更方便。
> 进入 Coding 个人设置，进入“访问令牌”，记住自己的令牌用户名（图中红色涂抹区域）
> ![Coding 个人设置页](/images/deploy-on-mobile/coding-auth.jpg)
> 点击“新建令牌”，名字任意取，权限勾选第一条 "*project:depot*" ，也就是完整的仓库控制权限。
> 点击“创建令牌”，<font color=red>复制接下来出现的密钥，它只会出现一次。</font>
> 回到你的 Coding 仓库，复制你的仓库地址，形如 "https://e.coding.net/xxx/xxx.git"
> 进入你的博客文件夹，找到 _config.yml，修改你的远程仓库地址为 **"https://用户名:密码@e.coding.net/xxx/xxx.git"**
> 例如你的令牌用户名是 AbCdEfG、密码是 asdfghj，那么地址就是 "https://AbCdEfG:asdfghj@e.coding.net/xxx/xxx.git"
> Git 的配置文件也可以改一下，在 “.git” 文件夹下的 “CONFIG” 文件，自行找到仓库地址，依葫芦画瓢。

## 开始编辑

因为Hexo支持跨平台，所以手机端编辑和部署操作与电脑端基本一致。这里讲一下大概的操作。

### 文件操作

#### 新建博文

```bash
$ hexo new "title"
```

新的文章在 `/source/_posts/title.md`

#### 新建页面

```bash
$ hexo new page title
```

新的页面在`/source/title`，页面文件在`/source/title/index.md`

文件可以手动删除，但是**不建议手动创建，有可能出奇奇怪怪的问题！**

### 生成 | 预览 | 部署

生成、预览、部署：

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

或者使用组合命令：清除缓存、生成、部署 → `hexo clean && hexo g && hexo d`

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

默认生成的远程仓库会被归为 “origin” 。

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

查看当前仓库有哪些分支（前面带 * 的是当前定位的分支，所有的相关操作在这个分支下执行）

```bash
$ git branch -v
*master
backup
```

创建并定位到新分支：

```bash
$ git checkout -b sample
Switched to a new branch "sample"
```

**搜索更新文件**：``git add .``

**提交更新内容**（显示在远程仓库的日志里）：```git commit -m "更新内容"```

**推送**：`git push <简称> <分支>`，如果只有 origin 仓库、设置了默认分支，可以直接 `git push`

Git 可能会要求输入你在托管方的账号密码。如果你有令牌或者密钥，就不需要。

```bash
$ git add .
$ git commit -m "Add new posts & debug"
$ git push origin master
```

### 从远程仓库同步（恢复）

```bash
$ git clone 仓库地址
$ cd 仓库名
$ git clone 主题地址(GitHub) themes/主题名
$ npm install
```



_________________________________________________________

**原作者：[Anotia](https://anotia.top)，转载请标明出处。**

博客：https://anotia.top

------------------------------------

# 参考资料

https://zhuanlan.zhihu.com/p/35668237

https://lanlan2017.github.io/blog/4a95e633/