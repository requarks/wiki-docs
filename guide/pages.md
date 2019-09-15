---
title: Pages
description: Create and edit content
published: true
date: 2019-09-15T20:30:39.296Z
tags: 
---

> This page is under development!
{.is-warning}

# Create a Page

There're multiple ways to create a new pages:

- From the **Page Menu**, located at the top-left corner of the page.
- By clicking a link pointing to a non-existing page.
- Manually type the path in the browser address bar.


# Edit a Page

You can edit an existing page by clicking the **Pencil** icon at the bottom-right corner of any page or using the **Page Menu**, located at the top-right corner of the page.

The editor selected when first creating the page will be loaded automatically. Note that it's not possible to change editor once a page is created.

# Naming Restrictions

The following paths cannot be used for content and are reserved for system use.

## Single-character pages

**All** single character paths are reserved to access various parts of the Wiki:

- `a`: Administration Area
- `e`: Page Editor
- `f`: Assets Manager
- `h`: Page History
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