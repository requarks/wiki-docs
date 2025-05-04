---
title: Install locally with Docker Desktop
description: The easiest and quickest way to install Wiki.js on your local machine
published: true
date: 2025-05-04T03:54:13.172Z
tags: setup, guide
editor: markdown
dateCreated: 2022-06-12T21:00:47.228Z
---

# Overview

This guide is a quick and simple guide to run Wiki.js on your local **macOS** or **Windows** machine.

# Installation

## 1. Install Docker Desktop

Install Docker Desktop which includes both Docker and Docker Compose:

- [macOS (Apple Silicon)](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
- [macOS (Intel)](https://desktop.docker.com/mac/main/amd64/Docker.dmg)
- [Windows](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)

## 2. Create the Installation Folder

Create a new folder named `wiki` at the location of your choice.

Inside this folder, create a new file named `docker-compose.yaml` and paste the following contents inside:

```yaml
version: "3"
services:

  db:
    image: postgres:17-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
```

This file simply defines a PostgreSQL container *(our database)* and the Wiki.js container.

## 3. Open Terminal / Command Prompt

On **macOS**, launch **Terminal** and navigate to the `wiki` folder you created earlier.

On **Windows**, open the folder `wiki` you created earlier in **File Explorer**.  
In the address bar, type `cmd` and press <kbd>ENTER</kbd> to launch a **Command Prompt** at that location.

## 4. Launch Wiki.js

Type the following command in the **Terminal** / **Command Prompt** to start Wiki.js:

```sh
docker compose up -d
```

## 5. Browse to Wiki.js

Open your browser and navigate to http://localhost to complete the installation and use Wiki.js!
