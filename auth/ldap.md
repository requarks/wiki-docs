---
title: LDAP / Active Directory
description: Authentication Module
published: true
date: 2020-06-12T20:34:21.239Z
tags: auth, module
editor: markdown
---

LDAP / Active Directory is an enterprise authentication solution developed by Microsoft.

# Setup

1. In the **Administration Area** of your wiki, click on **Authentication** in the left navigation.
1. Click on **LDAP / Active Directory**.
1. Enter the **LDAP URL** where the LDAP server can be reached.
1. Enter the distinguished name in **Admin Bind DN** of the account used for binding.
1. Enter the password in **Admin Bind Credentials** for the account specified above.
1. Enter the base DN to search users from, in the **Search Base** field.
1. Enter the query to match a user with the entered username/email in the **Search Filter** field. The value MUST include the `{{username}}` tag. For example, if the username is stored in the `uid` field, the query would be `(uid={{username}})`. The `{{username}}` tag will be interpolated at runtime when performing the search (the active directory default setting should be `(sAMAccountName={{username}})`) .
1. If a TLS certificate must be provided to the LDAP server, enable the **Use TLS** option and enter the absolute path to the certificate file in the **TLS Certificate Path** field.
1. In case your directory fields are different than those used by Wiki.js, you can specify a mapping for each using the following fields:
	- **Unique ID Field Mapping**
  	- **Email Field Mapping**
  	- **Display Name Field Mapping**
  	- **Avatar Picture Field Mapping**
1. Enable the **Self-registration** option. *(unless you plan on authorizing users manually)*
1. Select the **group** new users should be assigned to when they login for the first time.
1. Make sure the checkbox next to **LDAP / Active Directory** in the list of strategies is checked. The text should now say that the strategy is **active**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

# Test Your Configuration

Saving your LDAP configuration doesn't actually perform a connection to your LDAP Server. You need to perform an actual login to establish a connection.

To do so, open an incognito window in your browser and attempt to login to your wiki with a user in your directory.

# Troubleshooting

If you get errors while trying to login, you can enable a LDAP debugging flag to report internal LDAP error messages to the console (or docker logs).

From the **Administration Area**, click on **Developer Tools** in the sidebar, then on **Flags**. Enable the **LDAP Debug** flag.

> When using docker, type the command `docker logs wiki` to view the logs *(assuming a container named `wiki`)*. 
{.is-info}

