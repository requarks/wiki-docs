---
title: Algolia
description: 搜索引擎模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:36:54.753Z
---

Algolia 是一种功能强大的搜索即服务解决方案，可轻松与 API 客户端、UI 库和预构建集成一起使用。 

# 配置

1. 在 Wiki.js 管理区中，单击侧边栏中的 **搜索引擎**。
1. 选择 **Algolia** 作为搜索引擎
1. 输入您的 **应用 ID**（在fAlgolia面板中的**API 密钥**下查看）.
1. 输入您的 **管理API密钥**（与上一步的查看位置相同）. 您还可以创建一个特定于您的 wiki 的密钥。
1. 输入一个索引名称 (默认值: wiki).
1. 单击 **应用** 按钮保存并初始化搜索引擎。系统将自动创建一个索引。

请注意，如果您的 wiki 中已有内容，则必须在之后单击 **重建索引** 以将所有现有内容导入搜索引擎。从此时起，任何更改（新建、编辑、删除页面）都将自动处理。

![](https://static.requarks.io/logo/algolia.svg =x50){.align-abstopright}