---
title: Azure Active Directory
description: Authentication Module
published: true
date: 2022-08-31T17:01:57.649Z
tags: auth, module
editor: markdown
dateCreated: 2019-07-20T15:31:49.465Z
---

[Azure Active Directory (Azure AD)](https://azure.microsoft.com/en-ca/services/active-directory/) is Microsoft’s cloud-based identity and access management service, which helps your employee's sign in and access resources.

# Setup

## A) Copy the redirect URI

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Add a new **Azure Active Directory** auth strategy.
1. Copy the **Redirect URI** value found under the configuration reference section. Keep this page opened. We'll come back to it later.

## B) Create Azure AD Application

1. From the Azure Portal, open the **Azure Active Directory** resource.
1. Click on **App registrations** in the left navigation and then click **New registration** at the top.
1. Enter a **Name** (e.g. Wiki.js) and enter the **Redirect URI** you copied earlier.
1. Click **Register**.
1. Copy the **Application (client) ID**, you'll need it later.
1. Click on **Endpoints** at the top and copy the endpoint value for **OpenID Connect metadata document** (e.g. `https://login.microsoftonline.com/YOUR_TENANT_ID/v2.0/.well-known/openid-configuration`), you'll need it later.
1. *(Optional)* Click on **Branding** in the left navigation and enter the necessary info to make it easier for your users.
1. Click on **Authentication** in the left navigation and enter the **Logout URL** (`https://YOUR-WIKI.DOMAIN.COM`) and make sure the **ID tokens** checkbox under **Implicit grant** is checked, then click **Save** at the top.
1. Click on **API permissions** in the left navigation and ensure the **Microsoft Graph > User.Read** permission is listed.
1. *(Optional)* In the **API permissions** section, you can **Grant admin consent** on behalf of all users in the directory. This will prevent the consent screen from being shown to the user the first time they login, which is often preferable in an internal organization environment.

## C) Enable the Azure AD strategy in Wiki.js

1. Go back to the Wiki.js administration page from step A.
1. Enter the **Identity Metadata Endpoint** and **Client ID** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Azure Active Directory** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

<img src="https://static.requarks.io/logo/azure.svg" class="align-abstopright" style="width:150px;" />
  
