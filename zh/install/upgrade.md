---
title: Upgrade
description: 如何升级到最新版本
published: true
date: 2023-03-16T08:45:000Z
tags: setup, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:30.160Z
---

> **请勿使用以下说明从1.0.x升级**！请改用[从Wiki.js v1.x迁移](/install/migrate)教程。这些说明适用于`2.x`实例。
{.is-danger}

> 虽然升级通常是安全的，而且不太可能导致数据丢失，但**您有责任在执行升级之前对数据库进行适当的备份。** 请注意，一旦数据库架构升级，就不可能回退到以前版本的Wiki.js。
{.is-warning}

# 原地升级

选择您的平台：

## Platforms {.tabset}

### Docker <i class="mdi mdi-docker"></i>

#### 独立容器

只需使用最新的映像版本重新创建容器即可升级：

```bash
# 停止并删除容器`wiki`
docker stop wiki
docker rm wiki

# 拉取Wiki.js的最新映像
docker pull ghcr.io/requarks/wiki:2

# 在最新映像上创建新容器
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=mysql" -e "DB_HOST=db" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

查看[Docker安装指南](/install/docker)，了解创建Wiki.js容器时的所有可能选项。

#### Docker Compose

以下命令将拉取最新映像并重新创建docker compose文件中定义的容器：

```bash
docker-compose pull wiki
docker-compose up --force-recreate -d
```

### Linux / macOS <i class="mdi mdi-ubuntu"></i>

> 下面的命令假定Wiki.js安装在名为 `wiki`的子目录下.
{.is-info}

1) 停止正在运行的Wiki.js实例
2) 备份`config.yml`文件。
  ```bash
  cp wiki/config.yml ~/config.yml.bak
  ```
3) 删除应用程序文件夹。
  ```bash
  rm -rf wiki/*
  ```
4) 下载最新版本的Wiki.js。
  ```bash
  wget https://github.com/Requarks/wiki/releases/latest/download/wiki-js.tar.gz
  ```
5) 解压程序包
  ```bash
  tar xzf wiki-js.tar.gz -C ./wiki
  cd wiki
  ```
6) 将config.yml还原到其原始位置。
  ```bash
  cp ~/config.yml.bak ./config.yml
  ```
7) 启动 Wiki.js
  ```bash
  node server
  ```

### Windows <i class="mdi mdi-microsoft-windows"></i>

> 下面的命令假定Wiki.js安装在 `C:\wiki`.
{.is-info}

1. 在管理员模式下打开**Powershell**提示符。
1. 备份`config.yml`文件。
  ```powershell
  Copy-Item "C:\wiki\config.yml" -Destination "C:\config.yml.bak"
  ```
3. 删除应用程序文件夹。
  ```powershell
  Clear-Content "C:\wiki\*"
  ```
4. 如果您使用的是**Windows 7/Windows Server 2008 R2或更旧版本**，则必须运行以下命令 *（否则跳过此步骤）*
  ```powershell
  [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12
  ```
5. 下载最新版本的Wiki.js。
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/Requarks/wiki/releases/latest/download/wiki-js-windows.tar.gz" -OutFile "wiki-js.tar.gz"
  ```

4. 解压程序包
  ```powershell
  tar xzf wiki-js.tar.gz -C "C:\wiki"
  cd C:\wiki
  ```
  > tar程序仅在Windows 10上可用。在早期版本中，您需要第三方实用程序（如[7-zip](https://www.7-zip.org/)）来提取文件。
  {.is-warning}
5. 将`config.yml`备份文件复制回其原始位置。
  ```powershell
  Copy-Item "C:\config.yml.bak" -Destination "C:\wiki\config.yml"
  ```
6. 启动Wiki.js
  ```powershell
  node server
  ```
  
# 在服务器之间迁移

阅读[服务器间迁移](/install/transfe)指南，了解如何将现有的2.x Wiki.js实例迁移至新服务器。

> 注意，新服务器Wiki.js版本不需要与旧服务器匹配。还原后，实例将自动更新到最新版本。例如，将旧服务器上的2.2版本实例迁移到新服务器上的2.5版本实例是非常安全的。
{.is-info}

![](https://a.icons8.com/YTSPoggQ/4CQtQD/svg.svg){.align-abstopright}
