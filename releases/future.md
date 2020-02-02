---
title: Future Releases
description:  Long term plans and future major releases
published: true
date: 2020-02-02T21:19:26.210Z
tags: 
---

This page list possible important features and refactoring ideas for future major versions.

> These are not set in stone and only serve as a discussion point.
{.is-warning}

# Use PostgreSQL as sole database engine

The current implementation for database handling is done via Knex.js and Objection.js, which allows for various drivers to be used for PostgreSQL, MySQL, MariaDB, SQL Server and SQLite. While it offers broad compatibility for users, it also brings major limitations for the architecture and development in general:

- Many different configurations to support
- Some functions require different implementations based on the driver
- Some functions are simply not implemented in some database engines:
	- *Recursive Queries*
  - *Pub/Sub Notification*
  - *Advanced Search Capabilities*
- Some migrations can be complex (specifically MS SQL Server)

Supporting PostgreSQL as the only database engine in 3.x would greatly simplify development.