---
title: Generic OpenID / OAuth2
description: Authentication Module
published: true
date: 2021-09-16T05:35:30.088Z
tags: auth, module
---

# Generic OpenID / OAuth2
OAuth 2.0 is an open standard [RFC6749](https://datatracker.ietf.org/doc/html/rfc6749)/[RFC6750](https://datatracker.ietf.org/doc/html/rfc6750) for access delegation.

OpenID Connect (OIDC) is implemented on top of OAuth 2.0 as a standard for source of identification.

Some auth providers implement this spec differently, so it's very useful to have an understanding of how the different flows work (at least the Authorization code flow).  
A REST client (like Insomnia or Postman) can be very useful to understand specific implementations of the endpoints and flows.

## More information
- [An Illustrated Guide to OAuth and OpenID Connect](https://developer.okta.com/blog/2019/10/21/illustrated-guide-to-oauth-and-oidc) by David Neal at Okta is a great introduction to OAuth 2.0 and OIDC
- [oauth.com](https://www.oauth.com/) - More in depth information about OAuth. They also have a [playground](https://www.oauth.com/playground/) that might be smart to check out first.

## Setup
### Create a `Generic OpenID Connect / OAuth2` strategy instance on Wiki.js
1. In the Administration area of your wiki, click on `Authentication` in the left navigation menu
2. Click on `+ ADD STRATEGY`, scroll down and select `Generic OpenID Connect / OAuth2`
3. Go to the bottom of the page and copy/note the `Callback URL / Redirect URI`
4. Keep this page/tab open. We will fill out the rest after creating the client

### Creating a client
This varies between different authorization servers, but in general you first have to create a client.  
Options to configure:
| Option | Example | Description | Aliases |
|-|-|-|-|
| `Client ID` | `wikijs` | The identificator for the authorization server | `id` |
| `Redirect URI` | `https://wiki.example.com/login/b7df954e-0fcb-4251-9398-b68f53bae7ad/callback` | The URI the authorization server should redirect the browser to after authorization. Sometimes it only requires the Base URL or both. Use the `Redirect URI` you copied from Wiki.js. | `Callback URL`, `Allowed Web Origins`, `Root URL`, `Base URL` |
| `Client Type` | `confidential` | If the client is `public` or `confidential`. For Wiki.js it's `confidential` | `Access Type` |
| `Flow Type` | `Authorization Code Flow` | This should be set to what represents the `Authorization Code Flow` as that is what Wiki.js uses. Sometimes referred to as `Standard Flow` |  |
| `Client Authenticator` | Client ID and secret | Some authorization server require you to specify how the client will authenticate. Wiki.js uses a client ID (specified earlier) and a secret (You will need the secret in the next steps) | |

### Configure the strategy in Wiki.js
1. Go back to the page/tab we were on earlier in Wiki.js
3. Enter the **Client Id**, which is the `Client ID` from the previous section
4. Enter the **Client Secret**, which is the secret you should have gotten from the previous section
5. Enter the **Authorization Endpoint URL**, this depends on the authorization server, but it should be shown either in the software or documentation
6. Enter the **Token URL**, this depends on the authorization server, but it should be shown either in the software or documentation
7. Enter the **User Info URL**, this depends on the authorization server, but it should be shown either in the software or documentation
8. Enter the **Issuer**, this should be the URL of the authorization server. Ex. `https://auth.example.com`
9. You can enter the `Logout URL`, if it is provided by the authorizatin server. Ex. `https://auth.example.com/logout`
10. Check **Allow self-registration** to auto create users as they login for the first time.
11. Remember to add a group with at least read permissions in the **Assign to group** list
12. Click `Apply` in the top-right corner and try to login
