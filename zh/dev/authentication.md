---
title: 身份验证
description: 身份验证模块开发指南
published: true
date: 2023-01-30T08:34:27.283Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:34:51.033Z
---

An authentication module adds new ways for users to login to the application. It consists of properties that can be set by the user as well as methods that are called on certain events \(e.g. during initialization\). All authentication modules are based on Passport.js implementation, which is the de facto authentication library for Node.js.

身份验证模块为用户添加了登录应用程序的新方式。它包括用户可以设置的属性及在某些事件上调用的方法（例如在初始化期间）。所有身份验证模块都基于Passport.js实现，它事实上是Node.js的身份验证库。

身份验证模块位于 `/server/modules/authentication`.

每个模块对应一个唯一目录，该目录包含两个文件：

* **definition.yml**
* **authentication.js**

## definition.yml

这个文件包含您的模块的信息。
```yaml
key: example
title: Example Storage
author: John Doe
useForm: false
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### 属性

* **key**: 此模块的简短、唯一的驼峰格式名称。它必须与模块所在的目录名称完全一致。
* **title**: 此模块的全名。
* **author**: 此模块的作者。
* **useForm**: 是否应显示用户/电子邮件+密码表单。_（对于基于oauth2的策略应为`false`。）_ 
* **props**: 用户可编辑属性对象。 更多信息参见[模块属性](/dev/module-properties)。

## authentication.js

此文件包含初始化时调用的方法

```js
/* global WIKI */

// ------------------------------------
// 示例身份认证账户
// ------------------------------------

const ExampleStrategy = require('example')

module.exports = {
  init (passport, conf) {
    passport.use('example',
      new ExampleStrategy({
        propA: conf.propA,
        propB: conf.propB
      }, function (accessToken, refreshToken, profile, cb) {
        WIKI.db.users.processProfile(profile).then((user) => {
          return cb(null, user) || true
        }).catch((err) => {
          return cb(err, null) || true
        })
      }
      ))
  }
}
```

 必须实现所有方法。

### init

 初始化Wiki.js时将调用（启动或重新启动）。

```javascript
init (passport, conf) { }
```

**passport**参数是您要在Passport.js上添加的登录策略。

**conf** 参数是包含身份验证策略配置的对象。例如，如果您在模块属性中定义了`clientId`和`clientSecret`属性，`conf`将成为一个具有`clientId`和`clientSecret`属性的对象，其值为用户在管理区中输入的值。 

更多有关Passport.js的配置参见[此处](http://www.passportjs.org/docs/configure/)。
