---
title: 在Portainer上安装
description: 详细安装指南
published: true
date: 2023-02-11T07:40:17.004Z
tags: setup, guide, 指南, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:15.572Z
---

本指南详细介绍了在运行**Portainer**的计算机上安装Wiki.js的分步步骤。

1. 单击左侧边栏导航中的**堆栈**。
1. 单击 **\+ 添加堆栈** 按钮。
1. 输入堆栈的名称（例如`wiki`）。
1. 选择**Web编辑器**作为构建方法。
1. 在下面的Web编辑器中，粘贴以下代码块：
    ```yaml
    version: '2'
    services:
      db:
        image: postgres:11-alpine
        environment:
          POSTGRES_DB: wiki
          POSTGRES_PASSWORD: wikijsrocks
          POSTGRES_USER: wikijs
        logging:
          driver: "none"
        restart: unless-stopped
        volumes:
          - db-data:/var/lib/postgresql/data

      wiki:
        image: requarks/wiki:2
        depends_on:
          - db
        environment:
          DB_TYPE: postgres
          DB_HOST: db
          DB_PORT: 5432
          DB_USER: wikijs
          DB_PASS: wikijsrocks
          DB_NAME: wiki
        restart: unless-stopped
        ports:
          - "80:3000"

    volumes:
      db-data:
    ```
1. 单击**部署堆栈**按钮。
1. 没有第7步了，就是这么简单。

现在，您可以导航到服务器的IP/域名以完成配置并开始使用Wiki.js！
