---
title: Okta
description: Authentication Module
published: true
date: 2023-01-29T13:10:36.921Z
tags: auth, module
editor: markdown
dateCreated: 2023-01-08T10:34:31.005Z
---

Okta可为任意应用提供安全的身份管理和单点登录。

# 配置

## A) 创建Okta应用

1. 在Okta控制面板中，点击顶部导航栏中的**应用**。
1. 点击**添加应用**, 然后点击**创建新应用**。
1. 选择平台为**Web**， 登录方式为**OpenID Connect**。
1. 输入**应用名称** (如： Wiki.js) 并设置应用徽标（可选）
1. 以此格式输入**登录重定向URI**：`https://YOUR-WIKI-DOMAIN/login/okta/callback`
1. 以此格式输入**登出重定向URI**：`https://YOUR-WIKI-DOMAIN/`.
1. 点击**保存**.
1. 一个**客户端ID**和**客户端密钥**将会显示。复制这两项内容，以便后续使用。

## B) 在Wiki.js中启用Okta登录策略

1. 在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**。
1. 点击 **Okta**。
1. 输入之前复制的**客户端ID**和**客户端密钥**的值。
1. 启用 **开放注册** 选项 *(除非您希望人工验证每一个用户)*。
1. 选择用户首次登陆时会被分配到的**用户组**。
1. 确保**Okta**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。

![](https://static.requarks.io/logo/okta.svg =x50){.align-abstopright}