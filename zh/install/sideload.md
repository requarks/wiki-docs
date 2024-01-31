---
title: 侧载
description: 允许wiki在没有Internet访问的情况下运行
published: true
date: 2023-03-16T08:45:00.000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:36:21.519Z
---

# 基本信息

如果您的wiki安装在与Internet隔离的环境中，您可以侧载本应从Internet上下载的数据。

这是通过手动下载一组文件并将其放置在wiki实例的特定目录中实现的。这些文件将在初始化期间导入。

## 开始

在Wiki.js安装文件夹中的路径`data/sideload`处**创建一个新目录**。

*例如，如果wiki安装在路径`/home/wiki`，则需要在路径`/home/wiki/data/sideload`创建目录*

# 语言

为了安装语言环境包，您需要**主语言环境文件***+至少一个**语言环境包文件**。

> 文件可以从 https://github.com/Requarks/wiki-localization 下载，这些文件每天更新一次。
{.is-info}

## 1 - 主语言环境文件

主文件`locales.json`包含所有可用语言的信息，安装任何语言环境都**需要**此文件。

将此文件放在先前创建的`sideload`目录中。

## 2 - 语言环境包文件

语言环境包文件`xx.json`或`xx-zz.json`包含您选择的语言的所有翻译。您可以同时加载任意数量的语言环境包文件。

> 英文语言包`en.json`是**必需**加载的，因为这是安装期间的默认语言。之后您可以更改语言。
{.is-warning}

将文件放在主文件旁边先前创建的`sideload`目录中。现在，文件夹中应该有`locales.json`、`en.json`和其他语言。

## 3 - 侧载

运行Wiki.js（如果已经运行，则重新启动进程）以自动侧载`data/sideload`目录中的本地文件。

> 由于2.5之前版本中的一个bug，语言文件的加载顺序不正确，导致客户端无法获取翻译。
> 
> 解决方法是，Wiki.js完全启动后，请重新启动服务器。将正确加载语言数据（现在已存储在数据库中）。
{.is-danger}

# 主题

*即将支持*