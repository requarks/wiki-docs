---
title: Kubernetes
description: 使用Helm Charts开始Kubernetes安装
published: true
date: 2023-02-11T08:46:01.924Z
tags: setup, docker, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:03.943Z
---

# 要求

- 一个Kubernetes集群
- PostgreSQL数据库

# 重要提示

- **您必须部署单个实例才能安装应用程序。**安装完成后，可以将副本数量增加到任意数量。
- 尽管Wiki.js支持其他数据库引擎，但使用多个副本要求使用**PostgreSQL**。

# 使用 Helm

## 介绍

此图表使用[Helm](https://helm.sh)包管理器在[Kubernetes](http://kubernetes.io)集群上引导Wiki.js部署。

它还可以选择将[PostgreSQL](https://github.com/kubernetes/charts/tree/master/stable/postgresql)打包为数据库，但您可以自由引入自己的数据库。

## 要求

- 如果您需要数据持久性，则在基础基础架构中支持PV provisioner（启用持久性存储）

## 添加Wiki.js Helm存储库

```bash
helm repo add requarks https://charts.js.wiki
```

## 安装图表

要安装名为`my release`的图表，请执行以下操作：

### Helm 3:
```console
helm install my-release requarks/wiki
```
### Helm 2:
```console
helm install --name my-release requarks/wiki
```

该命令以默认配置在Kubernetes集群上部署Wiki.js。[配置](#配置)部分列出了安装期间可以配置的参数。

> **提示**: 使用`helm list`列出所有release
{.is-info}

## 卸载图表

要卸载/删除部署好的`my-release`，请执行以下操作：

```console
helm delete my-release
```

该命令删除与图表关联的所有Kubernetes组件并删除release。

> **警告**: 数据库的持久卷声明不会自动删除。您需要手动删除它们
{.is-warning}

```console
kubectl delete pvc/data-wiki-postgresql-0
```

## 配置

下表列出了Wiki.js图表的可配置参数及其默认值。

| 参数                                   | 描述                                                      | 默认值                                          |
| -------------------------------------- | --------------------------------------------------------- | ----------------------------------------------- |
| `image.repository`                     | Wiki.js 映像                                              | `requarks/wiki`                                 |
| `image.tag`                            | Wiki.js 映像标签                                          | `latest`                                        |
| `imagePullPolicy`                      | 映像拉取策略                                              | `IfNotPresent`                                  |
| `replicacount`                         | 要运行的Wiki.js服务节点的数量                             | `1`                                             |
| `revisionHistoryLimit`                 | 历史修订节点总数                                          | `10`                                            |
| `resources.limits`                     | wiki.js服务资源限制                                       | `nil`                                           |
| `resources.requests`                   | wiki.js服务资源请求                                       | `nil`                                           |
| `nodeSelector`                         | Wiki.js 节点分配的标签                                    | `{}`                                            |
| `affinity`                             | Wiki.js 节点分配的相关性设置                              | `{}`                                            |
| `schedulerName`                        | Wiki.js节点备用调度程序名称                               | `nil`                                           |
| `tolerations`                          | Wiki.jsk 节点分配的宽容（toleration）标签                 | `[]`                                            |
| `ingress.enabled`                      | 启用入口控制器资源                                        | `false`                                         |
| `ingress.annotations`                  | 入口注释                                                  | `{}`                                            |
| `ingress.hosts`                        | 入口规则列表                                              | `[{"host": "wiki.local", "paths": ["/"]}]`      |
| `ingress.tls`                          | 入口TLS配置                                               | `[]`                                            |
| `sideload.enabled`                     | 启用从git侧加载区域设置文件                               | `false`                                         |
| `sideload.repoURL`                     | 包含区域设置文件的Git存储库URL                            | `https://github.com/Requarks/wiki-localization` |
| `sideload.env`                         | 侧载容器的环境变量                                        | `{}`                                            |
| `postgresql.enabled`                   | 部署postgres服务器（见下文）                              | `true`                                          |
| `postgresql.postgresqlDatabase`        | Postgres数据库名称                                        | `wiki`                                          |
| `postgresql.postgresqlUser`            | Postgres用户名                                            | `postgres`                                      |
| `postgresql.postgresqlHost`            | 外部postgres主机                                          | `nil`                                           |
| `postgresql.postgresqlPassword`        | 外部postgres密码                                          | `nil`                                           |
| `postgresql.existingSecret`            | 为postgres提供现有的`Secret`                              | `nil`                                           |
| `postgresql.existingSecretKey`         | 现有`Secret`中的postgres密码键（password key）            | `postgresql-password`                           |
| `postgresql.postgresqlPort`            | 外部postgres端口                                          | `5432`                                          |
| `postgresql.ssl`                       | 启用外部postgres SSL连接                                  | `false`                                         |
| `postgresql.ca`                        | postgres的证书路径                                        | `nil`                                           |
| `postgresql.persistence.enabled`       | 使用PVC启用postgres持久化                                 | `true`                                          |
| `postgresql.persistence.existingClaim` | 为postgres提供现有的`PersistentVolumeClaim`（持久卷声明） | `nil`                                           |
| `postgresql.persistence.storageClass`  | Postgres PVC存储类（示例：`nfs`）                         | `nil`                                           |
| `postgresql.persistence.size`          | Postgers PVC存储请求                                      | `8Gi`                                           |

在`helm install`中使用`--set key=value[,key=value]`来指定参数。例如：

```console
helm install --name my-release \
  --set postgresql.persistence.enabled=false \
    requarks/wiki
```

或者，可以在安装图表时提供指定上述参数值的YAML文件。例如

```console
helm install --name my-release -f values.yaml requarks/wiki
```

> **提示**: 你可以使用默认的 [values.yaml](values.yaml)
{.is-info}

## PostgresSQL

默认情况下，PostgreSQL作为图表的一部分安装。

### 使用外部PostgreSQL服务器

要使用外部PostgreSQL服务器，请将`postgresql.enabled`设置为`false`，然后设置`postgresql.postgresqlHost`和`postgresql.postgresqlPassword`。要使用现有`Secret`，设置`postgresql.existingSecret`。其他选项（`postgressql.postgresqlDatabase`、`postgresql.postgresqlUser`、`postgresql.postgressqlPort`和`postgresql.existingSecretKey`）也可能需要更改默认值。

要使用SSL连接，可以将`postgresql.ssl`设置为`true`，如果需要，可以将`postgressql.ca`设为`/path/To/ca`(证书路径)。`postgresql.ssl`的默认值为`false`。

如果还未指定`postgresql.existingSecret`，则还需要将以下Helm模板添加到部署中，以创建postgresql`Secret`：

```yaml
kind: Secret
apiVersion: v1
metadata:
  name: {{ template "wiki.postgresql.secret" . }}
data:
  {{ template "wiki.postgresql.secretKey" . }}: "{{ .Values.postgresql.postgresqlPassword | b64enc }}"
```

## 持久化

持久卷声明用于跨部署保留数据。这在GCE、AWS和minikube中是众所周知的。
请参阅[配置](#配置)部分以配置PVC或禁用持久化。

## 入口（Ingress）

此图表为入口资源提供支持。如果您有一个可用的入口控制器，例如Nginx或Traefik，您可能希望将`ingress.enabled`设置为true，并为URL添加`ingress.hosts`。然后，您应该能够使用该地址访问实例。

## 图表来源

有关图表来源，参见[Wiki.js Helm repo](https://github.com/Requarks/wiki/tree/dev/dev/helm#introduction)。
