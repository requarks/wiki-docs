---
title: 身份验证
description: 身份验证模块开发指南
published: true
date: 2023-01-30T08:15:20.095Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:34:51.033Z
---

An authentication module adds new ways for users to login to the application. It consists of properties that can be set by the user as well as methods that are called on certain events \(e.g. during initialization\). All authentication modules are based on Passport.js implementation, which is the de facto authentication library for Node.js.

身份验证模块为用户添加了登录应用程序的新方式。它包括用户可以设置的属性及在某些事件上调用的方法（例如在初始化期间）。所有身份验证模块都基于Passport.js实现，它事实上是Node.js的身份验证库。

身份验证模块位于 `/server/modules/authentication`.

A unique folder is created for each module. The folder contains two files:

* **definition.yml**
* **authentication.js**

## definition.yml

This file contains information about your module.
```yaml
key: example
title: Example Storage
author: John Doe
useForm: false
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### Properties

* **key**: A short, unique and camelCase-formatted name for this module. It must match exactly the module folder name!
* **title**: The full name of the module.
* **author**: The name of the author of the module.
* **useForm**: Whether a user/email + password form should be displayed. _\(Should be_ `false` _for oauth2 based strategies.\)_
* **props**: An object of user editable properties. See [Module Properties](/dev/module-properties) for more info.

## authentication.js

This file contains methods that will be called upon initialization.

```js
/* global WIKI */

// ------------------------------------
// Example Auth Account
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

 All methods are required and must be implemented.

### init

 Upon initialization of Wiki.js \(both startups or restarts\).

```javascript
init (passport, conf) { }
```

Parameter **passport** is the Passport.js instance on which your strategy can be added.

Parameter **conf** is an object containing the configuration of the authentication strategy. For example, if you defined properties `clientId` and `clientSecret` for the module props, `conf` will be an object with properties `clientId` and `clientSecret` containing the values entered by the user in the administration area.

Learn more about Passport.js configuration [here](http://www.passportjs.org/docs/configure/).
