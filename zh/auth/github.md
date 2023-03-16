---
title: GitHub
description: 身份验证模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:16.712Z
---

GitHub Inc. 是一个基于web的托管服务，用于使用Git进行版本控制。

# 配置

## A) 创建 OAuth GitHub 应用

1. 转到GitHub上的[新建OAuth应用](https://github.com/settings/applications/new)页。
   - 你也可以进入您组织的设置页面，点击`OAuth应用`，然后点击`新建OAuth应用`，以您组织的身份（而不是您个人账户的身份）创建OAuth应用。
1. 输入**应用名称** （如：Wiki.js）
1. 输入您wiki的 **主页地址**。
1. 输入 **身份验证回调地址**。  
	这个值可以在您Wiki中GitHub配置下方的**配置参考**下找到。
1. 点击**注册应用**.
1. 一个**客户端ID**和**客户端密钥**将会显示。复制这两项内容，以便后续使用。
1. *(可选)*{.caption} 为创建的应用上传一个图标。

## B) 在Wiki.js中启用GitHub登录策略

1. 在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**。
1. 点击 **GitHub**。
1. 输入之前复制的**客户端ID**和**客户端密钥**的值。
	> **对GitHub Enterprise用户的专门说明：您需要：**
		> - 打开 **使用 GitHub Enterprise** 的开关。
  	> - 输入你的 **GitHub Enterprise 域名** *(不含http/https前缀及末尾的斜杠, 如： github.yourdomain.com)*
    > - 输入你的 **GitHub Enterprise 用户Endpoint** *(如： https://api.github.yourdomain.com)*
    {.is-info}
1. 启用 **开放注册** 选项 *(除非您希望人工验证每一个用户)*。
1. 选择用户首次登陆时会被分配到的**用户组**。
1. 确保**GitHub**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。

![](https://static.requarks.io/logo/github.svg =x50){.align-abstopright}
