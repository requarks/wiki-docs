---
title: Heroku
description: 在Heroku上安装Wiki.js
published: true
date: 2023-03-16T08:45:00.000Z
tags: setup, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:01.197Z
---

Heroku是一个流行的平台，可以快速运行任何类型的web应用程序。
为方便起见，提供了预配置的部署模板：

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/requarks/wiki-heroku/tree/2.x)

# 重要提示

- 部署模板将使用默认的PostgreSQL计划，即Hobby Dev（免费）计划。之后，您可以根据[Heroku文档](https://devcenter.heroku.com/articles/updating-heroku-postgres-databases)升级到更大的计划。另一个选项是克隆wiki heroku存储库并编辑清单文件，以使用您需要的特定计划。
- 虽然最初的部署非常快速和简单，但**升级到新版本却不是这样**。您需要向应用程序的git仓库推送新的提交，以便触发新的构建。除非您熟悉Heroku部署工作流，否则您可能需要寻找替代的托管解决方案。
- 免费dyno计划（默认）将在30分钟不活动后“休眠”。此类事件后的第一个页面加载将需要几秒钟才能完成，因为它必须生成一个新实例。升级到付费dyno计划以删除此限制。
- 数据库endpoint必须作为`DATABASE_URL`环境变量提供给应用程序（默认）。

# 数据库连接Bug

默认情况下，一个特定于Heroku的错误阻止Wiki.js连接到数据库。根本原因尚未查明。

此issue中提供了一种解决方法，包括将数据库降级到PostgreSQL 10：

https://github.com/Requarks/wiki/issues/2949#issuecomment-773412440

![](https://a.icons8.com/TgwPdfer/uNiaiQ/svg.svg){.align-abstopright}
