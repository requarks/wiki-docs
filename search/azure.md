---
title: Azure 搜索
description: 搜索引擎模块
published: true
date: 2023-02-12T08:43:28.446Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:37:00.317Z
---

Azure 搜索是一种基于 AI 的云搜索服务，用于 Web 和移动应用程序开发。 

# 配置

1. 登录您的 [Azure 门户](https://portal.azure.com)
1. 创建新 **Azure 搜索** 实例 .
1. 在 Wiki.js 管理区中，单击侧边栏中的 **搜索引擎**。
1. 选择 **Azure 搜索** 作为搜索引擎。
1. 输入刚刚创建的 Azure 搜索实例的**服务名称**。这是您在创建新实例时输入的名称。
1. 输入主要或次要管理密钥，可在 Azure 门户中的 **密钥** 下找到。
1. 输入所需的索引名称（默认值：wiki）。
1. 单击 **应用** 按钮保存并初始化搜索引擎。系统将自动创建一个索引。

请注意，如果您的 wiki 中已有内容，则必须在之后单击 **重建索引** 以将所有现有内容导入搜索引擎。从此时起，任何更改（新建、编辑、删除页面）都将自动处理。

<img src="https://static.requarks.io/logo/azure.svg" alt="" class="align-abstopright" style="width: 200px;">