---
title: Configuration
description: Detailed configuration options for Wiki.js
published: true
date: 2020-01-12T21:12:06.291Z
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

You need both the **private key** and **certificate** in **PEM** format:

```yml
ssl:
  enabled: false
  port: 3443
  provider: custom
  
  format: pem
  key: path/to/key.pem
  cert: path/to/cert.pem
  passphrase: null
  dhparam: null
```

It's also possible to use a **PFX** formatted certificate instead:

```yml
ssl:
  enabled: false
  port: 3443
  provider: custom
  
  format: pfx
  key: path/to/cert.pfx
  passphrase: null
  dhparam: null
```

The `passphrase` is optional and is only required when the certificate is encrypted passphrase. It should be set to `null` otherwise.

The `dhparam` is optional and can be used to set the Diffie Hellman parameters, with a key length being greater or equal to 1024 bits. It should be set to `null` if not used.

### Let's Encrypt

> This feature is available in version **2.1 and later**.
{.is-info}

## Database over SSL

## Database Connection Pool

## Bind IP

## Logging

## Upload Limits

## Offline Mode

## Data Paths