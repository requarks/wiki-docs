---
title: GraphQL API
description: Access ressources and perform actions using the GraphQL API
published: true
date: 2019-12-22T20:41:17.403Z
tags: dev, api
---

# Overview

*Coming soon*

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
