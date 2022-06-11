---
title: Developers
description: Getting started on Wiki.js development
published: true
date: 2022-06-11T20:18:43.212Z
tags: dev
editor: markdown
dateCreated: 2019-02-15T04:25:01.768Z
---

Wiki.js is fully modular, which allows any developer to write their own module.

There are 3 methods to develop for Wiki.js. You can either use the dockerized development environment for VS Code *(recommended)*, a generic docker environment or install all dependencies manually on your machine.

# Using Docker + Visual Studio Code

## Prerequisites

* Docker + Docker Compose (via [Docker Desktop](https://www.docker.com/products/docker-desktop/))
* Linux / macOS / Windows 10-11 Pro or Enterprise
* [Visual Studio Code](https://code.visualstudio.com/)

## Running the project
1. Clone the project from [GitHub](https://github.com/Requarks/wiki).
2. Open the project folder in **Visual Studio Code**
3. From the **Extensions** tab, install the **Remote Development** extension by Microsoft (*ms-vscode-remote.vscode-remote-extensionpack*)
4. Click the **green button** located in the bottom-left corner of VS Code: *(or open the command palette)*
	![ui-dev-vscode-remotebtn.png](/assets/ui/ui-dev-vscode-remotebtn.png =350x){.radius-5 .decor-shadow .ml-5}
5. Select **Remote Containers - Reopen in Container**
6. VS Code will now reload and start initializing the containers. Wait for it to complete. This **may take a while the very first time** as npm dependencies must be installed.
	![ui-dev-vscode-init.png](/assets/ui/ui-dev-vscode-init.png =500x){.radius-5 .decor-shadow .ml-5}
7. Open the **Terminal** *(View > Terminal)* and select "**1: bash**" from the dropdown selector on the right:
	![ui-dev-vscode-bash.png](/assets/ui/ui-dev-vscode-bash.png =400x){.radius-5 .decor-shadow .ml-5}
8. From the command line, type the following command to start Wiki.js in development mode:
    ```bash
      yarn dev
    ```
9. Wait for the initialization to complete. You'll be prompted to load **http://localhost:3000/** when ready.
9. Browse to **http://localhost:3000/** _(replace localhost with the hostname of your machine if applicable)_.
10. Complete the setup wizard to finish the installation.

## Stopping the project

Click on **File > Close Remote Connection** to stop the containers and close the Visual Studio Code instance.

## Removing the containers

When you're done and no longer need the development environment, open the **Remote Explorer** tab and remove all containers starting with the name `wiki`.

Alternatively, see the [generic method](#removing-the-containers-1) below.

# Using Docker (Generic)

## Prerequisites

* Docker + Docker Compose (via [Docker Desktop](https://www.docker.com/products/docker-desktop/))
* Linux / macOS / Windows 10-11 Pro or Enterprise

## Running the project
1. Clone the project from [GitHub](https://github.com/Requarks/wiki).
2. Run the following commands:
```bash
docker-compose -f dev/containers/docker-compose.yml up -d
docker exec wiki-app yarn   # only necessary the first time
docker exec wiki-app yarn dev

```
> Run your `docker-compose` commands from the `dev/containers/` directory if you'd prefer to omit the `-f` flag.
{.is-info}

## Stopping the project
1. Hit <kbd>Ctrl</kbd>+<kbd>C</kbd>
2. Run `docker-compose -f dev/containers/docker-compose.yml stop`

## Removing the containers
```
docker-compose -f dev/containers/docker-compose.yml down
```
To wipe the database as well, use
```
docker-compose -f dev/containers/docker-compose.yml down --volumes
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
4. Edit `config.yml` with your local dev machine settings *(port, database, etc.)*

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

## Build Production Images

Production docker images can be built using the following command:
```bash
docker build -t requarks/wiki -f dev/build/Dockerfile .
```

### ARM

Multi-architecture images for arm64 and arm/v7 can be built using the Docker experimental **buildx** plugin and **QEMU**. You can read more about how it works in [this article](https://engineering.docker.com/2019/04/multi-arch-images/).

```bash
docker buildx build --platform linux/arm64,linux/arm/v7 -t requarks/wiki:arm --push -f dev/build/Dockerfile .
```

Multiple architectures can be merged into a single manifest file using the `docker manifest` command. In the example below, the first reference is the final manifest list, followed by a list of docker image digest SHA256 that should be included in the manifest list:

```bash
docker manifest create requarks/wiki:arm requarks/wiki@sha256:abcdef123456 requarks/wiki@sha256:fedcba654321
docker manifest push -p requarks/wiki:arm
```

## Official Builds

Because the master branch contains pre-release code, it is not recommended to build directly from the source code. Doing so will result in a red warning banner being displayed during setup and in the header on all pages. **You should instead follow the [installation instructions](/install).**

A reproducable build workflow is however available [here](https://github.com/requarks/wiki/blob/main/.github/workflows/build.yml) should you want to build it yourself **from a production release tag**.

![](https://a.icons8.com/mZbXwZWa/PdY3mQ/svg.svg){.align-abstopright}
