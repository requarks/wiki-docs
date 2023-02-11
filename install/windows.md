---
title: Windows
description: Getting started with a Wiki.js installation on Windows
published: true
date: 2023-02-11T12:39:03.555Z
tags: setup
editor: markdown
dateCreated: 2023-01-08T10:36:32.850Z
---

在进一步操作之前，请确保您的系统满足所有[要求](/install/requirements)。

# 安装

1. 在管理员模式下打开**Powershell**提示符。
2. 如果您使用的是**Windows 7/Windows Server 2008 R2或更旧版本**，则必须运行以下命令 *（否则跳过此步骤）*
  ```powershell
  [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12
  ```
3. 下载最新版本的Wiki.js。
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/Requarks/wiki/releases/latest/download/wiki-js-windows.tar.gz" -OutFile "wiki-js.tar.gz"
  ```

4. 解压程序包到您选择的安装位置：
  ```powershell
  New-Item -Path "C:\" -Name "wiki" -ItemType "directory"
  tar xzf wiki-js.tar.gz -C "C:\wiki"
  cd C:\wiki
  ```
  > tar程序仅在Windows 10上可用。在早期版本中，您需要第三方实用程序（如[7-zip](https://www.7-zip.org/)）来提取文件。
  {.is-warning}
5. 将示例配置文件重命名为`config.yml`：
  ```powershell
  Rename-Item -Path config.sample.yml -NewName config.yml
  ```
6. 使用您熟悉的文本编辑器（如记事本）编辑配置文件并填写数据库和端口设置（[配置参考](/install/config)）：
  ```powershell
  notepad .\config.yml
  ```
7. ***仅适用于SQLite安装：** *（否则跳过此步骤）* 为本机获取SQLite3原生捆绑：
  ```bash
  npm rebuild sqlite3
  ```
8. 运行 Wiki.js
  ```powershell
  node server
  ```
9. 等待一会，直至系统提示您打开浏览器中的设置页面。
10. 完成安装向导以完成安装。

# 作为服务运行

有几种解决方案可以将Wiki.js作为后台服务运行，例如：

- [AlwaysUp](https://www.coretechnologies.com/products/AlwaysUp/)
- [PM2](http://pm2.keymetrics.io/) / [pm2-windows-service](https://www.npmjs.com/package/pm2-windows-service)
- [forever](https://www.npmjs.com/package/forever)
- [node-windows](https://github.com/coreybutler/node-windows)

![](https://a.icons8.com/djxbtnYm/GBjHDS/svg.svg){.align-abstopright}