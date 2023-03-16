---
title: MySQL 5.7 Notice
description: Limited support for this MySQL version
published: true
date: 2019-05-27T02:00:03.838Z
tags: 
---

# Affected versions

- MySQL **5.7.8** and up in the 5.7.x range.

# Limited Functionality

## Uploads

Uploading assets is only possible in the root folder. It's not possible to upload files in a folder or nested folders. Doing so will result in an error at upload time.

# Cause

MySQL 5.7.x does not support the `WITH RECURSIVE` expression, which is required to fetch the folder hierarchy. This expression was introduced in version 8.0.