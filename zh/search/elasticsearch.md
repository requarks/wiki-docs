---
title: Elasticsearch
description: 搜索引擎模块
published: true
date: 2023-03-16T08:45:00.000Z
tags: 
---

Elasticsearch是一种分布式的、RESTful的搜索和分析引擎，能够应对越来越多的使用场景。

# 设置

1. 在Wiki.js管理区中，单击侧边栏中的**搜索引擎**。
2. 选择将**Elasticsearch**作为搜索引擎。
3. 选择要使用的**Elasticsearch版本**。这应该与您正在使用的Elasticsearch版本相匹配。
4. 输入要连接到的主机（可以是单个主机或逗号分隔的主机列表）。确保包括端口（例如`es.yourdomain.com:9200`）。如果您正在使用Stack功能包（以前称为X-Pack）中的安全扩展，请将用户名和密码作为URL 的一部分包含在内。
5. 输入所需的索引名称（默认值：wiki）。不要自己创建此索引，因为它将自动创建。
6. <kbd>高级</kbd> 可选地启用 **启动时嗅探(Sniff on start)** 选项，在连接时自动尝试发现其余 Elasticsearch 集群。 您还可以使用 **嗅探间隔(Sniff interval)** 字段指定检查更新节点列表时间间隔。将值设为 `0` 将禁用此检查。

请注意，如果您的Wiki之前已有内容，则必须单击 **重建索引(Rebuild Index)** ，将所有现有内容导入到搜索引擎中。从此时开始，任何更改（新页面、编辑、删除页面）都会被自动处理。

<img src="https://static.requarks.io/logo/elasticsearch.svg" alt="" class="align-abstopright" style="width: 150px;">
