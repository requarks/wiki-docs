---
title: Users, Groups & Permissions
description: Manage access to your wiki
published: true
date: 2020-06-24T17:45:20.824Z
tags: 
editor: markdown
---

While a good wiki is one where anyone can contribute new content, it's always a good idea to restrict certain sections and specific actions to a list of selected users.

Wiki.js has a powerful permission system with fine grained control over what your users can see and do.

# Overview

The permission system of Wiki.js is based on 4 concepts:

- **Groups**
- **Users**
- **Permissions**
- **Page Rules**
{.grid-list}

A group contains multiple users, a set of permissions and a list of page rules.

![diag-permissions.jpg](/assets/diagrams/diag-permissions.jpg =1000x){.decor-shadow .radius-4}

A **user** can be part of **one or more** groups.

A **group** defines what users can see and what they can do. This is achieved by using 2 concepts: **Global Permissions** and **Page Rules**.

A **global permission** gives the right to a user to perform a very specific action. For example, the global permission `read:pages` allows the user to view pages, while the global permission `write:assets` allows the user to upload images and files. These global permissions act as a master switch to **allow or deny** a specific action on the wiki.

While global permissions are great a limiting the user to perform only a specific set of actions, it lacks control on **where** these permissions are applied. For example, you might want a user to be able to view pages under `/cities` but not pages under `/secret`. This is where **Page Rules** come into play.

A **page rule** specifies exactly where permissions are applicable.

---

**Let's use the following example:**
*We want users of group XYZ to be able to view pages and view assets where the path is exactly `/cities/montreal`.*

The page rule would be defined as:

- Allow or Deny: `Allow`
- Permissions: `read:pages, read:assets`
- Rule Pattern: `Path matches exactly...`
- Rule Value: `/cities/montreal`
{.grid-list}

![ss-pagerule-ex1.png](/assets/examples/ss-pagerule-ex1.png =1000x)

If we combine all the concepts together, the group would:

- Have one or more users
- Have the global permissions `read:pages` and `read:assets` enabled
- Have a page rule of `Allow` permissions `read:pages, read:assets` where `Path matches exactly`... `/cities/montreal`

---

***In which order are rules applied?***

Rules are applied in order of path specificity. A more precise path will always override a less defined path.

For example, `/geography/countries` will override `/geography`.

When 2 rules have the same specificity, the priority is given from lowest to highest as follows:
- Path Starts With... *(lowest)*{.caption}
- Path Ends With...
- Path Matches Regex...
- Path Is Exactly... *(highest)*{.caption}

When 2 rules have the same path specificity AND the same match type, `Deny` will always override an `Allow` rule.

***What is the default behavior for a permission?***

Unless you explicitely grant `Allow` on a permission, it will always be denied by default. Therefore, giving no permission is the same as adding a `Deny` rule for all permissions. As such, `Deny` rules are only needed to override a previous `Allow` rule. You do not need to add a `Deny` rule if you didn't `Allow` it in the first place at a lower level.

***Why have global permissions at all, instead of simply using page rules?***

Some actions are not tied to any particular path. For example, the ability to create users or manage groups. It's also useful to have a quick view of what a group can do without having to review a bunch of page rules to see whether a permission is applied. It's also easier to remove access globally to a specific action without modifying any page rule.

***Can I define a page rule with permissions that are not enabled in the global permissions?***

No. The global permissions always have priority over page rules. If a global permission is not enabled, the page rule will have no effect.

***Do I need to define page rules if I want users to have the permissions applied everywhere?***

Yes, for content permissions only. You need to define at least 1 page rule with the selected permissions and using the rule pattern where `Path starts with...` and a blank value.


# Groups

Manage groups in the **Administration Area** by clicking the **Groups** sidebar menu item.

There're 2 system groups that are predefined and cannot be deleted:

- **Administrators**
- **Guests**
{.grid-list}

They are identified by a lock icon in the list. The **administrators** group cannot be modified other than adding/removing users. The **guests** group can be modified with the exception of administrative roles which are locked.

# Users

Manage users in the **Administration Area** by clicking the **Users** sidebar menu item.

## Create New User

Click on the **New User** button to display the user creation dialog.

Select the authentication **Provider** to use for the user to be created. When selecting the **Local** authentication provider, you are creating a new user that lives uniquely in the database. For all other providers, a reference to the external service will be kept in the database to identify the user during login.

Fill in the details about the user:

![ui-user-create.png](/assets/ui/ui-user-create.png =450x){.radius-4 .decor-shadow}

**Tip:** You can click the dice icon to automatically generate a strong random password.

> **You must assign the user to at least 1 group.** Otherwise, they will not be able to access anything.
{.is-warning}

Click **Create and Close** to create the user. You can also click **Create** to create another user afterwards.


## Edit User

From the **Users** list, click on the user you want to edit.

Click the **pencil** icon next to the field(s) you want to edit. Click the **Update User** button, located at the top-right corner of the page to apply the modifications.

### Deactivate / Activate User

You can disable access to an account, without deleting it, by deactivating the user account. To do so, click on the **Actions** button and select **Deactivate**. The user will no longer be able to login.

Select **Activate** to enable access again.

### Manually Verify User

If the user was unable to verify their account or didn't receive the verification email, you can manually verify the action by clicking the **Actions** button and select **Set as Verified**.

## Delete User

While it's possible to delete an account, it's not recommended. It's always preferrable to deactivate the user instead.

To delete a user, select the account from the **Users** list, click the **Actions** button and select **Delete**. Confirm that you want to delete the account to proceed.

> Note that the **Guest** account cannot be deleted and some of its fields are locked.
{.is-info}

# Guides

## Private Wiki

To make your wiki completely private and require authentication in order to view any page, simply modify the **Guest** group in the **Administration Area -> Groups** section. Either change the default **Page Rule** from **Allow** to **Deny**, or remove all global permissions on the account. Both methods will result in the same behavior.

## Departments

To give a private space to each department of your company, create a **group** for each.

For each group, add a **Page Rule** with access to **path starting with...** a specific subfolder (e.g. `/accounting`, `/marketing`, etc.).

> Note that you cannot use 2 letters paths. Therefore, paths like `/hr` or `/it` will not work as they are reserved for languages.
{.is-warning}

Starting in Wiki.js **2.5**, you can redirect users directly to their subfolder upon login, instead of the homepage. In earlier versions, you should give read access to the `/home` path (using **Path matches exactly...** match) as this is the landing page for all users upon login.

![](https://a.icons8.com/kkjevabe/OINR8w/svg.svg){.align-abstopright}
