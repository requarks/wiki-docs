---
title: Auth0
description: Authentication Module
published: true
date: 2019-09-15T02:38:37.784Z
tags: 
---

Auth0 is a popular cloud service for managing authentication across your applications.
[auth0.com](https://auth0.com)

# Setup

## A) Create Auth0 Application

1. If not already the case, create an account on [Auth0](https://auth0.com/)
1. From the dashboard, click on **Applications** in the left navigation.
1. Click **Create Application**, enter a **name** (e.g. Wiki) and select **Regular Web Applications** as the type.
1. Click **Create**.
1. Once the application is created, switch to the **Settings** tab.
1. Copy the **Domain**, **Client ID** and **Client Secret** values. We'll need them later.

## B) Enable the Auth0 strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Auth0**.
1. Enter the **Domain**, **Client ID** and **Client Secret** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Auth0** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

## C) Enter the allowed endpoints on Auth0

Going back to the application page on the Auth0 dashboard website, you'll need to fill in the values for:
- Allowed Callback URLs
- Allowed Web Origins
- Allowed Logout URLs

These values can be found in Wiki.js under **Configuration Reference**, displayed below the settings of the Auth0 strategy. Click the **Save Changes** button at the bottom of the page when done. While optional, it's also recommended to set an **Application Logo** for easy identification by your end users.

![](https://static.requarks.io/logo/auth0.svg =x50){.align-abstopright}
  