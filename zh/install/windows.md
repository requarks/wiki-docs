---
title: Windows
description: Getting started with a Wiki.js installation on Windows
published: true
date: 2022-04-04T19:36:52.733Z
tags: setup
editor: markdown
dateCreated: 2019-05-04T04:36:05.505Z
---

Before going any further, make sure your system meets all the [requirements](/install/requirements).

# Install

1. Open a **Powershell** prompt in administrator mode.
2. If you are using **Windows 7 / Windows Server 2008 R2 or older**, you must run the following command. *(otherwise skip this step)*
  ```powershell
  [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12
  ```
3. Download the latest version of Wiki.js:
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/Requarks/wiki/releases/latest/download/wiki-js-windows.tar.gz" -OutFile "wiki-js.tar.gz"
  ```

4. Extract the package to the final destination of your choice:
  ```powershell
  New-Item -Path "C:\" -Name "wiki" -ItemType "directory"
  tar xzf wiki-js.tar.gz -C "C:\wiki"
  cd C:\wiki
  ```
  > The **tar** utility is only available on Windows 10 and later. On earlier versions, you'll need a 3rd-party utility like [7-zip](https://www.7-zip.org/) to extract the file.
  {.is-warning}
5. Rename the sample config file to `config.yml`:
  ```powershell
  Rename-Item -Path config.sample.yml -NewName config.yml
  ```
6. Edit the config file using your favorite text editor (e.g. Notepad) and fill in your database and port settings ([Configuration Reference](/install/config)):
  ```powershell
  notepad .\config.yml
  ```
7. ***For SQLite installations only:*** *(skip this step otherwise)* Fetch native bindings for SQLite3:
  ```bash
  npm rebuild sqlite3
  ```
8. Run Wiki.js
  ```powershell
  node server
  ```
9. Wait until you are invited to open to the setup page in your browser.
10. Complete the setup wizard to finish the installation.

# Run as service

There are several solutions to run Wiki.js as a background service, e.g.:

- [AlwaysUp](https://www.coretechnologies.com/products/AlwaysUp/)
- [PM2](http://pm2.keymetrics.io/) / [pm2-windows-service](https://www.npmjs.com/package/pm2-windows-service)
- [forever](https://www.npmjs.com/package/forever)
- [node-windows](https://github.com/coreybutler/node-windows)

![](https://a.icons8.com/djxbtnYm/GBjHDS/svg.svg){.align-abstopright}