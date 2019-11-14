---
title: Okta
description: Authentication Module
published: true
date: 2019-11-14T23:31:19.440Z
tags: auth, module
---

Okta provide secure identity management and single sign-on to any application.

# Setup

## A) Create Okta Application

1. From the Okta control panel, click on **Applications** in the top navigation bar.
1. Click on **Add Application**, then on **Create New App**.
1. Select **Web** as the platform and **OpenID Connect** as the sign-in method.
1. Enter the **Application Name** (e.g. Wiki.js) and optionally a logo.
1. Enter the **Login redirect URIs** using the format `https://YOUR-WIKI-DOMAIN/login/okta/callback`
1. Enter the **Logout redirect URIs** using the format `https://YOUR-WIKI-DOMAIN/`.
1. Click **Save**.
1. A **Client ID** and **Client Secret** will be shown to the bottom of the page. Copy these 2 keys. We'll need them later.

## B) Enable the Okta strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Okta**.
1. Enter the **Client ID** and **Client Secret** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Okta** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

![](https://static.requarks.io/logo/okta.svg =x50){.align-abstopright}