---
title: Future Releases
description:  Long term plans and future major releases
published: true
date: 2020-07-25T19:28:04.692Z
tags: 
editor: markdown
---

This page list possible important features and refactoring ideas for future major versions.

> These are not set in stone and only serve as a discussion point.
{.is-warning}

# 3.x

## Use PostgreSQL as sole database engine

The current implementation for database handling is done via Knex.js and Objection.js, which allows for various drivers to be used for PostgreSQL, MySQL, MariaDB, SQL Server and SQLite. While it offers broad compatibility for users, it also brings major limitations for the architecture and development in general:

- Many different configurations to support
- Some functions require different implementations based on the driver
- Some functions are simply not implemented in some database engines:
	- *Recursive Queries*
  - *Pub/Sub Notification*
  - *Advanced Search Capabilities*
- Some migrations can be complex (specifically MS SQL Server)

Supporting PostgreSQL as the only database engine in 3.x would greatly simplify development.

## Switch to a full SPA model for navigation

At the moment, only the administration area is using a SPA navigation model (switch views without reloading the page). Standard view pages don't use this model for easier SEO.

In 3.x, site-wide SPA should be implemented in addition to server-side rendering of page contents.

## Switch to Quasar Vue framework

- Allows for easier server-side rendering and mobile capabilities.
- Better components *(specifically the table component)*