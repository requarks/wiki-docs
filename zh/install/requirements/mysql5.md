---
title: MySQL 5.7 注意事项
description: Limited support for this MySQL version
published: true
date: 2023-03-16T08:45:00.000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:37:17.593Z
---

# 受影响的版本

- MySQL**5.7.8**以及5.7.x范围内的更高版本。

# 有限功能

## 上传

只能在根目录中上传资源。无法上传目录或嵌套目录中的文件。这样做将导致上传时出错。

# 原因

MySQL 5.7.x不支持提取目录层次结构所需的`WITH RECURSIVE`表达式。此表达式在8.0版=版本中引入。
