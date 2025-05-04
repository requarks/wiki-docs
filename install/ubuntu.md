---
title: Install on Ubuntu 18.04 / 20.04 / 22.04 LTS
description: Complete A to Z guide to setup a fully functioning Wiki.js installation
published: true
date: 2025-05-04T03:54:42.313Z
tags: setup, guide
editor: markdown
dateCreated: 2019-12-23T18:29:29.240Z
---

# Overview

This guide is a fully detailed guide to install everything necessary to run Wiki.js on a brand new Ubuntu 18.04 / 20.04 / 22.04 LTS machine.

## What's Included

At the end of the guide, you'll have a fully working Wiki.js instance with the following components:

- Docker
- PostgreSQL 17 *(dockerized)*{.caption}
- Wiki.js 2.x *(dockerized, accessible via port 80)*{.caption}
- Wiki.js Update Companion *(dockerized)*{.caption}
- OpenSSH with UFW Firewall preconfigured for SSH, HTTP and HTTPS

# Installation

## Update the machine

First, let's make sure the machine is up to date.

```bash
# Fetch latest updates
sudo apt -qqy update

# Install all updates automatically
sudo DEBIAN_FRONTEND=noninteractive apt-get -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' dist-upgrade
```

## Install Docker

```bash
# Install dependencies to install Docker
sudo apt -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' install ca-certificates curl gnupg lsb-release

# Register Docker package registry
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Refresh package udpates and install Docker
sudo apt -qqy update
sudo apt -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## Setup Containers

```bash
# Create installation directory for Wiki.js
mkdir -p /etc/wiki

# Generate DB secret
openssl rand -base64 32 > /etc/wiki/.db-secret

# Create internal docker network
docker network create wikinet

# Create data volume for PostgreSQL
docker volume create pgdata

# Create the containers
docker create --name=db -e POSTGRES_DB=wiki -e POSTGRES_USER=wiki -e POSTGRES_PASSWORD_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -v pgdata:/var/lib/postgresql/data --restart=unless-stopped -h db --network=wikinet postgres:17
docker create --name=wiki -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 ghcr.io/requarks/wiki:2
docker create --name=wiki-update-companion -v /var/run/docker.sock:/var/run/docker.sock:ro --restart=unless-stopped -h wiki-update-companion --network=wikinet ghcr.io/requarks/wiki-update-companion:latest
```

## Setup Firewall

```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https

sudo ufw --force enable
```

## Start the containers

```bash
docker start db
docker start wiki
docker start wiki-update-companion
```

## Access the setup wizard

On your browser, navigate to your server IP / domain name (e.g. http://your-server-ip/ ).

> If you can't load the page, wait 5 minutes and try again. It may take a few minutes for the containers to initialize on some systems.
{.is-info}

Complete the on-screen setup to finish your installation.

# Automatic HTTPS with Let's Encrypt *(optional)*

> You must complete the setup wizard (see [Getting Started](#getting-started)) **BEFORE** enabling Let's Encrypt!
{.is-warning}

1. Create an **A record** on your domain registrar to point a domain / sub-domain (e.g. wiki.example.com) to your server **public IP**.
2. Make sure you're able to load your wiki using that domain / sub-domain on HTTP (e.g. http://wiki.example.com).
3. Connect to your server via **SSH**.
4. **Stop** and **remove** the existing wiki container *(no data will be lost)* by running the commands below:

```bash
docker stop wiki
docker rm wiki
```

5. Run the following command by replacing the `wiki.example.com` and `admin@example.com` values with **your own domain / sub-domain** and the **email address** of your wiki administrator:

```bash
docker create --name=wiki -e LETSENCRYPT_DOMAIN=wiki.example.com -e LETSENCRYPT_EMAIL=admin@example.com -e SSL_ACTIVE=1 -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 ghcr.io/requarks/wiki:2
```

6. Start the container by running the command:
```bash
docker start wiki
```

7. **Wait** for the container to start and the Let's Encrypt provisioning process to complete. You can optionaly view the container logs by running the command:
```
docker logs wiki
```
> The process will be completed once you see the following lines in the logs:
>
> `(LETSENCRYPT) New certifiate received successfully: [ COMPLETED ]`
> `HTTPS Server on port: [ 3443 ]`
> `HTTPS Server: [ RUNNING ]`
{.is-success}

8. Load your wiki in your web browser using HTTPS (e.g. https://wiki.example.com). Your wiki is now accepting HTTPS requests using a free Let's Encrypt certificate!

## Automatic HTTP to HTTPS Redirect

By default, requests made to the HTTP port will not be redirect to HTTPS. You can enable this option using these instructions:

1. Navigate to the **Administration Area** by clicking on your avatar at the top-right corner of the page.
2. From the left navigation menu, click on **SSL**.
3. Next to the `Redirect HTTP requests to HTTPS` section, click on **TURN ON** to enable HTTP to HTTPS redirection.
4. Any requests made to the HTTP port will now automatically redirect to HTTPS!

## Renew the Certificate

You can renew the certificate at any time from the **Administration Area** > **SSL**.

If your certificate has expired and you cannot load the wiki UI to renew it, simply restart the container:

```bash
docker restart wiki
```

The renewal process will run automatically during initialization.

# Upgrade

During the installation guide, you installed the Wiki.js Update Companion. This feature automates the upgrade process when a new version is available.

When a new version is available, you'll be notified in the **Administration Area**. To perform the upgrade, follow these simple instructions:
1. Go to the **System Info** section and click the **Perform Upgrade** button.
1. Wait for the process to complete.
1. You should now be on the latest version. It's that simple!
