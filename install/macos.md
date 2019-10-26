---
title: macOS
description: Getting started with a Wiki.js installation on macOS
published: true
date: 2019-10-26T03:52:21.901Z
tags: 
---

Before going any further, make sure your system meets all the [requirements](/install/requirements).

# Install

1. Open **Terminal**.
2. Download the latest version of Wiki.js:
  ```bash
  wget https://github.com/Requarks/wiki/releases/download/2.0.0-rc.1/wiki-js.tar.gz
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
5. Edit the config file and fill in your database, redis and port settings:
  ```bash
  nano config.yml
  ```
6. Run Wiki.js
  ```bash
  node server
  ```
7. Wait until you are invited to open to the setup page in your browser.
8. Complete the setup wizard to finish the installation.

> Note that if you're using SQLite, you need to install the macOS native bindings for SQLite by running `npm rebuild` from the Terminal.
{.is-warning}

# Run as service

*Coming soon*

![](https://a.icons8.com/eSUcnrow/jfIq9Q/svg.svg){.align-abstopright}