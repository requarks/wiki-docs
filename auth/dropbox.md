---
title: Dropbox
description: Authentication Module
published: true
date: 2019-12-25T21:17:17.481Z
tags: auth, module
---

Dropbox is a file hosting service that offers cloud storage, file synchronization, personal cloud, and client software.
https://www.dropbox.com

# Setup
## A) Create an OAuth app

1. Browse to https://www.dropbox.com/developers/apps
1. Click on **Create app**
1. Choose **Dropbox API** and the access type **App folder**
1. Name your app, e.g. `Wiki.js` and click **Create app**
1. Copy the **App key** and **App secret** values. We'll need them later.
1. Keep this tab opened, we'll need to enter some more settings later.

## B) Enable the Dropbox strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Dropbox**.
1. Enter the **App key** and **App secret** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Dropbox** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

## C) Enter the allowed endpoints on Dropbox

Going back to the application page on the Dropbox app dashboard, you'll need to enter the **Redirect URIs**. This value can be found in Wiki.js under **Configuration Reference**, displayed below the settings of the Dropbox strategy.

Click the **Add** button  when done. While optional, it's also recommended to fill in the **Branding** section for easy identification by your end users.

![](https://static.requarks.io/logo/dropbox.svg =x50){.align-abstopright}
