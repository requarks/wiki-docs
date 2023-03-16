---
title: 开发
description: Wiki.js开发入门
published: true
date: 2023-03-16T08:45:000Z
tags: dev, 开发
editor: markdown
dateCreated: 2023-01-08T10:33:21.906Z
---

Wiki.js是完全模块化的，允许任何开发人员编写自己的模块。

进行Wiki.js相关开发有3中方法。您可以使用VS Code的docker化开发环境 *（推荐）*、通用docker开发环境，或手动在您的机器上安装所有依赖。

# 使用 Docker + Visual Studio Code

## 要求

* Docker + Docker Compose (使用 [Docker Desktop](https://www.docker.com/products/docker-desktop/))
* Linux / macOS / Windows 10-11 专业版或企业版
* [Visual Studio Code](https://code.visualstudio.com/)

## 运行项目
1. 从[GitHub](https://github.com/Requarks/wiki) clone此项目。
2. 在**Visual Studio Code**中打开项目目录
3. 在**拓展**标签页中，安装Microsoft开发的**远程拓展**插件。 (*ms-vscode-remote.vscode-remote-extensionpack*)
4. 点击VS Code左下角的**绿色按钮**: *(或打开命令选项板)*
	![ui-dev-vscode-remotebtn.png](/assets/ui/ui-dev-vscode-remotebtn.png =350x){.radius-5 .decor-shadow .ml-5}
5. 选择**远程容器 - 在容器中打开**
6. VS Code将重新加载并开始初始化容器。请等待初始化完成。**首次加载可能需要一定时间**来安装npm依赖。
	![ui-dev-vscode-init.png](/assets/ui/ui-dev-vscode-init.png =500x){.radius-5 .decor-shadow .ml-5}
7. 打开**终端** *(查看 > 终端)* 并在右侧的下拉菜单中选择 "**1: bash**" ：
	![ui-dev-vscode-bash.png](/assets/ui/ui-dev-vscode-bash.png =400x){.radius-5 .decor-shadow .ml-5}
8. 在命令行中，输入以下命令以开发模式启动Wiki.js：
    ```bash
      yarn dev
    ```
9. 等待初始化完成，准备就绪后系统将提示您打开 **http://localhost:3000/**。
9. 转到 **http://localhost:3000/** _(如果合适，用您计算机的主机名提婚localhost)_.
10. 完成安装向导以完成安装

## 停止项目

点击 **文件 > 关闭远程连接** 以停止容器并关闭Visual Studio Code实例。

## 删除容器

当您完成开发，不再需要开发环境后，请打开**远程资源管理器**选项卡并删除所有名称以`wiki`开头的容器。

或者，您也可以使用下面的[通用方法](#removing-the-containers-1)

# 使用 Docker (通用)

## 要求

* Docker + Docker Compose (使用 [Docker Desktop](https://www.docker.com/products/docker-desktop/))
* Linux / macOS / Windows 10-11 专业版或企业版

## 运行项目
1. 从[GitHub](https://github.com/Requarks/wiki) clone此项目。
2. 执行如下命令：
```bash
docker-compose -f dev/containers/docker-compose.yml up -d
docker exec wiki-app yarn   # only necessary the first time
docker exec wiki-app yarn dev

```
> 如果您想略去`-f`参数，您可以在`dev/containers`目录运行`docker-compose`命令。
{.is-info}

## 停止项目
1. 按下 <kbd>Ctrl</kbd>+<kbd>C</kbd>
2. 执行 `docker-compose -f dev/containers/docker-compose.yml stop`

## 删除项目
```
docker-compose -f dev/containers/docker-compose.yml down
```
要同时擦除数据库，请运行：
```
docker-compose -f dev/containers/docker-compose.yml down --volumes
```

# 手动安装

## 要求

* Wiki.js的全部标准安装[要求](/install/requirements)
* Yarn 1.x \(`npm i -g yarn`\)
* 本机编译依赖
  * Ubuntu:  `apt-get install build-essential`
  * Windows: 在具有管理员权限的Powershell中： `npm i -g --production windows-build-tools`

## 安装项目

1. 从[GitHub](https://github.com/Requarks/wiki) clone此项目。 \(确保使用 `dev` 分支\).
2. 在项目目录内，运行如下命令： `yarn`
3. 将 `config.sample.yml` 重命名为 `config.yml`.
4. 根据您本地开发设备的情况填写 `config.yml` *(端口，数据库等)*

## 运行项目

在项目目录下，执行 `yarn dev`

这个命令将以开发模式启动Wiki.js。程序将首先构建客户端资源（使用Webpack），然后自动启动服务端。请等待此过程完成后再打开app。

转到您在`config.yml`中设定的站点地址。例如，如果您使用了本地的3000端口，您应该打开 http://localhost:3000/ 。

首次进入wiki时，您将看到安装向导，您需要完成向导的所有步骤以完成安装。

## 构建生产环境资源

准备好部署您的修改后，您需要将客户端资源构建到生产优化捆绑包中：

```bash
yarn build
```

# 备注

## 推荐 IDE

Wiki.js 使用 [Visual Studio Code](https://code.visualstudio.com) 开发构建，并附带预置的拓展建议、项目设置与调试配置。您可以使用自己喜欢的IDE，但强烈建议您使用Visual Studio Code。

## 开发

对客户端文件所做的任何更改都将自动触发构建，站点将自动实时更新。如果无法内联替换更改，则页面将自动重新加载。

对服务端文件所做的任何更改都将自动触发服务端重启。您也可以在终端中输入`rs`，然后**回车**来强制重新启动。

要停止开发服务端，请按**CTRL-C**直到进程退出。

## 构建生产镜像

可以使用以下命令构建用于生产环境的docker镜像：
```bash
docker build -t requarks/wiki -f dev/build/Dockerfile .
```

### ARM

arm64与arm/v7的多架构镜像可以使用Docker的实验性**buildx**插件与**QEMU**构建。您可以在[此文](https://engineering.docker.com/2019/04/multi-arch-images/)中了解有关它如何工作的更多信息。
```bash
docker buildx build --platform linux/arm64,linux/arm/v7 -t requarks/wiki:arm --push -f dev/build/Dockerfile .
```

您可以使用`docker manifest`命令将多个架构合并到单个清单文件中。在下面的示例中，第一个引用的是最终清单列表，后面是应包含在清单列表中的docker镜像的SHA256摘要的列表：

```bash
docker manifest create requarks/wiki:arm requarks/wiki@sha256:abcdef123456 requarks/wiki@sha256:fedcba654321
docker manifest push -p requarks/wiki:arm
```

## 官方构建

因为主分支包含预发布代码，所以不建议直接从源代码构建。直接构建的版本将在设置区及所有页面标题中显示红色警告横幅。**您应该根据[安装指南](/install)进行操作**。

但是，如果您希望自己从生产环境发布标签构建，[此处](https://github.com/requarks/wiki/blob/main/.github/workflows/build.yml)提供了可复现构建工作流。

![](https://a.icons8.com/mZbXwZWa/PdY3mQ/svg.svg){.align-abstopright}
