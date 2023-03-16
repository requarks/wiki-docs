---
title: 本地登录
description: 身份认证模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: auth, module, 模块, 身份认证
editor: markdown
dateCreated: 2023-01-08T10:34:28.333Z
---

这是Wiki.js的默认内置身份验证模块。

该模块默认启用，且无法禁用。

# 配置
您无需进行任何配置就可使用此身份验证策略。但是，您可以启用其它设置，如开放注册。

There's nothing to configure in order to use this authentication strategy. However, there're extra settings you can enable, such as self-registration.

在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**，然后点击**本地登录**

## 开放注册

如果您启用了**开放注册**选项，用户就可以自行在您的wiki上创建账户。

一般情况下，建议您设置email**后缀白名单**。除非您的wiki完全开放，允许任何人创建账户。输入一个合法的域名并按下<kbd>Enter</kbd>，将其加入白名单。您可以根据需要添加任意多个域名。

请确保为新用户指定首次登录时会被分配到的**用户组**。

点击此页右上角的**应用**以保存并应用设置。

> :warning: 您**必须**配置好SMTP邮件设置（在管理区的**邮件**处）以发送注册邮件。用户只有使用发送到其电子邮件地址的链接验证其帐户后才能登录。
{.is-danger}