---
title: Docker
description: Getting started with the Docker image
published: true
date: 2019-11-10T19:44:46.879Z
tags: setup, docker
---

Before proceeding, make sure you meet the [system requirements](/install/requirements).

# Using the Docker image

Wiki.js is published as a Docker image on Docker Hub as `requarks/wiki`

> :warning: During the beta, you **must** specify the beta tag! e.g. `requarks/wiki:beta`
{.is-warning}

## Environment Variables
You must set the following environment variables. They are all **required** unless specified otherwise.

*For PostgreSQL, MySQL, MariaDB and MSSQL only:*

- **DB_TYPE** : Type of database (`mysql`, `postgres`, `mariadb`, `mssql` or `sqlite`)
- **DB_HOST** : Hostname or IP of the database
- **DB_PORT** : Port of the database
- **DB_USER** : Username to connect to the database
- **DB_PASS** : Password to connect to the database
- **DB_NAME** : Database name

*When connecting to a database server with SSL enforced:*

- **DB_SSL** : Set to either `1` or `true` to enable. *(optional, off if omitted)*

*Alternative way to provide the database password, via a local file secret:*

- **DB_PASS_FILE**: Path to the mapped file containing to the database password. *(optional, replaces DB_PASS)*

*For SQLite only:*

- **DB_FILEPATH** : Path to the SQLite file

## Example

Here's an example of a command to run Wiki.js:
```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=mysql" -e "DB_HOST=db" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" requarks/wiki:beta
```

## Alternative: Mount the config file

If using environment variables is not your cup of tea, you can also mount a config file instead.

Create a new file based on the [sample config file](https://github.com/Requarks/wiki/blob/master/config.sample.yml) and modify the values to match your setup. You can then mount the config file in the container:

```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -v YOUR-FILE.yml:/wiki/config.yml requarks/wiki:beta
```

It's also possible to define an alternate location for the config file to be loaded from. This is useful in scenarios where you want to mount a configuration folder instead. Define the environment variable **CONFIG_FILE** with the path to the config file.

# Using Docker Compose

Here's an example of a Docker Compose file, using PostgreSQL:

```yaml
version: "3"
services:

  db:
    image: postgres:9-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: requarks/wiki:beta
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    ports:
      - "3000:3000" # <-- here you can replace with "80:3000" to listen on port 80 instead, as an example

volumes:
  db-data:
```

![](https://a.icons8.com/jihZbhdR/4WJoF7/svg.svg){.align-abstopright}

# ARM images

In order to use the ARM64 / ARMv7 image variants, you must use the image tag `requarks/wiki:beta-arm`.

This image is compatible with:

- **ARM64**: Raspberry Pi 4, 3 and later Raspberry Pi 2 (v1.2)
- **ARMv7**: Early Raspberry Pi 2 (v1.1)

The original, first-generation Raspberry Pi is **not** supported *(ARMv6)*.

# OpenShift

An example OpenShift-compatible Dockerfile is available [here](https://github.com/Requarks/wiki/blob/master/dev/openshift/Dockerfile).
