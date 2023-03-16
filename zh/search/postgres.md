---
title: 数据库 - PostgreSQL
description: 搜索引擎模块
published: true
date: 2023-03-16T08:45:000Z
tags: 
editor: markdown
---

该引擎利用了PostgreSQL的高级功能，提供了一个“足够好”的搜索解决方案。

> 为了使用此引擎，您必须使用PostgreSQL数据库运行Wiki.js！
{.is-warning}

# 要求

对于此引擎正常工作，必须在PostgreSQL上启用**pg_trgm**扩展。它在大多数安装中默认启用，但如果不是这种情况，则可以通过运行以下命令来启用它：

```sql
CREATE EXTENSION pg_trgm;
```
> 扩展程序必须针对每个数据库进行激活，请确保为您的Wiki.js数据库启用它。
{.is-info}

# 设置

1. 在Wiki.js管理区中，在侧边栏中单击 **Search Engine（搜索引擎）**。
2. 选择 **数据库 - PostgreSQL** 作为搜索引擎。
3. 在下拉列表中选择要使用的字典语言。
4. 单击 **应用** 按钮以保存和初始化搜索引擎。将自动创建索引。

请注意，如果您的wiki之前已有内容，则必须单击 **重建索引** 将所有现有内容导入到搜索引擎中。从此时起任何更改(新建、编辑、删除页面)都将自动处理。
