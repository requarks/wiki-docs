---
title: 配置
description: Wiki.js的详细配置选项
published: true
date: 2023-02-09T03:07:40.821Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:35:49.445Z
---

Wiki.js的配置文件名为`config.yml`，必须位于Wiki.js安装的根目录下。

> **注意:** 如果你下载的是Wiki.js的zip/tar.gz压缩包，则必须将文件`config.sample.yml`重命名为`config.yml`。
{.is-info}

下面列出了可以在`config.yml`文件中输入的所有可选项。

# 基础设置

基础设置中的配置是**必需设置的**，必须在config.yml文件中定义。

## HTTP

指定HTTP服务器将侦听的端口。对于可直接访问的独立服务器，该端口通常为`80`，如果是反向代理，则为`3000`。

```yml
port: 3000
```

请注意，如果您选择在端口`80`上直接侦听，某些操作系统需要先启用特殊权限。如果权限不足，启动Wiki.js时将显示一个错误。

## 数据库

Wiki.js 需要一个在 [受支持的数据库](/install/requirements#database) 列表中的数据库。

### Tabset {.tabset}

#### PostgreSQL

> **PostgreSQL**（推荐使用）是性能、功能和未来兼容性最佳的引擎。
{.is-success}

```yml
db:
  type: postgres
  host: localhost
  port: 5432
  user: wikijs
  pass: wikijsrocks
  db: wiki
```
**注意**:
- 数据库必须已创建。Wiki.js**不会**为您创建它。
- 如果数据库需要SSL连接，请检查[通过SSL连接的数据库](#database-over-ssl)部分。

#### MySQL

```yml
db:
  type: mysql
  host: localhost
  port: 3306
  user: wikijs
  pass: wikijsrocks
  db: wiki
```
**注意**:
- 数据库必须已创建。Wiki.js**不会**为您创建它。
- 如果数据库需要SSL连接，请检查[通过SSL连接的数据库](#database-over-ssl)部分。

#### MariaDB

```yml
db:
  type: mariadb
  host: localhost
  port: 3306
  user: wikijs
  pass: wikijsrocks
  db: wiki
```
**注意**:
- 数据库必须已创建。Wiki.js**不会**为您创建它。
- 如果数据库需要SSL连接，请检查[通过SSL连接的数据库](#database-over-ssl)部分。

#### MS SQL Server

```yml
db:
  type: mssql
  host: localhost
  port: 1433
  user: wikijs
  pass: wikijsrocks
  db: wiki
```

**注意**:
- 数据库必须已创建。Wiki.js**不会**为您创建它。

#### SQLite

> **SQLite**不建议用于生产环境。它仅用于低端系统和开发目的。
{.is-warning}

```yml
db:
  type: sqlite
  storage: db.sqlite
```

`storage`值是将保存数据库的文件的路径。此路径必须可由Wiki.js node进程写入。它可以是绝对路径，也可以是相对于Wiki.js目录的路径。

# 高级设置

高级部分中的配置设置是可选的，如果不需要，可以省略。

## HTTPS

Wiki.js支持用户提供的自定义证书或自动Let's Encrypt证书配置。

> 如果在Wiki.js前面有一个反向代理服务器（例如**nginx**/**apache**），那么SSL应该由反向代理**而非**Wiki.js处理。
> 以下说明适用于Wiki.js直接暴露于互联网的使用情况。
{.is-warning}

### 自定义证书

您需要**PEM**格式的**私钥**（`key`）和**证书**（`cert`）：

```yml
ssl:
  enabled: true
  port: 3443
  provider: custom
  
  format: pem
  key: path/to/key.pem
  cert: path/to/cert.pem
  passphrase: null
  dhparam: null
```

也可以使用**PFX**（`pem`）格式的证书：

```yml
ssl:
  enabled: true
  port: 3443
  provider: custom
  
  format: pfx
  pfx: path/to/cert.pfx
  passphrase: null
  dhparam: null
```

`port`是HTTPS服务端将监听的端口。**它不能与HTTP端口相同**
`passphrase`是可选的，仅当证书被短语加密是才需要，否则应设为`null`
`dhparam`是可选的，可用于设置Diffie-Hellman参数（密钥长度须大于或等于1024位）。如果未使用，则应将其设置为空。

> 建议通过[启用HTTP到HTTPS重定向](#HTTP到HTTPS重定向)选项，将HTTP端口上的所有不安全请求自动重定向到HTTPS。
{.is-warning}

### Let's Encrypt

> 此功能在 **2.1及以上版本**可用。
{.is-info}

Let's Encrypt允许为您的wiki免费自动签发和续订SSL证书。

```yml
ssl:
  enabled: true
  port: 3443
  provider: letsencrypt

  domain: wiki.yourdomain.com
  subscriberEmail: admin@example.com
```

`port`是HTTPS服务端将监听的端口。**它不能与HTTP端口相同**

> 非安全HTTP端口**必须始终可以从互联网访问**，以便完成Let's Encrypt challenge过程以及自动续订证书。完成初始验证后，您可以通过[启用HTTP到HTTPS重定向](#HTTP到HTTPS重定向)选项，将在HTTP端口上发出的所有不安全请求自动重定向到HTTPS。
{.is-warning}

`domain`是指向wiki的完全域名。它必须**已有到服务器的解析**。

`subscriberEmail`是使用Let's Encrypt进行身份验证以请求证书时使用的电子邮件。它应该设置为您的系统管理员邮箱，以便接收有关SSL证书的重要电子邮件。

下图详细说明了证书配置过程。尽管所有这些步骤都是为您自动执行的，但它可以让您更好地理解过程。

![Let's Encrypt 配置过程](/assets/diagrams/diag-letsencrypt.png =800x){.decor-shadow .radius-5}

### HTTP到HTTPS重定向

一旦HTTPS启动并正常工作，就可以在**管理区**>**SSL**下启用HTTP到HTTPS重定向。

## 使用SSL连接数据库

一些数据库服务器需要SSL连接以获得额外的安全性。

### 自动

在大多数情况下，SSL连接可以由数据库客户端驱动程序自动建立。您只需将`db.ssl`参数设置为`true`即可：

例如，使用PostgreSQL配置时，请注意附加的`db.ssl`标志：

```yaml
db:
  type: postgres
  host: localhost
  port: 5432
  user: wikijs
  pass: wikijsrocks
  db: wiki
  ssl: true
```

### 自定义

> 此功能在 **2.1及以上版本**可用。
{.is-info}

如果服务器需要特定或自行生成的证书，则可以在`db.sslOptions`参数中指定自定义TLS选项（将`db.ssl`标志设置为`true`之外）：

```yaml
db:
  type: postgres
  host: localhost
  port: 5432
  user: wikijs
  pass: wikijsrocks
  db: wiki
  ssl: true
  
  sslOptions:
    auto: false
    # rejectUnauthorized: false
    ca: path/to/ca.crt
    cert: path/to/cert.crt
    key: path/to/key.pem
    # pfx: path/to/cert.pfx
    passphrase: xyz123
```

`auto`标志必须设置为`false`。并注释掉您不需要的行。

您可以在[Node.js TLS文档](https://nodejs.org/api/tls.html#tls_tls_createsecurecontext_options)中找到sslOptions对象可接受参数的完整列表。

## 数据库连接池

> 除非您知道自己在做什么，否则不建议更改这些设置。
{.is-warning}

Wiki.js使用到数据库的连接池来高效地管理请求。您可以使用`pool`选项更改默认设置：

```yml
pool:
  min: 2
  max: 10
```

有关所有可能的选项，请参阅[tarn.js](https://github.com/vincit/tarn.js)项目页面。

## 绑定IP地址

如果您有多个以太网接口，并且希望指定应使用哪个IP进行侦听，请使用`bindIP`参数：

```yml
bindIP: 0.0.0.0
```

保留默认值`0.0.0.0`以侦听所有接口。


## 日志

通过定义`logLevel`参数，定义要打印到输出的日志数量。

```yml
logLevel: info
```

接受的值有: `error`, `warn`, `info` *(默认)*, `verbose`, `debug`, `silly`.

## 上传限制

> **此选项在2.4版本中已弃用**，现在它通过web管理界面进行控制。
{.is-danger}

设置用户上传的最大文件大小：

```yml
uploads:
  maxFileSize: 5242880
  maxFiles: 10
```

`maxFileSize`参数以字节为单位定义。默认值为`5242880`，即5MB。
`maxFiles`参数定义一次上传中接受的最大文件数。默认值为`10`。

## 离线模式

如果您的wiki实例无法访问internet，请将`offline`参数设置为`true`。这将阻止wiki尝试下载最新的文件更新。

启用此选项后[侧载](/install/sideload)也将被启用。

```yml
offline: true
```

## 高可用

> 此功能在 **2.3及以上版本** 可用。
{.is-info}

> 启用此功能**需要**PostgreSQL。
>
> **您必须部署单个实例才能安装应用程序。** 安装完成后，可以将副本数量增加到任意数量。
{.is-warning}

如果在同一数据库上运行多个并发实例（例如Kubernetes pods/负载均衡实例），则设置为`true`。否则保留`false`。

```yml
ha: true
```

## 数据路径

Wiki.js需要一个文件夹来写入临时数据。默认情况下，此路径为相对于wiki安装路径的`./data`。如果无法向该路径授予写访问权限，则可以通过设置“dataPath”参数来更改该路径：

```yml
dataPath: /path/to/directory
```

# 环境变量插值

配置文件中的任何值都可以替换为`$(ENV_NAME)`，以便在运行时使用环境变量进行插值。

### 示例

对以下`config.yml`示例:
```yaml
db:
  type: $(DB_TYPE)
  host: '$(DB_HOST)'
  port: $(DB_PORT)
  user: '$(DB_USER)'
  pass: '$(DB_PASS)'
```
及以下环境变量而言：
- DB_TYPE=postgres
- DB_HOST=db.example.com
- DB_PORT=5432
- DB_USER=wiki
- DB_PASS=secret
{.grid-list}

系统将生成以下运行时配置：
```yaml
db:
  type: postgres
  host: 'db.example.com'
  port: 5432
  user: 'wiki'
  pass: 'secret'
```

# 示例配置文件

完整示例配置文件的最新版本可以在[GitHub](https://github.com/Requarks/wiki/blob/master/config.sample.yml)上找到。