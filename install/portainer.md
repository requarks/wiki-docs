---
title: Install using Portainer
description: Step-by-step installation guide
published: true
date: 2019-12-04T21:03:41.924Z
tags: setup, guide
---

This guide details the step-by-step procedure to install Wiki.js on a machine running **Portainer**.

1. Click on **Stacks** in the left sidebar navigation.
1. Click on the **+ Add stack** button.
1. Enter a name for the stack (e.g. `wiki`).
1. Select **Web editor** as the Build method.
1. In the Web editor below, paste the following block of code:

--> use the code for the YAML-file from here: https://github.com/requarks/wiki-docs/blob/master/install/docker.md#using-docker-compose

1. Click on **Deploy the stack** button.
1. There's no step 7, it was that easy.

You can now navigate to the IP / domain of your server to complete the configuration and start using Wiki.js!
