---
title: Pages
description: Create and edit content
published: true
date: 2020-05-15T17:55:58.198Z
tags: 
---

# Create a Page

There're multiple ways to create a new pages:

- From the **New Page** button, located at the top-right corner of the page.
- By clicking a link pointing to a non-existing page.
- Manually type the path in the browser address bar.

Check out the [Basics](/guide/intro) guide on how to create your first page step-by-step.


# Edit a Page

You can edit an existing page by clicking the **Pencil** icon at the bottom-right corner of any page or using the **Page Menu**, located at the top-right corner of the page.

The editor selected when first creating the page will be loaded automatically. Note that it's not possible to change editor once a page is created at the moment.

# Folders

Wiki.js doesn't rely on a traditional folder structure to organize pages. Instead, the path of the page is used.

For example, on a traditional system, in order to create a page at `universe/planets/earth`, you'd need to first create a folder `universe`, then open this folder and create a sub-folder named `planets` to finally be able to create a page inside named `earth`.

In Wiki.js, you can directly create a page at path `universe/planets/earth`. Folders `universe` and `planets` will be automatically inferred, but they don't really exist outside of the page path context. Therefore, you don't have to manage folders and you can instead focus solely on the path you want for your pages.

For this reason, there's no option to create folders. Simply type the full path you want. Folders will be inferred automatically upon creation.

Check out the [Folder Structure & Tags](/guide/structure) guide for more details.

# Naming Restrictions

The following paths cannot be used for content and are reserved for system use.

## Single-character pages

**All** single character paths are reserved to access various parts of the Wiki:

- `a`: Administration Area
- `c`: Comments
- `e`: Page Editor
- `f`: Assets Manager
- `h`: Page History
- `i`: Browse Page by ID
- `p`: User Profile
- `s`: Page Source
- `t`: Tags
- `u`: Upload Endpoint *(API)*
- `w`: Personal Wiki
{.grid-list}

## IETF Language tags

Language tags in the formats listed below are reserved to specify the locale namespace to use.

- Two-letter language code (e.g. `en`, `fr`)
- Country specific locale code (e.g. `en-us`, `fr-ca`)
{.grid-list}

## Words

Paths cannot match exactly the terms below or be the first part of path. For example, `register` or `register/test` are not valid paths, but `registering` is fine.

### 2.4 and later

- _assets
- favicon *\[.ico]*
- graphql
- healthz
- home *(reserved for the root homepage)*
- login
- logout
- register
{.grid-list}

### 2.0 to 2.3

- browserconfig *\[.xml]*
- css
- favicon *\[.ico]*
- favicons
- fonts
- graphql
- healthz
- home *(reserved for the root homepage)*
- img
- js
- login
- logout
- manifest *\[.json]*
- register
- svg
{.grid-list}

## Illegal Characters

Paths cannot contain the following characters:

- Space *(use dashes instead)*
- Period *(reserved for file extensions)*
- Unsafe URL characters *(such as punctuation marks, quotes, math symbols, etc.)*