---
title: Azure Web App
description: 安装指南
published: true
date: 2023-03-16T08:45:000Z
tags: setup, guide, 指南, 安装
editor: markdown
dateCreated: 2023-01-08T10:35:46.596Z
---

本指南详细介绍了在带有**Azure Database for PostgreSQL**的**Azure Web App**上安装Wiki.js的分步步骤。

# 1. 数据库

我们将首先为wiki创建数据库。

虽然可以在Azure Web App上与应用程序一起托管数据库，但不建议这样做，因为这会影响性能，而且不可扩展。

## 1.1 创建数据库

1. 创建新资源，搜索**Azure Database for PostgreSQL**，然后单击**创建**。
1. 选择**单个服务器**
1. 填写服务器详细信息。
	- 您必须选择**9.6或更高版本**。
  	- 使用**1 vCore**时，最小服务器大小为**Basic**，但如果选择Basic，则无法在之后升级到**通用**。
1. 点击创建资源完成创建。
## 1.2 配置数据库

1. 创建资源后，转到**连接安全**。
1. 启用**允许访问Azure服务**，以便您的Azure Web App能够访问您的数据库。
1. 单击**添加客户端IP**将您自己的IP地址添加到白名单中。
1. 单击**保存**并等待应用更改。

> :vertical_traffic_light: 本指南假设数据库将专用于wiki。如果计划与其他应用程序共享数据库，则应连接到服务器并创建专用的用户+数据库。
{.is-warning}

# 2. Azure Web App

现在，我们可以创建运行wiki的应用程序服务。

## 2.1 创建 Web App

1. 创建新资源，搜索**Web App**，然后单击**创建**。
1. 填写实例详细信息。
	- 对于**Publish**类型，选择**Docker 镜像**。
  	- 选择**Linux**作为**操作系统**。
    - 应用程序服务计划的最小规模为**B1**。对生产场景，请考虑至少选择**P1V2**。
1. 点击 **下一步: Docker**
1. 设置以下选项：
	- **单个容器**
  	- 镜像源: **Docker Hub**
    - 访问类型: **Public**
    - 镜像与标签: `requarks/wiki:2`
1. 单击**确认并创建**（其他步骤是可选的）。

## 2.2 配置 Web App

1. 创建资源后，转到**配置**。
1. 添加以下**应用程序设置**：*（用之前创建DB时输入的值替换`xyz`）*
	 ```
   DB_TYPE: postgres
   DB_HOST: xyz.postgres.database.azure.com
   DB_PORT: 5432
   DB_NAME: postgres
   DB_USER: xyz@xyz
   DB_PASS: xyz
   DB_SSL: true
   ```
1. 单击**保存**以应用配置。
1. 转到**概述**选项卡，然后单击**重新启动**。
1. 等待容器准备就绪。您可以使用**日志**窗口在**容器设置**选项卡中监视应用程序状态。查找类似于`站点xyz的容器xyz_0已成功初始化并准备好服务请求`的消息应记录。

# 3. 配置 Wiki.js

1. 浏览到你Web App的公共URL*（可在Web App资源的**概述**选项卡中找到）*
1. 按照说明创建管理员帐户并开始使用wiki。

# 4. 疑难解答

## 4.1 431 Request Header Fields Too Large 问题

在**Azure**中启用**应用程序服务身份验证**可能会导致“请求标头字段太大”错误。
要修复此问题：
1. 在Azure Web App中，转到**配置**。
1. 添加以下**应用程序设置**：
   ```
   WEBSITE_AUTH_DISABLE_IDENTITY_FLOW: true
   ```

在Wiki.js中启用SAML 2.0身份验证时，即使有上述修复，graphql查询也可能再次出现此问题。
为了解决这个问题，我们需要增加NodeJS的最大标头大小。
1. 在Azure Web App中，导航到**配置**。
1. 添加以下**应用程序设置**：
   ```
   NODE_OPTIONS: --max-http-header-size=81920
   ```

![](https://a.icons8.com/cqaghpTd/Zi0crm/svg.svg){.align-abstopright}
