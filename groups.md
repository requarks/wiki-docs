---
title: Users, Groups & Permissions
description: Manage access to your wiki
published: true
date: 2019-07-20T03:22:54.795Z
tags: 
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

A **group** defines what the user can see and what he can do. This is achieved by using 2 concepts: **Global Permissions** and **Page Rules**.

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

***So why have global permissions at all, instead of simply using page rules?***

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

You can either create new users or pre-authorize users from external authentication systems.

## Create New User

When selecting the **Local** authentication strategy, you are creating a new user that lives in the database. For all other strategies, refer to the **Pre-authorize External User** chapter below.

*-- Coming soon --*

## Pre-authorize External User

*-- Coming soon --*

## Edit User

*-- Coming soon --*

## Delete User

*-- Coming soon --*

> Note that the **Guest** account cannot be deleted and some of its fields are locked.
{.is-info}

# Private Wiki

To make your wiki completely private and require authentication in order to view any page, simply modify the **Guest** group in the **Administration Area -> Groups** section. Either change the default **Page Rule** from **Allow** to **Deny**, or remove all global permissions on the account. Both methods will result in the same behavior.

![](https://a.icons8.com/kkjevabe/OINR8w/svg.svg){.align-abstopright}