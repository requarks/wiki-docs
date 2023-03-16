---
title: macOS
description: 在macOS上安装Wiki.js
published: true
date: 2023-03-16T08:45:000Z
tags: setup, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:09.860Z
---

在进一步操作之前，请确保您的系统满足所有[要求](/install/requirements)。

# 安装

1. 打开 **终端**.
2. 下载最新版本的Wiki.js：
  ```bash
  wget https://github.com/Requarks/wiki/releases/latest/download/wiki-js.tar.gz
  ```
3. 解压安装包到你选择的安装目录：
  ```bash
  mkdir wiki
  tar xzf wiki-js.tar.gz -C ./wiki
  cd ./wiki
  ```
4. 将示例配置文件重命名为`config.yml`：
  ```bash
  mv config.sample.yml config.yml
  ```
5. 编辑配置文件并填写数据库和端口设置（[配置参考](/install/config)）：
  ```bash
  nano config.yml
  ```
6. ***仅适用于SQLite安装：** *（否则跳过此步骤）* 为本机获取SQLite3原生捆绑：
  ```bash
  npm rebuild sqlite3
  ```

7. 运行Wiki.js：
  ```bash
  node server
  ```
8. 等待一会，直至系统提示您打开浏览器中的设置页面。
9. 完成安装向导以完成安装。

# 作为服务运行

*即将支持*

![](https://a.icons8.com/eSUcnrow/jfIq9Q/svg.svg){.align-abstopright}