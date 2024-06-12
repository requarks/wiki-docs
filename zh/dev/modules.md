---
title: 模块
description: 面向开发者的模块简介
published: true
date: 2023-03-16T08:45:00.000Z
tags: dev, 开发
editor: markdown
dateCreated: 2023-01-08T10:35:02.667Z
---

Wiki.js 2.0为关键组件（如身份验证和存储）引入了一种完全模块化的方法。这允许开发人员轻松地将应用程序与现有基础设施集成。

所有模块组件均位于 `server/modules`。

针对每种模块类型的详细指南参见：

* [身份认证](/dev/authentication)
* [评论](/dev/comments)
* [渲染](/dev/rendering)
* [搜索引擎](/dev/search)
* [存储](/dev/storage)
{.links-list}

模块共享相同的基本结构。它们由一个定义文件和一个代码文件组成，定义文件(`definition.yml`)内含您模块的信息与配置，代码文件包含模块的实际逻辑。模块是完全独立的，除非在文档中明确指定，否则不会在与Wiki.js核心应用程序相同的上下文中运行。这也意味着默认情况下Wiki.js中未包含的任何依赖项都必须位于模块目录中。

## 模块依赖

某些模块可能需要Wiki.js主程序的package.json中不存在的npm依赖项。请首先验证所需的依赖项是否已存在于主项目中。不要将依赖项添加到主package.json中。这是为核心Wiki.js应用程序保留的，这样做可能会带来破坏性的更改。

如果所需的依赖包尚未存在，则必须在与模块定义文件相同目录中安装额外的依赖项。必须首先从模块目录创建本地package.json：

```bash
npm init
```

接受所有默认值。现在您可以添加本地依赖：

```bash
npm install your-dependency
```

这将创建一个`node_modules`文件夹并在本地安装依赖项，然后您就可以在代码中`require()`（请求）模块。


> **请勿使用本机编译的依赖** \(使用 node-gyp 或下载针对特定操作系统可执行文件的依赖包\). 这些爆需要构建工具（如python、c++编译器等），而这些工具不会出现在客户机上，且通常无法安装于低内存系统上。
{.is-danger}

![](https://a.icons8.com/Ufcf0eoh/d5D6Em/svg.svg){.align-abstopright}