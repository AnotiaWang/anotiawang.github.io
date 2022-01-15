---
title: Dr.com 一键登录脚本
copyright: true
description: '使用 Python 编写的一个小脚本，自动登录校园网。'
comments: true
date: 2021-12-14 13:55:34
tags: Python, Drcom
categories: 教程
sticky: false
top_img:
cover:
published:
---

# Dr.com 一键登录脚本

>  By [AnotiaWang](https://github.com/AnotiaWang) ，最后修改：2022.1.10

## 介绍

发现登录校园网操作的本质是给认证服务器发送请求，遂用 Python 写了个一键登录校园网的脚本，测试过 **WLAN 和宽带都可以使用**。除了没有 GUI，其它方面都完爆宽带认证客户端好吧。涉及知识点比较简单，手法拙劣勿怪（

我用 PyInstaller 打包好了一份 Windows 的程序，可以直接拿来用，本地有 Python 环境即可。账号密码会存在 .exe 文件同目录下的 secrets.d 文件，~~明文保存~~，建议把程序妥善放在其它盘里，然后拉一个快捷方式到桌面。如要修改账号密码，可以直接编辑 secrets.d 文件，也可以删了再运行程序，重新生成。

SZUer 不骗 SZUer，请放心使用。如果嫌交互式麻烦~~（只有数据文件有问题才会提示交互，不会吧不会吧）~~或者有其他顾虑，也可以把 login 函数的内容扒出来，把自己账号密码写死然后打包一份。打包命令是 `pyinstaller -F --hidden-import=pywintypes 文件名` 。

## 原理

抓包分析

### 登录

向 `http://172.30.255.42:801/eportal/portal/login` 发送 POST 请求，包含以下参数（实际只有前两个为必选）：

- `user_account`: 校园卡号
- `user_password`: 校园网登录密码
- `callback`: 大概是楼栋代码吧
- `login_method`: 未知
- `wlan_user_ip`: 客户端的内网 IP 地址
- `wlan_user_ipv6`: 空值
- `wlan_user_mac`: 一串 0
- `wlan_ac_ip`: 空值
- `wlan_ac_name`: 空值
- `jsVersion`: JS Version
- `terminal_type`: 未知
- `lang`: 语言（`zh`）
- `v`: 未知

服务器返回一串数据，形如：`callback[{result: 0, ret_code: 0, msg: '登录成功'}]`，具体几种情况抓包即可，这里不赘述。

### 登出

比登录简单多了，直接一个 `GET http://172.30.255.42:801/eportal/portal/logout`

## 下载

[蓝奏云](https://anotia.lanzouy.com/ie17Oyshr1c)
