---
title: 在DigitalOcean上安装
description: 使用DigitalOcean市场上的预构建镜像
published: true
date: 2023-03-16T08:45:00.000Z
tags: install, 安装
editor: markdown
dateCreated: 2023-01-08T10:35:52.439Z
---

# 概述

DigitalOcean市场上的Wiki.js映像是一个预先配置的环境，由Wiki.js的开发人员制作，包含开始使用Wiki.js所需的一切。

## 映像规格

预装了下列软件的Ubuntu 20.04 LTS：

- Docker
- PostgreSQL 11 *(docker化)*{.caption}
- Wiki.js 2.x *(docker化, 可从80端口访问)*{.caption}
- Wiki.js Update Companion *(docker化)*{.caption}
- 带有启用了SSH, HTTP and HTTPS规则的UFW防火墙的OpenSSH

## 虚拟机规格

Wiki.js可在最低规格的虚拟机上流畅运行 (**1GB RAM + 1 CPU**).

但是，为了获得最佳性能，我们建议至少使用**2GB RAM+2 CPU**规格的虚拟机。Wiki.js将后台进程用于CPU密集型任务（例如页面渲染）。因此，拥有至少2个CPU内核将提高此类任务的性能。

请注意，您可以随时从DigitalOcean控制面板升级到更强大的虚拟机配置。

# 开始配置

1. 转到Digital Ocean市场中的[**Wiki.js**](https://marketplace.digitalocean.com/apps/wiki-js?refcode=5f7445bfa4d0)，然后单击创建Wiki.js 虚拟机实例。
1. 选择虚拟机规格、数据中心区域和其它选项
1. 输入所有必要信息后，单击**创建虚拟机**。
1. 等待虚拟机创建完成。
1. 单击新创建的虚拟机并复制**公共IP**地址。
1. 在新的浏览器选项卡中，导航到http://YOUR-PUBLIC-IP *（替换为您的IP）*
  > **服务器开始接受请求可能需要几分钟的时间。** 在您能够访问wiki之前，系统必须首先初始化各种服务。如果第一次尝试访问时未加载，请等待5分钟，然后重试。
  {.is-info}
8. 此时应该会出现Wiki.js的设置屏幕。为管理员帐户输入所需的**电子邮件地址**和**密码**。
1. 输入wiki的**完整URL**，不带结尾斜杠。建议将子域名/域名指向您的公共IP（例如wiki.example.com）。如果您还没有配置域名，则可以使用您的公网地址作为URL（例如。http://xx.xx.xx.xx). 这可以稍后在**管理区**（在**常规**部分下）中更改。
1. 单击**安装**以完成安装。完成后，您将自动重定向到登录页面。输入您先前输入的管理员帐户的电子邮件和密码。

# 配置Let's Encrypt证书和自动HTTPS跳转

> 在启用Let's Encrypt**之前**，您必须完成安装向导（请参阅[入门](#getting-started)）！
{.is-warning}

1. 在您的域注册商上创建一个**记录**，以将域名/子域名（例如wiki.example.com）指向您的虚拟机**公网IP**。
2. 确保您能够通过HTTP访问这个域名/子域名（例如。http://wiki.example.com).
3. 通过**SSH**连接到你的虚拟机。
4. 运行以下命令，**停止**并**删除**现有wiki容器 *（此操作不会丢失任何数据）*：

```bash
docker stop wiki
docker rm wiki
```

5. 将`wiki.example.com`和`admin@example.com`替换为**您自己的域名/子域名**和wiki管理员的**电子邮件地址**，执行如下命令：

```bash
docker create --name=wiki -e LETSENCRYPT_DOMAIN=wiki.example.com -e LETSENCRYPT_EMAIL=admin@example.com -e SSL_ACTIVE=1 -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 requarks/wiki:2
```

6. 执行以下命令启动容器：
```bash
docker start wiki
```

7. **等待**容器启动和Let's Encrypt配置过程完成。您可以选择通过运行以下命令查看容器日志：
```
docker logs wiki
```
> 在日志中看到以下行，代表该过程完成：
>
> `(LETSENCRYPT) New certifiate received successfully: [ COMPLETED ]`
> `HTTPS Server on port: [ 3443 ]`
> `HTTPS Server: [ RUNNING ]`
{.is-success}

8. 使用HTTPS连接wiki（例如。https://wiki.example.com). 您的wiki现在已经在使用免费Let's Encrypt证书接受HTTPS请求！

## 自动重定向HTTP到HTTPS

默认情况下，对HTTP端口的请求不会重定向到HTTPS。您可以使用以下说明启用此选项：

1. 单击页面右上角的头像，导航到**管理区**。
2. 在左侧导航菜单中，单击**SSL**。
3. 在`将HTTP请求重定向到HTTPS`部分旁边，单击**打开**以启用HTTP到HTTPS重定向。
4. 对HTTP端口的任何请求现在都将自动重定向到HTTPS！

## 续订证书

您可以随时从**管理区域***>**SSL**续订证书。

如果您的证书已过期，并且无法加载wiki UI来续订，只需重新启动容器：

```bash
docker restart wiki
```

证书续订过程将在初始化期间自动运行。

# 升级

这个映像附带Wiki.js Update Companion，当新版本可用时，它可以自动执行升级过程。

当新版本可用时，您将在**管理区**中收到通知。要执行升级，请遵循以下简单说明：
1. 转到**系统信息**部分，然后单击**执行升级**按钮。
1. 等待升级完成
1. 您现在应该可以使用最新版本。就这么简单！

![](https://static.requarks.io/logo/digitalocean-alt.svg){.align-abstopright}