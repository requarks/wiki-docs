---
title: Create Pages
description: Write and edit pages
published: true
date: 2019-05-19T00:36:23.533Z
tags: 
---

*Coming soon*

# Naming rules

The following paths cannot be used for content and are reserved for system use.

## Single-character pages

**All** single character paths are reserved to access various parts of the Wiki:

- `a`: Administration Area
- `e`: Page Editor
- `f`: Assets Manager
- `h`: Page History
- `p`: User Profile
- `s`: Page Source
- `u`: Upload Endpoint *(API)*
- `w`: Personal Wiki

## IETF Language tags

Language tags in the formats listed below are reserved to specify the locale namespace to use.

- Two-letter language code (e.g. `en`, `fr`)
- Country specific locale code (e.g. `en-us`, `fr-ca`)

## Words

- favicons
- fonts
- graphql
- healthz
- img
- js
- login
- logout
- register
- svg

The paths must match exactly or be the first part of subfolder path. For example, the path `registering` is accepted while `register/test` is not.