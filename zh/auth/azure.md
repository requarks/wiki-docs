---
title: Azure Active Directory
description: 身份验证模块
published: true
date: 2023-01-29T08:46:29.108Z
tags: auth, module, 身份验证, 模块
editor: markdown
dateCreated: 2023-01-08T10:34:08.166Z
---

[Azure Active Directory (Azure AD)](https://azure.microsoft.com/en-ca/services/active-directory/)是Microsoft基于云的身份和访问管理服务，可帮助您的员工登录和访问资源。

# 配置

## A) 复制跳转URI

1. 在您wiki的**管理区**，点击左侧导航栏中的**身份验证**。
1. 添加一个新的**Azure Active Directory**验证策略。
1. 复制配置参考部分中**跳转URI**的值，并保持此页面打开，供后续使用。

## B) 创建Azure AD应用

1. 在Azure门户中，打开**Azure Active Directory**资源。
1. 点击左侧导航栏中的**应用注册**，然后点击顶部的**新注册**。
1. 输入**应用名称** （如：Wiki.js）并填入之前复制的**跳转URI**。
1. 点击**注册**。
1. 复制**应用 (客户端) ID**，供后续使用。
1. 点击顶部的**Endpoints**，然后复制**OpenID Connect元数据文档**的Endpoint值， （如： `https://login.microsoftonline.com/YOUR_TENANT_ID/v2.0/.well-known/openid-configuration`），供后续使用。
1. *(可选)* 点击左侧导航栏中的 **品牌配置** 并填入必要的信息，以使登录流程对您的用户更加友好。
1. 点击左侧导航栏中的 **身份验证** 并填入 **登出URL** (`https://YOUR-WIKI.DOMAIN.COM`) 并确保**隐性授权（Implicit grant）** 下的 **ID 密钥** 复选框为已勾选状态，然后点击顶部的**保存**。
1. 点击左侧导航栏中的**API权限**并确保**Microsoft Graph > User.Read** 权限被列出。
1. *(可选)* 在**API 权限**中， 您可以代表您域下的所有用户 **授予管理员许可**，这在内部组织环境中通常更合适。

## C) 在Wiki.js中启用Azure AD登录策略

1. 回到步骤A中打开的Wiki.js管理区页面。
1. 输入之前复制的 **身份元信息Endpoint** 和 **客户端ID**的值。
1. 启用 **开放注册** *(除非你想人工验证每一个用户)*.
1. 选择新用户首次登录时会被分配到的**用户组**。
1. 确保登陆策略列表中**Azure Active Directory**旁边的复选框为已勾选状态，对应的文本现在应该提示此策略处于**启用**状态。
1. 点击此页右上角的 **应用** 来保存并应用配置。

<img src="https://static.requarks.io/logo/azure.svg" class="align-abstopright" style="width:150px;" />
  
