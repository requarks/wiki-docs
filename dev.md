---
title: Developers
description: Getting started on Wiki.js development
published: true
date: 2019-09-15T20:28:20.326Z
tags: 
---

Wiki.js is fully modular, which allows any developer to write their own module or theme.

There are 2 methods to develop for Wiki.js. You can either use the dockerized development environment *(recommended)* or install all dependencies manually on your machine.

# Using Docker

## Prerequisites

* Docker
* Docker Compose
* Linux / macOS

> :information_source: **Developing on Docker for Windows**
>
> The instructions and commands below are made using `make` and unix-based commands. They will not work on Windows. While you can port these commands to their Windows equivalent, they will not be provided here. It's recommended that you use the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) if you wish to use the commands below. It provides a native GNU/Linux environment without the overhead of a virtual machine.
>
> Otherwise, consider using the [non-docker instructions](#manually).
{.is-warning}

## Run the project

1. Clone the project from [GitHub](https://github.com/Requarks/wiki).
2. Start the development environment:
    ```bash
    make docker-dev-up

    # You may need to start the above command with `sudo` depending on your OS configuration.
    ```
3. Wait for the initialization to complete. This **may take a while the very first time** as the wiki container image must be built. Subsequent startups will be extremely fast.
4. Browse to **http://localhost:3000/** _(replace localhost with the hostname of your machine if applicable)_.
5. Complete the setup wizard to finish the installation.

## Stopping the project

When you're done and no longer need the development environment. Simply run the following command to stop and remove the containers:

```bash
make docker-dev-down

# You may need to start the above command with `sudo` depending on your OS configuration.
```

## Other commands

| Command | Description |
| :--- | :--- |
| docker-dev-up | Starts the development environment. |
| docker-dev-down | Stops and remove the development environment. |
| docker-dev-clean | Flush DB and cache. *(Must run `docker-dev-up` first!)* |
| docker-dev-rebuild | Rebuilds the wiki container image. *(Must run `docker-dev-down` first!)* |
| docker-build | Builds the client assets files using a temporary environment. |

## Using alternate databases

The default docker environment is using PostgreSQL as the database engine. However it's sometimes useful to debug using other database engines. You can switch to any of the supported engines (`mariadb`, `mssql`, `mysql`, `postgres`, `sqlite`) by adding the `DEVDB` variable at the end of any of commands above, e.g.:

```bash
make docker-dev-up DEVDB=mariadb

make docker-dev-rebuild DEVDB=mssql
```
> :warning: Make sure to shutdown any running instances **BEFORE** switching engines and then **REBUILD** the wiki image using `make docker-dev-rebuild`. Otherwise Wiki.js will still use the old configuration file and connect to the previous database configuration.
{.is-warning}

### MS SQL Server - Additional Notes

The MS SQL image does not allow for a default database to be created by default. To create the database, you must:
1. Run `make docker-dev-up DEVDB=mssql`
2. Wait for all containers to start. The Wiki.js process should crash, being unable to connect to the DB.
3. Exit the dev process: <kbd>CTRL</kbd>+<kbd>C</kbd>
4. Run `make docker-dev-clean DEVDB=mssql`
5. Wait for the database to be created.
6. Run `make docker-dev-up DEVDB=mssql` again

Alternatively, you can also use [Microsoft SQL Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) to connect to the container and create the initial database.

## Build Production Images

Production docker images can be built using the following command:
```bash
docker build -t requarks/wiki -f dev/build/Dockerfile .
```

### ARM

Multi-architecture images for arm64 and arm/v7 can be built using the Docker experimental **buildx** plugin and **QEMU**. You can read more about how it works in [this article](https://engineering.docker.com/2019/04/multi-arch-images/).

```bash
docker buildx build --platform linux/arm64,linux/arm/v7 -t requarks/wiki --push -f dev/build/Dockerfile .
```

# Manually

## Prerequisites

* All standard Wiki.js [prerequisites](/install/requirements)
* Yarn 1.x \(`npm i -g yarn`\)
* Native compilation dependencies
  * Ubuntu:  `apt-get install build-essential`
  * Windows: from an administrator Powershell: `npm i -g --production windows-build-tools`

## Installing the project

1. Clone the project from GitHub \(make sure to use the `dev` branch\).
2. From the project folder, run the command: `yarn`
3. Rename `config.sample.yml` to `config.yml`.
4. Edit `config.yml` with your local dev machine settings *(db, redis, etc.)*

## Run the project

From the project folder, simply run `yarn dev`

This will start Wiki.js in dev mode. Client assets are compiled first \(using Webpack\), then the server will start automatically. Wait for this process to complete before loading the app!

Browse to the site, using the configuration you defined in `config.yml`. For example, if using port 3000 on your local machine, you would browse to http://localhost:3000/.

The first time you load the wiki, you'll get greeted with the setup wizard. Complete all the steps to finish the installation.

## Building production assets

Once you're ready to deploy your changes, you need to build the client assets into a production optimized bundle:

```bash
yarn build
```

# Notes

## Recommended IDE

Wiki.js is built using [Visual Studio Code](https://code.visualstudio.com) and comes with pre-defined extension recommendations, project settings and debug configuration. You can use your favorite IDE but Visual Studio Code is highly recommended.

## Development

Any changes made to client files will automatically trigger a build and the site will be updated live automatically. If the changes cannot be replaced inline, the page will reload automatically.

Any changes made to the server files will automatically trigger a server restart. You can also force a restart by typing `rs` in the terminal followed by **Enter**.

To stop the development server, use **CTRL-C** until the process exits.

![](https://a.icons8.com/mZbXwZWa/PdY3mQ/svg.svg){.align-abstopright}