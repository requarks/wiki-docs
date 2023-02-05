---
title: 存储
description: 开发存储模块
published: true
date: 2023-02-05T05:11:27.202Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:35:11.490Z
---

存储模块将Wiki.js与本地或远程存储提供者连接起来，作为内容的备份或直接来源。它由用户可以设置的属性以及在某些事件（例如创建、更新和删除内容）上调用的方法组成。

每个模块对应一个唯一目录，该目录包含两个文件：

* **definition.yml**
* **storage.js**

## definition.yml

这个文件包含您的模块的信息。

```yaml
key: example
title: Example Storage
description: A short description about Example Storage
author: John Doe
logo: https://../example.svg
website: https://www.example.com/
isAvailable: true
supportedModes:
	- push
defaultMode: push
schedule: false
props:
  firstExampleProperty: String
  secondExampleProperty: Number
actions:
	- handler: firstAction
    label: First Action Example
    hint: Description of what this action does
```

### Properties

* **key**: 此模块的简短、唯一的驼峰格式名称。它必须与模块所在的目录名称完全一致。
* **title**: 此模块的全名。
* **description**: 该模块的简短描述。
* **author**: 此模块的作者。
* **logo**: 指向此模块徽标的绝对URL，使用SVG矢量图。
* **website**: 指向此模块的官网的URL
* **isAvailable**: 模块是否可以由管理员激活/配置。
* **supportedModes**: 支持的同步模式列表。除非您的模块支持双向同步，否则只应列出“推送（push）”选项。可能值由：
	* `sync`: 首先从存储目标中拉取内容。任何更新的内容都将覆盖本地内容。之后，自上次同步以来的新内容被推送到存储目标，覆盖目标上的任何内容（如果存在）。
  * `push`: 内容始终被推送到存储目标，覆盖任何现有内容。
  * `pull`: 始终从存储目标中拉取内容，覆盖任何已存在的本地内容。
* **defaultMode**: 上面列出的选项中的默认值。一般为 `push`.
* **schedule**: 一个[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Time_intervals)格式的时间间隔，在该时间间隔内同步功能将被触发，设为`false`以禁用。
* **props**: 用户可编辑属性对象。 更多信息参见[模块属性](/dev/module-properties)。
* **actions**: *(可选)* 管理员可以在此存储模块上执行的手动操作列表。
  * **handler**: 将调用的函数名
  * **label**: 函数名称
  * **hint**: 对该操作内容的描述

## storage.js

此文件包含创建、修改、删除等新页面时将调用的方法。

```javascript
module.exports = {
  async activated () {
​
  },
  async deactivated () {
​
  },
  async init () {
  
  },
  async created (page) {
​
  },
  async updated (page) {
​
  },
  async deleted (page) {
​
  },
  async renamed (page) {
​
  },
  async sync () {
  
  }
}
```

除非另有规定，否则必须实现所有方法。

### activated

从管理区激活存储模块后调用此方法。这通常是检查存储前提条件的地方 _（例如，检查设置、尝试连接、创建容器、初始化存储库等）_。

```javascript
async activated () { }
```

在此方法中，使用**this.config**可访问存储策略的配置。例如，如果在模块属性中定义了`clientId` 和 `clientSecret`属性，`this.config`将是一个具有`clientId` 和 `clientSecret`属性的对象，其值为用户在管理区中输入的值。

任何抛出的错误（或返回被拒绝的promise）都将报告给用户，并且不会启用存储策略。

### deactivated

从管理区域停用存储模块后调用此方法。如果需要，可以在此处断开与存储提供程序的连接。您不应在停用时删除任何内容，因为用户可能会选择稍后重新启用此存储策略，或者只是想保留当前内容作为备份。

```javascript
async deactivated () { }
```

