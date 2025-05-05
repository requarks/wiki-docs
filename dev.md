---
title: Developers
description: Getting started on Wiki.js development
published: true
date: 2024-10-31T02:12:28.000Z
tags: dev
editor: markdown
dateCreated: 2019-02-15T04:25:01.768Z
---

Wiki.js is fully modular, which allows any developer to write their own module.

There are 4 methods to develop for Wiki.js. You can either use the dockerized development environment for VS Code *(recommended)*, the remote development environment for WebStorm, a generic docker environment or install all dependencies manually on your machine.

> JetBrains WebStorm was recently, October 2024, made free with a community version for **non-commercial** use. For more details see §2, paragraph 3 of the [Toolbox Subscription Agreement for Non-Commercial Use](https://www.jetbrains.com/legal/docs/toolbox/license_non-commercial/){.is-info}

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

Alternatively, see the [generic method](#removing-the-containers-2) below.

# Using Docker + JetBrains WebStorm

> This section is under development

## Prerequisites

* Docker + Docker Compose (via [Docker Desktop](https://www.docker.com/products/docker-desktop/))
* Linux / macOS / Windows 10-11 Pro or Enterprise
* [JetBrains WebStorm](https://www.jetbrains.com/webstorm/)

> WebStorm on Linux can either be setup from the downloadable tarball or installing via Flathub. If using the Flathub version of WebStorm it executes webstorm.sh instead of webstorm from the /bin directory of the application and will give you a notification on startup.{.is-info}

> WebStorm (*version 2024.2.4*) by default only has a **4.19 GB (4000 MiB) heap size** and can crash during development tasks of Wiki.js. To expand the limit, go to **Help** > **Change Memory Settings** and enter in the new value in MiB. When done, click **Save and Restart** so the changes take effect.{.is-info}

## Running the project
1. Clone the project from [GitHub](https://github.com/Requarks/wiki).
2. Open the project folder in **WebStorm**
3. If a dev container is currently setup, right-click on the *devcontainer.json* file from the file tree and select **Dev Containers** > **Create Dev Container and Mount Sources** > **ContainerName** > **WebStorm** and skip to [Starting Dev Container](#starting-dev-container).

### Setting Up A New Dev Container
1. From the **File** menu, go to Remote Development and select the **Dev Containers** connections option
2. Click on **New Dev Container** to start creating a new container.
    ![ui-dev-webstorm-container-selection.png](/assets/ui/ui-dev-webstorm-container-selection.png =400x){.radius-5 .decor-shadow .ml-5}
3. Change the dev container source to **From Local Project** from **From VCS Project** and either enter the path to the *devcontainer.json* file in the cloned repo or navigate to it by clicking on the folder icon.
    ![ui-dev-webstorm-new-container-creation.png](/assets/ui/ui-dev-webstorm-new-container-creation.png =400px){.radius-5 .decor-shadow .ml-5}

> The IDE can be changed to another product offered by JetBrains from WebStorm, but since development of Wiki.js is based in JavaScript there is no reason to change this.{.is-info}

> If a red circle appears next to the name of the Docker container (*as shown in the above picture*) ensure that Docker Desktop is running on your machine.{.is-info}

4. If a Docker Container already exists (*or was imported from VS Code to WebStorm*), skip this step and proceed to step 7 to start the development container.
    1. To create a new Docker Container in WebStorm, click on the **...** next to the first drop-down list on the new dev container creation window.
    2. Click on the **+** icon to create a new Docker container.
    3. Setup the Docker daemon connection settings using either a *Unix socket* or a *TCP socket*. A **Unix Socket** is the easiest connection to setup as it works directly with Docker Desktop.
    4. Change the name of the container, if desired, and click **OK** to complete the new container setup and initialize the Docker container startup.
    ![ui-dev-webstorm-new-docker-connection-setup.png](/assets/ui/ui-dev-webstorm-new-docker-connection-setup =500px){.radius-5 .decor-shadow .ml-5}

> If the connection for the selected Unix socket cannot locate the Docker daemon, choose from another available Docker Unix socket and see if the status changes to *Connection successful*.{.is-info}

### Starting Dev Container
1. Once the container finishes initializing, a notification will pop up saying **Dev Container build is finished** and will prompt you to connect to the container. Click **Connect** from either the notification or from the Services pane to start the development connection.
2. Once the development IDE instance is created a new IDE window will pop up and the title bar will now show the remote connection type. The connection dropdown can be clicked on to view information about the Docker environment. To start Wiki.js in development mode, open the *Terminal* pane and enter the following command:
    ```bash
      yarn dev
    ```
3. Wait for the initialization to complete. Once the initialization process is completed, a message will appear above the terminal saying **Your application is listening on ports: 3000 forward to xxxx**.
4. Click on the forwarded port number to expand the dropdown list and click on **Open in browser**.
    ![ui-dev-webstorm-remote-project-intialization.png](ui/assets/ui-dev-webstorm-remote-project-intialization.png =400px){.radius-5 .decor-shadow .ml-5}

5. Complete the setup wizard to finish the installation.

## Stopping the project

To stop the remote connection, simply close the remote IDE window and stop the dev container service in the main WebStorm IDE window.

## Removing the containers

When you're done and no longer need the development environment, go back to **File** > **Remote Development** and remove any development containers created that are no longer needed.

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
