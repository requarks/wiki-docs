---
title: Requirements
description: Prerequisites to install Wiki.js
published: true
date: 2025-05-04T03:57:54.793Z
tags: setup
editor: markdown
dateCreated: 2019-02-15T04:21:32.940Z
---

# Server Requirements

Wiki.js runs on virtually any system where Node.js is supported.
This means it runs on **Linux**, **macOS**, **Windows** as well as container solutions such as **Docker / Kubernetes** and **Heroku**.

### CPU
Wiki.js runs perfectly fine on a single CPU core. However, **2 cores or more are recommended** to fully make use of the background workers.

### RAM
Linux systems should have **at least 1GB of RAM** to run Wiki.js. Windows and macOS systems usually require a bit more RAM.

While the process itself usually sits at around 70MB of RAM, some events *(such as page rendering, indexing, etc.)* result in short bursts in RAM usage.

### Storage
Storage requirements are based on the content you will enter. Wikis that consists almost exclusively of text are not likely to exceed a few megabytes. However, as soon as you upload images, videos or other files, you should plan your storage requirements accordingly.

At least 1 GB of storage dedicated to Wiki.js is recommended.

### Internet Access
Wiki.js will automatically check for new updates, languages, themes, etc. from time to time. You can [read more](/install/requirements/internet) about what data is downloaded.

An alternate method of [sideloading files](/install/sideload) is also available if your environment is cut from the internet.

# Domain

Wiki.js requires a dedicated sub-domain / domain *(e.g. `wiki.example.com`)*. You cannot map Wiki.js to a subfolder.

# Database

For best performance, features and future compatibility, it's highly recommended to use **PostgreSQL**.

- ![](https://static.requarks.io/logo/postgresql.svg =24x){.mr-2} PostgreSQL **9.5 or later**
{.grid-list}

> It's recommended you use the latest version of PostgreSQL when possible.
{.is-success}

> Note that in order to use the PostgreSQL search module, the `pg_trgm` extension must be available on the host. The extension is part of the `postgresql-contrib` package in most Linux distributions. The docker PostgreSQL image already includes the extension.
{.is-info}

---

Wiki.js is also compatible with the following database systems:

- ![](https://static.requarks.io/logo/mysql.svg =24x){.mr-2} MySQL **8.0 or later** *(MySQL **5.7.8** is partially supported, [read more](/install/requirements/mysql5))*
- ![](https://static.requarks.io/logo/mariadb.svg =24x){.mr-2} MariaDB **10.2.7 or later**
- ![](https://static.requarks.io/logo/microsoft-sql-server-alt.svg =24x){.mr-2} MS SQL Server **2012 or later**
- ![](https://static.requarks.io/logo/sqlite-alt.svg =24x){.mr-2} SQLite **3.9 or later**
{.grid-list}

> **These engines *(MySQL, MariaDB, MS SQL Server and SQLite)* will NOT be supported in the next major version of Wiki.js**. Make sure you understand the implications of migrating your database to PostgreSQL if you plan on upgrading to 3.x+ in the coming years. An export + import tool will be made available at / shortly after release.
> 
> SQLite is **not recommended** for production deployments.
{.is-warning}

You're expected to have installed one of these database engines already *(either locally, on another server or using a cloud service)*. Wiki.js requires an empty database and preferably a unique user / pass to connect to the database.

# Node.js

The [Node.js](https://nodejs.org/) runtime is required. The following versions are supported:

- **Node.js 22**: version **22.0** or later. *(since v2.5.302)*{.text-caption}
- **Node.js 20**: version **20.0** or later. *(since v2.5.300)*{.text-caption}
- **Node.js 18**: version **18.0** or later. *(since v2.5.300)*{.text-caption}
{.grid-list}

> Odd-numbered versions (e.g. `23x`, `21.x`, `19.x`) are **NOT** officially supported.
{.is-danger}

### **Using Docker?** :whale:

> **Skip this requirement!** You don't need to install Node.js on your machine! It's included in the Docker image already.
{.is-info}

### **Web Server** :cloud:

Wiki.js doesn't need any actual web server (such as nginx or Apache). However, you might need to put a reverse proxy in front of Wiki.js if you require advanced network / DNS configuration.

# Supported Browsers

The following browsers are supported:

- Google Chrome (including Android version)
- Mozilla Firefox
- Microsoft Edge
- Apple Safari (including iOS version)

Note that only the latest stable version of these browsers are supported. All browsers are automatically updated in the background by default.

> There's limited compatibility with **IE11**. Users will be able to read content but not perform any editing action or use interactive features.
{.is-info}

![](https://a.icons8.com/ViUXyjOj/f4tFww/svg.svg){.align-abstopright}