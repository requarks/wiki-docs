---
title: macOS
description: Getting started with a Wiki.js installation on macOS
published: true
date: 2022-04-04T19:36:37.695Z
tags: setup
editor: markdown
dateCreated: 2019-05-04T04:13:20.311Z
---

Before going any further, make sure your system meets all the [requirements](/install/requirements).

# Install

1. Open **Terminal**.
2. Download the latest version of Wiki.js:
  ```bash
  wget https://github.com/Requarks/wiki/releases/latest/download/wiki-js.tar.gz
  ```
3. Extract the package to the final destination of your choice:
  ```bash
  mkdir wiki
  tar xzf wiki-js.tar.gz -C ./wiki
  cd ./wiki
  ```
4. Rename the sample config file to `config.yml`:
  ```bash
  mv config.sample.yml config.yml
  ```
5. Edit the config file and fill in your database and port settings ([Configuration Reference](/install/config)):
  ```bash
  nano config.yml
  ```
6. ***For SQLite installations only:*** *(skip this step otherwise)* Fetch native bindings for SQLite3:
  ```bash
  npm rebuild sqlite3
  ```

7. Run Wiki.js
  ```bash
  node server
  ```
8. Wait until you are invited to open to the setup page in your browser.
9. Complete the setup wizard to finish the installation.

# Run as service

*Coming soon*

![](https://a.icons8.com/eSUcnrow/jfIq9Q/svg.svg){.align-abstopright}