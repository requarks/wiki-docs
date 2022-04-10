---
title: Kubernetes
description: Getting started with a Kubernetes installation using Helm Charts
published: true
date: 2022-04-10T00:31:01.610Z
tags: setup, docker
editor: markdown
dateCreated: 2019-03-31T01:25:29.636Z
---

# Prerequisites

- A Kubernetes cluster
- PostgreSQL Database

# Important

- **You must deploy a single instance in order to setup the application.** Once setup is completed, you can increase the number of replicas to any amount.
- Even though Wiki.js supports other database engines, using **PostgreSQL is a requirement** for multiple replicas.

# Using Helm

## Introduction

This chart bootstraps a Wiki.js deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

It also optionally packages the [PostgreSQL](https://github.com/kubernetes/charts/tree/master/stable/postgresql) as the database but you are free to bring your own.

## Prerequisites

- PV provisioner support in the underlying infrastructure (with persistence storage enabled) if you want data persistance

## Adding the Wiki.js Helm Repository

```bash
helm repo add requarks https://charts.js.wiki
```

## Installing the Chart

To install the chart with the release name `my-release` run the following:

### Using Helm 3:
```console
helm install my-release requarks/wiki
```
### Using Helm 2:
```console
helm install --name my-release requarks/wiki
```

The command deploys Wiki.js on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`
{.is-info}

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

> **Warning**: Persistant Volume Claims for the database are not deleted automatically. They need to be manually deleted
{.is-warning}

```console
kubectl delete pvc/data-wiki-postgresql-0
```

## Configuration

The following table lists the configurable parameters of the Wiki.js chart and their default values.

| Parameter                            | Description                                 | Default                                                    |
| -------------------------------      | -------------------------------             | ---------------------------------------------------------- |
| `image.repository`                   | Wiki.js image                                | `requarks/wiki`                                           |
| `image.tag`                          | Wiki.js image tag                            | `latest`                                                      |
| `imagePullPolicy`                    | Image pull policy                           | `IfNotPresent`                                             |
| `replicacount`                   | Amount of wiki.js service pods to run                   | `1`                                                        |
| `revisionHistoryLimit`                   | Total amount of revision history points                   | `10`                                        |
| `resources.limits`               | wiki.js service resource limits                         | `nil`                               |
| `resources.requests`             | wiki.js service resource requests                       | `nil`                               |
| `nodeSelector`                   | Node labels for wiki.js pod assignment          | `{}`                                                       |
| `affinity`                       | Affinity settings for wiki.js pod assignment    | `{}`                                                       |
| `schedulerName`                  | Name of an alternate scheduler for wiki.js pod  | `nil`                                                      |
| `tolerations`                    | Toleration labels for wiki.jsk pod assignment    | `[]`                                                       |
| `ingress.enabled`                    | Enable ingress controller resource          | `false`                                                    |
| `ingress.annotations`                | Ingress annotations                         | `{}`                                                       |
| `ingress.hosts`                      | List of ingress rules                        | `[{"host": "wiki.local", "paths": ["/"]}]`                |
| `ingress.tls`                        | Ingress TLS configuration                   | `[]`                                                       |
| `sideload.enabled`                   | Enable sideloading of locale files from git | `false`                                                    |
| `sideload.repoURL`                   | Git repository URL containing locale files  | `https://github.com/Requarks/wiki-localization`            |
| `sideload.env`                       | Environment variables for sideload Container | `{}`                                                      |
| `postgresql.enabled`                 | Deploy postgres server (see below)          | `true`                                                     |
| `postgresql.postgresqlDatabase`        | Postgres database name                      | `wiki`                                                   |
| `postgresql.postgresqlUser`            | Postgres username                           | `postgres`                                                   |
| `postgresql.postgresqlHost`            | External postgres host                      | `nil`                                                      |
| `postgresql.postgresqlPassword`        | External postgres password                  | `nil`                                                      |
| `postgresql.existingSecret`            | Provide an existing `Secret` for postgres   | `nil`                                                      |
| `postgresql.existingSecretKey`          | The postgres password key in the existing `Secret`   | `postgresql-password`                              |
| `postgresql.postgresqlPort`            | External postgres port                      | `5432`                                                     |
| `postgresql.ssl`                       | Enable external postgres SSL connection     | `false`                                                   |
| `postgresql.ca`                        | Certificate of Authority path for postgres  | `nil`                                                     |
| `postgresql.persistence.enabled`                | Enable postgres persistence using PVC                | `true`                                                     |
| `postgresql.persistence.existingClaim`          | Provide an existing `PersistentVolumeClaim` for postgres | `nil`                                                      |
| `postgresql.persistence.storageClass`           | Postgres PVC Storage Class (example: `nfs`)                           | `nil`                 |
| `postgresql.persistence.size`                   | Postgers PVC Storage Request                         | `8Gi`                                                     |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install --name my-release \
  --set postgresql.persistence.enabled=false \
    requarks/wiki
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install --name my-release -f values.yaml requarks/wiki
```

> **Tip**: You can use the default [values.yaml](values.yaml)
{.is-info}

## PostgresSQL

By default, PostgreSQL is installed as part of the chart.

### Using an external PostgreSQL server

To use an external PostgreSQL server, set `postgresql.enabled` to `false` and then set `postgresql.postgresqlHost` and `postgresql.postgresqlPassword`. To use an existing `Secret`, set `postgresql.existingSecret`. The other options (`postgresql.postgresqlDatabase`, `postgresql.postgresqlUser`, `postgresql.postgresqlPort` and `postgresql.existingSecretKey`) may also want changing from their default values.

To use an SSL connection you can set `postgresql.ssl` to `true` and if needed the path to a Certificate of Authority can be set using `postgresql.ca` to `/path/to/ca`. Default `postgresql.ssl` value is `false`.

If `postgresql.existingSecret` is not specified, you also need to add the following Helm template to your deployment in order to create the postgresql `Secret`:

```yaml
kind: Secret
apiVersion: v1
metadata:
  name: {{ template "wiki.postgresql.secret" . }}
data:
  {{ template "wiki.postgresql.secretKey" . }}: "{{ .Values.postgresql.postgresqlPassword | b64enc }}"
```

## Persistence

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube.
See the [Configuration](#configuration) section to configure the PVC or to disable persistence.

## Ingress

This chart provides support for Ingress resource. If you have an available Ingress Controller such as Nginx or Traefik you maybe want to set `ingress.enabled` to true and add `ingress.hosts` for the URL. Then, you should be able to access the installation using that address.

## Chart Source

See the [Wiki.js Helm repo](https://github.com/Requarks/wiki/tree/dev/dev/helm#introduction) for the chart source.
