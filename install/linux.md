---
title: Linux
description: Getting started with a Wiki.js installation on Linux
published: true
date: 2019-09-14T19:59:44.301Z
tags: 
---

Before going any further, make sure your system meets all the [requirements](/install/requirements).

# Install

1. Download the latest version of Wiki.js:
  ```bash
  wget https://github.com/Requarks/wiki/releases/download/2.0.0-beta.303/wiki-js.tar.gz
  ```
2. Extract the package to the final destination of your choice:
  ```bash
  mkdir wiki
  tar xzf wiki-js.tar.gz -C ./wiki
  cd ./wiki
  ```
3. Rename the sample config file to `config.yml`:
  ```bash
  mv config.sample.yml config.yml
  ```
4. Edit the config file and fill in your database, redis and port settings:
  ```bash
  nano config.yml
  ```
5. Run Wiki.js
  ```bash
  node server
  ```
6. Wait until you are invited to open to the setup page in your browser.
7. Complete the setup wizard to finish the installation.

# Run as service

There are several solutions to run Wiki.js as a background service. We'll focus on **systemd** in this guide as it's available in nearly all linux distributions.

1. Create a new file named `wiki.service` inside directory `/etc/systemd/system`.
  ```bash
  nano /etc/systemd/system/wiki.service
  ```
2. Paste the following contents (assuming your wiki is installed at `/var/wiki`):
  ```ini
  [Unit]
  Description=Wiki.js
  After=network.target

  [Service]
  Type=simple
  ExecStart=/usr/bin/node server
  Restart=always
  # Consider creating a dedicated user for Wiki.js here:
  User=nobody
  Environment=NODE_ENV=production
  WorkingDirectory=/var/wiki

  [Install]
  WantedBy=multi-user.target
  ```
3. Save the service file (<kbd>CTRL</kbd>+<kbd>X</kbd>, followed by <kbd>Y</kbd>).
4. Reload systemd:
  ```bash
  systemctl daemon-reload
  ```
5. Run the service:
  ```bash
  systemctl start wiki
  ```
6. Enable the service on system boot.
  ```bash
  systemctl enable wiki
  ```

*Note:* You can see the logs of the service using `journalctl -u wiki`

![](https://a.icons8.com/TqgWTTfw/Oy7xHF/svg.svg){.align-abstopright}