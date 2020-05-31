---
title: Default
description: Comments Module
published: true
date: 2020-05-31T22:41:50.697Z
tags: module, comments
---

This is the default, built-in commenting module for Wiki.js

# Setup

1. In the **Administration Area** of your wiki, click on **Comments** in the left navigation.
1. Click on **Default**.
1. Click **Apply** on the upper right of the page to save and apply the configuration.

The built-in comments UI will now be displayed at the end of all your wiki pages.

# Spam Protection

## Akismet

New comments can optionally be verified against the Akismet service. This is the same service used by Wordpress to prevent and block spam comments.

In order to use it, you need to create a free account on https://akismet.com/ and get an **API key**.

## Minimum Post Delay

You can set the minimum delay (in seconds) between new posts per account. The default value is **30** seconds. Note that while you can set a value lower than 15, the rate limiter (see below) will automatically trigger for any new comment request made before a 15 seconds delay for their IP.

> If you allowed guests to post comments, note that they are considered as a single account and the delay will therefore apply to all guests.
{.is-info}

## Rate Limiting

The endpoint for posting new comments is protected by a rate limiting of one request per IP every 15 seconds. This limit is hardcoded and cannot be changed.

Since rate limiter works per unique IP addresses, each guest is a different user (unlike the above Minimum Post Delay).