---
title: 在Ubuntu 18.04 / 20.04 / 22.04 LTS上安装
description: 完整的Wiki.js安装和全功能配置指南
published: true
date: 2023-03-16T08:45:000Z
tags: setup, guide, 指南, 安装
editor: markdown
dateCreated: 2023-01-08T10:36:27.239Z
---

# 概述

这是一篇完整详细的指南，用于在全新的Ubuntu 18.04/2.04/22.04 LTS机器上安装运行Wiki.js所需的一切。

## 包含内容

在本指南的最后，您将拥有一个完整的Wiki.js实例，其中包含以下组件：

- Docker
- PostgreSQL 11 *(docker化)*{.caption}
- Wiki.js 2.x *(docker化, 可从80端口访问)*{.caption}
- Wiki.js Update Companion *(docker化)*{.caption}
- OpenSSH和预先配置了SSH、HTTP和HTTPS规则的UFW防火墙

# 安装

## 更新您的系统

首先，让我们确保您的系统处于最新状态。

```bash
# 获取最新更新
sudo apt -qqy update

# 自动安装所有更新
sudo DEBIAN_FRONTEND=noninteractive apt-get -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' dist-upgrade
```

## 安装Docker

```bash
# 安装安装Docker所需的依赖
sudo apt -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' install ca-certificates curl gnupg lsb-release

# 注册Docker包安装源
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 刷新包管理器并安装Docker
sudo apt -qqy update
sudo apt -qqy -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## 配置容器

```bash
# 创建Wiki.js的安装目录
mkdir -p /etc/wiki

# 创建数据库密码
openssl rand -base64 32 > /etc/wiki/.db-secret

# 创建Docker内部网络
docker network create wikinet

# 为PostgreSQL创建数据卷
docker volume create pgdata

# 创建容器
docker create --name=db -e POSTGRES_DB=wiki -e POSTGRES_USER=wiki -e POSTGRES_PASSWORD_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -v pgdata:/var/lib/postgresql/data --restart=unless-stopped -h db --network=wikinet postgres:11
docker create --name=wiki -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 ghcr.io/requarks/wiki:2
docker create --name=wiki-update-companion -v /var/run/docker.sock:/var/run/docker.sock:ro --restart=unless-stopped -h wiki-update-companion --network=wikinet ghcr.io/requarks/wiki-update-companion:latest
```

## 配置防火墙

```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https

sudo ufw --force enable
```

## 启动容器

```bash
docker start db
docker start wiki
docker start wiki-update-companion
```

## 访问安装向导

在浏览器上，转到您服务器的IP/域名（例如。http://your-server-ip/ ).

> 如果无法加载页面，请等待5分钟，然后重试。在某些系统上，容器初始化可能需要几分钟。
{.is-info}

完成屏幕上的设置以完成安装。

# 使用Let's Encrypt自动部署HTTPS *(可选)*

> 在启用Let's Encrypt**之前**，您必须完成安装向导（参见[开始安装](#开始安装)）！
{.is-warning}

1. 在域注册商上创建一个**A记录**，以将域/子域（例如wiki.example.com）指向您的EC2实例**公共IP**。
2. 确保您能够使用HTTP上的域/子域（例如。http://wiki.example.com).
3. 通过**SSH**连接到您的EC2实例。
4. 运行以下命令，**停止**并**删除**现有wiki容器 *（不会丢失任何数据）*：

```bash
docker stop wiki
docker rm wiki
```

5. 替换`wiki.example.com`和`admin@example.com`为**您自己的域/子域**和wiki管理员的**电子邮件地址**的值，执行以下命令：

```bash
docker create --name=wiki -e LETSENCRYPT_DOMAIN=wiki.example.com -e LETSENCRYPT_EMAIL=admin@example.com -e SSL_ACTIVE=1 -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 ghcr.io/requarks/wiki:2
```

6. 执行以下命令，启动容器
```bash
docker start wiki
```

7. **等待**容器启动，Let's Encrypt配置过程完成。您可以通过运行以下命令查看容器日志：
```
docker logs wiki
```
> 当您在日志中看到以下行时，代表过程完成：
>
> `(LETSENCRYPT) New certifiate received successfully: [ COMPLETED ]`
> `HTTPS Server on port: [ 3443 ]`
> `HTTPS Server: [ RUNNING ]`
{.is-success}

8. 使用HTTPS连接（例如。https://wiki.example.com)。 您的wiki现在可以使用免费Let's Encrypt证书接受HTTPS请求！

## 自动重定向HTTP到HTTPS

默认情况下，对HTTP端口的请求不会重定向到HTTPS。您可以使用以下说明启用此选项：

1. 击页面右上角的头像，导航到**管理区域**。
2. 左侧导航菜单中，单击**SSL**。
3. 在“将HTTP请求重定向到HTTPS”部分旁边，单击**打开**以启用HTTP到HTTPS重定向。
4. HTTP端口的任何请求现在都将自动重定向到HTTPS！

## 更新证书

您可以随时从**管理区***>**SSL**续订证书。

如果您的证书已过期，并且无法加载Wiki UI来续订，只需重新启动容器：

```bash
docker restart wiki
```

更新过程将在初始化期间自动运行。

# 升级

这个映像附带Wiki.js Update Companion，当新版本可用时，它可以自动执行升级过程。

当新版本可用时，您将在**管理区**中收到通知。要执行升级，请遵循以下简单说明：
1. 转到**系统信息**部分，然后单击**执行升级**按钮。
1. 等待升级完成
1. 您现在应该可以使用最新版本。就这么简单！
