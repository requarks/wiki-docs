---
title: Authentication
description: List of supported Authentication Modules
published: true
date: 2023-01-15T02:28:15.032Z
tags: auth
editor: markdown
dateCreated: 2019-04-29T00:57:43.566Z
---

Authentication modules allows for secure and simple login.

From the administration area, you can enable authentication strategies that work best for you. Multiple strategies can be enabled at the same time. For example, you could allow your users to login using their Google, Facebook or GitHub account.

Note that the default **Local** strategy cannot be disabled as it is required for root administrator login.

Most strategies require some configuration. Check out the links below for module specific configuration instructions.

# Modules

- [Auth0](/auth/auth0)
- [Azure AD](/auth/azure)
- CAS
- [Discord](/auth/discord)
- [Dropbox](/auth/dropbox)
- [Facebook](/auth/facebook)
- Firebase
- [GitHub](/auth/github)
- [Google](/auth/google)
- [Keycloak OpenID Connect](/auth/keycloak)
- [LDAP / Active Directory](/auth/ldap)
- [Local](/auth/local)
- Microsoft
- Generic OpenID / OAuth2
- [Okta](/auth/okta)
- [SAML 2.0](/auth/saml)
- [Slack](/auth/slack)
- [Twitch](/auth/twitch)
{.links-list}

# Self-registration

**By default, new users are not authorized to access anything.** They must either be pre-authorized by an administrator or be put into an existing group using the self-registration option.

The latter greatly simplifies the onboarding of new users. The self-registration option can be enabled on a per authentication strategy basis.

## Setup

On the authentication module configuration page, enable the **Self-registration** option.

You can optionally set a domain whitelist so that only users with a specific email domain can proceed. To do so, enter a list of domains, e.g.: `company.com` then press <kbd>Enter</kbd>. Repeat for all domains you want to authorize.

Finally, select the group new users will be assigned to the first time they log in.

Click **Apply** to save the configuration.

# Two-Factor Authentication

> This feature is available from version **2.5 and up**.
{.is-info}

Two-Factor Authentication (2FA) adds an extra layer of protection to user accounts. It combines something you know *(your password)* with something you have / are *(mobile phone, fingerprint, security key, etc.)*.

Even if a malicious user obtain your password, they will be unable to login because they don't have the second authentication factor.

## Getting Started

2FA can be enabled globally to all users or on per-user basis.

### Global

To force all users to use 2FA on their account, go to the **Administration Area** and click on **Security** in the sidebar navigation.

Enable the **Enforce 2FA** option and click **Apply**.

All users will be required to setup 2FA on their account the next time they login.

### Per User

In the **Administration Area**, click on **Users** in the sidebar navigation.

Select the user to edit and click on the **ON** switch next to the **Two Factor Authentication** row.

The user will be required to setup 2FA on their account the next time they login.

> At the moment, only the administrator can enable 2FA for a user. Users will be able to self-enable 2FA in a future release.
{.is-info}

## Supported Methods

- **OTP (One-Time Passwords)** <i class="mdi mdi-check green--text"></i>
	- TOTP *(Authy, Google Authenticator, Microsoft Authenticator)*{.caption} <i class="mdi mdi-check green--text"></i>
- **WebAuthn** <i class="mdi mdi-clock-outline orange--text"></i> *(Planned for a future update)*{.caption .orange--text .text--darken-3}
	- Windows Hello
  - FIDO2 *(Yubikey 5)*{.caption}
  - FIDO U2F *(Yubikey 4 and earlier, Google Titan Key)*{.caption}
- **SMS Codes** <i class="mdi mdi-close red--text"></i> *(No plan to support in the future as this method is **unsafe** and unreliable.)*{.caption .red--text}

# Customize Login Flow

It's possible to modify how the login experience is presented to the user from the **Administration Area** > **Security** section:

## Login Background Image

An alternate image background can be set for the login screen. Enter the full path to an image *(.jpg / .png)*.

> Note that if you upload an image directly to the wiki, you must ensure that this path is accessible to guest users! It's recommended to upload the image to a dedicated asset folder and give `read:assets` permission to that folder path on the **Guests** group.
{.is-warning}

## Bypass Login Screen

When using a social provider *(e.g. Google authentication)*, you may want to skip the login screen altogether and redirect the user directly to the social provider for a faster login.

> You can always access the login screen even when this option is enabled by adding `?all=1` to the login URL. *(e.g. `https://wiki.example.com/login?all=1`)*
{.is-info}

## Hide Local Provider

If you have multiple authentication providers enabled but wish to hide the default local provider, you can enable this option to hide it.

> You can always unhide it when this option is enabled by adding `?all=1` to the login URL. *(e.g. `https://wiki.example.com/login?all=1`)*
{.is-info}