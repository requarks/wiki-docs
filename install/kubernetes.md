---
title: Kubernetes
description: Getting started with a Kubernetes installation using Helm Charts
published: true
date: 2021-07-09T04:06:09.498Z
tags: setup, docker
editor: markdown
dateCreated: 2019-03-31T01:25:29.636Z
---

# Prerequisites

- A Kubernetes cluster
- [Helm 3](https://helm.sh/docs/using_helm/#installing-helm)
- PostgreSQL Database

# Important

- **You must deploy a single instance in order to setup the application.** Once setup is completed, you can increase the number of replicas to any amount.
- Even though Wiki.js supports other database engines, using **PostgreSQL is a requirement** for multiple replicas.

# Install the Helm Chart

See the [Wiki.js Helm repo](https://github.com/Requarks/wiki/tree/dev/dev/helm#introduction) for detailed installation instructions.
