---
title: Google
description: Authentication Module
published: true
date: 2019-09-14T23:12:15.831Z
tags: 
---

Google specializes in Internet-related services and products, which include online advertising technologies, search engine, cloud computing, software, and hardware.
[Google Cloud Console](https://console.developers.google.com/)

# Setup

## A) Create Google Cloud Project

1. Launch the [Google Cloud Console](https://console.cloud.google.com/) and create a new project *(if not already the case)*.
1. From the left sidebar, click on **APIs & Services**.
1. At the top, click on **Enable APIs and Services**
1. Click on the **Google+ API** tile and enable it.
1. From the left sidebar, mouse over **APIs & Services** and choose **Credentials** in the sub-menu.
1. Click on the blue **Create credentials** button and choose **OAuth client ID**.
1. Select **Web application** as the application type.
1. Give a proper name *(e.g. Wiki.js)*
1. Leave the other fields empty for now, we'll fill them later.
1. Click **Create** to be presented with the **Client ID** and **Client Secret**. Copy these 2 keys. We'll need them later.

## B) Enable the Google strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Google**.
1. Enter the **Client ID** and **Client Secret** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Google** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

## C) Enter the allowed endpoints on Google

Going back to the **Credentials** page on the Google Cloud Console, click the edit icon next to the OAuth client you created earlier.

Enter the wiki's domain for **Authorized JavaScript origins**.

Enter the redirect URI (found under **Configuration Reference** displayed below the settings of the Google strategy in Wiki.js) in **Authorized redirect URIs**

Click **Save**.

## D) Set the OAuth consent screen

From the same Credentials page, click on the **OAuth consent screen** tab.

Fill in the name, logos, emails, etc. as needed.

In the **Scopes for Google APIs**, make sure the following scopes are listed:
- email
- profile
- openid

In the **Authorized domains**, make sure the domain of your wiki is listed.

![](https://static.requarks.io/logo/google.svg =x50){.align-abstopright}
  