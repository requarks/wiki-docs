---
title: 评论
description: 评论模块开发者指南
published: true
date: 2023-01-30T09:46:24.128Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:34:56.776Z
---

> 在**2.4及以上版本**可用。
{.is-info}

评论模块为wiki添加评论功能。它包括用户可以设置的属性及在某些事件上调用的方法（例如：发布新评论）。

评论模块位于`/server/modules/comments`.

评论模块有2种支持格式：

- **代码模板**: 在页面种嵌入外部服务的HTML/JS代码以显示评论。
- **原生**: 使用Wiki.js的界面来显示与发送评论。评论在服务端处理。

每个模块对应创建一个唯一目录，此目录须包含以下文件：

* **definition.yml**
* **code.yml** *(仅代码模板)*
* **comment.js** *(仅原生)*

## definition.yml

此文件包含有关模块的信息：
```yaml
key: 示例
title: 示例评论提供程序
author: John Doe
logo: https://static.requarks.io/logo/example.svg
website: https://example.com/
codeTemplate: true
isAvailable: true
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### 属性

* **key**: 此模块的简短、唯一的驼峰格式名称。它必须与模块所在的目录名称完全一致。
* **title**: 此模块的全名。
* **author**: 此模块的作者。
* **logo**: 指向此模块徽标的URL
* **website**: 指向此模块的官网/开发者站点的URL
* **codeTemplate**: 指定使用代码模板格式 (`true`) 还是原生格式 (`false`)
* **isAvailable**: 用户是否可以使用此模块。
* **props**:用户可编辑属性对象。 更多信息参见[模块属性](/dev/module-properties)。

## code.yml

该文件包含要插入到头部、正文和评论区中的代码片段。

```yaml
main: |
  <div id="external_thread"></div>
body: |
  <script>
    var something = remote()
  </script>
```

### 属性

* **main**: The HTML code snippet where the comments will be displayed. *(Required, HTML only)*
* **head**: The HTML code snippet to inject in the page head. *(Optional, JS and CSS only)*
* **body**: The HTML code snippet to inject at the end of the page body. *(Optional, JS and CSS only)*

## comment.js

此文件包含将在特定事件上调用的方法。

```js
// ------------------------------------
// Example Comments Provider
// ------------------------------------

module.exports = {
  async create ({ pageId, replyTo, content, guestName, guestEmail, user }) {
		// Code to create a comment here...
  },
  async update ({ id, content, user }) {
		// Code to update a comment here...
  },
  async remove ({ id, user }) {
		// Code to delete a comment here...
  },
  async count ({ pageId }) {
		// Code to get the comment count for a page...
  }
}
```

所有方法都必须实现。
