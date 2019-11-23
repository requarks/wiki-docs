---
title: Install on DigitalOcean
description: Using the DigitalOcean Marketplace Pre-Built Image
published: true
date: 2019-11-23T18:59:01.479Z
tags: install
---

> :warning: **The DigitalOcean Marketplace Wiki.js image is not yet available but will be shortly!** Thank you for your patience!
{.is-warning}

# Overview

The DigitalOcean Marketplace Wiki.js image is a pre-configured environment, made by the developers of Wiki.js, containing everything you need to get started with Wiki.js.

## Image Specifications

Ubuntu 18.04 LTS with the following software pre-installed:

- Docker
- PostgreSQL 11 *(dockerized)*{.caption}
- Wiki.js 2.x *(dockerized, accessible via port 80)*{.caption}
- Wiki.js Update Companion *(dockerized)*{.caption}
- OpenSSH with UFW Firewall preconfigured for SSH, HTTP and HTTPS

## Droplet Size

Wiki.js works great on even the smallest Droplet size (**1GB RAM + 1 CPU**).

However, for best performance, we recommend using at least the **2GB RAM + 2 CPU** droplet size. Wiki.js use background processes for CPU intensive tasks (e.g. page rendering). Therefore, having at least 2 CPU cores will results in improved performance for such tasks.

Note that you can always upgrade to a more powerful droplet configuration in the future from the DigitalOcean control panel.

# Getting Started

1. From the DigitalOcean control panel, click on **Marketplace**.
1. Find the **Wiki.js** listing and click **Create Wiki.js Droplet**.
1. Select a droplet size, datacenter region and additional options.
1. Click **Create droplet** once you entered all necessary info.
1. Wait for the droplet to be created.
1. Click on the newly created droplet and copy the **public IP** address.
1. In a new browser tab, navigate to http://YOUR-PUBLIC-IP *(replace with your IP)*
1. A setup screen for Wiki.js should appear. Enter the desired **email address** and **password** for the administrator account.
1. Enter the **full URL** to your wiki, without the trailing slash. It's recommended to point a sub-domain / domain to your public IP (e.g. wiki.example.com). If you don't have a domain setup yet, you can use your public IP as the URL (e.g. http://xx.xx.xx.xx). This can be changed later in the **Adminitration Area** (under the **General** section).
1. Click on **Install** to complete the installation. You'll automatically be redirected to the login page once completed. Enter the email and password for the administrator account you entered earlier.

# Automatic HTTPS with Let's Encrypt

> *Native Let's Encrypt support is coming soon!*
{.is-warning}

*In the meantime, use a reverse-proxy such as nginx (hard) or a cloud solution like Cloudflare (easy). Both options are free.*

# Upgrade

This image comes with the Wiki.js Update Companion. This feature automates the upgrade process when a new version is available.

When a new version is available, you'll be notified in the **Administration Area**. To perform the upgrade, follow these simple instructions:
1. Go to the **System Info** section and click the **Perform Upgrade** button.
1. Wait for the process to complete.
1. You should now be on the latest version. It's that simple!

![](https://static.requarks.io/logo/digitalocean-alt.svg){.align-abstopright}