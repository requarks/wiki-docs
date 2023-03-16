---
title: 渲染
description: 开发渲染模块
published: true
date: 2023-03-16T08:45:000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:35:05.760Z
---

渲染模块为wiki添加了额外的内容处理功能。它是渲染流水线的一部分，在流水线中，原始内容被解析并转换为最终的html表单。

# 架构

## 创建新页面

![创建新页面流程图](/assets/diagrams/diag-create-page-flow.jpg =1000x){.decor-shadow .radius-4}

## 查看页面
![查看页面流程图](/assets/diagrams/diag-view-page-flow.jpg =1000x){.decor-shadow .radius-4}

# 渲染模块

有两种类型的渲染模块：**核心渲染模块**和**扩展渲染模块**。

## 核心渲染模块

核心渲染模块（CRM）采用特定格式作为输入（例如Markdown），可选地使用一个或多个扩展渲染模块（ERM），并将结果输出为另一种格式（通常为HTML）。

每个输入格式类型通常有一个CRM，但可以串行执行多个CRM。但需要注意的是，无法保证同一输入类型的CRM之间的顺序。

CRM的工作是加载要被应用的ERM，并在渲染过程中按顺序执行它们。

## 拓展渲染模块

拓展渲染模块（ERM）由核心渲染模块（CRM）使用。它们不饿能自己运行，通常处理核心模块的某个特定部分。

例如，Markdown CRM的ERM可以将表情符号标记转换为符号。这是一个依赖于Markdown CRM引擎的特定功能。

![渲染流水线示意图](/assets/diagrams/diag-rendering-pipeline.jpg =1000x){.decor-shadow .radius-4}
