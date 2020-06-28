---
title: Kubernetes
description: Getting started with a Kubernetes installation using Helm Charts
published: true
date: 2020-06-28T23:57:59.929Z
tags: setup, docker
editor: markdown
---

# Prerequisites

- A Kubernetes cluster
- [Helm](https://helm.sh/docs/using_helm/#installing-helm)
- PostgreSQL Database

# Important

- **You must deploy a single instance in order to setup the application.** Once setup is completed, you can increase the number of replicas to any amount.
- Even though Wiki.js supports other database engines, using **PostgreSQL is a requirement** for multiple replicas.

# Install the Helm Chart

https://github.com/Requarks/wiki/tree/master/dev/helm