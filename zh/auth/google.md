---
title: Google
description: 身份验证模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:19.798Z
---

谷歌专注于互联网相关服务和产品，包括在线广告技术、搜索引擎、云计算、软件和硬件。
[Google Cloud Console](https://console.developers.google.com/)

# 配置

## A) 创建 Google Cloud 项目

1. 打开 [Google Cloud Console](https://console.cloud.google.com/) 并创建一个新项目 *(如果还没有创建)*.
1. 在左侧边栏中,点击 **API与服务**.
1. 点击最上方的 **启用API与服务**
1. 点击**Google+ API** 并启用.
1. 在左侧边栏中，将鼠标悬停在**API与服务**上，然后在子菜单中选择**凭据**。
1. 点击蓝色的 **创建凭据** 按钮并选择 **OAuth客户端ID**.
1. 选择应用类型为**Web应用**.
1. 为应用起一个合适的名字 *(如: Wiki.js)*
1. 暂时将其他字段留空,待稍后填写
1. 点击 **创建** 就能看到 **客户端ID** 和 **客户端密钥**. 复制这两个键的值,供稍后使用

## B) 在Wiki.js中启用Google登录策略

1. 在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**。
1. 点击 **Google**。
1. 输入之前复制的**客户端ID**和**客户端密钥**的值。
1. 启用 **开放注册** 选项 *(除非您希望人工验证每一个用户)*。
1. 选择用户首次登陆时会被分配到的**用户组**。
1. 确保**Google**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。

## C) 在Google中输入允许的endpoints

回到Google Cloud Console上的**凭据** 页面, 单击之前创建的OAuth客户端旁边的编辑图标。

在 **已授权的JavaScript源** 内输入您wiki的域名.

在**授权重定向URI**中输入重定向URI（位于Wiki.js中Google策略设置下方的**配置参考**下）

点击 **保存**.

## D) 设置OAuth授权界面

在上一步打开的凭据页面, 点击**OAuth授权界面**选项卡.

填入需要的名称、徽标、email等。

在**Google API范围**中，确保覆盖以下范围
- email
- profile
- openid

在**已授权域**中，确保您wiki的域名已被列出。

![](https://static.requarks.io/logo/google.svg =x50){.align-abstopright}
  