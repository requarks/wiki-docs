---
title: GraphQL API
description: 使用GraphQL API访问资源并执行操作
published: true
date: 2023-03-16T08:45:00.000Z
tags: dev, api, 开发
editor: markdown
dateCreated: 2023-01-08T10:34:47.855Z
---

# 概述

Wiki.js公开了一个[GraphQL](https://graphql.org/) API，您可以从中访问和修改Wiki的所有资源。如果您是GraphQL新手，那么[How to GraphQL](https://www.howtographql.com/)网站是一个很好的学习资源。

> 您wiki的 **GraphQL endpoint** 位于站点的 `/graphql` 路径下。
{.is-success}

您可以从浏览器访问此endpoint，以加载**GraphQL Playground**工具，该工具允许您构建和测试查询语句，以及探索您可以访问的所有可能资源。所有可用查询和修改语句的文档都可以在屏幕右侧访问。

大多数编程语言都有各种[客户端库](https://github.com/chentsulin/awesome-graphql#libraries) ，可以轻松地进行GraphQL查询。**Postman**、 **Insomnia** 和**Firecamp**等桌面API客户端都支持GraphQL查询。

# 身份验证

> API访问功能在 **2.2及以上版本**可用.
{.is-info}

访问资源需要**合法API令牌**，该令牌可以从**管理区**（在**API访问**下）生成。

该令牌必须以`Bearer`令牌格式置于`Authorization`请求头中，包含于向GraphQL endpoint发出的任何请求，例如：

```css
Authorization: Bearer eyJhbGc...aXczt18H6437W
```

要查询/修改的资源不同，需要的权限范围也不同。请确保您创建的API令牌包含这些权限范围。

# 示例

以下示例期望在`Authorization`请求头中提供有效的Bearer令牌，如上面的[身份验证](#authentication)部分所述。

对于GraphQL Playground，您可以在**HTTP请求头面板**中使用以下格式：

```json
{ "Authorization": "Bearer eyJhbGc...aXczt18H6437W" }
```

> 注意，为了简单起见，下面的示例使用了硬编码值。在实际应用程序中，最好使用[变量](https://graphql.org/learn/queries/#variables)。
{.is-info}

## 获取所有页面

获取按标题排序的所有页面的列表，只返回`id`、`path`和`title`属性。

```graphql
{
  pages {
    list (orderBy: TITLE) {
      id
      path
      title
    }
  }
}
```

## 获取特定页面

获取ID为`15`的单个页面，只返回`path`、`title`、`createdAt`和`updatedAt`属性。

```graphql
{
  pages {
    single (id: 15) {
      path
      title
      createdAt
      updatedAt
    }
  }
}
```


## 获取所有用户组

获取所有用户组，只返回`id`和`name`属性。

```graphql
{
  groups {
    list {
      id
      name
    }
  }
}
```

## 搜索用户

列出姓名或电子邮件地址中与`john`匹配的所有用户，只返回`id`、`name`和`email`属性。

```graphql
{
  users {
    search (query: "john") {
      id
      name
      email
    }
  }
}
```

## 创建新用户

创建一个新的本地用户，将其分配ID为`1`的用户组并返回生成的用户`ID`。如果操作成功，则响应中的属性`successed`将为`true`。否则，`message`属性将包含阻止用户创建的错误消息。

```graphql
mutation {
  users {
    create (
      email: "john.doe@example.com"
      name: "John Doe"
      passwordRaw: "Password123"
      providerKey: "local"
      groups: [1]
      mustChangePassword: true
      sendWelcomeEmail: false
    ) {
      responseResult {
        succeeded
        slug
        message
      }
      user {
        id
      }
    }
  }
}

```


# 错误参照

修改语句始终返回具有`responseResult`属性的`ResponseStatus`类的对象：

```graphql
type ResponseStatus {
  succeeded: Boolean!
  errorCode: Int!
  slug: String!
  message: String
}
```

*示例回复：*
```json
{
  "responseResult": {
    "succeeded": true
    "errorCode": 0
    "slug": "success",
    "message": "The operation completed successfully"
  }
}
```

使用下面的代码参照表查找错误代码对应的错误简称与详细信息。

## 身份验证 / 用户

**1xxx**范围内的错误代码专用于身份验证/用户错误。

| 错误代码 | 错误简称                           | 详细信息                           |
| -------- | ---------------------------------- | ---------------------------------- |
| 1001     | AuthGenericError                   | 登录期间发生意外错误。             |
| 1002     | AuthLoginFailed                    | 电子邮件/用户名或密码无效。        |
| 1003     | AuthProviderInvalid                | 身份验证提供程序无效。             |
| 1004     | AuthAccountAlreadyExists           | 使用此电子邮件地址的帐户已存在。   |
| 1005     | AuthTFAFailed                      | 两步验证安全代码不正确。           |
| 1006     | AuthTFAInvalid                     | 两步验证安全代码或登录令牌无效。   |
| 1007     | BruteInstanceIsInvalid             | Brute Force实例无效。              |
| 1008     | BruteTooManyAttempts               | 尝试次数太多！请稍后再试。         |
| 1009     | UserCreationFailed                 | 创建用户时发生意外错误。           |
| 1010     | AuthRegistrationDisabled           | 注册已禁用。请与系统管理员联系。   |
| 1011     | AuthRegistrationDomainUnauthorized | 您无权注册。您的域名未列入白名单。 |
| 1012     | InputInvalid                       | 输入数据非法。                     |
| 1013     | AuthAccountBanned                  | 您的帐户已被停用。                 |
| 1014     | AuthAccountNotVerified             | 您必须验证您的帐户才能登录。       |
| 1015     | AuthValidationTokenInvalid         | 验证令牌无效。                     |
| 1016     | UserNotFound                       | 用户不存在。                       |
| 1017     | UserDeleteForeignConstraint        | 由于内容关系约束，无法删除用户。   |
| 1018     | UserDeleteProtected                | 无法删除受保护的系统帐户。         |
| 1019     | AuthRequired                       | 您必须经过身份验证才能访问此资源。 |
| 1020     | AuthPasswordInvalid                | 密码不正确。                       |

## 资源

**2xxx**范围内的错误代码专用于资源错误。

| 错误代码 | 错误简称                   | 详细信息                           |
| -------- | -------------------------- | ---------------------------------- |
| 2001     | AssetGenericError          | 操作资源期间发生意外错误。         |
| 2002     | AssetFolderExists          | 目录下已存在同名资源文件夹。       |
| 2003     | AssetDeleteForbidden       | 您无权删除此资源                   |
| 2004     | AssetInvalid               | 资源不存在或非法。                 |
| 2005     | AssetRenameCollision       | 该目录下已存在同名资源。           |
| 2006     | AssetRenameForbidden       | 您无权重命名此资源。               |
| 2007     | AssetRenameInvalid         | 资源新名称不合法。                 |
| 2008     | AssetRenameInvalidExt      | 无法更改现有资源的文件扩展名。     |
| 2009     | AssetRenameTargetForbidden | 您无权将此资源重命名为请求的名称。 |

## 邮件

**3xxx**范围内的错误代码专用于邮件错误。

| 错误代码 | 错误简称             | 详细信息                   |
| -------- | -------------------- | -------------------------- |
| 3001     | MailGenericError     | 邮件操作期间发生意外错误。 |
| 3002     | MailNotConfigured    | 邮件配置不完整或无效。     |
| 3003     | MailTemplateFailed   | 无法加载邮件模板。         |
| 3004     | MailInvalidRecipient | 收件人的电子邮件地址无效。 |

## 搜索

**4xxx**范围内的错误代码专用于搜索错误。

| 错误代码 | 错误简称               | 详细信息                   |
| -------- | ---------------------- | -------------------------- |
| 4001     | SearchGenericError     | 搜索操作期间发生意外错误。 |
| 4002     | SearchActivationFailed | 搜索引擎激活失败。         |

## 本地化

**5xxx**范围内的错误代码专用于本地化错误。

| 错误代码 | 错误简称               | 详细信息                     |
| -------- | ---------------------- | ---------------------------- |
| 5001     | LocaleGenericError     | 本地化操作期间发生意外错误。 |
| 5002     | LocaleInvalidNamespace | 区域设置或命名空间无效。     |

## 页面

**6xxx**范围内的错误代码专用于页面/渲染错误。

| 错误代码 | 错误简称             | 详细信息                                   |
| -------- | -------------------- | ------------------------------------------ |
| 6001     | PageGenericError     | 页面操作期间发生意外错误。                 |
| 6002     | PageDuplicateCreate  | 无法创建此页，因为同一路径下已存在此条目。 |
| 6003     | PageNotFound         | 页面不存在。                               |
| 6004     | PageEmptyContent     | 页面内容不可为空。                         |
| 6005     | PageIllegalPath      | 页面路径不能包含非法字符。                 |
| 6006     | PagePathCollision    | 页面目标路径已存在。                       |
| 6007     | PageMoveForbidden    | 您无权移动此页面。                         |
| 6008     | PageCreateForbidden  | 您无权创建此页面。                         |
| 6009     | PageUpdateForbidden  | 您无权更新此页面，                         |
| 6010     | PageDeleteForbidden  | 您无权删除此页面。                         |
| 6011     | PageRestoreForbidden | 您无权回滚此页面历史版本。                 |
| 6012     | PageHistoryForbidden | 您无权查看此页的编辑历史。                 |
| 6013     | PageViewForbidden    | 您无权查看此页面。                         |

## 系统

**7xxx**范围内的错误代码专用于系统相关错误。

| 错误代码 | 错误简称                      | 详细信息                        |
| -------- | ----------------------------- | ------------------------------- |
| 7001     | SystemGenericError            | 发生未知错误。                  |
| 7002     | SystemSSLDisabled             | SSL未启用。                     |
| 7003     | SystemSSLRenewInvalidProvider | 当前提供程序不支持SSL证书续订。 |
| 7004     | SystemSSLLEUnavailable        | Let's Encrypt 尚未初始化。      |

## 评论

**8xxx**范围内的错误代码专用于评论相关错误。

| 错误代码 | 错误简称               | 详细信息                 |
| -------- | ---------------------- | ------------------------ |
| 8001     | CommentGenericError    | 发生未知错误。           |
| 8002     | CommentPostForbidden   | 您无权在此页发布评论。   |
| 8003     | CommentContentMissing  | 评论内容缺失或过短。     |
| 8004     | CommentManageForbidden | 您无权管理此页面的评论。 |
| 8005     | CommentNotFound        | 该评论不存在。           |
| 8006     | CommentViewForbidden   | 您无权查看此页面的评论。 |
