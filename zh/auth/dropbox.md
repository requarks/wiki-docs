---
title: Dropbox
description: 身份验证模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:13.852Z
---

Dropbox是一个文件托管服务，提供云存储、文件同步、个人云和客户端软件。
https://www.dropbox.com

# 配置
## A) 创建一个 OAuth 应用

1. 访问 https://www.dropbox.com/developers/apps
1. 点击 **创建应用**
1. 选择 **Dropbox API** 和访问类别为 **App folder**
1. 为您的应用起名， 如： `Wiki.js` ，并点击 **创建应用**
1. 复制 **应用key** 和 **应用secret**的值，供后续使用。
1. 保持此页面打开，供后续添加更多设置。

## B) 在Wiki.js中启用Dropbox登录策略

1. 在您wiki的**管理区**，点击左侧导航栏中的**身份验证**。
1. 点击**Dropbox**.
1. 输入之前复制的**应用key** 和 **应用secret**的值。
1. 启用 **开放注册** *(除非你想人工验证每一个用户)*.
1. 选择新用户首次登录时会被分配到的**用户组**。
1. 确保登陆策略列表中**Dropbox**旁边的复选框为已勾选状态，对应的文本现在应该提示此策略处于**启用**状态。
1. 点击此页右上角的 **应用** 来保存并应用配置。

## C) 在Dropbox中输入允许的endpoints

回到之前打开的Dropbox应用面板，你将需要输入**跳转URI**。这个值可以在您Wiki中Dropbox配置下方的**配置参考**下找到。

填写完毕后，点击**添加**按钮. 作为可选选项，建议您填写**品牌识别**一栏的信息以便终端用户识别。

![](https://static.requarks.io/logo/dropbox.svg =x50){.align-abstopright}
