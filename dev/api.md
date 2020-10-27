---
title: GraphQL API
description: Access ressources and perform actions using the GraphQL API
published: true
date: 2020-05-31T21:46:50.626Z
tags: dev, api
---

# Overview

Wiki.js exposes a [GraphQL](https://graphql.org/) API from which you can access and modify all the resources of your wiki.

> The **GraphQL endpoint** is located at `/graphql`
{.is-success}

You can access this endpoint from your browser to load the **GraphQL Playground** tool which lets you build and test queries, as well as explore all the possible resources you can access.

There're various [client libraries](https://github.com/chentsulin/awesome-graphql#libraries) available for most programming languages to easily make GraphQL queries. Desktop API clients like **Postman**, **Insomnia** and **Firecamp** all support GraphQL queries.

# Authentication

> The API Access feature is available from version **2.2 and up**.
{.is-info}

Access to resources requires a **valid API token**, which can be generated from the **Administration Area** (under **API Access**).

The token must be passed in the `Authorization` header, as a `Bearer` token, of any request made to the GraphQL endpoint, e.g.:
```css
Authorization: Bearer eyJhbGc...aXczt18H6437W
```

Different **permission scopes** are required based on the resource you wish to query / mutate. Ensure the API token you created contains these permission scopes.

# Error Reference

Mutations always return a `responseResult` property object of type `ResponseStatus`:
```graphql
type ResponseStatus {
  succeeded: Boolean!
  errorCode: Int!
  slug: String!
  message: String
}
```

*Example Response:*
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

Use the reference below to match codes to their slugs and detailed message.

## Authentication / Users

Error codes in the **1xxx** range are dedicated to authentication / users errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 1001 | AuthGenericError | An unexpected error occured during login. |
| 1002 | AuthLoginFailed | Invalid email / username or password. |
| 1003 | AuthProviderInvalid | Invalid authentication provider. |
| 1004 | AuthAccountAlreadyExists | An account already exists using this email address. |
| 1005 | AuthTFAFailed | Incorrect TFA Security Code. |
| 1006 | AuthTFAInvalid | Invalid TFA Security Code or Login Token. |
| 1007 | BruteInstanceIsInvalid | Invalid Brute Force Instance. |
| 1008 | BruteTooManyAttempts | Too many attempts! Try again later. |
| 1009 | UserCreationFailed | An unexpected error occured during user creation. |
| 1010 | AuthRegistrationDisabled | Registration is disabled. Contact your system administrator. |
| 1011 | AuthRegistrationDomainUnauthorized | You are not authorized to register. Your domain is not whitelisted. |
| 1012 | InputInvalid | Input data is invalid. |
| 1013 | AuthAccountBanned | Your account has been disabled. |
| 1014 | AuthAccountNotVerified | You must verify your account before your can login. |
| 1015 | AuthValidationTokenInvalid | Invalid validation token. |
| 1016 | UserNotFound | This user does not exist. |
| 1017 | UserDeleteForeignConstraint | Cannot delete user because of content relational constraints. |
| 1018 | UserDeleteProtected | Cannot delete a protected system account. |
| 1019 | AuthRequired | You must be authenticated to access this resource. |
| 1020 | AuthPasswordInvalid | Password is incorrect. |

## Assets

Error codes in the **2xxx** range are dedicated to assets errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 2001 | AssetGenericError | An unexpected error occured during asset operation. |
| 2002 | AssetFolderExists | An asset folder with the same name already exists. |
| 2003 | AssetDeleteForbidden | You are not authorized to delete this asset. |
| 2004 | AssetInvalid | This asset does not exist or is invalid. |
| 2005 | AssetRenameCollision | An asset with the same filename in the same folder already exists. |
| 2006 | AssetRenameForbidden | You are not authorized to rename this asset. |
| 2007 | AssetRenameInvalid | The new asset filename is invalid. |
| 2008 | AssetRenameInvalidExt | The file extension cannot be changed on an existing asset. |
| 2009 | AssetRenameTargetForbidden | You are not authorized to rename this asset to the requested name. |

## Mail

Error codes in the **3xxx** range are dedicated to mail errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 3001 | MailGenericError | An unexpected error occured during mail operation. |
| 3002 | MailNotConfigured | The mail configuration is incomplete or invalid. |
| 3003 | MailTemplateFailed | Mail template failed to load. |
| 3004 | MailInvalidRecipient | The recipient email address is invalid. |

## Search

Error codes in the **4xxx** range are dedicated to search errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 4001 | SearchGenericError | An unexpected error occured during search operation. |
| 4002 | SearchActivationFailed | Search Engine activation failed. |

## Localization

Error codes in the **5xxx** range are dedicated to localization errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 5001 | LocaleGenericError | An unexpected error occured during locale operation. |
| 5002 | LocaleInvalidNamespace | Invalid locale or namespace. |

## Pages

Error codes in the **6xxx** range are dedicated to pages / rendering errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 6001 | PageGenericError | An unexpected error occured during a page operation. |
| 6002 | PageDuplicateCreate | Cannot create this page because an entry already exists at the same path. |
| 6003 | PageNotFound | This page does not exist. |
| 6004 | PageEmptyContent | Page content cannot be empty. |
| 6005 | PageIllegalPath | Page path cannot contains illegal characters. |
| 6006 | PagePathCollision | Destination page path already exists. |
| 6007 | PageMoveForbidden | You are not authorized to move this page. |
| 6008 | PageCreateForbidden | You are not authorized to create this page. |
| 6009 | PageUpdateForbidden | You are not authorized to update this page. |
| 6010 | PageDeleteForbidden | You are not authorized to delete this page. |
| 6011 | PageRestoreForbidden | You are not authorized to restore this page version. |
| 6012 | PageHistoryForbidden | You are not authorized to view the history of this page. |
| 6013 | PageViewForbidden | You are not authorized to view this page. |

## System

Error codes in the **7xxx** range are dedicated to system related errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 7001 | SystemGenericError | An unexpected error occured. |
| 7002 | SystemSSLDisabled | SSL is not enabled. |
| 7003 | SystemSSLRenewInvalidProvider | Current provider does not support SSL certificate renewal. |
| 7004 | SystemSSLLEUnavailable | Let's Encrypt is not initialized. |

## Comments

Error codes in the **8xxx** range are dedicated to comments related errors.

| Code | Slug | Message |
|------|------------------|-------------------------------------------|
| 8001 | CommentGenericError | An unexpected error occured. |
| 8002 | CommentPostForbidden | You are not authorized to post a comment on this page. |
| 8003 | CommentContentMissing | Comment content is missing or too short. |
| 8004 | CommentManageForbidden | You are not authorized to manage comments on this page. |
| 8005 | CommentNotFound | This comment does not exist. |
| 8006 | CommentViewForbidden | You are not authorized to view comments for this page. |
