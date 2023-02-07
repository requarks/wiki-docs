---
title: 页面
description: 创建和编辑内容
published: true
date: 2023-02-07T16:05:38.473Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:35:37.988Z
---

# 创建页面

您可以通过多种方式来创建新页面。

- 单击位于页面右上角的 **新建页面** 按钮。
- 单击指向不存在页面的链接。
- 手动在浏览器地址栏打出要创建的页面的路径。

查看 [Wiki.js简介](/guide/intro) 了解如何逐步创建您的第一个页面。

# 编辑页面

您可以通过单击任何页面右下角的**铅笔**图标或使用位于页面右上角的**页面菜单**来编辑现有页面。

首次创建页面时选择的编辑器将自动加载。请注意，一旦创建了页面，就不可能更改编辑器。

# 目录

Wiki.js没有传统意义上的目录结构。您不需要先创建目录再创建新页面。相反，您可以直接在您选择的路径上创建页面。

例如，在传统系统中，为了在`宇宙/行星/地球`上创建页面，您需要首先创建一个目录`宇宙`，然后打开该目录并创建一个名为`行星`的子目录，最后才能在其中创建名为`地球`的页面。

在Wiki.js中，你可以直接在路径`宇宙/行星/地球`上创建页面，`universe`和`planet`目录将被系统自动推断，但它们并不真正存在于页面路径上下文之外。因此，您不必管理目录，而可以只关注页面所需的路径。

因此，没有创建目录的选项。您只需键入所需的完整路径。系统将在创建时自动推断目录。

详细信息参见[目录结构 & 标签](/guide/structure)。

# 命名限制
以下路径不能用于内容，而是保留给系统使用。

## 单字符页面

**所有**单字符路径都是保留路径，以便访问Wiki的各个部分：

- `a`: 管理区
- `c`: 评论
- `e`: 页面编辑器
- `f`: 资源管理器
- `h`: 页面历史
- `i`: 按id浏览页面
- `p`: 用户个人资料
- `s`: 页面源代码
- `t`: 标签
- `u`: 上传Endpoint *(API)*
- `w`: 个人Wiki
{.grid-list}

## IETF 语言标签

以下格式的语言标记保留用于指定要使用的语言环境命名空间。

- 双字母语言代码 (如： `en`, `fr`)
- 特定于国家/地区的区域设置代码 (如： `en-us`, `fr-ca`)
{.grid-list}

## 单词

路径不能与下面的术语完全匹配，也不能是路径的第一部分。例如，`register`或`register/test`不是有效路径，但`registering`是有效路径。

### 2.4 及以上版本

- _assets
- favicon *\[.ico]*
- graphql
- healthz
- home *(reserved for the root homepage)*
- login
- logout
- register
{.grid-list}

### 2.0 到 2.3 版本

- browserconfig *\[.xml]*
- css
- favicon *\[.ico]*
- favicons
- fonts
- graphql
- healthz
- home *(reserved for the root homepage)*
- img
- js
- login
- logout
- manifest *\[.json]*
- register
- svg
{.grid-list}

## 非法字符

路径不能包含以下字符：

- 空格 *(请以英文破折号代替)*
- 句点 *(为文件拓展名保留)*
- 不安全的 URL 字符 *(例如标点符号、引号、数学符号等。)*