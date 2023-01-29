---
title: Discord
description: 身份验证模块
published: true
date: 2023-01-29T08:46:06.048Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:11.093Z
---

Discord是一种流行的游戏交流工具。
https://discordapp.com/

# 配置

## A) 在Discord上创建应用

1. 访问 [Discord 开发者门户](https://discordapp.com/developers/applications/)。 您需要拥有一个账号才可以继续。
1. 点击 **新应用** 并输入一个 **应用名称** (如：Wiki)。点击 **创建**。
1. 复制 **客户端ID** 和 **客户端密钥**的值，供后续使用。

## B) 在Wiki.js上启用Discord登陆策略

1. 在您wiki的 **管理区**，点击左侧导航栏中的**身份验证**。
1. 点击**Discord**。
1. 输入之前复制的 **客户端ID** 和 **客户端密钥** 的值。
1. 启用 **开放注册** *（除非你想人工验证每一个用户）*.
1. 选择新用户首次登录时会被分配到的 **用户组**。
1. 确保**Discord**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。

## C) 在Discord中输入OAuth2设置
回到Discord开发者门户，你将需要设置跳转URI。在应用页面中，点击左侧边栏中的**OAuth2**并添加回调跳转URI。您可以在Wiki.js中Discord登陆策略下的**配置参考**中中找到要填入的值。

填写完成后，点击页面底部的 **保存更改** 按钮。

虽然设置应用徽标是可选的, 但仍然推荐设置一个**应用徽标**以便最终用户识别。

![](https://static.requarks.io/logo/discord.svg){.align-abstopright}
