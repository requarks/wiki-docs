---
title: Install on AWS
description: Using the DigitalOcean Marketplace Pre-Built Image
published: true
date: 2019-12-24T03:26:06.809Z
tags: setup, guide
---

# Overview

The AWS Marketplace Wiki.js image is a pre-configured environment, made by the developers of Wiki.js, containing everything you need to get started with Wiki.js.

## Image Specifications

Ubuntu 18.04 LTS with the following software pre-installed:

- Docker
- PostgreSQL 11 *(dockerized)*{.caption}
- Wiki.js 2.x *(dockerized, accessible via port 80)*{.caption}
- Wiki.js Update Companion *(dockerized)*{.caption}
- OpenSSH with UFW Firewall preconfigured for SSH, HTTP and HTTPS

## Instance Type

Wiki.js requires at least the **t3.micro** instance size. *The **t3.nano** instance type is not supported.*{.red--text}

However, for best performance, we recommend using at least the **t3.small** or preferrably the **c5.large** instance size. Wiki.js use background processes for CPU intensive tasks (e.g. page rendering). Therefore, having at least 2 dedicated CPU cores will results in improved performance for such tasks.

# Getting Started

1. From the [Wiki.js Product Page](https://aws.amazon.com/marketplace/pp/B0832LDTKQ) on AWS Marketplace, click the **Continue to subscribe** button located at the top of the page.
1. Follow the on-screen instructions to launch an instance.
1. Once the instance is running, go to the instance details in the AWS Management Console.
1. Copy the **Public DNS** endpoint for your instance.
1. In a new browser tab, navigate to http://YOUR-PUBLIC-DNS *(replace with your Public DNS endpoint or IP)*
  > **It can take several minutes before the server starts accepting requests.** Various services must initialize for the first time before you'll be able to access your wiki. If it doesn't load on first attempt, wait 5 minutes and try again.
  {.is-info}
6. A setup screen for Wiki.js should appear. Enter the desired **email address** and **password** for the administrator account.
1. Enter the **full URL** to your wiki, without the trailing slash. It's recommended to point a sub-domain / domain to your public IP (e.g. wiki.example.com). If you don't have a domain setup yet, you can use your public DNS endpoint or IP as the URL (e.g. http://xx.xx.xx.xx). This can be changed later in the **Adminitration Area** (under the **General** section).
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

![](https://static.requarks.io/logo/aws.svg){.align-abstopright}