---
title: Authentication
description: List of supported Authentication Modules
published: true
date: 2019-09-15T02:39:42.263Z
tags: 
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
- [LDAP / Active Directory](/auth/ldap)
- [Local](/auth/local)
- Microsoft
- Generic OAuth2
- Generic OpenID
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

![](https://a.icons8.com/dhhZkYZk/0ICOP9/svg.svg){.align-abstopright}