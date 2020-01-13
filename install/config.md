---
title: Configuration
description: Detailed configuration options for Wiki.js
published: true
date: 2020-01-13T00:13:09.032Z
tags: setup
---

A config file, named `config.yml`, must be located at the root of your Wiki.js installation.

> **Note:** If you downloaded Wiki.js as a zip / tar.gz package, you must rename the file `config.sample.yml` to `config.yml`
{.is-info}

# Basics

The configuration settings in the basics section are **required** and must be defined in your config.yml file.

## HTTP

Specify the port the HTTP server will listen on. This is usually `80` for a standalone server that is directly accessible or `3000` if behind a reverse-proxy.

```yml
port: 3000
```

Note that if you choose to listen directly on port `80`, some operating systems requires special permissions to be enabled first. An error will be displayed when starting Wiki.js if that is the case.

## Database

Wiki.js requires one of the many [supported database engines](/install/requirements#database).

### Using PostgreSQL

> **PostgreSQL** is the recommended engine for best performance and features.
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
**Notes**:
- The database must already be created. Wiki.js will **not** create it for you.
- If your database requires an SSL connection, check the [Database over SSL](#database-over-ssl) section.

### Using MySQL

```yml
db:
  type: mysql
  host: localhost
  port: 3306
  user: wikijs
  pass: wikijsrocks
  db: wiki
```
**Notes**:
- The database must already be created. Wiki.js will **not** create it for you.
- If your database requires an SSL connection, check the [Database over SSL](#database-over-ssl) section.

### Using MariaDB

```yml
db:
  type: mariadb
  host: localhost
  port: 3306
  user: wikijs
  pass: wikijsrocks
  db: wiki
```
**Notes**:
- The database must already be created. Wiki.js will **not** create it for you.
- If your database requires an SSL connection, check the [Database over SSL](#database-over-ssl) section.

### Using MS SQL Server

```yml
db:
  type: mssql
  host: localhost
  port: 1433
  user: wikijs
  pass: wikijsrocks
  db: wiki
```

### Using SQLite

> **SQLite** is not recommended for production use. It is only provided for low-end systems and development purposes.
{.is-warning}

```yml
db:
  type: sqlite
  storage: db.sqlite
```

The `storage` value is a path to the file where the database will be saved. This path must be **writable** by the Wiki.js node process. It can be either an absolute path or relative to the Wiki.js directory.

# Advanced

The configuration settings in the advanced section are optional and can be omitted if not needed.

## HTTPS

Wiki.js supports both user-provided custom certificates or automated Let's Encrypt certificate provisioning.

### Custom Certificate

You need both the **private key** (`key`) and **certificate** (`cert`) in **PEM** format:

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

It's also possible to use a **PFX** (`pem`) formatted certificate instead:

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

The `port` is the port the HTTPS server will listen on. **It cannot be the same as the HTTP port.**

The `passphrase` is optional and is only required when the certificate is encrypted passphrase. It should be set to `null` otherwise.

The `dhparam` is optional and can be used to set the Diffie Hellman parameters, with a key length being greater or equal to 1024 bits. It should be set to `null` if not used.

### Let's Encrypt

> This feature is available from version **2.1 and up**.
{.is-info}

Let's Encrypt allows for free, automated and auto-renewing SSL certificates for your wiki.

```yml
ssl:
  enabled: true
  port: 3443
  provider: letsencrypt

  domain: wiki.yourdomain.com
  subscriberEmail: admin@example.com
```

The `port` is the port the HTTPS server will listen on. **It cannot be the same as the HTTP port.**

> The non-secure HTTP port **must be accessible from the internet, at all times,** in order for the Let's Encrypt challenge process to complete, as well as for automated certificate renewals. Once the initial verification is completed, all insecure requests made on the HTTP port will automatically be redirected to HTTPS.
{.is-warning}

The `domain` is the fully-qualified domain name pointing to the wiki. **It must already resolve to the server.**

The `subscriberEmail` is the email used when authenticating with Let's Encrypt to request a certificate. It should be set to your sysadmin so that important emails concerning the domain SSL certificate can be received.

The following diagram details the certificate provisioning process. Although all these steps are performed automatically for you, it gives you a better understanding of the process.

![Let's Encrypt Process](/assets/diagrams/diag-letsencrypt.png =800x){.decor-shadow .radius-5}

## Database over SSL

Some database servers require an SSL connection for extra security.

### Automatic

In most scenarios, the SSL connection can be automatically established by the database client driver. You simply need to set the `db.ssl` parameter to `true`:

For example, using a PostgreSQL configuration, note the additional `db.ssl` flag:

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

### Custom

If your server requires a specific or self-generated certificate, you can specify the custom TLS options in the `db.sslOptions` parameter (in addition to setting the `db.ssl` flag to `true`):

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

The `auto` flag must be set to `false`. Comment the lines you don't need.

You can find a complete list of accepted parameters for the `sslOptions` object in the [Node.js TLS documentation](https://nodejs.org/api/tls.html#tls_tls_createsecurecontext_options).

## Database Connection Pool

> It's not recommended to change these settings unless you know what you're doing.
{.is-warning}

Wiki.js uses a pool of connections to the database to efficiently manage requests. You can change the default settings using the `pool` option:

```yml
pool:
	min: 2
  max: 10
```

Refer to to the [tarn.js](https://github.com/vincit/tarn.js) project page for all possible options.

## Bind IP

## Logging

## Upload Limits

## Offline Mode

## Data Paths