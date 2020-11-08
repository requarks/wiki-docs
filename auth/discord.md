---
title: Discord
description: Authentication Module
published: true
date: 2019-09-15T02:39:23.450Z
tags: 
---

Discord is a popular gaming communication tool.
https://discordapp.com/

# Setup

## A) Create the application on Discord

1. Browse the [Discord Developer Portal](https://discordapp.com/developers/applications/). You'll need an existing account to proceed.
1. Click on **New Application** and enter a **name** (e.g. Wiki). Click **Create**.
1. Copy the **Client ID** and **Client Secret** values. We'll need them later.

## B) Enable the Discord strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Discord**.
1. Enter the **Client ID** and **Client Secret** values copied earlier.
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Discord** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

## C) Enter the OAuth2 settings on Discord

Going back to the Discord developer portal, you'll need to set the redirect URI. On the application page, click on **OAuth2** in the left sidebar and add the callback redirect URI. This value can be found in Wiki.js under **Configuration Reference**, displayed below the settings of the Discord strategy.

Click the **Save Changes** button at the bottom of the page when done.

While optional, it's also recommended to set an **Application Logo** for easy identification by your end users.

![](https://static.requarks.io/logo/discord.svg){.align-abstopright}
