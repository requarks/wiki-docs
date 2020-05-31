---
title: Comments
description: List of supported Commenting Modules
published: true
date: 2020-05-31T22:49:35.277Z
tags: comments
---

> Available from version **2.4 and up**
{.is-info}

Comments modules add discussion capabilities to your pages.

From the administration area, you can enable a comment provider that work best for you.
Most modules require some configuration. Check out the links below for module specific configuration instructions.

# Enable Comments

The **Comments** feature must be enabled under **Administration > General** before you can start using comments.

# Modules

- [Commento](/comments/commento)
- [Default](/comments/default)
- [Disqus](/comments/disqus)
{.links-list}

# Permissions

> Permissions only apply to the **Default** module.
>
> External modules like Commento or Disqus are not tied to any Wiki.js group permissions or users. Moderation and authentication is handled exclusively by the module provider.
{.is-warning}

The ability to read, post or manage comments is controlled via group permissions. Ensure the group the user is member of has both the global permission and the page rule assigned to perform the desired comment action.

The following permissions are applied on a per-page basis as specified by the page rules:

- The `read:comments` permission grants the ability to read all comments.
- The `write:comments` permission grants the ability write new comments.
- The `manage:comments` permission grants the ability to edit and delete **all** comments *(not just their own)*. This should be given for moderation purposes only.
{.grid-list}

> If guests are allowed to post comments, they will be prompted to enter a **name** and an **email address**. This info will be stored along the comment. The guest email address and IP address can only be seen by administrators with the `manage:system` permission.
{.is-info}