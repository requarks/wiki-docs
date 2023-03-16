---
title: 使用Docker Desktop在本地安装
description: 在本地计算机上安装Wiki.js的最简单快捷的方法
published: true
date: 2023-03-16T08:45:000Z
tags: setup, guide, 指南, 安装
editor: markdown
dateCreated: 2023-01-08T10:35:55.379Z
---

# 概述

本指南是在本地**macOS**或**Windows**计算机上运行Wiki.js的快速简单指南。

# 安装

## 1. 安装 Docker Desktop

安装包含Docker和Docker Compose的Docker Desktop：

- [macOS (Apple Silicon)](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
- [macOS (Intel)](https://desktop.docker.com/mac/main/amd64/Docker.dmg)
- [Windows](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)

## 2. 创建安装目录

在您选择的位置创建名为`wiki`的新文件夹。

在此文件夹中，创建一个名为`docker-compose.yaml`的新文件，并在其中粘贴以下内容：

```yaml
version: "3"
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
    image: ghcr.io/requarks/wiki:2
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

这个文件只定义了PostgreSQL容器*（我们的数据库）*和Wiki.js容器。

## 3. 打开终端/命令提示符

在**macOS**上，启动**终端**并导航到您先前创建的`wiki`文件夹。

在**Windows**上，打开之前在**文件资源管理器**中创建的文件夹`wiki`。
在地址栏中，键入“cmd”，然后按<kbd>ENTER</kbd>在该位置启动**命令提示符**。

## 4. 启动 Wiki.js

在**终端**/**命令提示符**中键入以下命令以启动Wiki.js：

```sh
docker compose up -d
```

## 5. 浏览Wiki.js

打开浏览器并导航到http://localhost以完成安装并使用Wiki.js！
