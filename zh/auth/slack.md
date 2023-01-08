---
title: Slack
description: Authentication Module
published: true
date: 2019-10-05T03:48:02.570Z
tags: 
---

Slack is a cloud-based set of proprietary team collaboration tools and services.
[slack.com](https://slack.com)

# Setup

## A) Create Slack Application

1. If not already the case, create a workspace for your organization on [Slack](https://slack.com/).
1. Nagivate to the [Your Apps](https://api.slack.com/apps?new_app=1) page to create a new app.
1. Enter a **name** (e.g. Wiki) and select your workspace.
1. Click **Create App**.
1. Once the app is created, click on **OAuth & Permissions** from the left sidebar.
1. Under the **Scope** section, add the following scopes:
	- `identity.avatar` - *View user’s Slack avatar*
  	- `identity.basic` - *Confirm user’s identity*
  	- `identity.email` - *View user’s email address*
1. Click on **Basic Information** from the left sidebar.
1. Under the **App Credentials** section, copy the **Client ID** and **Client Secret** values. We'll need them later.

## B) Enable the Slack strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **Slack**.
1. Enter the **Client ID** and **Client Secret** values copied earlier.
1. Enter the **Team / Workspace ID**. (e.g. If your url is **acme**.slack.com, you would enter **acme**)
1. Enable the **Self-registration** option *(unless you plan on authorizing users manually)*.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **Slack** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.
1. Copy the **Callback URL / Redirect URI** value found below the settings.

## C) Enter the allowed endpoints on Slack

Going back to the app page on the Slack website, click on **OAuth & Permissions** in the left sidebar. Under the **Redirect URLs** section, add the redirect URL to your wiki you just copied. Click the **Save URLs** button when done.

While optional, it's also recommended to set a description and logo under **Basic Information** > **Display Information** for easy identification by your end users.

Finally, click the **Install App to Workspace** button at the top to authorize this application on your workspace.

![](https://static.requarks.io/logo/slack.svg =x50){.align-abstopright}
  