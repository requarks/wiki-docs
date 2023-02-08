---
title: 要求
description: 安装Wiki.js的先决条件
published: true
date: 2023-02-08T01:16:57.600Z
tags: setup, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:18.438Z
---

# 服务器要求

Wiki.js几乎可以在任何支持Node.js的系统上运行。
这意味着它可以在**Linux**、**macOS**、**Windows**以及**Docker/Kubernetes**和**Heroku**等容器解决方案上运行。

### CPU
Wiki.js在单个CPU内核上可以运行得很好。但是，建议配备**2个或更多内核**以充分利用后台workers线程。

### RAM（运存）
Linux系统应该有**至少1GB的RAM**来运行Wiki.js。Windows和macOS系统通常需要更多的RAM。

虽然进程本身通常占用70MB左右的RAM，但一些事件*（如页面渲染、索引等）*会导致RAM使用量的短暂上涨。

### 内存
存储要求基于您将输入的内容。几乎完全由文本组成的Wiki不太可能超过几兆字节。但是，一旦您上传了图像、视频或其他文件，就应该相应地规划存储需求。

建议至少为Wiki.js提供1 GB的专用存储空间。

### 互联网
Wiki.js会不时自动检查新的更新、语言、主题等。您可以阅读有关下载数据的[更多信息](/install/requirements/internet)。

如果您的环境与互联网断开，也可以使用[侧载文件](/install/sideload)的方法。

# 域名

Wiki.js需要专用的子域名/域名（例如`wiki.example.com`）。不能将Wiki.js映射到子目录。

# 数据库

为了获得最佳性能、功能和高版本兼容性，强烈建议使用**PostgreSQL**。

- ![](https://static.requarks.io/logo/postgresql.svg =24x){.mr-2} PostgreSQL **9.5 及以上版本**
{.grid-list}

> 建议尽可能使用最新版本的PostgreSQL。
{.is-success}

> 请注意，为了使用PostgreSQL搜索模块，主机上必须有`pg_trgm`扩展。在大多数Linux发行版中，该扩展是`postgresqlcontrib`包的一部分。docker PostgreSQL镜像已包含此扩展。
{.is-info}

---

Wiki.js还与以下数据库系统兼容：

- ![](https://static.requarks.io/logo/mysql.svg =24x){.mr-2} MySQL **8.0 及以上版本** *(MySQL **5.7.8** is partially supported, [read more](/install/requirements/mysql5))*
- ![](https://static.requarks.io/logo/mariadb.svg =24x){.mr-2} MariaDB **10.2.7 及以上版本**
- ![](https://static.requarks.io/logo/microsoft-sql-server-alt.svg =24x){.mr-2} MS SQL Server **2012 及以上版本**
- ![](https://static.requarks.io/logo/sqlite-alt.svg =24x){.mr-2} SQLite **3.9 及以上版本**
{.grid-list}

> **Wiki.js的下一个主要版本将不支持这些引擎 *（MySQL、MariaDB、MS SQL Server和SQLite）***. 如果您计划在未来几年升级到3.x+，请确保您了解将数据库迁移到PostgreSQL。我们将在下一个主要版本发布后不久提供导出+导入工具。
> 
> 生产环境**不建议**使用SQLite。
{.is-warning}

您应该已经安装了其中一个数据库引擎 *（本地、其他服务器或使用云服务）*。Wiki.js需要一个空数据库，最好是通过一个唯一的用户名/密码才能连接到数据库。

# Node.js

必须安装[Node.js](https://nodejs.org/)运行时。Wiki.js支持以下版本：

- **Node.js 12**: **12.0** 及以上版本。
- **Node.js 14**: **14.0** 及以上版本。
- **Node.js 16**: **16.0** 及以上版本。
{.grid-list}

> Wiki.js 2.x与Node.js**18**不兼容。
> Wiki.js 3.0将提供对Node.js**18及更高版本**的支持。
>
> 奇数版本（例如`13.x`、`15.x`、`17.x`）**不受**官方支持。
{.is-danger}

### **如果你在使用Doker** :whale:

> **请跳过此要求！** 您不需要在机器上安装Node.js！它已经包含在Docker镜像中。
{.is-info}

### **Web 服务器** :cloud:

Wiki.js不需要任何实际的Web服务器（如Nginx或Apache）。然而，如果需要高级网络/DNS配置，则可能需要在Wiki.js前面部署一个反向代理。

# 支持的浏览器

支持以下浏览器：

- Google Chrome (包括安卓版)
- Mozilla Firefox
- Microsoft Edge
- Apple Safari (包括iOS版)

请注意，仅支持这些浏览器的最新稳定版本。默认情况下，所有浏览器都会在后台自动更新。

> Wiki.js对**IE11**有限兼容。用户将能够阅读内容，但不能执行任何编辑操作或使用交互功能。
{.is-info}

![](https://a.icons8.com/ViUXyjOj/f4tFww/svg.svg){.align-abstopright}