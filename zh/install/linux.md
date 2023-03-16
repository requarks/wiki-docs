---
title: Linux
description: 在Linux上安装Wiki.js
published: true
date: 2023-03-16T08:45:000Z
tags: setup, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:06.981Z
---

在进一步操作之前，请确保您的系统满足所有[要求](/install/requirements)。

> 正在查找完整、简单(包括所有依赖项和自动更新程序)的分步安装指南？查看[基于Ubuntu](/install/ubuntu)的安装指南。
{.is-info}

# 安装

1. 下载最新版本的Wiki.js：
  ```bash
  wget https://github.com/Requarks/wiki/releases/latest/download/wiki-js.tar.gz
  ```
2. 解压安装包到你选择的安装目录：
  ```bash
  mkdir wiki
  tar xzf wiki-js.tar.gz -C ./wiki
  cd ./wiki
  ```
3. 将示例配置文件重命名为`config.yml`：
  ```bash
  mv config.sample.yml config.yml
  ```
4. 编辑配置文件并填写数据库和端口设置（[配置参考](/install/config)）：
  ```bash
  nano config.yml
  ```
5. ***仅适用于SQLite安装：** *（否则跳过此步骤）* 为本机获取SQLite3原生捆绑：
  ```bash
  npm rebuild sqlite3
  ```
6. 运行Wiki.js：
  ```bash
  node server
  ```
7. 等待一会，直至系统提示您打开浏览器中的设置页面。
8. 完成安装向导以完成安装。

# 作为服务运行

有几种解决方案可以将Wiki.js作为后台服务运行。我们将在本指南中重点介绍**systemd**，因为它几乎在所有的linux发行版中都可用。

1. 在`/etc/systemd/system`目录内创建名为`wiki.service`的新文件。
  ```bash
  nano /etc/systemd/system/wiki.service
  ```
2. 粘贴以下内容（假设您的wiki安装在`/var/wiki`）：
  ```ini
  [Unit]
  Description=Wiki.js
  After=network.target

  [Service]
  Type=simple
  ExecStart=/usr/bin/node server
  Restart=always
  # Consider creating a dedicated user for Wiki.js here:
  User=nobody
  Environment=NODE_ENV=production
  WorkingDirectory=/var/wiki

  [Install]
  WantedBy=multi-user.target
  ```
3. 保存服务文件 (先按<kbd>CTRL</kbd>+<kbd>X</kbd>, 再按 <kbd>Y</kbd>).
4. 重载systemd：
  ```bash
  systemctl daemon-reload
  ```
5. 启动服务：
  ```bash
  systemctl start wiki
  ```
6. 启用开机自启动：
  ```bash
  systemctl enable wiki
  ```
  
*注意：* 您可以使用`journalctl -u wiki`查看服务日志。

![](https://a.icons8.com/TqgWTTfw/Oy7xHF/svg.svg){.align-abstopright}