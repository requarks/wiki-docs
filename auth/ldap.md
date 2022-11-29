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
1. Enter the query to match a user with the entered username/email in the **Search Filter** field. The value MUST include the `{{username}}` tag. For example, if the username is stored in the `uid` field, the query would be `(uid={{username}})`. The `{{username}}` tag will be interpolated at runtime when performing the search.
1. If a TLS certificate must be provided to the LDAP server, enable the **Use TLS** option and enter the absolute path to the certificate file in the **TLS Certificate Path** field.
1. In case your directory fields are different than those used by Wiki.js, you can specify a mapping for each using the following fields:
	- **Unique ID Field Mapping**
  	- **Email Field Mapping**
  	- **Display Name Field Mapping**
  	- **Avatar Picture Field Mapping**
1. If you want your wiki to assign groups to users that match their LDAP groups, enable the **Map Groups** option.
> This also removes any existing group assignments that don't match LDAP, so consider this carefully before enabling for existing installations. If you have disabled any local wiki accounts you can lock yourself out. {.is-warning}
1. If you enabled the **Map Groups** option, enter the base DN to search for your LDAP groups in the **Group Search Base**.
1. The **Group Search Filter** is to specify the LDAP group property that contains group membership. The default works in most LDAP configurations, but will not search nested groups in Active Directory. For Active Directory, use something like **(member:1.2.840.113556.1.4.1941:={{dn}})** to search nested groups. See [Microsoft's documentation](https://social.technet.microsoft.com/wiki/contents/articles/5392.active-directory-ldap-syntax-filters.aspx) for more information. Any other LDAP provider you will need to modify the filter accordingly. {{dn}} will get replaced with the user property specified in **Group DN Property**.
1. Change the **Group Search Scope** from **sub** (search the base dn and any entries below the base dn) to **base** (search only the base dn) or **one** (search the base dn and one level below) only if your environment requires it.
1. Change the **Group DN Property** only if you assign group membership based on something other than the user's Distinguished Name.
1. Change the **Group Name Field** to the LDAP property that your groups define their name in. This is the LDAP field that your wiki will match group names on.
1. Enable the **Self-registration** option. *(unless you plan on authorizing users manually)*
1. Select the **group** new users should be assigned to when they login for the first time. Don't do this if you have **Map Groups** enabled.
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

