---
title: Slack
description: 身份验证模块
published: true
date: 2023-03-16T08:45:000Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:36.683Z
---

Slack是一个基于云的专有团队协作工具和服务。
[slack.com](https://slack.com)

# 配置

## A) 创建Slack应用

1. 如果还未创建工作区，请在[Slack](https://slack.com/)上为您的组织创建一个工作区。
1. 转到[您的应用](https://api.slack.com/apps?new_app=1)页面来新建应用。
1. 输入一个**应用名称** (如：Wiki) 并选择您的工作区。
1. 点击**创建应用**.
1. 应用创建完成后，点击左侧边栏中的**OAuth与权限**。
1. 在**范围**部分, 选中以下范围:
	- `identity.avatar` - *查看用户的Slack头像*
  	- `identity.basic` - *确认用户身份*
  	- `identity.email` - *查看用户的email地址*
1. 点击左侧边栏中的**基本信息**。
1. 在**应用凭据**部分, 复制**客户端ID** 和 **客户端密钥** 的值，供后续使用。

## B) 在Wiki.js中启用Slack登录策略

1. 在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**。
1. 点击 **Slack**。
1. 输入之前复制的**客户端ID**和**客户端密钥**的值。
1. 输入**团队 / 工作区 ID**. (例： 如果您的地址是**acme**.slack.com, 您就需要输入**acme**)
1. 启用 **开放注册** 选项 *(除非您希望人工验证每一个用户)*。
1. 选择用户首次登陆时会被分配到的**用户组**。
1. 确保**Slack**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。
1. 复制设置下方**回调URL / 重定向URI**的值。

## C) 在Slack上填入允许的endpoint

回到Slack网站上的app页面，点击左侧边栏中的**OAuth与权限**。在 **重定向URL** 部分下， 添加您之前从wiki设置页面复制的重定向URL，完成后点击**保存URL**按钮。

作为可选选项，建议您在 **基本信息** > **显示信息** 下设置应用描述和徽标，便于最终用户识别。

最后，点击顶部的**将应用安装至工作区**按钮来在您的工作区上授权应用。

![](https://static.requarks.io/logo/slack.svg =x50){.align-abstopright}
  