**this.config**是包含存储策略配置的对象。详细信息请参考[activated](#activated)事件。

任何抛出的错误（或返回被拒绝的promise）都将报告给用户，并且不会停用存储策略。

### init

在初始化Wiki.js（启动或重新启动）时和`activated`事件后调用此方法。这对在某些存储策略中建立连接有用。

```javascript
async init () { }
```

**this.config**是包含存储策略配置的对象。详细信息请参考[activated](#activated)事件。

任何抛出的错误（或返回被拒绝的promise）都阻止存储策略并报告给用户，直到Wiki.js重新启动或用户在管理区确认错误。

### created

在页面创建时调用的方法。

```javascript
async created (page) { }
```

在方法中使用**this**上下文可访问以下属性：

```javascript
{
    config: Object // Object containing the storage configuration
}
```

第一个参数**pages**具有以下属性：

```javascript
    {
        id: Number, // 该页的唯一ID
        localeCode: String, // 2字符的语言代码 (如： en).
        path: String, // 该页面的唯一路径 (e.g. some/page)
        title: String, // 页面标题
        description: String, // 页面描述
        isPrivate: Boolean, // 页面是否位于用户私有命名空间内
        isPublished: Boolean, // 页面是否已发布
        publishStartDate: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        publishEndDate: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        contentType: String, // 页面内容的原始格式 (如： markdown, html等)
        content: String, // 页面内容
        createdAt: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        authorId: Number, // 作者唯一ID
        authorName: String, // 作者全名
        authorEmail: String // 作者的电子邮件地址
    }
```

任何抛出的错误（或返回被拒绝的promise）都将被记录，但不会阻止页面的创建。

### updated

页面内容被修改时会调用此方法。

```javascript
async updated (page) { }
```

在方法中使用**this**上下文可访问以下属性：

```javascript
{
    config: Object // Object containing the storage configuration
}
```
第一个参数**pages**具有以下属性：

```javascript
    {
        id: Number, // 该页的唯一ID
        localeCode: String, // 2字符的语言代码 (如： en).
        path: String, // 该页面的唯一路径 (e.g. some/page)
        title: String, // 页面标题
        description: String, // 页面描述
        isPrivate: Boolean, // 页面是否位于用户私有命名空间内
        isPublished: Boolean, // 页面是否已发布
        publishStartDate: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        publishEndDate: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        contentType: String, // 页面内容的原始格式 (如： markdown, html等)
        content: String, // 页面内容
        createdAt: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        creatorId: Number, // 首次创建页面的用户的唯一ID
        creatorName: String, // 首次创建页面的用户的全名
        creatorEmail: String // 首次创建页面的用户的电子邮件地址
    }
```
任何抛出的错误（或返回被拒绝的promise）都将被记录，但不会阻止页面的修改。

### deleted

删除页面时将调用此方法。

```javascript
async deleted (page) { }
```

在方法中使用**this**上下文可访问以下属性：

```javascript
{
    config: Object // Object containing the storage configuration
}
```

第一个参数**pages**具有以下属性：

```javascript
    {
        id: Number, // 该页的唯一ID
        localeCode: String, // 2字符的语言代码 (如： en).
        path: String, // 该页面的唯一路径 (e.g. some/page)
        title: String, // 页面标题
        description: String, // 页面描述
        isPrivate: Boolean, // 页面是否位于用户私有命名空间内
        createdAt: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        deletedAt: String, // ISO-8601 格式的日期 (YYYY-MM-DDTHH:mm:ss.sssZ)
        authorId: Number, // 作者唯一ID
        authorName: String, // 作者全名
        authorEmail: String // 作者的电子邮件地址
        creatorId: Number, // 首次创建页面的用户的唯一ID
        creatorName: String, // 首次创建页面的用户的全名
        creatorEmail: String // 首次创建页面的用户的电子邮件地址
    }
```

任何抛出的错误（或返回被拒绝的promise）都将被记录，但不会阻止页面被删除。

### renamed

Upon rename of a page or when a page is moved to another location.

```javascript
async renamed (page) { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object // Object containing the storage configuration
}
```

The first argument **page** has the following properties:

```javascript
{
    id: Number, // Unique ID of the page
    localeCode: String, // 2 letter code (e.g. en).
    sourcePath: String, // Previous path of the page (e.g. some/oldpage)
    destinationPath: String, // New path of the page (e.g. some/newpage)
    title: String, // Title of the page
    description: String, // Short description of the page
    isPrivate: Boolean, // Is the page inside the user private namespace
    isPublished: Boolean, // Is the page published
    publishStartDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    publishEndDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    contentType: String, // The content original type (e.g. markdown, html, etc.)
    content: String, // The content
    createdAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    updatedAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    authorId: Number, // The Unique ID of the author (user renaming the page)
    authorName: String, // The full name of the author (user renaming the page)
    authorEmail: String, // The email address of the author (user renaming the page)
    creatorId: Number, // The Unique ID of the user that first created the page
    creatorName: String, // The full name of the user that first created the page
    creatorEmail: String // The email address of the user that first created the page
}
```

Any error thrown \(or returning a rejected promise\) will be logged but will not prevent the page from being renamed internally.

### sync

> *Should only be implemented if a schedule is defined in the module properties.*

Upon schedule trigger.

```javascript
async sync () { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object, // Object containing the storage configuration
    mode: String // The selected sync mode (sync, push or pull)
}
```

Any error thrown \(or returning a rejected promise\) will be logged.