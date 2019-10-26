---
title: Upgrade
description: How to upgrade to the latest version
published: true
date: 2019-10-26T16:36:21.597Z
tags: 
---

> :warning: **DO NOT** upgrade from `1.0.x` using these instructions! Use the [Migrate from Wiki.js v1.x](/install/migrate) instructions instead.
>
> These instructions are for `2.x` installations.
{.is-danger}

**Choose your platform:**
- [Docker](#docker)
- [Linux / macOS](#linux-macos)
- [Windows](#windows)
{.links-list}

# Docker

## Standalone Container

Upgrading is simply a matter of recreating the container with the latest image version:

```bash
# Stop and remove container named "wiki"
docker stop wiki
docker rm wiki

# Pull latest image of Wiki.js
docker pull requarks/wiki:beta

# Create new container of Wiki.js based on latest image
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=mysql" -e "DB_HOST=db" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" requarks/wiki:beta
```

Check out the [Docker installation guide](/install/docker) for all the possible options when creating a Wiki.js container.

## Docker Compose

The following commands will pull the latest image and recreate the containers defined in the docker-compose file:

```bash
docker-compose pull wiki
docker-compose up --force-recreate
```

# Linux / macOS

> The commands below assume an installation within a subfolder named `wiki`.
{.is-info}

1) Stop the running Wiki.js instance
2) Make a backup of your `config.yml` file.
  ```bash
  cp wiki/config.yml ~/config.yml.bak
  ```
3) Delete the application folder.
  ```bash
  rm -rf wiki/*
  ```
4) Download the latest version of Wiki.js.
  ```bash
  wget https://github.com/Requarks/wiki/releases/download/2.0.0-rc.1/wiki-js.tar.gz
  ```
5) Extract the package
  ```bash
  tar xzf wiki-js.tar.gz -C ./wiki
  cd wiki
  ```
6) Restore your config.yml back to its original location.
  ```bash
  cp ~/config.yml.bak ./config.yml
  ```
7) Start Wiki.js
  ```bash
  node server
  ```

# Windows

> The commands below assume an installation at folder location `C:\wiki`.
{.is-info}

1. Open a **Powershell** prompt in administrator mode.
1. Make a backup of `config.yml` file.
  ```powershell
  Copy-Item "C:\wiki\config.yml" -Destination "C:\config.yml.bak"
  ```
3. Delete the application folder contents.
  ```powershell
  Clear-Content "C:\wiki\*"
  ```
4. If you are using **Windows 7 / Windows Server 2008 R2 or older**, you must run the following command. *(otherwise skip this step)*
  ```powershell
  [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12
  ```
5. Download the latest version of Wiki.js:
  ```powershell
  Invoke-WebRequest -Uri "https://github.com/Requarks/wiki/releases/download/2.0.0-rc.1/wiki-js-windows.tar.gz" -OutFile "wiki-js.tar.gz"
  ```

4. Extract the package to the final destination of your choice:
  ```powershell
  tar xzf wiki-js.tar.gz -C "C:\wiki"
  cd C:\wiki
  ```
  > :warning: The **tar** utility is only available on Windows 10. On earlier versions, you'll need a 3rd-party utility like [7-zip](https://www.7-zip.org/) to extract the file.
  {.is-warning}
5. Copy your `config.yml` backup file back to it's original location.
  ```powershell
  Copy-Item "C:\config.yml.bak" -Destination "C:\wiki\config.yml"
  ```
6. Run Wiki.js
  ```powershell
  node server
  ```

![](https://a.icons8.com/YTSPoggQ/4CQtQD/svg.svg){.align-abstopright}