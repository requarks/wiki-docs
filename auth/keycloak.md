---
title: Keycloak
description: Authentication Module
published: true
date: 2021-09-15T07:49:57.150Z
tags: auth, module
---

# Keycloak
[Keycloak](https://keycloak.org) is an Open Source Identity and Access Management solution for modern Applications and Services.

## Relevant information
- [Keycloak OIDC Endpoints](https://www.keycloak.org/docs/latest/server_admin/#keycloak-server-oidc-uri-endpoints)
- [Keycloak OIDC Clients](https://www.keycloak.org/docs/latest/server_admin/#_clients)

## Setup
### Create Keycloak strategy instance on Wiki.js
1. In the Administration area of your wiki, click on `Authentication` in the left navigation menu
2. Click on `+ ADD STRATEGY`, scroll down and select `Keycloak`
3. Go to the bottom of the page and copy/note the `Callback URL / Redirect URI`
4. Keep this page/tab open. We will fill out the rest after setting up the Keycloak client

### Creating a Keycloak client
1. At the Keycloak administration page, go to the `Clients` menu, and click `Create` button on the right
2. Enter a **Client ID**, for example `wikijs` (You wil need the `Client ID` later)
3. Select **openid-connect** as `Client Protocol`
4. And **Root URL** is the base URL to Wikijs (for example `https://wiki.example.com`)
5. Click **Save**
6. Change **Access Type** to `confidential`
7. Enter the **Valid Redirect URIs**, which is the `Callback URL / Redirect URI` from Wiki.js (ex. `https://wiki.example.com/login/d03f689b-0dd0-44d6-90ca-6386ec41d799/callback`, or just the path `/login/{GUID}/callback`)
8. Set **Base URL** to the same as `Root URL`
9. Set **Web Origins** to `+`, which means to use the URIs in the `Valid Redirect URIs` entry.
10. Now click **Save** at the bottom of the page
11. Go to the **Credentials** tab and copy the `Secret` (You will need this one later too)

### Configure the Keycloak strategy in Wiki.js
1. If you're not already there. Go to the Administration area of your wiki, click on `Authentication` in the left navigation menu
2. Click on **Keycloak**
3. Enter the **Host**, which is the domain (incl. the scheme) of your Keycloak server (Example: `https://keycloak.example.com`)
4. Enter the **Realm**, which is the realm you are using in Keycloak (Default is: `master`)
5. Enter the **Client Id**, which is the `Client ID` from Keycloak
6. Enter the **Client Secret**, which is the `Secret` from Keycloak
7. Enter the **Authorization Endpoint URL**, which is `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/auth`
8. Enter the **Token URL**, which is `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/token`
9. Enter the **User Info URL**, which is `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/userinfo`
10. If you want the user to be logged out of Keycloak when logging out of Wiki.js, enable `Logout from Keycloak on Logout`
11. Enter the `Logout Endpoint URL`, which is `https://keycloak.example.com/auth/realms/master/protocol/openid-connect/logout`
12. Check **Allow self-registration** to enable the Keycloak login button, and auto create users as they login for the first time.
13. Remember to add a group with at least read permissions in the **Assign to group** list
14. Click `Apply` in the top-right corner and try to login

### Seamless login
If the login worked, you can enable `Bypass Login Screen` under the `Security` tab in the left navigation menu.  
Make sure the Keycloak provider is at the top of the list in the `Authentication` tab.

![](https://static.requarks.io/logo/keycloak.svg =x50){.align-abstopright}