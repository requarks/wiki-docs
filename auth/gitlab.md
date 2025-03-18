---
title: GitLab
description: Authentication Module
published: true
date: 2023-12-04T09:56:00.798Z
tags: auth, module
---

GitLab Inc. is a web-based hosting service for version control using Git. It can be self-hosted.

# Setup

## A) Create (OAuth) Application

https://docs.gitlab.com/ee/integration/oauth_provider.html#create-a-user-owned-application

1. Go To GitLab -> On the left sidebar, select your avatar -> Select Edit profile -> On the left sidebar, select Applications -> Select Add new application 
 	- You can also use a group or the whole instance instead of your personal account. Refer to the [GitLab Documentation](https://docs.gitlab.com/ee/integration/oauth_provider.html#create-a-user-owned-application).
1. Enter an **Name** (e.g. Wiki.js).
1. Enter the **Redirect URI**. (e.g. enter your wikijs domain for now.)
	This value can be found later in Wiki.js under **Callback-URL**, displayed below the settings of the GitLab strategy.
1. Tick ☑️ Confidential
Scopes
    - Tick ☑️ read_user (Read the authenticated user's personal information)
    - Tick ☑️ openid (Authenticate using OpenID Connect)
    - Tick ☑️ profile (Allows read-only access to the user's personal information using OpenID Connect)
    - Tick ☑️ email (Allows read-only access to the user's primary email address using OpenID Connect)
1. Click **Save application**.
1. A **Application ID** and **Secret** will be shown. Copy these 2 keys. We'll need them later.
    - Leave this application detail view open as we'll have to edit the application later.

## B) Enable the GitLab strategy in Wiki.js

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **GitLab**.
1. Enter the **Client ID** and **Client Secret** values copied earlier.
1. For self-hosted GitLab enter the **Base URL** (e.g. gitlab.mydomain.com)
1. For special setups of self-hosted GitLab behind firewalls refer to **Authorization URL** and **Token URL**.
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **GitLab** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Copy **Callback URL/ Redirekt-URI** we need it back in the GitLab Application.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

## C) Enter the Wiki Redirect to GitLab Application.

1. Go back to your GitLab, in the application detail view -> Select Edit
1. Edit the **Redirect URI**, by entering the **Callback URL/ Redirekt-URI** from before.
1. Click **Save Application**.

![](https://static.requarks.io/logo/gitlab.svg =x50){.align-abstopright}
