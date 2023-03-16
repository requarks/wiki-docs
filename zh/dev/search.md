---
title: 搜索引擎
description: 开发搜索引擎模块
published: true
date: 2023-03-16T08:45:000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:35:08.579Z
---

搜索引擎模块将Wiki.js与外部搜索引擎连接，以执行页面搜索和单词建议查询。它由用户可以设置的属性以及在某些事件上调用的方法组成，例如创建、更新和删除内容。

搜索引擎模块位于 `/server/modules/search`.

为每个模块创建一个唯一的文件夹。该文件夹包含两个文件：

- **definition.yml**
- **storage.js**

## definition.yml

该文件含有关于您模块的信息。

```yaml
key: example
title: 搜索引擎示例模块
author: John Doe
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### Properties

* **key**: 此模块的简短、唯一的驼峰格式名称。它必须与模块所在的目录名称完全一致。
* **title**: 此模块的全名。
* **author**: 此模块的作者。
* **props**: 用户可编辑属性对象。 更多信息参见[模块属性](/dev/module-properties)。


## engine.js

此文件包含执行搜索查询和创建、修改、删除新页面时将调用的方法。

```javascript
module.exports = {
  async activated () {

  },
  async deactivated () {

  },
  async init () {
  
  },
  async suggest (q, opts) {
  
  },
  async query (q, opts) {
  
  },
  async created (page) {

  },
  async updated (page) {

  },
  async deleted (page) {

  },
  async renamed (page) {

  },
  async rebuild () {
  
  }
}
```